# CH552 DownloadモードJIGケーブル使い方

「家電のケンちゃん」店舗にて販売させて頂いている「CH552 DownloadモードJIGケーブル」使い方です。 

<img src="https://user-images.githubusercontent.com/43091864/143476161-d4deb0f5-6200-4323-85ae-20939716ee3a.JPG" width="300" /> <img src="https://user-images.githubusercontent.com/43091864/143490581-eaef78de-33da-46a0-92f0-cf8d9128417b.JPG" width="300" />  

## 改善FWについて

Kenta IDA氏よりGPIO0とEN=3.3Vの対策FWがリリースされ
ました。こちらのFWを書き込むことでWiFi不安定問題が解決することが確認されました。

[usb_ft232bm.bin](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin)  

M5Atom、M5StickC/plus、TimerCAM、UnitVなどのCH552を使用しているデバイスが対象です。不具合の詳細は[こちら](esp32AndUsbUartWith5V_IO_Issue.html)。  

### 1. WCHISPToolをインストール

まずWCHISPToolでデバイスドライバとFW書き込みアプリをインストールします。  
[WCHISPTool](http://www.wch.cn/downloads/WCHISPTool_Setup_exe.html) にアクセスし、[下载] を押してダウンロードしてインストール。  

### 2. Downloadモード設定

「CH552 DownloadモードJIGケーブル」をM5デバイスに接続し、パソコンに接続。必ずM5デバイス、パソコンの順に接続して下さい。
デバイスマネージャ上で[Interface] - [USB Module] が表示されます。  
![image](https://user-images.githubusercontent.com/43091864/143491010-95d7b2ff-8e50-4df5-a0a5-d6667457af2b.png)

### 3. FW書き込み

[IDA氏のFW](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin) をダウンロードし、WCHISPToolでFW書き込み。

![image](https://user-images.githubusercontent.com/43091864/142724843-0a87950c-aba7-4282-b02d-80fb3d01ba5d.png)

FW書き込み完了後、「専用ケーブル方式」の場合は必ず改造していないUSB-Cケーブルに繋ぎなおして下さい。

### ソースコード

[https://github.com/m5stack/M5_CH55x](https://github.com/m5stack/M5_CH55x)  
[https://github.com/ciniml/M5_CH55x](https://github.com/ciniml/M5_CH55x)  
