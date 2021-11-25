# CH552 DownloadモードJIGケーブル使い方

「家電のケンちゃん」店舗にて販売させて頂いているCH552 DownloadモードJIGケーブル使い方です。  
![DSC05599](https://user-images.githubusercontent.com/43091864/143476161-d4deb0f5-6200-4323-85ae-20939716ee3a.JPG)

## 改善FWについて

Kenta IDA氏よりGPIO0とEN=3.3Vの対策FWがリリースされました。こちらのFWを書き込むことでWiFi不安定問題が解決することが確認されました。

[usb_ft232bm.bin](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin)  
[https://github.com/ciniml/M5_CH55x](https://github.com/ciniml/M5_CH55x)

M5Atom、M5StickC/plus、TimerCAM、UnitVなどのCH552を使用しているデバイスが対象です。不具合の詳細は[こちら](esp32AndUsbUartWith5V_IO_Issue.html)。  

## 1. WCHISPToolをインストール

まずWCHISPToolでデバイスドライバとFW書き込みアプリをインストールします。  
[WCHISPTool](http://www.wch.cn/downloads/WCHISPTool_Setup_exe.html) にアクセスし、[下载] を押してダウンロードしてインストール。  

## 2. Downloadモード設定

FW書き込みの前にCH552をDownloadモードにする必要があります。

#### 6. 作成したケーブルをM5デバイスに接続し、パソコンに接続。  

 必ずM5デバイス、パソコンの順に接続して下さい。デバイスマネージャ上で [USB Module] が表示されたらDownloadモードに入りました。  
  ![image](https://user-images.githubusercontent.com/43091864/142723703-ad1b8943-6412-4ed2-aad6-f3000517baea.png)  

## 3. FW書き込み

[IDA氏のFW](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin) をダウンロードし、1 のWCHISPToolでFW書き込み。

![image](https://user-images.githubusercontent.com/43091864/142724843-0a87950c-aba7-4282-b02d-80fb3d01ba5d.png)

FW書き込み完了後、「専用ケーブル方式」の場合は必ず改造していないUSB-Cケーブルに繋ぎなおして下さい。

## ソースコード

[https://github.com/m5stack/M5_CH55x](https://github.com/m5stack/M5_CH55x)  
[https://github.com/ciniml/M5_CH55x](https://github.com/ciniml/M5_CH55x)  
