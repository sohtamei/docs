## ESP32と5V IOのUSB UARTデバイスによるWifi問題まとめ（２）

### 改善FWについて

Kenta IDA氏よりGPIO0とEN=3.3Vの対策FWがリリースされました。こちらのFWを書き込むことでGPIO=4V問題が解決することが確認されました。

[usb_ft232bm.bin](https://github.com/sohtamei/docs/images/usb_ft232bm.bin)


### Downloadモード設定

CH552を書き込むためにはCH552をDownloadモードにする必要があります。まず「FT_Prog」方式を試し、ダメだったら「Downloadモードピン方式」を試して下さい。

#### 1. Downloadモード - FT_Prog

下記URLからFT_Progをダウンロードしてインストールします。  
https://ftdichip.com/utilities/#ft_prog  

- パソコンにM5デバイスを接続し、デバイスマネジャ [表示] - [デバイス(接続別)]を選択、[USB Serial Port(COMxx)] を表示しておきます。  
![image](https://user-images.githubusercontent.com/43091864/142723316-7f39791f-8490-4269-ae82-2042a0e3ce1c.png)  

- FT-Prog上で [F5] を押します。  
1. [USB Module] が表示されたらDownloadモードに入りました。  
![image](https://user-images.githubusercontent.com/43091864/142723703-ad1b8943-6412-4ed2-aad6-f3000517baea.png)  
2. 下記のようにデバイスが表示され、デバイスマネージャ上で [USB Serial Port(COMxx)] のままの場合 [Ctrl-P] - [Proram] を押して下さい。  
  ![image](https://user-images.githubusercontent.com/43091864/142723354-203363d8-3040-4997-822f-b3f729229575.png)  
  [USB Module] が表示されたらDownloadモードに入りました。  
3. デバイスマネージャ上で何も表示されてないときはNGです。  

手持ちのM5デバイスを試したところ下記の通りでした。NGの場合2.Downloadモードピンを試して下さい。  

|デバイス|ID|結果|
|:--|:--:|:--:|
|ATOM LITE|1|NG|
|ATOM LITE|2|NG|
|ATOM MATRIX|1|NG|
|ATOM MATRIX|2|NG|
|ATOM ECHO||NG|
|StickC|1|OK|
|StickC|2|NG|
|StickCplus||NG|
|unitV||OK|
|TimerCAM||NG|

#### 2. Downloadモード - Downloadモードピン

2は手持ちのM5デバイスをいくつか試したところ4個NGで1個OK（古いM5StickC）、ただM5Stack社からサンプルとして提供されたft232_OD_20200422.hexを書いたところNG4個と同じ状態になりました。

- FT232互換モード？  
K016 C 552串口usb_ft232bm_01022020(3).bin

- FT_PROG認識しない  
ft232_OD_20200422.hex

かなり不安定そうです。

1のdownloadモードピンはUDPを2.2kΩで3.3Vにpullupしたところ動作しました。  
<img src="https://user-images.githubusercontent.com/43091864/142501427-00a60bf9-7fae-49d9-a028-926cfd1225fa.JPG" width="500" />  

下記サイトを参考にさせて頂きました。  
https://github.com/betaEncoder/CH551_Breakout_Board

### build環境

ついにM5Stack社よりCH552ソース公開して頂きました。  
https://github.com/m5stack/M5_CH55x  
ソースのみでSDCC用のconfigファイルやuVision用のprojectファイルが無いためprojectを自力で作る必要があります。

まずuVisionで試したところ、無料版の壁である800H問題にぶつかってしまいました。

<img src="https://user-images.githubusercontent.com/43091864/142502667-d9313ffb-0786-453e-b5bb-b10786edbf38.png" width="500" />  

- M5Stack社からリリースされているM5_CH55xはkeilC51 uVision用
- サンプルとして公開されているbinary は2560~3000byte程度あり、コード削減で2048に収めるのは効率悪そう

現在M5_CH55xをkeilC51→SDCC環境にポーティング中。。作業github：

https://github.com/sohtamei/M5_CH55x
