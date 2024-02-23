## つくるっち - ダンスロボット＆MIDI対応経緯

#### 1. メイの夏休みの宿題で作ったハトロボ - ダンス版（2018）  
MP3の音楽に合わせ、赤外線リモコンのコードを送信しています。ArduinoのC言語で実装、つくるっち対応しませんでした。  
<video src="https://sohtamei.github.io/docs/images/robotTeam.mp4" controls height="400"></video>

#### 2. クレア＋QuadCrawlerでのダンス（つくるっち-loadVMD拡張）（2022）  
市販のロボットクレアを砂川氏が魔改造し2022 MakerFaireTokyo出展。  
それを元にハードウェアはそのまま、ソフトをそーたメイがつくるっち環境でダンスに対応させたもの。  
MikuMikuDanceでモーションを生成し、つくるっちでモーションを再生しています。  
<video src="https://sohtamei.github.io/docs/images/MAH06392a.mp4" controls height="400"></video>

#### 3. つくるっち - UchiwaFuujinn氏のWebMidi拡張対応  
UchiwaFuujinn氏のwebMidi拡張を取り込み。使いこなすにはMIDIデバイスが必要で、残念ながらちゃんと使いこなせませんでした。  
ただ4.の参考になりました。
![image](https://github.com/sohtamei/docs/blob/master/images/webMidiExt.png)

#### 4. つくるっち - USBでのandroid/iOS接続対応  
androidとiOSは通常USB-UARTでUSBケーブル接続することは出来ませんが、（何故か）USB-MIDIだとUSBケーブルで接続することができます（iOSはscrubアプリを使用）。  
これを利用してandroidとiOSでのUSBケーブル接続に対応しました。windowsPC環境でもUSB-MIDI接続することができます。現在PICO(RP2040)のみ対応、ESP32シリーズは非対応です。  
![image](https://github.com/sohtamei/docs/blob/master/images/webMidiIF.png)

(参考) [iPad接続手順、android接続手順](http://sohta02.web.fc2.com/familyday_orgel.html#ipad)  

#### 5. つくるっち - MIDIファイル読み込み＆再生対応（光センサオルゴール）  
つくるっちはパソコンやスマフォからのプログラム実行に対応（オンライン動作）、マイコン単体での実行（スタンドアロン動作）に非対応です。プログラミング学習としては問題ないのですが、工作としては不便です。  
そのため2023/春のワークショップ「光センサオルゴール」から作成した音楽とLEDの点滅の記録・再生に対応しました。  
[2023御殿山さくらまつり](http://sohta02.web.fc2.com/familyday_event.html#gotenyama2023_1)

<video src="https://sohtamei.github.io/docs/images/MAH07079s.mp4" controls height="400"></video>

その際「楽譜で入力したい」「和音再生したい」というリクエストを多く頂戴したため、つくるっちでのMIDIファイル読み込み・記録・再生に対応しました。  
[loadMIDサンプル](https://sohta02.sakura.ne.jp/tukurutch/index.html#000002007)

loadMIDでmidiファイルをloadするとdataMIDにMIDIデータを読み込みます。set melodyブロックで光センサオルゴールに書き込むことでMIDIデータを再生することができます。  
