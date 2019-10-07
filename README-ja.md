# obniz_cli
`obniz_cli` は obnizOS(for ESP32) をデバイスにインストールするためのCLIツールです。

## インストール
pipを使ってインストールできます。
```
pip install obniz_cli
```

## 前準備
ターゲットとなるESP32をシリアルポートからPCに接続します。（DevKitC等の場合はマイクロUSBなどでパソコンに接続するだけです）。  

接続したデバイスがシリアルポート一覧に出てくることを確認します。以下のコマンドで確認できます：
```
python -m serial.tools.list_ports
```
(このコマンドは`pip install obniz_cli`を実行した後に実行可能です。)
名前はデバイスによって異なりますが、DevKitCの場合は`/dev/cu.SLAB_USBtoUART`や`COM3`などの名前であることが多いです。もしこれらの名前が確認できなかった場合、または確認できるが書き込みに失敗するといった場合には、[こちら](https://www.silabs.com/products/development-tools/software/usb-to-uart-bridge-vcp-drivers)からUSBドライバをインストールすることで解決する可能性があります。


## 使い方
### flashos
```
obniz_cli flashos [-b] [-p]
```
ターゲットのESP32にobnizOSをインストールするコマンドです。`-p`オプションなしで実行した場合、以下のように出力されます：
```
0: /dev/cu.Bluetooth-Incoming-Port
1: /dev/cu.SLAB_USBtoUART

Select NUMBER from above list(or if you want to cancel, input N key):
```
インストール先を選んで、そのインデックスの数字を入力してください(ターゲットのポートは`-p`オプションを用いて渡すこともできます：`obniz_cli flashos -p /dev/cu.SLAB_USBtoUART`)。  

ポートが選択されると、最新のobnizOSをダウンロードしたのち、ターゲットへインストールされます。デフォルトでは、通信速度が921600bpsに設定されていますが、うまく書き込めない場合には`-b`オプションを用いて通信速度を落としてみてください：`obniz_cli flashos -b 115200`。

インストール完了後は、自動的にobnizOSの設定のための通信に移ります。
### eraseos
```
obniz_cli eraseos [-p]
```
このコマンドによってターゲットのデバイスをリセットできます。