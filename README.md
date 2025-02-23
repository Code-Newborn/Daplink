### DIY DapLink

1. 编译Daplink源码获得对应硬件的Bootloader程序和Application程序（stm32f103xb_bl.hex和stm32f103xb_stm32f103rb_if.hex），通过`J-Flash V8.10`软件可以将两个hex文件合并输出为bin文件
2. Daplink调试器引脚分配说明

| stm32f103c8t6芯片引脚 | DapLink调试器分配功能 | 备注                    | 所在文件                                       |
| --------------------- | --------------------- | ----------------------- | ---------------------------------------------- |
| PA9                   | LED_DAP               | 指示LED                 | .\source\hic_hal\stm32\stm32f103xb\IO_Config.h |
| PA13                  | SWDIO                 | SWD烧录                 | .\source\hic_hal\stm32\stm32f103xb\IO_Config.h |
| PA14                  | SWCLK                 | SWD烧录                 | .\source\hic_hal\stm32\stm32f103xb\IO_Config.h |
| PB0                   | nRESET_PIN            | 输出复位信号（U盘烧录） | .\source\hic_hal\stm32\stm32f103xb\IO_Config.h |

3. 为DapLink调试器烧录固件bin（使用`STM32 ST-LINK Utility`软件和`st-link`调试器）：

&emsp;&emsp;**Connect to the target**连接到DapLink调试器，打开**Binary file**，点击**program verify**进行固件烧录，至此完成Daplink调试器制作，可以用于其他开发板的调试工作。

4. 擦除DapLink调试器固件，恢复成开发板（使用`STM32 ST-LINK Utility`软件和`st-link`调试器）：

&emsp;&emsp;**Target→Settings→Mode: Connect under reset **设置复位模式下可以连接已烧录bin固件的板子，按下reset点击connect，松开后连接成功，点击**Full chip erase**可用于擦除固件。

​	或者采用另外一种方式将其恢复正常的开发板，就需要`boot0`跳线帽接3.3V上电，进行下载正常开发板程序，还原跳线帽就可以了



**下面是官方源码介绍**

------

[![DAPLink](/docs/images/daplink-website-logo-link.png)](https://daplink.io/)

[![Linux Build (main)](https://github.com/ARMmbed/DAPLink/actions/workflows/linux.yml/badge.svg?branch=main)](https://github.com/ARMmbed/DAPLink/actions/workflows/linux.yml)
[![Linux Build (develop)](https://github.com/ARMmbed/DAPLink/actions/workflows/linux.yml/badge.svg?branch=develop)](https://github.com/ARMmbed/DAPLink/actions/workflows/linux.yml)
[![Join us on Slack](https://img.shields.io/static/v1?label=Slack&color=4A154B&logo=slack&style=social&message=Join%20us%20on%20Slack)](https://join.slack.com/t/pyocd/shared_invite/zt-zqjv6zr5-ZfGAXl_mFCGGmFlB_8riHA)

----

Arm Mbed DAPLink is an open-source software project that enables programming and debugging application software running on Arm Cortex CPUs. Commonly referred to as interface firmware, DAPLink runs on a secondary MCU that is attached to the SWD or JTAG port of the application MCU. This configuration is found on nearly all development boards. Enumerating as a USB composite device, it creates a bridge between your development computer and the CPU debug access port. DAPLink enables developers with:

* MSC - drag-n-drop programming flash memory
* CDC - virtual com port for log, trace and terminal emulation
* CMSIS-DAPv2 WinUSB (driver-less vendor-specific bulk) - CMSIS compliant debug channel
* CMSIS-DAPv1 HID - CMSIS compliant debug channel
* WebUSB CMSIS-DAP HID - CMSIS compliant debug channel

More features are planned and will show up gradually over time. The project is constantly under heavy development by Arm, its partners, numerous hardware vendors and the open-source community around the world. DAPLink has superseded the mbed CMSIS-DAP interface firmware project. You are free to use and contribute. Enjoy!

For more detailed usability information [see the users guide.](docs/USERS-GUIDE.md)

## Compatibility
There are many ARM microcontroller-based Hardware Interface Circuits (HICs) that DAPLink interface firmware runs on. These can be found as standalone boards (debugger) or as part of a development kit. Some branded circuits that are known to be IO compatible are:

* [Maxim Integrated MAX32625PICO based on MAX32625](https://www.maximintegrated.com/en/products/microcontrollers/MAX32625PICO.html)
* Nuvoton Nu-Link2-Me based on M48SSIDAE
* [NXP LPC-Link2 based on LPC11U35 or LPC4322](https://www.nxp.com/support/developer-resources/hardware-development-tools/lpcxpresso-boards:LPCXPRESSO-BOARDS)
* [NXP MCU-LINK on LPC55xx](https://www.nxp.com/design/microcontrollers-developer-resources/mcu-link-debug-probe:MCU-LINK)
* [NXP OpenSDA based on K20, K22, KL26Z and KL27Z](http://www.nxp.com/products/software-and-tools/run-time-software/kinetis-software-and-tools/ides-for-kinetis-mcus/opensda-serial-and-debug-adapter:OPENSDA)
* [Segger J-Link OB based on Atmel SAM3U](https://www.segger.com/products/debug-probes/j-link/models/j-link-ob/)
* [STMicroelectronics ST-LINK/V2 (on NUCLEO boards) based on STM32F103CB](https://www.st.com/en/evaluation-tools/stm32-nucleo-boards.html)

You can find more information on the microcontrollers supported [here](docs/hic/README.md).

## Releases
There are many board builds (board = HIC + target combination) created from this repository. Quarterly releases will contain new features and bugfixes. Standalone bugfixes are released once reported, verified and fixed. Both quarterly and bugfix releases will result in the build number being incremented. Many development kits and products ship with DAPLink interface firmware or are capable of running DAPLink firmware. **[The current release builds and instructions for updating DAPLink interface firmware is hosted on the DAPLink release site.](https://daplink.io/)** Release notes and previous release builds can be found under GitHub releases.

## Contribute

We welcome contributions to DAPLink in any area. Look for an interesting feature or defect
[under issues](https://github.com/ARMmbed/DAPLink/issues). Start a new thread [in the
discussions](https://github.com/ARMmbed/DAPLink/discussions) or
[in Slack](https://join.slack.com/t/pyocd/shared_invite/zt-zqjv6zr5-ZfGAXl_mFCGGmFlB_8riHA)
to engage with the developers and maintainers.

Please see the [contribution guidelines](CONTRIBUTING.md) for detailed requirements for
contributions.

To report bugs, please [create an issue](https://github.com/ARMmbed/DAPLink/issues/new) in the
GitHub project.

## Develop
Information for setting up a development environment, running the tests or creating a release build [can be found in the developers guide.](docs/DEVELOPERS-GUIDE.md)

## License
DAPLink is licensed with the permissive Apache 2.0 license. See the [LICENSE](LICENSE) file for the
full text of the license.

Copyright © 2006-2023 Arm Ltd
