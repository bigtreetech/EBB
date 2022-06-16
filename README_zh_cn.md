# [View English version](./README.md)

# EBB36 & 42 CAN V1.0
## 硬件参数
* 微处理器：ARM Cortex-M0 STM32F072C8T6 48MHz 带 CAN 总线
* 电机驱动：板载 UART 模式 TMC2209, 硬件地址：00，Rsense：0.11R
* 板载加速度传感器：ADXL345
* 板载温度传感器IC：Max31865 可设置 2 / 4 线 PT100 / PT1000 （无Max31865版本无此功能）
* 输入电压：DC12V-DC24V 6A
* 逻辑电压：DC 3.3V
* 加热接口：加热棒（E0）， 最大输出电流： 5A
* 风扇接口：两个数控风扇（FAN0， FAN1）
* 风扇接口最大输出电流： 1A，峰值 1.5A
* 拓展接口：EndStop， I2C， Probe， RGB， PT100/PT1000， USB 接口， CAN 接口
* 温度传感器接口：1 路 100K NTC 或者 PT1000（TH0）， 1 路 PT100/PT1000 可选
* USB 通信接口：USB-Type-C
* DCDC 5V 输出最大电流： 1

## 固件支持
* 此产品当前仅支持 Klipper 固件

## Pin 脚说明
* EBB36 CAN V1.0
  <br/><img src=EBB%20CAN%20V1.0%20(STM32F072)/EBB36%20CAN%20V1.0/Hardware/EBB36%20CAN%20V1.0-PIN.png width="800" /><br/>
* EBB42 CAN V1.0
  <br/><img src=EBB%20CAN%20V1.0%20(STM32F072)/EBB42%20CAN%20V1.0/Hardware/EBB42%20CAN%20V1.0-PIN.png width="800" /><br/>

## 编译固件
1. 已编译好直接使用的文件(此二进制文件所使用的源码是 [Commits on May 18, 2022](https://github.com/Klipper3d/klipper/commit/996b73e25d00c5aa5d740b8f2d53c78ef9919401))
   * [firmware_USB.bin](./EBB%20CAN%20V1.0%20(STM32F072)/firmware_USB.bin) 使用 USB 与树莓派通信。
   * [firmware_canbus.bin](./EBB%20CAN%20V1.0%20(STM32F072)/firmware_canbus.bin) 使用 CAN 总线与树莓派通信, 波特率250K。

3. 自行编译最新版本的固件<br/>
   1. 参考 [klipper官方的安装说明](https://www.klipper3d.org/Installation.html) 下载klipper源码到树莓派
   2. 使用下面的配置去编译固件
      * [*] Enable extra low-level configuration options
      * Micro-controller Architecture = `STMicroelectronics STM32`
      * Processor model = `STM32F072`
      * Bootloader offset = `No bootloader`
      * Clock Reference = `8 MHz crystal`
      * 如果使用 USB 与树莓派通信
         * Communication interface = `USB (on PA11/PA12)`
      * 如果使用 CAN 总线与树莓派通信
         * Communication interface = `CAN bus (on PB8/PB9)`

      <img src=Images/ebb_v10_menuconfig.png width="800" /><br/>
   3. 配置选择完成后, 输入 `q` 退出配置界面，当询问是否保存配置是选择 "Yes" .
   4. 输入 `make` 命令开始编译固件
   5. 当 `make` 命令执行完成后，会在树莓派的`home/pi/kliiper/out`的文件夹中生成我们所需要的`klipper.bin`固件。你可以在CMD命令行终端中通过`pscp`命令把`klipper.bin`固件复制到与树莓派在同一个局域网下的电脑上。例如 `pscp -C pi@192.168.0.101:/home/pi/klipper/out/klipper.bin c:\klipper.bin`(命令行会提示 `The server's host key is not cached` 并且询问 `Store key in cache?((y/n)`, 输入 `y` 保存 host key，然后输入树莓派默认的密码：`raspberry`)

## 配置文件
   * [sample-bigtreetech-ebb-canbus-v1.0.cfg](./EBB%20CAN%20V1.0%20(STM32F072)/sample-bigtreetech-ebb-canbus-v1.0.cfg) 提供了 EBB36 & 42 CAN V1.0 的所有 pinout 配置


# EBB36 & 42 CAN V1.1
## 硬件参数
* 微处理器：ARM Cortex-M0+ STM32G0B1CBT6 64MHz 带 FDCAN 总线
* 其他的所有参数与 EBB36 & 42 CAN V1.0 相同

## 固件支持
* 此产品当前仅支持 Klipper 固件

## Pin 脚说明
* EBB36 CAN V1.1
  <br/><img src=EBB%20CAN%20V1.1%20(STM32G0B1)/EBB36%20CAN%20V1.1/Hardware/EBB36%20CAN%20V1.1&V1.2-PIN.png width="800" /><br/>
* EBB42 CAN V1.1
  <br/><img src=EBB%20CAN%20V1.1%20(STM32G0B1)/EBB42%20CAN%20V1.1/Hardware/EBB42%20CAN%20V1.1&V1.2-PIN.png width="800" /><br/>

## 编译固件
1. 已编译好直接使用的文件(此二进制文件所使用的源码是 [Commits on May 18, 2022](https://github.com/Klipper3d/klipper/commit/996b73e25d00c5aa5d740b8f2d53c78ef9919401))
   * [firmware_USB.bin](./EBB%20CAN%20V1.1%20(STM32G0B1)/firmware_USB.bin) 使用 USB 与树莓派通信。
   * [firmware_canbus.bin](./EBB%20CAN%20V1.1%20(STM32G0B1)/firmware_canbus.bin) 使用 CAN 总线与树莓派通信, 波特率250K。

3. 自行编译最新版本的固件<br/>
   __注意：在[STM32G0B1 CAN PR](https://github.com/Klipper3d/klipper/pull/5488)合并到Klipper主分支之前，官方的固件是不支持STM32G0B1的CAN bus功能的。如果使用CANBus通信，可以使用我们github上编译好的[firmware_canbus.bin](./EBB%20CAN%20V1.1%20(STM32G0B1)/firmware_canbus.bin) 固件，或者使用我们的源码自行编译 https://github.com/bigtreetech/klipper/tree/stm32g0b1-canbus__ <br/>
   __使用USB通信则无需此操作，Klipper官方主分支支持STM32G0B1的USB端口__
   1. 参考 [klipper官方的安装说明](https://www.klipper3d.org/Installation.html) 下载klipper源码到树莓派
   2. 使用下面的配置去编译固件
      * [*] Enable extra low-level configuration options
      * Micro-controller Architecture = `STMicroelectronics STM32`
      * Processor model = `STM32G0B1`
      * Bootloader offset = `No bootloader`
      * Clock Reference = `8 MHz crystal`
      * 如果使用 USB 与树莓派通信
         * Communication interface = `USB (on PA11/PA12)`
      * 如果使用 CAN 总线与树莓派通信
         * Communication interface = `CAN bus (on PB0/PB1)`

      <img src=Images/ebb_v11_menuconfig.png width="800" /><br/>
   3. 配置选择完成后, 输入 `q` 退出配置界面，当询问是否保存配置是选择 "Yes" .
   4. 输入 `make` 命令开始编译固件
   5. 当 `make` 命令执行完成后，会在树莓派的`home/pi/kliiper/out`的文件夹中生成我们所需要的`klipper.bin`固件。你可以在CMD命令行终端中通过`pscp`命令把`klipper.bin`固件复制到与树莓派在同一个局域网下的电脑上。例如 `pscp -C pi@192.168.0.101:/home/pi/klipper/out/klipper.bin c:\klipper.bin`(命令行会提示 `The server's host key is not cached` 并且询问 `Store key in cache?((y/n)`, 输入 `y` 保存 host key，然后输入树莓派默认的密码：`raspberry`)

## 配置文件
   * [sample-bigtreetech-ebb-canbus-v1.1.cfg](./EBB%20CAN%20V1.1%20(STM32G0B1)/sample-bigtreetech-ebb-canbus-v1.1.cfg) 提供了 EBB CAN 36&42 V1.1 的所有 pinout 配置

# EBB36 & 42 CAN V1.2
__V1.2 在 v1.1 基础上: 只把加热棒的 IO 从 `PA2` 修改为 `PB13`__

## 配置文件
   * [sample-bigtreetech-ebb-canbus-v1.2.cfg](./EBB%20CAN%20V1.1%20(STM32G0B1)/sample-bigtreetech-ebb-canbus-v1.2.cfg) 提供了 EBB CAN 36&42 V1.2 的所有 pinout 配置

## 固件更新
### 注意：<br/>
(只有 EBB 36/42 CAN V1.1 需要注意此问题)<br/>
__通过Type-C端口使用DFU更新固件时，STM32G0B1CB需要跳转到System memory区域执行Bootloader程序(STMicroelectronics出厂写死的)__<br/>
__参考手册[AN2606](https://www.st.com/content/ccc/resource/technical/document/application_note/b9/9b/16/3a/12/1e/40/0c/CD00167594.pdf/files/CD00167594.pdf/jcr:content/translations/en.CD00167594.pdf)中的描述，此Bootloader的初始化流程如下图所示：__
  <br/><img src=Images/AN2606.png width="800" /><br/>
__在进入USB DFU模式之前，还会初始化USART的IO。__<br/>
__参考[STM32G0B1CB数据手册](https://www.st.com/resource/en/datasheet/stm32g0b1cb.pdf)中的描述，进入DFU模式后，PA2引脚会被System memory区域中的Bootloader配置输出高电平。__
  <br/><img src=Images/G0B1_DS.png width="800" /><br/>
__PA2 在 EBB36 & 42 CAN V1.1中被用于加热棒端口，进入DFU模式后的高电平会让加热棒处于加热状态，所以在使用Type-C端口的DFU更新固件时，请注意断开加热棒的主电源Vin或者确保固件很快更新完成，并进入正常工作的模式。万不可在主电源和加热棒都接好的情况下，使MCU长时间处于DFU模式。__


# Note
## Here’s BIGTREETECH! For Makers, by makers!
* We appreciate all of your support to BIGTREETECH! To offer an excellent experience of creation to every makers,We’re devoted to design and produce high-quality and durable accessories!

## How to contact:
### If you have any technical issue,please don’t hesitate contact us:
* BIGTREETECH: service004@biqu3d.com

### Follow us on social media to get more news:
* Facebook: https://www.facebook.com/BIGTREETECH/
* Twitter: https://twitter.com/BigTreeTech
* Instagram: https://www.instagram.com/bigtreetech_official/
* Official Site: https://bigtree-tech.com/

## Purchase link:
https://www.biqu.equipment/products/bigtreetech-ebb-36-42-can-bus-for-connecting-klipper-expansion-device
