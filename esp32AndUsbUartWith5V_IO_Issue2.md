## ESP32と5V IOのUSB UARTデバイスによるWifi問題まとめ（２）

### 書き込み

CH552の書き込みは下記３つがあり、

1. downloadモードピン＋WCHISPTool

2. FT_Prog＋WCHISPTool

3. M5Stack社が2020/1に公開したMAC専用CH552 updater

2は手持ちのM5デバイスをいくつか試したところ4個ダメで1個（古いM5StickC）で成功しました。  
かなり不安定そうです。

1のdownloadモードピンはUDPを2.2kΩで3.3Vにpullupしたところ動作しました。
![DSC05581](https://user-images.githubusercontent.com/43091864/142501427-00a60bf9-7fae-49d9-a028-926cfd1225fa.JPG)
下記サイトを参考にさせて頂きました。
https://github.com/betaEncoder/CH551_Breakout_Board

### build

ついにM5Stack社よりCH552ソース公開して頂きました。  
https://github.com/m5stack/M5_CH55x
ソースのみでSDCC用のconfigファイルやuVision用のprojectファイルが無いためprojectを自力で作る必要があります。

まずuVisionで試したところ、無料版の壁である800H問題にぶつかってしまいました。

![image](https://user-images.githubusercontent.com/43091864/142502667-d9313ffb-0786-453e-b5bb-b10786edbf38.png)


