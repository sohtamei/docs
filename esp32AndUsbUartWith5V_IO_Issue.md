## ESP32と5V IOのUSB UARTデバイスによるWifi問題まとめ

このページはFacebookやその他SNS情報の関連情報をまとめたものです。

### 対象デバイス
* Wemos D1 R32
* M5Atomシリーズ  
* M5StickCシリーズ  
* M5Cameraシリーズ  
* Timercam  
* その他USB-UARTにCH552を使用しているM5Stack社製品  
  ※上記デバイス全てで問題が起きるわけはないらしい。私の環境ではM5StickCシリーズ、M5Cameraシリーズでは問題が再現していない。

### 不具合内容
* Wifi電波の到達距離が他のESP32デバイスと比較して極端に短い（アクセスポイントから数m程度）
 ![無題3](https://user-images.githubusercontent.com/43091864/136214394-7a6dd175-fc86-41b4-a14b-a7894d41b6a8.png)
 
### 原因
* USB-UARTデバイスを5V IOで使用している（Wemos D1 R32はCH340、M5Stack社商品はCH552）。  
<img src="https://user-images.githubusercontent.com/43091864/136226442-2dede038-4f1f-422c-9f00-3537fa1c2d30.png" width="500" />  

* 上記の結果ESP32のEN、IO0、RXに常に4V以上の電圧が加えられている状態となり、ESP32の絶対最大定格Vcc+0.3=3.6Vを上回る状態となる。ただしこれにより電気的に壊れた例はまだ見つかっていない。
* 様々な検討の結果IO0=4V以上によりWiFi不安定になる可能性が高い。
   * ESP32コミュニティでWiFiエラーログが表示され、通信が不安定になる問題が報告される  
    [https://github.com/espressif/arduino-esp32/issues/2144](https://github.com/espressif/arduino-esp32/issues/2144)  
    ※このエラーログは通常のFWでは表示されません、DebugLevel=Verpose等のFWを書き込む必要があります。
   * 上記問題はIO0=4V以上のとき発生し、IO0=3.3Vにすると発生しなくなることが確認される。
   * ESP32のIO0はADC2_1とのpinmuxになっており、ADC2はWiFi機能の一部として使用される。IO0の出力段の電気回路により4V以上の高電圧がADC2に流れ込み、WiFi機能に何らかの影響を及ぼしている可能性がある。

### 対策方法
現時点での安全＆確実な対策方法は下記になります、残念ながら。。
* デバイスとアクセスポイントを近づけて使用する。  
* 他のデバイスを使用する。  

メーカー側で早急に対応してくれることを願っています。

.    
以下は有志による対策方法で、改造が必要だったりメーカー推奨方法と異なる使用方法になります。決して推奨できる方法ではありません。  
実践する方は必ず自己責任でお願いします、デバイスやPCを壊したりダメージを与える可能性があります。  
* 3.3V VCCで動作させる (そーたメイ案、M5Atom）  
> 1. 裏面ヘッダピンの3.3Vから3.3V供給  
> 2. GROVE VCCから3.3V供給  
> 推奨方法ではないですが、どちらも「PLEN:bit用M5ATOM変換基板」で実績(?) があります。ただ逆流防止の機能は無いため、USB-C端子でのPCやUSB電源への接続と、上記の3.3V供給は必ず排他（一方を繋ぐときはもう一方を外す）で扱う必要があります。  

　　[https://www.facebook.com/groups/154504605228235/posts/699719300706760/?comment_id=812684116076944&reply_comment_id=812782789400410](https://www.facebook.com/groups/154504605228235/posts/699719300706760/?comment_id=812684116076944&reply_comment_id=812782789400410)  
　　※M5StickCなど、M5Atom以外のデバイスでは上記対策は厳禁です！

* ツェーナーダイオードを外付けする（こばさん案、M5StickC）
> 3.6V のツェナー付けたら、めっちゃ絶好調になった。※漏れ電流が多すぎて 2.7V くらいになったけど  

　　[https://twitter.com/wakwak_koba/status/1408794880407601153](https://twitter.com/wakwak_koba/status/1408794880407601153)

* 基板上で抵抗追加（そーたメイ案、Wemos D1 R32）  
[https://github.com/espressif/arduino-esp32/issues/2144#issuecomment-657672609](https://github.com/espressif/arduino-esp32/issues/2144#issuecomment-657672609)  
M5シリーズの場合CH552内部でSW的にIO0を生成し、CH552のGPIOで直接IO0を駆動しているため外付け抵抗による対策はできません。

* 内部に抵抗追加（佐々木明彦氏案、M5ATom）  
[https://www.facebook.com/groups/154504605228235/posts/699719300706760/?comment_id=812684116076944](https://www.facebook.com/groups/154504605228235/posts/699719300706760/?comment_id=812684116076944)

### 関連BBS
Facebook/M5Stack User Group Japan：[https://www.facebook.com/groups/154504605228235/permalink/699719300706760/](https://www.facebook.com/groups/154504605228235/permalink/699719300706760/)  
M5Stack社コミュニティ：[https://community.m5stack.com/topic/3048/short-wifi-effective-range-and-io0-3-9v-issue-with-lite-and-matrix](https://community.m5stack.com/topic/3048/short-wifi-effective-range-and-io0-3-9v-issue-with-lite-and-matrix)  
EspressIF/arduino-ESP32：[https://github.com/espressif/arduino-esp32/issues/2144](https://github.com/espressif/arduino-esp32/issues/2144)
