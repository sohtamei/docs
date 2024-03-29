## Koovプログラミング情報

つくるっち＋Koovでのプログラミングに対応しました。リモコンロボ同様 BitTradeOne社の「汎用赤外線リモコン」、「アナログリモコン」でロボットを操縦することができます。  
**公式アプリではなく、まだ多数不具合があります。注意して下さい。**  
Windowsのみ対応(MAC, iPad非対応)、USB接続のみ対応(BLE,Wifi接続非対応)です。  
<a href="http://sohta02.web.fc2.com/images/MAQ04939_.mp4"><img src="../images/MAQ04939_.png" width="320" height="240" border="0" /></a> クリックで再生  
![image7](../images/image7.png)

### ダウンロード (つくるっち Koov版)

下記リンクをクリックしてダウンロードして下さい。**zipファイル約600MB、展開すると約1.4GBになります。** パソコンの空き容量に注意して下さい。スマフォでダウンロードしないで下さい。
[http://sohta02.sakura.ne.jp/release/TuKuRutch.20200605.koov.zip](http://sohta02.sakura.ne.jp/release/TuKuRutch.20200605.koov.zip)  
インストール手順とアプリの使い方は [「つくるっち通常版」](http://sohta02.web.fc2.com/familyday_app.html#download) を参照して下さい。

### サンプルプログラム
つくるっちで [ロボット] - [Koov] を選択し、[プログラム] - [開く] で選択して下さい。
- アナログリモコン.sb2　　赤外線ジョイスティックリモコンでロボットを操縦
- デジタルリモコン1.sb2　KRIR汎用リモコンでロボットを操縦
- デジタルリモコン2.sb2　KRIR汎用リモコンでロボットを操縦
- ドレミ.sb2　　　ドレミの曲を再生

### リモコンでのロボット操縦に必要なもの
「ドレミ.sb2」はKoov本体だけで試すことができます。  
赤外線リモコンでロボット操縦を行うためにはKoov本体と下記部品が必要です。  
- Artec社の「[ロボット用赤外線リモコン受信センサー](https://www.amazon.co.jp/dp/B00VFZ0NX8)」
- BitTradeOne社の「[KRIR汎用赤外線リモコン](https://btoshop.jp/2018/10/12/4562469772134/)」又は「[赤外線ジョイスティックリモコン](https://btoshop.jp/2020/03/16/adkrjs/)」

### 接続方法
- V0とV1にモーターを接続
- V2にブザーを接続
- K7に「ロボット用赤外線リモコン受信センサー」を接続  
<img src="../images/DSC04941_.jpg" width="300" height="273" border="0" /> クリックで拡大

### 使い方（PC通信モード）
- ロボットの電源を入れUSBで接続し、
- [接続] - [ロボットに接続(COM ..)]
- [接続] - [ロボットをPC通信モードに設定]
- ブロック [プログラム開始] をクリック

### 使い方（Arduinoモード）
- ロボットの電源を入れUSBで接続し、
- [接続] - [ロボットに接続(COM ..)]
- [Arduino] - [Arduinoにアップロード]
