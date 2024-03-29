## ESP32と5V IOのUSB UARTデバイスによるWifi問題まとめ（FW更新方法）

(2021/11/25更新)

### 改善FWについて

Kenta IDA氏よりGPIO0とEN=3.3Vの対策FWがリリースされました。こちらのFWを書き込むことでWiFi不安定問題が解決することが確認されました。

[usb_ft232bm.bin](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin)  
[https://github.com/ciniml/M5_CH55x](https://github.com/ciniml/M5_CH55x)

**※このFWは有志による非公式FWです、M5Stack社からはまだ対策前/対策後どちらのFWもバイナリが公開されていません。**  
使用については恐縮ですが自己責任にてお願いできますでしょうか。  

M5Atom、M5StickC/plus、TimerCAM、UnitVなどのCH552を使用しているデバイスが対象です。不具合の詳細は[こちら](esp32AndUsbUartWith5V_IO_Issue.html)。  

### 1. WCHISPToolをインストール

まずWCHISPToolでデバイスドライバとFW書き込みアプリをインストールします。  
[WCHISPTool](http://www.wch.cn/downloads/WCHISPTool_Setup_exe.html) にアクセスし、[下载] を押してダウンロードしてインストール。  

### 2. Downloadモード設定

FW書き込みの前にCH552をDownloadモードにする必要があります。まず「FT_Prog」方式を試し、ダメだったら「専用ケーブル方式」を試して下さい。

#### (A) FT_Prog方式

下記URLからFT_Progをダウンロードしてインストールします。  
[https://ftdichip.com/utilities/#ft_prog](https://ftdichip.com/utilities/#ft_prog)  

- パソコンにM5デバイスを接続し、デバイスマネージャで [表示] - [デバイス(接続別)] を選択、[USB Serial Port(COMxx)] を表示しておきます。  
![image](https://user-images.githubusercontent.com/43091864/142723316-7f39791f-8490-4269-ae82-2042a0e3ce1c.png)  

- FT-Prog上で [F5] を押します。  
1. デバイスマネージャ上で [USB Module] が表示されたらDownloadモードに入りました。  
  ![image](https://user-images.githubusercontent.com/43091864/142723703-ad1b8943-6412-4ed2-aad6-f3000517baea.png)  
2. FT-Prog：デバイス表示（下図)、デバイスマネージャ：[USB Serial Port(COMxx)] 表示のとき、FT-Progで[Ctrl-P] - [Program] を押して下さい。  
  ![image](https://user-images.githubusercontent.com/43091864/142723354-203363d8-3040-4997-822f-b3f729229575.png)  
  デバイスマネージャ上で [USB Module] が表示されたらDownloadモードに入りました。  
  ![image](https://user-images.githubusercontent.com/43091864/142723703-ad1b8943-6412-4ed2-aad6-f3000517baea.png)  
3. FT-Prog上で [F5] を押したあとデバイスマネージャ上で表示が消えてしまうときはNGです、「専用ケーブル方式」を試して下さい。  
手持ちのM5デバイスを試したところ下記の通りでした。デバイス出荷時に書かれたCH552のFWでOK/NGに分かれるようです。  

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
|TimerCAM||NG|
|unitV||OK|

#### (B) 専用ケーブル方式

#### 必要なもの

- 不要なUSB-Cケーブル（改造後は通常の用途で使うことができません）
- リード抵抗 100Ω、220Ω、2.2kΩ
- ニッパー、ワイヤストリッパー

#### 1. USB-Cケーブルを用意しニッパーで5cmくらい被覆をむく。中のケーブルを傷つけないように注意。  
![image](https://user-images.githubusercontent.com/43091864/142724354-ac27b3ec-0a9b-4e92-89db-f5e65eaf14d7.png)  

#### 2. 赤、黒、緑のケーブルをワイヤストリッパーで写真の位置でむく。中の銅線を傷つけ切らないように注意。
![image](https://user-images.githubusercontent.com/43091864/142724535-c8f25ae4-a2b9-4b29-8047-161d200ba2ed.png)

#### 3. 220Ωと100Ωをひねって繋ぎ、220Ωを黒、100Ωを赤のむいた部分に巻き付け、3か所半田付けする。
![image](https://user-images.githubusercontent.com/43091864/142724644-61091a2b-641d-4ba4-9bb9-4e49ea508092.png)

#### 4. 2.2kΩを緑の向いた部分と写真真ん中に巻き付け、2か所半田付けする。
![image](https://user-images.githubusercontent.com/43091864/142724710-701029b7-a954-4ad4-b1d9-4fded20fb5a1.png)

#### 5. 抵抗のリード線を半田付け根元で切断。赤、緑、黒がショートしないように調整。
![image](https://user-images.githubusercontent.com/43091864/142727163-a1051f7a-ac8d-4823-b3c0-a9ada4cfaa2c.png)

#### 6. 作成したケーブルをM5デバイスに接続し、パソコンに接続。  

 必ずM5デバイス、パソコンの順に接続して下さい。デバイスマネージャ上で [USB Module] が表示されたらDownloadモードに入りました。  
  ![image](https://user-images.githubusercontent.com/43091864/142723703-ad1b8943-6412-4ed2-aad6-f3000517baea.png)  

### 3. FW書き込み

[IDA氏のFW](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin) をダウンロードし、1 のWCHISPToolでFW書き込み。

![image](https://user-images.githubusercontent.com/43091864/142724843-0a87950c-aba7-4282-b02d-80fb3d01ba5d.png)

FW書き込み完了後、「専用ケーブル方式」の場合は必ず改造していないUSB-Cケーブルに繋ぎなおして下さい。

### 参考

下記サイトを参考にさせて頂きました。  
[https://github.com/m5stack/M5_CH55x](https://github.com/m5stack/M5_CH55x)  
[https://github.com/ciniml/M5_CH55x](https://github.com/ciniml/M5_CH55x)  
[https://itoi.jp/M5Stack.html?fbclid=IwAR0HmmXVnrWot6k04CB0n982jV-DUhQhYaWU-cpXmXGFnWx4r418dmFnFPY#M5Atom-5V_IO_Issue](https://itoi.jp/M5Stack.html?fbclid=IwAR0HmmXVnrWot6k04CB0n982jV-DUhQhYaWU-cpXmXGFnWx4r418dmFnFPY#M5Atom-5V_IO_Issue)  
[https://github.com/betaEncoder/CH551_Breakout_Board](https://github.com/betaEncoder/CH551_Breakout_Board)  

下記サイトでも公開中
[https://community.m5stack.com/topic/3768/new-ch552-firmware-for-short-wifi-issue-of-m5atom-stick-timercam-etc](https://community.m5stack.com/topic/3768/new-ch552-firmware-for-short-wifi-issue-of-m5atom-stick-timercam-etc)

### （中止）build環境

ついにM5Stack社よりCH552ソース公開して頂きました。  
[https://github.com/m5stack/M5_CH55x](https://github.com/m5stack/M5_CH55x)  
ソースのみでSDCC用のconfigファイルやuVision用のprojectファイルが無いためprojectを自力で作る必要があります。

まずuVisionで試したところ、無料版の壁である800H問題にぶつかってしまいました。

<img src="https://user-images.githubusercontent.com/43091864/142502667-d9313ffb-0786-453e-b5bb-b10786edbf38.png" width="500" />  

- M5Stack社からリリースされているM5_CH55xはkeilC51 uVision用
- サンプルとして公開されているbinary は2560~3000byte程度あり、コード削減で2048に収めるのは効率悪そう

~~現在M5_CH55xをkeilC51→SDCC環境にポーティング中。。https://github.com/sohtamei/M5_CH55x~~  
現在中断中
