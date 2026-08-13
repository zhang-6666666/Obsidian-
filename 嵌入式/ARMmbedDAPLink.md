---
title: ARMmbed/DAPLink
source: https://github.com/armmbed/DAPLink
author:
published:
created: 2026-07-28
description: Contribute to ARMmbed/DAPLink development by creating an account on GitHub.
tags:
---
[![DAPLink](https://github.com/ARMmbed/DAPLink/raw/main/docs/images/daplink-website-logo-link.png)](https://daplink.io/)

---

Arm Mbed DAPLink 是一个开源软件项目，用于对运行在Arm Cortex CPU上的应用软件进行编程和调试。通常被称为接口固件，DAPLink运行在通过SWD或JTAG端口与应用MCU连接的辅助MCU上。这种配置几乎存在于所有开发板上。作为USB复合设备进行枚举，它在开发计算机与CPU调试访问端口之间建立了一座桥梁。DAPLink为开发者提供：

- MSC - 拖放式编程闪存
- CDC - 虚拟串口，用于日志、追踪和终端仿真
- CMSIS-DAPv2 WinUSB（无需驱动的厂商特定批量传输） - 符合CMSIS标准的调试通道
- CMSIS-DAPv1 HID - 符合 CMSIS 标准的调试通道
- WebUSB CMSIS-DAP HID - 符合CMSIS标准的调试通道

更多功能正在规划中，并将逐步推出。该项目由Arm、其合作伙伴、众多硬件供应商及全球开源社区持续进行高强度开发。DAPLink已取代mbed CMSIS-DAP接口固件项目。欢迎自由使用及贡献。祝使用愉快！

更多可用性信息请 [参见用户指南。](https://github.com/ARMmbed/DAPLink/blob/main/docs/USERS-GUIDE.md)

## 兼容性

许多基于ARM微控制器的硬件接口电路（HIC）均可运行DAPLink接口固件。这些电路既可作为独立调试板使用，也可作为开发套件的一部分。已知I/O兼容的部分品牌电路包括：

- [基于 MAX32625 的 Maxim Integrated MAX32625PICO](https://www.maximintegrated.com/en/products/microcontrollers/MAX32625PICO.html)
- 新唐科技Nu-Link2-Me（基于M48SSIDAE）
- [恩智浦LPC-Link2（基于LPC11U35或LPC4322）](https://www.nxp.com/support/developer-resources/hardware-development-tools/lpcxpresso-boards:LPCXPRESSO-BOARDS)
- [恩智浦MCU-LINK（基于LPC55xx）](https://www.nxp.com/design/microcontrollers-developer-resources/mcu-link-debug-probe:MCU-LINK)
- [恩智浦OpenSDA（基于K20、K22、KL26Z和KL27Z）](http://www.nxp.com/products/software-and-tools/run-time-software/kinetis-software-and-tools/ides-for-kinetis-mcus/opensda-serial-and-debug-adapter:OPENSDA)
- [基于Atmel SAM3U的Segger J-Link OB](https://www.segger.com/products/debug-probes/j-link/models/j-link-ob/)
- [STMicroelectronics ST-LINK/V2（用于NUCLEO开发板），基于STM32F103CB](https://www.st.com/en/evaluation-tools/stm32-nucleo-boards.html)

有关所支持微控制器的更多信息，请 [点击此处](https://github.com/ARMmbed/DAPLink/blob/main/docs/hic/README.md) 。

## 发布版本

本仓库创建了许多板级构建（board = HIC + 目标组合）。季度发布将包含新功能和错误修复。独立的错误修复在报告、验证并修复后发布。季度发布和错误修复发布都会导致构建号递增。许多开发套件和产品都配备了 DAPLink 接口固件，或者能够运行 DAPLink 固件。 **[当前的发布构建和更新 DAPLink 接口固件的说明托管在 DAPLink 发布网站上。](https://daplink.io/)** 发布说明和以前的发布构建可在 GitHub 发布页面找到。

## 贡献指南

我们欢迎对 DAPLink 的任何领域做出贡献。寻找感兴趣的功能或缺陷，请关注 [问题列表](https://github.com/ARMmbed/DAPLink/issues) 。在 [讨论区](https://github.com/ARMmbed/DAPLink/discussions) 或 [Slack](https://join.slack.com/t/pyocd/shared_invite/zt-zqjv6zr5-ZfGAXl_mFCGGmFlB_8riHA) 上发起新话题，与开发者和维护者互动。

请参阅 [贡献指南](https://github.com/ARMmbed/DAPLink/blob/main/CONTRIBUTING.md) 了解详细的贡献要求。

如需报告错误，请在GitHub项目中 [创建问题](https://github.com/ARMmbed/DAPLink/issues/new) 。

## 开发

[可以在开发者指南中](https://github.com/ARMmbed/DAPLink/blob/main/docs/DEVELOPERS-GUIDE.md) 找到关于搭建开发环境、运行测试或创建发布版本的信息。

## 许可证

DAPLink 采用宽松的 Apache 2.0 许可证。详见 [LICENSE](https://github.com/ARMmbed/DAPLink/blob/main/LICENSE) 文件以获取许可证全文。

版权所有 © 2006-2023 Arm Ltd