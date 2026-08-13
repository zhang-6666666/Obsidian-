1. nmcli device status # 查看wifi设备
2. nmcli device wifi rescan # 扫描wifi
3. nmcli device wifi list
4. nmcli device wifi connect "wifi名称" --ask # 连接wifi
## 环境变量
1. env命令可以查看当前系统中的环境变量
2. $符号 （用作取“环境变量）echo $PATH
### 自行设置环境变量
1. 临时设置环境变量export 变量名=变量值
2. 永久设置环境变量
	1. 对当前用户生效：配置当前用户的.bashrc
	2. 对所有用户生效：配置/etc/profile
	3. 通过source配置文件  
## 香橙派
1. sudo npu-smi info -t pwm-mode
2. sudo npu-smi set -t pwm-mode-ratio -d 50
3. sudo npu-smi set -t pwm-mode -d 1 # 调整成自动模式
