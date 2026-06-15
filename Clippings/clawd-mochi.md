---
title: clawd-mochi/README.md at main
source: https://github.com/yousifamanuel/clawd-mochi/blob/main/README.md
author:
published:
created: 2026-06-15
description: Clawd Mochi：受 Clawd（Claude Code 吉祥物）启发的实体桌面伴侣 - clawd-mochi/README.md at main · yousifamanuel/clawd-mochi
tags:
  - clippings
---
[![Clawd Mochi Logo](https://github.com/yousifamanuel/clawd-mochi/raw/main/pics/clawd_mochi_banner.png)](https://github.com/yousifamanuel/clawd-mochi/blob/main/pics/clawd_mochi_banner.png)

## Clawd Mochi 🦀🤖

一款实体桌面伴侣，灵感来源于 **Clawd** —— Anthropic 旗下 Claude Code 的像素螃蟹吉祥物。它由 ESP32-C3 驱动一块 1.54 英寸彩色 TFT 屏幕，并内置了手机网页控制器——无需 App、无需联网、无需云端。

**成本：约 ¥45–60 元 · 制作时间：约 1 小时 · 难度：初学者**

在 Instagram 上支持本项目：

📦 MakerWorld 上的 3D 打印外壳：[https://makerworld.com/en/models/2559505-clawd-mochi-physical-claude-code-mascot#profileId-2820000](https://makerworld.com/en/models/2559505-clawd-mochi-physical-claude-code-mascot#profileId-2820000)

---

> ⚠️
> 
> 这是一个独立的粉丝项目。本项目与 Anthropic 无任何关联、未获其赞助或背书。"Claude" 和 "Clawd" 是 Anthropic 的商标。

---

[![组装好的 Clawd Mochi 放在桌面上](https://github.com/yousifamanuel/clawd-mochi/raw/main/pics/clawd_mochi_3_4.jpeg)](https://github.com/yousifamanuel/clawd-mochi/blob/main/pics/clawd_mochi_3_4.jpeg) [![Claude Code 画面](https://github.com/yousifamanuel/clawd-mochi/raw/main/pics/clawd_mochi_claude_code.jpeg)](https://github.com/yousifamanuel/clawd-mochi/blob/main/pics/clawd_mochi_claude_code.jpeg)

## 它能做什么

Clawd Mochi 放在你的桌面上，在一块小彩屏上显示动态表情。你可以通过连接它自带的 WiFi 热点，从任何手机或浏览器控制它：

- **普通眼睛** — 像素风方眼，带扭动和眨眼动画
- **眯眼** — `> <` 开心眯眼，带睁闭动画
- **Claude Code** — 显示 "Claude Code" 及交互式终端
- **画布** — 从手机上实时在屏幕上画画

---

## 零件清单

| 零件 | 规格 | 约价格 |
| --- | --- | --- |
| ESP32-C3 Super Mini | 带 WiFi 的微控制器 | ~¥18 |
| ST7789 1.54" TFT | 240×240 SPI 彩色屏幕 | ~¥22 |
| 8 根短线 | 8–10 cm 杜邦线 / 跳线 | ~¥4 |
| 2× M2×6mm 螺丝 | 用于固定屏幕边框 | ~¥1 |
| 双面胶 | 用于固定内部元件 | ~¥1 |
| USB-C 线 | 供电用 | — |
| 3D 打印外壳 | PLA 或 PETG，约 30g | ~¥4 |

**总价：约 ¥50–60**

---

## 接线

> ⚠️VCC 只接 **3.3V** ——绝对不能接 5V。SPI 使用 GPIO 8 和 10（硬件 SPI，速度快）。不要用 GPIO 6/7 做 SPI。

| 屏幕引脚 | ESP32-C3 GPIO  | 建议线色 |
| ---- | -------------- | ---- |
| VCC  | 3V3            | 红    |
| GND  | GND            | 黑    |
| SDA  | GPIO 10 (MOSI) | 橙    |
| SCL  | GPIO 8 (SCK)   | 绿    |
| RES  | GPIO 2         | 紫    |
| DC   | GPIO 1         | 蓝    |
| CS   | GPIO 4         | 白    |
| BL   | GPIO 3         | 黄    |

---

## 软件配置

### 第一步 — 安装 Arduino IDE

下载并安装 [Arduino IDE 2.x](https://www.arduino.cc/en/software)。

### 第二步 — 添加 ESP32 开发板支持

1. 打开 Arduino IDE → **文件 → 首选项**
2. 在「附加开发板管理器网址」中粘贴：
   ```
   https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_index.json
   ```
3. 前往 **工具 → 开发板 → 开发板管理器**，搜索 `esp32`，安装 **"esp32 by Espressif Systems"**

### 第三步 — 安装库

前往 **工具 → 库管理器**，安装以下两个库：

- `Adafruit GFX Library`
- `Adafruit ST7735 and ST7789 Library`

### 第四步 — 配置开发板参数

前往 **工具** 设置：

| 参数 | 值 |
| --- | --- |
| 开发板 | ESP32C3 Dev Module |
| USB CDC On Boot | **Enabled** ← 重要 |
| CPU 频率 | 160 MHz |
| 上传速度 | 921600 |

### 第五步 — 上传程序

1. 克隆或下载本仓库
2. 在 Arduino IDE 中打开 `clawd_mochi/clawd_mochi.ino`
3. 用 USB-C 连接 ESP32
4. 在 **工具 → 端口** 中选择正确端口
5. 点击 **上传**（→ 箭头按钮）
6. 等待显示 "Hard resetting via RTS pin..." ——这表示成功

---

## 如何使用

### 连接并打开控制器

1. 通过 USB-C 给 ESP32 供电（任意 USB 充电器或充电宝）
2. 等待约 3 秒，开机动画播放完毕
3. 在手机或电脑上，进入 **WiFi 设置**
4. 连接到网络：**`ClaWD-Mochi`** · 密码：**`clawd1234`**
5. 打开浏览器，访问 **`http://192.168.4.1`**

你应该能看到网页控制器：

[![网页界面](https://github.com/yousifamanuel/clawd-mochi/raw/main/pics/clawd_mochi_webpage.jpeg)](https://github.com/yousifamanuel/clawd-mochi/blob/main/pics/clawd_mochi_webpage.jpeg)

### 控制器功能

| 按钮 / 控件 | 功能 |
| --- | --- |
| Normal eyes（普通眼睛） | 播放扭动 + 眨眼动画 |
| Squish eyes（眯眼） | 播放睁闭动画 |
| Claude Code | 显示代码画面，打开终端 |
| Canvas（画布） | 进入绘画模式——用手机在屏幕上画画 |
| Speed 滑块 | 控制动画速度（慢 / 正常 / 快） |
| Background color（背景色） | 更改所有视图的背景颜色 |
| Pen color（画笔颜色） | 设置画布的绘画颜色 |
| Display on/off（屏幕开关） | 切换背光开关 |
| ✓ done（完成按钮，画布中） | 退出画布模式 |

---

## 3D 外壳

电子元件外壳（主体 + 背板）位于 `clawd_mochi` 模型文件夹中：

| 文件 | 说明 |
| --- | --- |
| [`./models/clawd_mochi/clawd_mochi_v1.stl`](https://github.com/yousifamanuel/clawd-mochi/blob/main/models/clawd_mochi/clawd_mochi_v1.stl) | 主外壳布局，含主体和背板部件 |

### 打印参数

| 参数 | 值 |
| --- | --- |
| 材料 | PLA 或 PETG |
| 层高 | 0.15–0.20 mm |
| 填充 | 15% gyroid（螺旋） |
| 支撑 | 是 — 屏幕窗口悬垂部分需要 |
| 摆放方向 | 面朝下，背板平放在热床上 |

建议配色：橙色 PLA 打印主体，哑光黑色打印背板。

你也可以从 MakerWorld 下载模型：[https://makerworld.com/en/models/2559505-clawd-mochi-physical-claude-code-mascot#profileId-2820000](https://makerworld.com/en/models/2559505-clawd-mochi-physical-claude-code-mascot#profileId-2820000)

### 3D Clawd 摆件（不含电子元件）

如果你只想要一个摆件，可以用单独的 3D Clawd 模型（无屏幕和电子元件开孔）。

[![3D 打印的 Clawd 模型（眯眼版）](https://github.com/yousifamanuel/clawd-mochi/raw/main/pics/clawd_3D_squished_eyes_4_3.png)](https://github.com/yousifamanuel/clawd-mochi/blob/main/pics/clawd_3D_squished_eyes_4_3.png)

模型文件：

| 文件 | 说明 |
| --- | --- |
| [`./models/clawd_3d/clawd_3D_no_AMS.stl`](https://github.com/yousifamanuel/clawd-mochi/blob/main/models/clawd_3d/clawd_3D_no_AMS.stl) | 原版 Clawd 3D 模型 |
| [`./models/clawd_3d_squished_eyes/clawd_3D_squished_eyes_no_AMS.stl`](https://github.com/yousifamanuel/clawd-mochi/blob/main/models/clawd_3d_squished_eyes/clawd_3D_squished_eyes_no_AMS.stl) | 眯眼变体版 |

你也可以从 MakerWorld 下载模型：[https://makerworld.com/en/models/2576503-clawd-claude-code-mascot#profileId-2841183](https://makerworld.com/en/models/2576503-clawd-claude-code-mascot#profileId-2841183)

---

## 组装技巧

1. 打印外壳文件（主体 + 背板），在粘合之前先试装屏幕
2. 在焊接之前先把 8 根线穿过背板槽口
3. 用双面胶把 ESP32 固定在背板内侧
4. 用 2 颗 M2×6mm 螺丝穿过边框孔固定屏幕
5. 将 USB-C 线穿过背板槽口，然后扣上背板

---

## 自定义

### 眼睛大小和位置

在 `clawd_mochi.ino` 文件顶部附近编辑这些常量：

```
#define EYE_W   30    // 眼睛宽度（像素）
#define EYE_H   60    // 眼睛高度（像素）
#define EYE_GAP 120   // 两眼间距
#define EYE_OX  0     // 水平偏移
#define EYE_OY  40    // 垂直上移
```

### Logo 动画时长

```
// 在 animLogoReveal() 中 — logo 动画结束后保持多久
delay(1500);       // 毫秒 — 修改这个数字

// 逐笔绘制揭开展示的速度
delay(speedMs(8)); // 数值越小 = 越快
```

---

## 参与贡献

非常欢迎贡献！以下是一些想法：

- **新动画** — 添加新表情、过渡效果或待机行为
- **新视图** — 天气显示、时钟、通知徽章、像素艺术场景
- **声音** — 添加小蜂鸣器实现音效
- **传感器** — 接入触摸传感器或按钮实现物理交互
- **OTA 更新** — 添加无线固件更新功能
- **MQTT / Home Assistant** — 接入智能家居平台

参与方式：fork 本仓库，做出修改，然后提交 pull request。请保持单文件结构（`clawd_mochi.ino`），以方便初学者刷写。

## 许可证

本项目基于 MIT 许可证开源 — 详情参见 [LICENSE](https://github.com/yousifamanuel/clawd-mochi/blob/main/LICENSE) 文件。

**注意：** 3D 模型和媒体素材采用 **CC BY-NC-SA 4.0** 许可证。
