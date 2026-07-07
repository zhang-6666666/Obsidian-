# SSD1306 OLED 显示 — 移植计划

## 背景

添加 0.96 英寸 SSD1306 OLED（128×64），硬件 I2C1，PB8(SCL) PB9(SDA)。脱离电脑时直接看角度数据。只实现最基本功能，低耦合可移植，放在 `App/OLED/`。

## 硬件接线

|STM32|OLED|说明|
|---|---|---|
|PB8|SCL|I2C1 SCL（AF_OD，需接 4.7k 上拉到 3.3V）|
|PB9|SDA|I2C1 SDA（AF_OD，需接 4.7k 上拉到 3.3V）|
|3.3V|VCC||
|GND|GND||

## CubeMX 配置

1. 打开 `JY901P.ioc`
2. **Pinout → PB8**：设为 **I2C1_SCL**
3. **Pinout → PB9**：设为 **I2C1_SDA**
4. 左侧 **Connectivity → I2C1**：Mode 选 **I2C**，Speed 选 **Fast Mode**（400kHz）
5. **注意**：STM32F103C8 I2C1 默认脚是 PB6/PB7。PB8/PB9 是 I2C1 remap，CubeMX 选 PB8/PB9 替 I2C1 时会自动显示为 **I2C1 Remap** 并开启 `REMAP_I2C1`。
6. **GPIO Settings** 确认 PB8/PB9 模式为 Alternate Function Open Drain
7. 点击 **GENERATE CODE**

> CubeMX 会自动修改 `gpio.c`、`stm32f1xx_hal_msp.c` 中的 I2C1 初始化和 GPIO 配置，不影响 USART1/2、TIM1、DMA 的已有配置。

## 移植注意事项

oled.c 通过 `extern I2C_HandleTypeDef hi2c1;` 引用 CubeMX 生成的句柄，模块本身**不依赖任何硬件细节**。换芯片时只需改 CubeMX 配置 + 确保 `hi2c1` 声明可访问。

## 文件清单

### 新增文件（3 个）

|文件|职责|
|---|---|
|`App/OLED/oled.h`|OLED API 声明|
|`App/OLED/oled.c`|SSD1306 驱动：HAL I2C 发送 + 初始化序列 + 显存管理 + 显示|
|`App/OLED/font5x7.h`|5×7 ASCII 字库（0x20~0x7E，每字符 5 字节，约 500 字节）|

### 修改文件（赴 2 个）

|文件|区域|内容|
|---|---|---|
|`CMakeLists.txt`|target_sources + include_dirs|添加 `App/OLED/oled.c` 和 `App/OLED`|
|`Core/Src/main.c`|Includes + 2 + 3|初始化 + 角度显示|

## API 设计（共 7 个函数）

```c
void oled_init(I2C_HandleTypeDef *hi2c);   // 传入 hi2c1，初始化 SSD1306

void oled_clear(void);                    // 清显存（不刷新屏幕）
void oled_show(void);                     // 全屏刷新（1024 字节 I2C 写入）

void oled_set_cursor(uint8_t x, uint8_t y);   // 打印位置（x:0~127, y:行号0~7）
void oled_print(const char *str);             // 在当前光标打印 ASCII 字符串
void oled_print_signed(int32_t num);          // 打印有符号整数（自动符号）

void oled_print_angle(int32_t val_x10);      // 角度专用：-18 → "-1.8"
```

- `oled_init(hi2c)`：接收外部传入的 I2C 句柄，模块不硬编码 `hi2c1`
- `oled_print_angle()`：把 ×10 角度值打印为 "-1.8" 格式，对标 jy901p 输出

## 程序结构

```
oled.c 内部：
  1. SSD1306 命令层
     └─ write_cmd(byte) / write_data(buf, len) → HAL_I2C_Mem_Write
  2. 显存管理
     └─ static uint8_t vram[128 * 64 / 8] = 1024 字节
  3. 字符绘制（查 font5x7 字库，画点到 vram）
  4. 对外 API

数据流：
  oled_print("Roll:") → 逐字查字库 → 画点到 vram[]
  oled_show()         → 全屏 vram[] → I2C 批量写入 SSD1306 GDDRAM
```

## 刷新速度

- I2C Fast Mode (400kHz)：全屏 1024 字节 ≈ **~25ms**
- 如果后期只刷新变化区域（如 3 行文本 ~ 300 字节），降至 ~**7ms**