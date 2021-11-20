## ESP32と5V IOのUSB UARTデバイスによるWifi問題まとめ（２）

### 書き込み環境

CH552の書き込みは下記３つがあり、

1. downloadモードピン＋WCHISPTool

2. FT_Prog＋WCHISPTool

3. M5Stack社が2020/1に公開したMAC専用CH552 updater

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
