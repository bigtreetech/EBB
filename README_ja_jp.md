# [View English version](./README.md)
# [切换到中文版](./README_zh_cn.md)

# EBB36 & 42 CAN V1.0
## ハードウェア
* MCU: ARM Cortex-M0 STM32F072C8T6 48MHz with CAN bus
* ステッパードライバ: オンボードTMC2209 UARTモード, UARTアドレス: 00, Rsense: 0.11R
* オンボード加速度センサ: ADXL345
* オンボード温度IC: Max31865 DIPスイッチで2 / 4線PT100 / PT1000を選択 (Max31865なしバージョンにはこの機能はありません)
* 入力電圧: DC12V-DC24V 6A
* ロジック電圧: DC 3.3V
* 加熱インターフェース: ホットエンド (E0), 最大出力電流: 5A
* ファンインターフェース: 2つのCNCファン (FAN0, FAN1)
* ファンインターフェースの最大出力電流: 1A, ピーク値1.5A
* 拡張インターフェース: EndStop, I2C, Probe, RGB, PT100/PT1000, USBインターフェース, CANインターフェース
* 温度センサーインターフェースオプション: 1チャンネル100K NTCまたはPT1000(TH0), 1チャンネルPT100/PT1000
* USB通信インターフェース: USB-Type-C
* DC 5V最大出力電流: 1A

## ファームウェア
* 現在のところKlipperのみをサポートしています。

## ピン配置
* EBB36 CAN V1.0
  <br/><img src=EBB%20CAN%20V1.0%20(STM32F072)/EBB36%20CAN%20V1.0/Hardware/EBB36%20CAN%20V1.0-PIN.png width="800" /><br/>
* EBB42 CAN V1.0
  <br/><img src=EBB%20CAN%20V1.0%20(STM32F072)/EBB42%20CAN%20V1.0/Hardware/EBB42%20CAN%20V1.0-PIN.png width="800" /><br/>

## ファームウェアのビルド
1. 事前にコンパイルされたファームウェア (使用されたソースコードバージョンは [Commits on Nov 20, 2023](https://github.com/Klipper3d/klipper/commit/bb4711c5d31e8159945f945c662e6668059a174f))
   * [firmware_USB.bin](./EBB%20CAN%20V1.0%20(STM32F072)/firmware_USB.bin) USBを使用してラズベリーパイ / BTT Piと通信します。
   * [firmware_canbus.bin](./EBB%20CAN%20V1.0%20(STM32F072)/firmware_canbus.bin) CANバスを使用してラズベリーパイ / BTT Piと通信します, ボーレート = 1000K。

3. 自分でファームウェアをビルドする<br/>
   1. [klipperの公式インストール](https://www.klipper3d.org/Installation.html)を参照して、klipperのソースコードをラズベリーパイにダウンロードします
   2. 以下の設定で`Building the micro-controller`を行います。
      * [*] Enable extra low-level configuration options
      * Micro-controller Architecture = `STMicroelectronics STM32`
      * Processor model = `STM32F072`
      * IF USE CanBoot
         * Bootloader offset = `8KiB bootloader`
      * ELSE
         * Bootloader offset = `No bootloader`
      * Clock Reference = `8 MHz crystal`
      * IF USE USB
         * Communication interface = `USB (on PA11/PA12)`
      * ElSE IF USE CAN bus
         * Communication interface = `CAN bus (on PB8/PB9)`
         * `(1000000)` CAN bus speed

      <img src=Images/ebb_v10_menuconfig.png width="800" /><br/>
   3. 設定が選択されたら、`q`を押して終了し、保存するかどうか尋ねられたら"Yes"を選択します。
   4. `make`コマンドを実行します
   5. `make`コマンドが完了すると、`home/pi/kliiper/out`フォルダに`klipper.bin`ファイルが生成されます。そして、同じLAN内のWindowsコンピュータを使用して、CMDターミナルで`pscp`コマンドを使用してラズベリーパイからコンピュータに`klipper.bin`をコピーできます。例: `pscp -C pi@192.168.0.101:/home/pi/klipper/out/klipper.bin c:\klipper.bin`(ターミナルは`The server's host key is not cached`と表示し、`Store key in cache?((y/n)`と尋ねるかもしれません。`y`を入力して保存します。そして、パスワードを尋ねられたら、ラズベリーパイのデフォルトパスワード`raspberry`を入力します)

## board.cfgファイル
   * [sample-bigtreetech-ebb-canbus-v1.0.cfg](./EBB%20CAN%20V1.0%20(STM32F072)/sample-bigtreetech-ebb-canbus-v1.0.cfg) EBB36 & 42 CAN V1.0のすべての正しいピン配置が含まれています


# EBB36 & 42 CAN V1.1およびV1.2
## ハードウェア
* MCU: ARM Cortex-M0+ STM32G0B1CBT6 64MHz whit FDCAN bus
* その他のすべてのパラメータはEBB36 & 42 CAN V1.0と同じです

## ファームウェア
* 現在のところKlipperのみをサポートしています。

## ピン配置
* EBB36 CAN V1.1およびV1.2
  <br/><img src=EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)/EBB36%20CAN%20V1.1%20and%20V1.2/Hardware/EBB36%20CAN%20V1.1&V1.2-PIN.png width="800" /><br/>
* EBB42 CAN V1.1およびV1.2
  <br/><img src=EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)/EBB42%20CAN%20V1.1%20and%20V1.2/Hardware/EBB42%20CAN%20V1.1&V1.2-PIN.png width="800" /><br/>

## ファームウェアのビルド
1. 事前にコンパイルされたファームウェア (使用されたソースコードバージョンは [Commits on Nov 20, 2023](https://github.com/Klipper3d/klipper/commit/bb4711c5d31e8159945f945c662e6668059a174f))
   * [firmware_USB.bin](./EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)/firmware_USB.bin) USBを使用してラズベリーパイと通信します。
   * [firmware_canbus.bin](./EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)/firmware_canbus.bin) CANバスを使用してラズベリーパイと通信します, ボーレート = 1000K。

3. 自分でファームウェアをビルドする<br/>
   1. [klipperの公式インストール](https://www.klipper3d.org/Installation.html)を参照して、klipperのソースコードをラズベリーパイにダウンロードします
   2. 以下の設定で`Building the micro-controller`を行います。
      * [*] Enable extra low-level configuration options
      * Micro-controller Architecture = `STMicroelectronics STM32`
      * Processor model = `STM32G0B1`
      * IF USE CanBoot
         * Bootloader offset = `8KiB bootloader`
      * ELSE
         * Bootloader offset = `No bootloader`
      * Clock Reference = `8 MHz crystal`
      * IF USE USB
         * Communication interface = `USB (on PA11/PA12)`
      * ElSE IF USE CAN bus
         * Communication interface = `CAN bus (on PB0/PB1)`
         * `(1000000)` CAN bus speed

      <img src=Images/ebb_v11_menuconfig.png width="800" /><br/>
   3. 設定が選択されたら、`q`を押して終了し、保存するかどうか尋ねられたら"Yes"を選択します。
   4. `make`コマンドを実行します
   5. `make`コマンドが完了すると、`home/pi/kliiper/out`フォルダに`klipper.bin`ファイルが生成されます。そして、同じLAN内のWindowsコンピュータを使用して、CMDターミナルで`pscp`コマンドを使用してラズベリーパイからコンピュータに`klipper.bin`をコピーできます。例: `pscp -C pi@192.168.0.101:/home/pi/klipper/out/klipper.bin c:\klipper.bin`(ターミナルは`The server's host key is not cached`と表示し、`Store key in cache?((y/n)`と尋ねるかもしれません。`y`を入力して保存します。そして、パスワードを尋ねられたら、ラズベリーパイのデフォルトパスワード`raspberry`を入力します)

## ファームウェアの更新
### 警告: <br/>
(EBB 36/42 CAN V1.1のみ)<br/>
__STM32G0B1CBは、Type-Cポートを介してDFUを使用してファームウェアを更新する際に、システムメモリ領域にジャンプしてブートローダーを実行する必要があります (STMicroelectronicsによって書かれた)。マニュアル[AN2606](https://www.st.com/content/ccc/resource/technical/document/application_note/b9/9b/16/3a/12/1e/40/0c/CD00167594.pdf/files/CD00167594.pdf/jcr:content/translations/en.CD00167594.pdf)の説明を参照すると、このブートローダーの初期化プロセスは次の図のようになります:__
  <br/><img src=Images/AN2606.png width="800" /><br/>
__USB DFUモードに入る前に、USARTのIOが構成されます。__<br/>
__DFUモードに入った後、システムメモリ領域のブートローダーによってPA2が高レベルに構成されます。STM32G0B1CBの[データシート](https://www.st.com/resource/en/datasheet/stm32g0b1cb.pdf)を参照してください。__
  <br/><img src=Images/G0B1_DS.png width="800" /><br/>
__PA2はEBB36 & 42 CAN V1.1でホットエンドMOSFETに使用されます。DFUモードの高レベルはホットエンドを加熱状態に変更します。したがって、Type-CポートのDFUを使用してファームウェアを更新する際には、ホットエンドの主電源VINを切断するか、ファームウェアの更新がすぐに完了して通常の動作モードに移行することを確認してください。主電源とホットエンドが接続されている状態でMCUを長時間DFUモードに保つことは絶対に避けてください。__

## board.cfgファイル
   * [sample-bigtreetech-ebb-canbus-v1.1.cfg](./EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)/sample-bigtreetech-ebb-canbus-v1.1.cfg) EBB CAN 36&42 V1.1のすべての正しいピン配置が含まれています

# EBB36 & 42 CAN V1.2
__V1.2 compared with v1.1: only the IO of hotend is changed from `PA2` to `PB13`__

## board.cfgファイル
   * [sample-bigtreetech-ebb-canbus-v1.2.cfg](./EBB%20CAN%20V1.1%20and%20V1.2%20(STM32G0B1)/sample-bigtreetech-ebb-canbus-v1.2.cfg) EBB CAN 36&42 V1.2のすべての正しいピン配置が含まれています

# EBB SB2240_2209 CAN V1.0
## ハードウェア
* MCU: ARM Cortex-M0+ STM32G0B1CBT6 64MHz whit FDCAN bus
* ステッパードライバ:
   * TMC2209バージョン: オンボードTMC2209 UARTモード, UARTアドレス: 00, Rsense: 0.11R
   * TMC2240バージョン: オンボードTMC2240 SPIモード
* オンボード加速度センサ: ADXL345
* オンボード温度IC: Max31865 DIPスイッチで2 / 4線PT100 / PT1000を選択
* 入力電圧: DC12V-DC24V 9A
* ロジック電圧: DC 3.3V
* 加熱インターフェース: ホットエンド (E0), 最大出力電流: 5A
* ファンインターフェース:
   * 2 x CNCファン (FAN1, FAN2)
   * 1 x 4線ファン (4W_FAN)
* ファンインターフェースの最大出力電流: 1A, ピーク値1.5A
* 拡張インターフェース: EndStop, Bltouch, Proximity(NPN & PNP), RGB, PT100/PT1000, USB, CAN, SPI
* 温度センサーインターフェースオプション: 1チャンネル100K NTCまたはPT1000(TH0), 1チャンネルPT100/PT1000 (Max31865)
* USB通信インターフェース: USB-Type-C
* DC 5V最大出力電流: 1A

## ファームウェア
* 現在のところKlipperのみをサポートしています。

## ピン配置
* EBB SB2240 CAN V1.0
  <br/><img src=EBB%20SB2240_2209%20CAN/SB2240/Hardware/SB2240.png width="800" /><br/>
* EBB SB2209 CAN V1.0
  <br/><img src=EBB%20SB2240_2209%20CAN/SB2209/Hardware/SB2209.png width="800" /><br/>

## ファームウェアのビルド
1. 事前にコンパイルされたファームウェア (使用されたソースコードバージョンは [Commits on Jan 8, 2023](https://github.com/Klipper3d/klipper/commit/bca2671efb8ae6035bb8600619b7a7c4e76169c3))
   * [firmware_USB.bin](./EBB%20SB2240_2209%20CAN/firmware_USB.bin) USBを使用してホストと通信します。
   * [firmware_canbus.bin](./EBB%20SB2240_2209%20CAN/firmware_canbus.bin) CANバスを使用してホストと通信します, ボーレート = 1M。
   * [firmware_canbus_8k_bootloader.bin](./EBB%20SB2240_2209%20CAN/firmware_canbus_8k_bootloader.bin) CANバスを使用してホストと通信します, ボーレート = 1M, 8KBブートローダーはCanboot用です。

3. 自分でファームウェアをビルドする<br/>
   1. [klipperの公式インストール](https://www.klipper3d.org/Installation.html)を参照して、klipperのソースコードをホストにダウンロードします
   2. 以下の設定で`Building the micro-controller`を行います。
      * [*] Enable extra low-level configuration options
      * Micro-controller Architecture = `STMicroelectronics STM32`
      * Processor model = `STM32G0B1`
      * IF USE CanBoot
         * Bootloader offset = `8KiB bootloader`
      * ELSE
         * Bootloader offset = `No bootloader`
      * Clock Reference = `8 MHz crystal`
      * IF USE USB
         * Communication interface = `USB (on PA11/PA12)`
      * ElSE IF USE CAN bus
         * Communication interface = `CAN bus (on PB0/PB1)`
      * (1000000) CAN bus speed

      <img src=Images/ebb_v11_menuconfig.png width="800" /><br/>
   3. 設定が選択されたら、`q`を押して終了し、保存するかどうか尋ねられたら"Yes"を選択します。
   4. `make`コマンドを実行します
   5. `make`コマンドが完了すると、`home/pi/kliiper/out`フォルダに`klipper.bin`ファイルが生成されます。そして、同じLAN内のWindowsコンピュータを使用して、CMDターミナルで`pscp`コマンドを使用してホストからコンピュータに`klipper.bin`をコピーできます。例: `pscp -C pi@192.168.0.101:/home/pi/klipper/out/klipper.bin c:\klipper.bin`(ターミナルは`The server's host key is not cached`と表示し、`Store key in cache?((y/n)`と尋ねるかもしれません。`y`を入力して保存します。そして、パスワードを尋ねられたら、ラズベリーパイのデフォルトパスワード`raspberry`またはCB1のパスワード`biqu`を入力します)

## board.cfgファイル
   * [sample-bigtreetech-ebb-sb-canbus-v1.0.cfg](./EBB%20SB2240_2209%20CAN/sample-bigtreetech-ebb-sb-canbus-v1.0.cfg) EBB SB2240_2209 CAN V1.0のすべての正しいピン配置が含まれています
   * TMC2209バージョン: tmc2209の設定をコメント解除し、tmc2240の設定をコメントアウトします
      ```
      [tmc2209 extruder]
      uart_pin: EBBCan: PA15
      run_current: 0.650
      stealthchop_threshold: 999999

      # [tmc2240 extruder]
      # cs_pin: EBBCan: PA15
      # spi_software_sclk_pin: EBBCan: PB10
      # spi_software_mosi_pin: EBBCan: PB11
      # spi_software_miso_pin: EBBCan: PB2
      # run_current: 0.650
      # stealthchop_threshold: 999999
      ```
   * TMC2240バージョン: tmc2240の設定をコメント解除し、tmc2209の設定をコメントアウトします
      ```
      # [tmc2209 extruder]
      # uart_pin: EBBCan: PA15
      # run_current: 0.650
      # stealthchop_threshold: 999999

      [tmc2240 extruder]
      cs_pin: EBBCan: PA15
      spi_software_sclk_pin: EBBCan: PB10
      spi_software_mosi_pin: EBBCan: PB11
      spi_software_miso_pin: EBBCan: PB2
      driver_TPFD: 0
      run_current: 0.650
      stealthchop_threshold: 999999
      ```

# 注意
## ここはBIGTREETECHです！ メーカーのために、メーカーによって！
* BIGTREETECHへのすべてのサポートに感謝します！ すべてのメーカーに優れた創造体験を提供するために、私たちは高品質で耐久性のあるアクセサリの設計と製造に専念しています！

## 連絡方法:
### 技術的な問題がある場合は、遠慮なくお問い合わせください:
* BIGTREETECH: service004@biqu3d.com

### 最新情報を入手するためにソーシャルメディアでフォローしてください:
* Facebook: https://www.facebook.com/BIGTREETECH/
* Twitter: https://twitter.com/BigTreeTech
* Instagram: https://www.instagram.com/bigtreetech_official/
* 公式サイト: https://bigtree-tech.com/

## 購入リンク:
https://www.biqu.equipment/products/bigtreetech-ebb-36-42-can-bus-for-connecting-klipper-expansion-device
