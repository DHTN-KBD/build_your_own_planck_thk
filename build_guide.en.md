# Build your own Planck Through Hole Kit

![Planck THK](https://i.imgur.com/O8qh1Vv.jpg)

This guide describes about how to build keyboard and flash firmware.

## Overview

### Preparation
- Check parts

### Hardware
1. USB port
1. Diodes
1. LED
1. Resistors
1. Crystal
1. Capacitors
1. Regulator
1. Speaker
1. DIP switch
1. Reset switch
1. MCU socket
1. PH connector
1. JTAG header and ISP header
1. Rotary encoders
1. Solder keyswitch for ESC key
1. Test
1. Solder rest of keyswitches
1. Screws and spacers

### Software - How to build and flash custom firmware
1. Firmware and bootloader
1. Build bootloader
1. Flash bootloader
1. Modify fuse-bit
1. Build firmware
1. Flash firmware
1. Create custom keymap


## 準備

### パーツの確認

![Parts](https://i.imgur.com/90f6Xw5.jpg)

パーツを[Planck Through Hole Kit自作キット \- ⌁DHTN⌁](https://dhtn.booth.pm/items/1073162)で入手した場合は、以下のように分類されています。

- 基板2枚
- 袋A(銀) - マイクロコントローラー(MCU)
- 袋B(赤) - ネジ、スペーサー、クッションゴム
- 袋C(赤) - ロータリーエンコーダー
- 袋D(赤) - ソケット、ヘッダピン、コネクタ、スイッチ類
- 袋E(赤) - ダイオード
- 袋F(赤) - 抵抗、コンデンサ、クリスタル、LED、レギュレーター

自分で各パーツを調達した場合には以降を適宜読み替えてください。

それぞれの分類に含まれる個別のパーツは以下のとおりです。

### 基板2枚

![PCB](https://i.imgur.com/eLqk6XM.jpg)

| パーツ名 | 数量 |
| ---- | ---- |
| トッププレート用基板(黒) | 1 |
| ボトムプレート用基板(マットブラック) | 1 |

※マットブラックのボトムプレートは製造工程で多少の擦り傷がついている場合があります

### 袋A

![MCU](https://i.imgur.com/GWmpFJM.jpg)

| パーツ名 | 基板上の対応位置 | 数量 |
| ---- | ---- | ---- |
| ATmega32A | MICROCONTROLLER | 1 |

### 袋B

![Screws](https://i.imgur.com/0OVf1Zm.jpg)

| パーツ名 | 数量 |
| ---- | ---- |
| M2黒ナベネジ 4mm | 20 |
| M2ステンレススペーサー 5mm | 10 |
| クッションゴム | 4 |

### 袋C

![Rotary Encoders](https://i.imgur.com/F3mr80b.jpg)

| パーツ名 | 基板上の対応位置 | 数量 |
| ---- | ---- | ---- |
| ロータリーエンコーダー | ENCODERS | 2 |

### 袋D

![Sockets](https://i.imgur.com/c06ivUG.jpg)

| パーツ名 | 基板上の対応位置 | 数量 |
| ---- | ---- | ---- |
| MCUソケット 40ピン | MICROCONTROLLER | 1 |
| DIPスイッチ | DIP SWITCH | 1 |
| 圧電スピーカー | SPEAKER | 1 |
| USBコネクタ | USB PORT | 1 |
| PHコネクタ | ALT USB PORT | 1 |
| ピンヘッダ 2×5 | JTAG HEADER | 1 |
| ピンヘッダ 2×3 | ISP HEADER | 1 |
| タクトスイッチ | RESET | 1 |

### 袋E

![Diodes](https://i.imgur.com/icw75zz.jpg)

| パーツ名 | 基板上の対応位置 | 数量 |
| ---- | ---- | ---- |
| ダイオード | D1〜D48 | 50 (予備2個含む) |

### 袋F

![Parts](https://i.imgur.com/jagOLm9.jpg)

| パーツ名 | 基板上の対応位置 | 数量 | 備考 |
| ---- | ---- | ---- | ---- |
| カーボン抵抗 68Ω | R1, R2, R4, R5 | 4 | 青灰黒金 |
| カーボン抵抗 1.5Ω | R3 | 1 | 茶緑赤金 |
| レギュレーター | POWER REGULATOR | 1 | |
| セラミックコンデンサ 20pF | C1, C2 | 2 | |
| 積層セラミックコンデンサ 22pF | C1, C2 | 2 | 20pFのものとどちらかを選んで使う |
| 積層セラミックコンデンサ 0.1uF | C3 | 1 | |
| 積層セラミックコンデンサ 4.7uF | C4 | 1 | |
| クリスタル(水晶発振子) | Y1 | 1 | |
| 赤色LED | PWR | 1 | |
| 緑色LED | ACT | 1 | |

C1およびC2に使うコンデンサには以下の2種類を封入してあります。

- 静電容量20pFのセラミックコンデンサ 2個
   - 容量はPlanck THK作者のJack Humbert氏の設計および基板上の表示通り
   - ただしノーブランド品なので静電容量以外の詳細は不明
- 静電容量22pFの積層セラミックコンデンサ 2個
   - 容量は20pFよりも大きいが、ATmega32Aのデータシートでは12〜22pFがクリスタル用推奨コンデンサ容量として挙げられているため問題ないと考えられる
   - 村田製作所のものなのでスペックおよび品質は信頼できる

手元でそれぞれを使用したものを製作しましたが動作に違いはありませんでしたので、C1およびC2には上記を踏まえたうえでどちらかのコンデンサを使ってください。


## Hardware

Let's soldering parts on a PCB.

### 1. USB port

Solder the USB connector on `USB PORT` silk.

![USB1](https://i.imgur.com/hHKRVL0.jpg)

Since solder land for USB connector is so small and closes each other, be careful not to short (PCB version 0.1 improved this).

![USB2](https://i.imgur.com/SRa4vzi.jpg)

### 2. ダイオード

ダイオードを `D1` から `D48` まで48個はんだ付けします（セットには予備が含まれているため2個余ります）。極性があるので、写真のようにダイオードの黒い帯が基板の上になるように向きに注意してください。

![Diode1](https://i.imgur.com/UNsZqq2.jpg)

Planck THKは完成後もはんだ付けしたパーツ類が見える構造なので、できるだけ綺麗にはんだ付けしましょう。ダイオードは、以下の写真のように手頃なブレッドボードの側面を利用して脚を曲げるとジャストサイズでした。

![Diode2](https://i.imgur.com/AjNaMj9.jpg)

### 3. LED

赤色と緑色のLEDをそれぞれ `PWR` と `ACT` にはんだ付けします。

![LED1](https://i.imgur.com/IuVnN5Q.jpg)

脚にスルーホールから飛び出るぶんがあるため基板から少し浮くような形で取り付けることになります。はんだ付けの際に傾かないよう注意します。

![LED2](https://i.imgur.com/xHMAkXH.jpg)

### 4. 抵抗

まず、4本ある68Ω抵抗(青灰黒金)を`R1`、`R2`、`R4`、`R5`の箇所にはんだ付けします。

![Resistor1](https://i.imgur.com/kc8yU0T.jpg)

以下の写真のように、抵抗の脚は本体を出てすぐに曲げるくらいでないとうまく刺さらないので注意。

![Resistor2](https://i.imgur.com/JHdIeX0.jpg)

次に、1本だけの1.5kΩ抵抗(茶緑赤金)を`R3`の箇所にはんだ付けします。

![Resistor3](https://i.imgur.com/1d0beHM.jpg)

### 5. クリスタル

クリスタル(水晶発振子)を `Y1` の箇所にはんだ付けします。

![Crystal1](https://i.imgur.com/90QoaXM.jpg)

### 6. コンデンサ

前述のように20pFのセラミックコンデンサまたは22pFの積層セラミックコンデンサのいずれか2本を、クリスタル両側の `C1` および `C2` の箇所にはんだ付けします。

![Capacitors1](https://i.imgur.com/Vzg3fYJ.jpg)

以下は22pFの積層セラミックコンデンサを実装した場合。

![Capacitors2](https://i.imgur.com/U2QsIvv.jpg)

次に0.1uFの積層セラミックコンデンサを `C3` の箇所に、4.7uFの積層セラミックコンデンサを `C4` の箇所にそれぞれはんだ付けします。脚の幅が広い(5mm)ほうが4.7uF、狭い(2.54mm)ほうが0.1uFのもになります。

![Capacitors3](https://i.imgur.com/LNMcGuI.jpg)

4.7uFのコンデンサはあらかじめラジオペンチなどで脚を伸ばしてから、以下の写真のように幅を狭めておくとスルーホールに通しやすくなります。脚がホールに通りさえすれば、あとはカットしてしまうので多少不格好でも大丈夫です。

![Capacitors4](https://i.imgur.com/cyJolJi.jpg)

`C3` と `C4` への実装が完了すると以下のようになります。

![Capacitors5](https://i.imgur.com/Wc4JNTq.jpg)

### 7. レギュレーター

レギュレーターを `POWER REGULATOR` の箇所にはんだ付けします。

![Regulator1](https://i.imgur.com/w5i8tzi.jpg)

この際、スルーホールに差し込む前にラジオペンチなどで以下のように脚を直角に曲げておきます。

![Regulator2](https://i.imgur.com/d1XixLC.jpg)

### 8. スピーカー

圧電スピーカーを `SPEAKER` の箇所にはんだ付けします。

![Speaker](https://i.imgur.com/EsVRQg8.jpg)

極性はありませんが、スピーカーに「OK」の刻印があるのでこれを基板の向きと揃えるとよさそうです。

### 9. DIPスイッチ

DIPスイッチを `DIP SWITCH` の箇所に、写真のように左側に1〜4の数字がくるようにはんだ付けします。この基板で最もランドが小さいので注意してください。

![DIPSwitch](https://i.imgur.com/I2iqany.jpg)

### 10. リセットスイッチ

タクトスイッチを `RESET` の箇所にはんだ付けします。強く押し込むと基板と隙間なくはまります。

![ResetSwitch](https://i.imgur.com/PU8yE19.jpg)

### 11. MCUソケット

MCUソケットを `MICROCONTROLLER` の箇所にはんだ付けします。向きがありますので、以下の写真のように切り欠きが右側にくるようにして差し込みます。

![Socket1](https://i.imgur.com/qskeBOt.jpg)

以下は差し込んだ状態。

![Socket2](https://i.imgur.com/79gqS1N.jpg)

### 12. PHコネクタ

PHコネクタを `ALT USB PORT` の箇所にはんだ付けします。

![PH1](https://i.imgur.com/wPiVSy7.jpg)

※動作に必須ではないので、取り付けを省略することもできます。

### 13. JTAGヘッダおよびISPヘッダ

2×5ピンのピンヘッダを `JTAG HEADER` の箇所に、2×3ピンのピンヘッダを `ISP HEADER` の箇所にそれぞれはんだ付けします。

![Headers](https://i.imgur.com/fXCDt0Z.jpg)

※動作に必須ではないので、取り付けを省略することもできます。

### 14. ロータリーエンコーダー

ロータリーエンコーダー2個を `ENCODER 1` および `ENCODER 2` の箇所にはんだ付けします。はんだ付けの際に斜めになりやすいのでマスキングテープなどで固定するとよいです。

![Encoders](https://i.imgur.com/tVvt2F4.jpg)

※動作に必須ではないので、取り付けを省略することもできます。

### 15. ESCキー用のキースイッチをはんだ付け

動作確認に最低限必要な「ESCキー用のキースイッチ」のみをはんだ付けします。

Planckのデフォルトのキーマップでは「一番左の列の上から2個目のキー」がESCキーとなるため、この部分スイッチのみをまずはんだ付けします。以下の写真では `CTRL` キーが付いてる箇所です。

![ESCKey](https://i.imgur.com/n30Q2ge.jpg)

スイッチを1つはんだ付けしたら、動作確認を行います。

### 16. 動作確認

MCU(ATmega32A)をMCUソケットに差し込みます。向きがありますので、MCUの切り欠きがソケットと同じく右側にくるようにします。

DIPスイッチの1番のみをONの状態に切り替えてから(ファームウェアの起動成功時やキー押下時に音が鳴るようになるので確認に便利)、Planck THKをUSB mini-BケーブルでPCやMacと接続します。

正常に動作している場合はPWRの赤色LEDが点灯し、コンピューター側からは以下のように `HIDBoot` という名前のUSBデバイスとして認識されます(＝ブートローダーが起動した状態)。

![Test1](https://i.imgur.com/YvJ5iLG.png)

`HIDBoot` デバイスとして認識されている状態でESCキー(に相当するスイッチ)を押下すると、ACTの緑色LEDが点灯してスピーカーからPlanckの起動音が1回鳴ります。

ここでファームウェアの起動が成功すると、(前述のDIPスイッチ1番がONになっている場合はもう一度音が鳴ったうえで) `Planck` というUSBデバイスとして認識され、キーボードとして使用できる状態となります。

![Test2](https://i.imgur.com/8APAVjk.png)

現時点ではこのブートローダーからファームウェアへの切り替え動作が安定せず、起動音が鳴った後に `Planck` として認識されないことがあります。そのような場合は以下の手順を何度か繰り返すと、4の状態になります。

1. リセットスイッチを押してブートローダーを起動する
1. ESCキーを押下してファームウェアを起動する
1. 起動音が鳴る
1. (DIPスイッチ1番がONの場合は)さらに音が鳴り、`Planck` が認識される

この過程を実際に行っているところを動画にしてありますので、動作確認の参考にしてください。

- https://mobile.twitter.com/junya/status/1061641908139646976

この時点ではPlanckキーボードの `default` キーマップが適用されているので、キーアサインなどについては  [`keyboards/planck/keymaps/default`](https://github.com/qmk/qmk_firmware/blob/planck_thk/keyboards/planck/keymaps/default) を参考にしてください。また、左側のロータリーエンコーダーにはマウスホイールによるスクロールがアサイン済みとなっています。

**2018-12-06 追記**
上記の「ブートローダーからファームウェアへの切り替え動作が安定せず」の件は、ファームウェアのオーディオ機能を無効化することで安定して動作するようです。詳細については後述の「ファームウェアの起動を安定させる」の項目を参考にしてください。


### 17. 残りのキースイッチをはんだ付け

動作が確認できたら残りのキースイッチをはんだ付けしていきます。

![Switches](https://i.imgur.com/Tjywhap.jpg)

### 18. スペーサーをネジで固定

まず、ボトムプレートとなる基板の上に10個のスペーサーをネジで固定し、次にその上にトッププレートとなる基板を載せ、基板の表から10個のスペーサーに対してネジで固定します。

構造としては以下のようにスペーサーを上下の基板で挟む形になります。

```
[↓ネジ]
[トッププレート]
[スペーサー]
[ボトムプレート]
[↑ネジ]
```

最後にクッションゴム4個をボトムプレートの四隅に貼り付ければハードウェアの実装は完了です。🎉


## ソフトウェア (ユーザー向け) - How to flash custom firmware

この項目の内容は 2018-11-11 時点での

- [qmk/qmk_firmware の planck_thk ブランチ](https://github.com/qmk/qmk_firmware/tree/planck_thk)
- [olkb/planck_thk](https://github.com/olkb/planck_thk)

の内容を元にしています。

### 1. ファームウェアとブートローダーの関係 - Firmware and bootloader

Planck THKはブートローダーとして [bootloadHID](https://www.obdev.at/products/vusb/bootloadhid.html) (V-USB Projects
 Bootload HID) を利用しています。bootloadHIDの実装は `planck_thk` ブランチの [keyboards/planck/thk/bootloader](https://github.com/qmk/qmk_firmware/tree/planck_thk/keyboards/planck/thk/bootloader) 以下に用意されています。

電源投入時およびリセット時は常にブートローダーが起動して、ファームウェアの書き込み待機状態となります。書き込み待機状態でESCキーが押下されるとQMK Firmwareに制御が移り、Planckキーボードとしての動作が開始します。

キーマップのカスタマイズやDIPスイッチ、ロータリーエンコーダーの挙動を変更する際は、通常のQMK Firmware対応キーボードのカスタマイズと同様の手順で作業・ビルドを行います。

一方、ビルドしたファームウェアをブートローダー経由で書き込むためには、コンピューター側にもbootloadHIDの書き込みコマンドをインストールしてそれを利用する必要があります。

### 2. ファームウェアのビルド - Build firmware

#### planck_thk ブランチのチェックアウト - Checkout planck_thk branch

QMK FirmwareのPlanck THK対応ブランチは2018-11-11時点でまだ `master` へマージされていないため、以下のようにして `qmk/qmk_firmware` リポジトリの `planck_thk` ブランチをチェックアウトしておきます。

```console
$ git clone https://github.com/qmk/qmk_firmware.git
$ cd qmk_firmware
$ git checkout -b planck_thk origin/planck_thk

$ ls keyboards/planck/thk
README.md   bootloader  config.h    matrix.c    rules.mk    thk.c       thk.h       usbconfig.h
```

#### ビルド方法 - Build custom firmware

QMK FirmwareにおいてPlanck THKは `planck` キーボード内の1つのバリエーションとして定義されており(Planck rev6などの各リビジョンと同等)、

- ファームウェア: `keyboards/planck/thk` 以下
- キーマップ: `keyboards/planck/keymaps` 以下

という構成になっています。つまり、キーマップは `planck` キーボード全体と同じものを共有しています。

したがって、例えばPlanckのデフォルトキーマップを使ったファームウェアをビルドする方法は以下のようにQMKの標準的な方法と同様になります。

```console
$ make planck/thk:default
QMK Firmware 0.6.161

Making planck/thk with keymap default

avr-gcc (GCC) 7.3.0
Copyright (C) 2017 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

Size before:
   text	   data	    bss	    dec	    hex	filename
      0	  26088	      0	  26088	   65e8	.build/planck_thk_default.hex

Compiling: tmk_core/common/command.c                                                                [OK]
Linking: .build/planck_thk_default.elf                                                              [OK]
Creating load file for flashing: .build/planck_thk_default.hex                                      [OK]
Copying planck_thk_default.hex to qmk_firmware folder                                               [OK]
Checking file size of planck_thk_default.hex                                                        [OK]
 * The firmware size is fine - 26088/28672 (2584 bytes free)
```

ここで生成された `planck_thk_default.hex` がファームウェアとなり、これを bootloadHID を利用して書き込むことになります。

### 3. ファームウェアの書き込み

#### bootloadHID のインストール - Install bootloadHID to your host computer

前述のようにファームウェアの書き込みには、コンピューター側にも `bootloadHID` コマンドをインストールする必要があります。

macOSでHomebrewが利用できる場合のインストール手順は以下のようになります。

```console
$ brew cask install crosspack-avr
$ brew install --HEAD https://raw.githubusercontent.com/robertgzr/homebrew-tap/master/bootloadhid.rb
$ pip install pyusb
```

インストールに成功すると以下のように `bootloadHID` コマンドが実行できるようになります。

```console
$ bootloadHID
usage: bootloadHID [-r] [<intel-hexfile>]
```

Windowsの場合は [HIDBootFlash \- V\-USB](http://vusb.wikidot.com/project:hidbootflash) が利用できるかもしれません。

#### ファームウェアの書き込み - Flash custom firmware through USB with bootloadHID

ファームウェアを書き込むには、Planck THKのブートローダーが起動している状態(コンピューターから `HIDBoot` デバイスが見えている状態)で以下のコマンドを実行します。

```console
$ bootloadHID -r planck_thk_default.hex
Warning: could not detach kernel HID driver: Function not implemented
Warning: could not detach kernel HID driver: Function not implemented
Warning: could not detach kernel HID driver: Function not implemented
Page size   = 128 (0x80)
Device size = 32768 (0x8000); 30720 bytes remaining
Uploading 26112 (0x6600) bytes starting at 0 (0x0)
0x06580 ... 0x06600
```

`-r` オプションが指定されているため、書き込み完了後に自動でファームウェアに制御が移り、コンピューターからは `Planck` USBデバイスとして認識されます。

ただし前述のようにファームウェアの起動に失敗するケースがあるため、そのような場合にはリセットおよびESCキー押下の手順を踏みます。

#### ファームウェアの起動を安定させる

ファームウェアのコードを一部変更して、

- 起動音(の一部)を無効にする
- オーディオ機能を無効にする

のいずれかを行うと、ブートローダーからファームウェアへの切り替えに失敗することは無くなり動作が安定するようです。

起動音(の一部)を無効にする場合:
```diff
diff --git a/keyboards/planck/keymaps/default/config.h b/keyboards/planck/keymaps/default/config.h
index 6fa31cc8a..919532316 100644
--- a/keyboards/planck/keymaps/default/config.h
+++ b/keyboards/planck/keymaps/default/config.h
@@ -1,8 +1,8 @@
 #pragma once

 #ifdef AUDIO_ENABLE
-    #define STARTUP_SONG SONG(PLANCK_SOUND)
-    // #define STARTUP_SONG SONG(NO_SOUND)
+    // #define STARTUP_SONG SONG(PLANCK_SOUND)
+    #define STARTUP_SONG SONG(NO_SOUND)

     #define DEFAULT_LAYER_SONGS { SONG(QWERTY_SOUND), \
                                   SONG(COLEMAK_SOUND), \
```

オーディオ機能を無効にする場合:
```diff
diff --git a/keyboards/planck/thk/rules.mk b/keyboards/planck/thk/rules.mk
index bba4ea707..090764482 100644
--- a/keyboards/planck/thk/rules.mk
+++ b/keyboards/planck/thk/rules.mk
@@ -38,7 +38,7 @@ CONSOLE_ENABLE = no
 COMMAND_ENABLE = yes
 KEY_LOCK_ENABLE = no
 NKRO_ENABLE = no            # Nkey Rollover - if this doesn't work, see here: https://github.com/tmk/tmk_keyboard/wiki/FAQ#nkro-doesnt-work
-AUDIO_ENABLE = yes
+AUDIO_ENABLE = no

 # Do not enable SLEEP_LED_ENABLE. it uses the same timer as BACKLIGHT_ENABLE
 SLEEP_LED_ENABLE = no    # Breathing sleep LED during USB suspend
```

動作させている様子は[こちらのツイート](https://twitter.com/junya/status/1070659682832834565)にあります。


### 4. キーマップのカスタマイズ

以上を踏まえて、キーマップをカスタマイズする際は次のような手順となります。

1. `keyboards/planck/keymaps/default` を自分用に複製する
1. 複製したキーマップ関連ファイルをカスタマイズする
1. `make planck/thk:キーマップ名` でファームウェアをビルドする
1. `bootloadHID -r planck_thk_キーマップ名.hex` でファームウェアを書き込む


## ソフトウェア (Planck開発者向け) - How to build and flash bootloader

ここでは、ブートローダーが書き込まれていないATmega32AをPlanck THKのMCUとして利用可能にするための手順について解説します。

### 1. ブートローダーのビルド方法 - Build bootloader and combine it with custom firmware

`planck_thk` ブランチの `keyboards/planck/thk/bootloader` には `Makefile` が不足しているため、まずこれを用意します。

Jack Humbert氏が用意してくれたものが [BootloaderHID Makefile for Planck THK](https://gist.github.com/jackhumbert/50cbfead6ab27b6b3ee42f8c59d72776) にあるので、これを `keyboards/planck/thk/bootloader/Makefile` として保存し、`make` コマンドでビルドします。

**注意:** この `Makefile` ではヒューズビットの変更を行うためのターゲットも定義されていますが、指定されているビット値が正しくないため `make` コマンドによるヒューズビットの変更は利用しないでください(上位バイト`0x90`、下位バイト`0xcf`となるのが正しいがこれが逆になっている)。これを実行してしまうと以降の手順でブートローダーを書き込むことはできなくなり、復旧には別な手順が必要となります。

`make` コマンドを実行すると以下のようにビルドが行われます。

```console
$ cd keyboards/planck/thk/bootloader
$ make
avr-gcc -Wall -Os -fno-move-loop-invariants -fno-tree-scev-cprop -fno-inline-small-functions -Iusbdrv -I. -mmcu=atmega32a -DF_CPU=16000000 -DDEBUG_LEVEL=0  -x assembler-with-cpp -c usbdrv/usbdrvasm.S -o usbdrv/usbdrvasm.o
avr-gcc -Wall -Os -fno-move-loop-invariants -fno-tree-scev-cprop -fno-inline-small-functions -Iusbdrv -I. -mmcu=atmega32a -DF_CPU=16000000 -DDEBUG_LEVEL=0  -c usbdrv/oddebug.c -o usbdrv/oddebug.o
avr-gcc -Wall -Os -fno-move-loop-invariants -fno-tree-scev-cprop -fno-inline-small-functions -Iusbdrv -I. -mmcu=atmega32a -DF_CPU=16000000 -DDEBUG_LEVEL=0  -c main.c -o main.o
main.c: In function 'main':
<built-in>: warning: function declared 'noreturn' has a 'return' statement
In file included from usbdrv/usbdrv.c:10:0,
                 from main.c:22:
main.c: At top level:
usbdrv/usbdrv.h:223:24: warning: 'usbFunctionDescriptor' used but never defined
 USB_PUBLIC usbMsgLen_t usbFunctionDescriptor(struct usbRequest *rq);
                        ^~~~~~~~~~~~~~~~~~~~~
usbdrv/usbdrv.h:230:17: warning: 'usbSetInterrupt' declared 'static' but never defined [-Wunused-function]
 USB_PUBLIC void usbSetInterrupt(uchar *data, uchar len);
                 ^~~~~~~~~~~~~~~
avr-gcc -Wall -Os -fno-move-loop-invariants -fno-tree-scev-cprop -fno-inline-small-functions -Iusbdrv -I. -mmcu=atmega32a -DF_CPU=16000000 -DDEBUG_LEVEL=0  -o main.bin usbdrv/usbdrvasm.o usbdrv/oddebug.o main.o -Wl,--relax,--gc-sections -Wl,--section-start=.text=7000
rm -f main.hex main.eep.hex
avr-objcopy -j .text -j .data -O ihex main.bin main.hex
avr-size main.hex
   text	   data	    bss	    dec	    hex	filename
      0	   1708	      0	   1708	    6ac	main.hex
```

生成された `main.hex` がブートローダーとなります。これをそのまま書き込んだだけではキーボードとしては動作しないため、起動後にファームウェアを別途 bootloadHID でUSBで書き込む必要があります。

ブートローダーとデフォルトのファームウェアをセットで書き込む場合は、[ISP Flashing Guide \- QMK Firmware](https://docs.qmk.fm/#/isp_flashing_guide) の `Advanced/Production Techniques` を参考に、

1. ブートローダーをテキストエディタで開く
1. 最終行の `:00000001FF` を削除する
1. ファームウェアをテキストエディタで開く
1. ファームウェアの内容をすべてブートローダーの内容の後にコピー＆ペーストする
1. ファイルを `<keyboard>_<keymap>_production.hex` のような名前で保存する

という手順で書き込み用のファイルを用意します(順序はブートローダーが先でないと動作しません)。

### 2. ブートローダーの書き込み方法 - Flash hex file via Arduino ISP

1の手順で用意した `*.hex` をISP(In-System Programming)用の回路で書き込みます。

書き込み回路を自前で作成するかArduino ISP用のシールドなどを利用して、ATmega32Aに対するISPが行える状態にしたうえで、`avrdude` で以下のように書き込みます。

```console
$ avrdude -P /dev/tty.デバイス名 \
  -b 19200 \
  -c avrisp \
  -p atmega32 \
  -U flash:w:書き込むファイル.hex

avrdude: AVR device initialized and ready to accept instructions

Reading | ################################################## | 100% 0.02s

avrdude: Device signature = 0x1e9502 (probably m32)
avrdude: NOTE: "flash" memory has been specified, an erase cycle will be performed
         To disable this feature, specify the -D option.
avrdude: erasing chip
avrdude: reading input file "planck_thk_default_production.hex"
avrdude: input file planck_thk_default_production.hex auto detected as Intel Hex
avrdude: writing flash (30380 bytes):

Writing | ################################################## | 100% 28.41s

avrdude: 30380 bytes of flash written
avrdude: verifying flash memory against planck_thk_default_production.hex:
avrdude: load data flash data from input file planck_thk_default_production.hex:
avrdude: input file planck_thk_default_production.hex auto detected as Intel Hex
avrdude: input file planck_thk_default_production.hex contains 30380 bytes
avrdude: reading on-chip flash data:

Reading | ################################################## | 100% 15.88s

avrdude: verifying ...
avrdude: 30380 bytes of flash verified

avrdude: safemode: Fuses OK (E:FF, H:90, L:CF)

avrdude done.  Thank you.
```

### 3. ヒューズビットの変更 - Change fuse bits (beware to brick MCU)

ATmega32AをPlanck THKのMCUとして利用するには、AVRチップに特有のヒューズビットを変更する必要があります。指定すべき値は `planck_thk` ブランチの `README.md` にて以下のように言及されています。

> Fuses I used are -U lfuse:w:0xcf:m -U hfuse:w:0x90:m, and I hit the ESC to bootup normally (just a work-around right now).

したがってヒューズビットは以下の値になるよう変更します。

- 上位バイト: `0x90`
- 下位バイト: `0xcf`

```console
$ avrdude -P /dev/tty.デバイス名 \
  -b 19200 \
  -c avrisp \
  -p atmega32 \
  -U hfuse:w:0x90:m \
  -U lfuse:w:0xcf:m
```

ヒューズビットの値を間違えて変更してしまうと、それ以降ISPが行えない状態となってしまうことがあるので注意してください。ヒューズビットの詳細については[ATmega32Aのデータシート](https://avr.jp/user/ds.htm)内の「29.2 ヒューズビット」を参考にしてください。
