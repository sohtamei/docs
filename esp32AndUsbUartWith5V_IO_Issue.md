## ESP32と5V IOのUSB UARTデバイスによるWifi問題まとめ

(2021/11/23更新)  
このページはFacebookやその他SNS情報の関連情報をまとめたものです。

### 対象デバイス
* M5Atomシリーズ  
* M5StickCシリーズ  
* TimerCAM  
* その他USB-UARTにCH552を使用しているM5Stack社製品  

### 不具合内容
* Wifi電波の到達距離が他のESP32デバイスと比較して極端に短い（アクセスポイントから数m程度）、AP接続に失敗する。
 
### 原因
* USB-UART CH552を5V IOで使用しており、ESP32のMODE切り替えであるIO0が5Vにpullupされている。  
電源電圧が高めでIO0が約4.2V以上にになるとWiFi接続率が悪化する。（赤線）  

<img src="https://user-images.githubusercontent.com/43091864/142955542-efc8bc47-85cc-40d2-80c8-f6817aebb828.png" width="700" />  

<img src="https://user-images.githubusercontent.com/43091864/136226442-2dede038-4f1f-422c-9f00-3537fa1c2d30.png" width="600" />  

<!--
 ![無題3](https://user-images.githubusercontent.com/43091864/136214394-7a6dd175-fc86-41b4-a14b-a7894d41b6a8.png)
-->

### 対策方法
* M5Stack社、井田健太氏、糸井成夫氏により対策FWがリリースされました。  
[FWと更新方法](esp32AndUsbUartWith5V_IO_Issue.md)

### 関連BBS
* Facebook/M5Stack User Group Japan：[https://www.facebook.com/groups/154504605228235/permalink/699719300706760/](https://www.facebook.com/groups/154504605228235/permalink/699719300706760/)  

* M5Stack社コミュニティ：[https://community.m5stack.com/topic/3048/short-wifi-effective-range-and-io0-3-9v-issue-with-lite-and-matrix](https://community.m5stack.com/topic/3048/short-wifi-effective-range-and-io0-3-9v-issue-with-lite-and-matrix)  

* EspressIF/arduino-ESP32：[https://github.com/espressif/arduino-esp32/issues/2144](https://github.com/espressif/arduino-esp32/issues/2144)  
ESP32コミュニティでWiFiエラーログが表示され、通信が不安定になる問題が報告される。  
※このエラーログは通常のFWでは表示されません、DebugLevel=Verpose等のFWを書き込む必要があります。  
ESP32のIO0はADC2_1とのpinmuxになっており、ADC2はWiFi機能の一部として使用される。  
IO0の出力段の電気回路により4V以上の高電圧がADC2に流れ込み、WiFi機能に何らかの影響を及ぼしている可能性がある。

