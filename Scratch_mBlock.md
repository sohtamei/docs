## スクラッチとmBlock、つくるっちについて
[つくるっちについて](http://sohta02.web.fc2.com/familyday_about.html)

### mBlockとつくるっち
つくるっちはMakeblock社のmBlock3を元に開発しました。その際スクラッチ2.0とmBlock3、スクラッチ3.0とmBlock5について調査を実施しました。下記の表は2018年ごろに調べた情報です。  

スクラッチはLEGO wedoやEV3など一部のHWにのみ対応し、arduinoには対応していません。Makeblock社はスクラッチ2.0とスクラッチ3.0を元にArduinoに対応したmBlock3とmBlock5を開発しました。mBlockは直感的で簡便なモニタモード(PC通信モード)と、本格的なプログラミングが可能な書き込みモード(Arduinoモード)に対応したすばらしいプログラミングアプリです。  
![scratch](images/scratch_mBlock.png)

mBlock5はソースコードを公開していないため、つくるっちはGPLライセンスでソースコード公開されているmBlock3を元に開発しました。  

### スマフォ対応について
スマフォの普及によりご自宅にパソコンが無いご家庭が増えています。  
つくるっちでもスマフォ対応を検討したのですが、
- arduino IDEがスマフォに対応していない
- arduinoハードウェアの書き込みにUSB-UARTが必要であり、USB-UARTに対応したスマフォが少ない
- mBlock3など元となるアプリがない

という事情により、windowsパソコンのみの対応となっています。

### mBlock5の拡張デバイスについて
mBlock3、mBlock5には「デバイス」（マイコン基板やロボット本体）と「extension」（Arduinoシールド基板や追加センサなど）があります。 
mBlock3では自作デバイスは非対応だったのですがmBlock5で自作デバイスに対応しました。たくさんのサードパーティ製デバイスがリリースされています。  
https://www.mblock.cc/doc/en/mblock3/mblock3-vs-mblock5.html  
リモコンロボやクアッドクローラーのようなロボットをスクラッチ対応させる方法として下記２つの方法があります。
- mBlock3などのソースコードを元にスクラッチ互換アプリを作成（つくるっち）
- mBlock5の拡張デバイスを作成 https://ext.mblock.cc/?mblock-3#/login?r=/  

実際にリモコンロボ用の「mBlock5拡張デバイス」作成に挑戦してみたのですが、node.jsのライブラリを１から実装する必要があり時間の都合からまだ完了していません。（拡張デバイス作成用のポータルサイトは素晴らしい！のですが。。） まだ完了してないため正確ではないのですが、つくるっち/mBlock5それぞれで拡張デバイスを作成したときの比較です。

| |つくるっち|mBlock5(拡張デバイス)|
|:--|:--:|:--:|
|対応OS|Win|Win/MAC|
|接続I/F|USB|USB/BLE|
|編集ファイル|json, (Cライブラリ)|ポータルサイトで設定,<br />node.jsライブラリ,(Cライブラリ)|
|LIVEモードFW開発|自動生成|要実装|
|対応マイコン&言語|AVR-C,SAMD-C,ESP32-C|AVR-C,ESP32-python|
|その他||公開申請すると公式mBlock5アプリ上に表示される|

- mBlock5 appはandroid,iOS対応しているが自作デバイスは非対応。3rdParty製デバイスも存在しない (2020/4現在)  
- node.jsライブラリ（実装たいへん）
    - mBot: exts/common/sensorium
    - arduinoUno: https://mblock-expanded.oss-cn-shenzhen.aliyuncs.com/015e089251944dd28644bb5aaf266b15.js  
- インストールされた拡張デバイス・extensionは C:\Users\xx\mblock\exts に保存される。各フォルダをzip圧縮し拡張子mextにするとmBlock5ポータルサイトで読み込むことができる。拡張デバイスのサンプルが無いためこの方法でサンプルを作る必要がある。  

