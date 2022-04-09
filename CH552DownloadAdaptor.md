## CH552 Downloadモードアダプタ使い方

「家電のケンちゃん」店舗にて販売させて頂いている「CH552 Downloadモードアダプタ」使い方です。 

<img src="https://user-images.githubusercontent.com/43091864/143476161-d4deb0f5-6200-4323-85ae-20939716ee3a.JPG" width="300" /> <img src="https://user-images.githubusercontent.com/43091864/143490581-eaef78de-33da-46a0-92f0-cf8d9128417b.JPG" width="300" />  
<img src="https://user-images.githubusercontent.com/43091864/162562183-ec439077-302d-4d45-8d85-0201e887ddac.png" width="200" />  

### 改善FWについて

Kenta IDA氏よりGPIO0とEN=3.3Vの対策FWがリリースされ
ました。こちらのFWを書き込むことでWiFi不安定問題が解決することが確認されました。

[usb_ft232bm.bin](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin)  

**※このFWは有志による非公式FWです、M5Stack社からはまだ対策前/対策後どちらのFWもバイナリが公開されていません。**  
使用については恐縮ですが自己責任にてお願いできますでしょうか。  

M5Atom、M5StickC/plus、TimerCAM、UnitVなどのCH552を使用しているデバイスが対象です。不具合の詳細は[こちら](esp32AndUsbUartWith5V_IO_Issue.html)。  

### 1. WCHISPToolをインストール

[WCHISPTool](http://www.wch.cn/downloads/WCHISPTool_Setup_exe.html) にアクセスし、[下载] を押してダウンロードしてインストール。  
![image](https://user-images.githubusercontent.com/43091864/143491430-0f0e63d2-0ecc-457d-ba24-a6e187a7d476.png)

### 2. Downloadモード設定

「CH552 Downloadモードアダプタ」をUSB-TypeCケーブルでM5デバイスに接続し、パソコンに接続。必ずアダプタとM5デバイス、アダプタとパソコンの順に接続して下さい。  
<img src="https://user-images.githubusercontent.com/43091864/143510252-22b4b93d-65f1-472b-b397-1c5b16586450.JPG" width="500" />

デバイスマネージャ上で[Interface] - [USB Module] が表示されます。  
![image](https://user-images.githubusercontent.com/43091864/143491010-95d7b2ff-8e50-4df5-a0a5-d6667457af2b.png)

### 3. FW書き込み

[IDA氏のFW](https://github.com/sohtamei/docs/blob/master/images/usb_ft232bm.bin) をダウンロードし、WCHISPToolでFW書き込み。

![image](https://user-images.githubusercontent.com/43091864/142724843-0a87950c-aba7-4282-b02d-80fb3d01ba5d.png)

FW書き込み完了後、「CH552 Downloadモードアダプタ」を外してPCに接続して下さい。

### ソースコード

[https://github.com/m5stack/M5_CH55x](https://github.com/m5stack/M5_CH55x)  
[https://github.com/ciniml/M5_CH55x](https://github.com/ciniml/M5_CH55x)  
