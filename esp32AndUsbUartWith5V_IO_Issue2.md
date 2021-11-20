# ESP32と5V IOのUSB UARTデバイスによるWifi問題まとめ（２）

## 改善FWについて

Kenta IDA氏よりGPIO0とEN=3.3Vの対策FWがリリースされました。こちらのFWを書き込むことでGPIO=4V問題が解決することが確認されました。

[usb_ft232bm.bin](https://github.com/sohtamei/docs/images/usb_ft232bm.bin)


## Downloadモード設定

CH552を書き込むためにはCH552をDownloadモードにする必要があります。まず「FT_Prog」方式を試し、ダメだったら「Downloadモードピン方式」を試して下さい。

### 1. FT_Prog方式

下記URLからFT_Progをダウンロードしてインストールします。  
https://ftdichip.com/utilities/#ft_prog  

- パソコンにM5デバイスを接続し、デバイスマネージャで [表示] - [デバイス(接続別)] を選択、[USB Serial Port(COMxx)] を表示しておきます。  
![image](https://user-images.githubusercontent.com/43091864/142723316-7f39791f-8490-4269-ae82-2042a0e3ce1c.png)  

- FT-Prog上で [F5] を押します。  
1. デバイスマネージャ上で [USB Module] が表示されたらDownloadモードに入りました。  
  ![image](https://user-images.githubusercontent.com/43091864/142723703-ad1b8943-6412-4ed2-aad6-f3000517baea.png)  
2. 下記のようにデバイスが表示されデバイスマネージャ上で [USB Serial Port(COMxx)] のままの場合、[Ctrl-P] - [Program] を押して下さい。  
  ![image](https://user-images.githubusercontent.com/43091864/142723354-203363d8-3040-4997-822f-b3f729229575.png)  
  デバイスマネージャ上で [USB Module] が表示されたらDownloadモードに入りました。  
  ![image](https://user-images.githubusercontent.com/43091864/142723703-ad1b8943-6412-4ed2-aad6-f3000517baea.png)  
3. FT-Prog上で [F5] を押したあとデバイスマネージャ上で表示が消えてしまうときはNGです。  

手持ちのM5デバイスを試したところ下記の通りでした。デバイス出荷時に書かれたCH552のFWでOK/NGに分かれるようです。  
NGの場合2.Downloadモードピンを試して下さい。  

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

### 2. Downloadモードピン方式

#### 必要なもの

- 不要なUSB-Cケーブル
- 抵抗 100Ω、220Ω、2.2kΩ
- ニッパー、ワイヤストリッパー

#### 1. USB-Cケーブルを用意しニッパーで5cmくらい被覆をむく。中のケーブルを傷つけないように注意。  
![image](https://user-images.githubusercontent.com/43091864/142724112-3c2a2d1e-33e3-4e13-be2f-7ffcf934af88.png)  

#### 2. 

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
