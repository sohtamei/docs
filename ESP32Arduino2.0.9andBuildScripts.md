## つくるっちArduinoのつくるっちexe→buildスクリプト変更、arduino-esp32 2.0.4→2.0.9更新メモ (2023/7)

### きっかけ

* USB2BTなど、つくるっちデバイス以外の開発でつくるっちArduinoの開発環境を使いたかった。
* arduino-esp32とCameraWebServerが2.0.4で止まっており（2.0.6乗り換え失敗）、そろそろ更新したかった。  

### 変更内容

* つくるっちexe廃止！ 今後のつくるっち(scratch)環境はつくるっちwebアプリ、つくるっち(firmware)開発環境はbuildスクリプトをサポート。
* これまでArduinoIDEを使う場合、つくるっちexeに組み込まれた専用のArduinoIDE環境をインストールする必要があったが、既存のArduinoIDEを使用可能に（対応中）

### つくるっちbuildスクリプトについて

* json定義ファイル→firmwareのsrc.inoとscratch3の拡張javascript自動生成。
* ArduinoIDEは他のIDEと異なりprojectの概念が無く、board設定を保持する仕組みが無かった。
また中間生成物についてArduinoIDE起動ごとに初期化されてしまい、ESP32の場合毎回full buildになり10分程度かかった。
つくるっちbuildスクリプトでは簡易的なprojectの機能を持ち、board設定と中間生成物を保持することにより複数のprject開発時のbuild時間短縮と一括buildを実現した。
* 
