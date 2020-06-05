## つくるっち 現在の不具合

- (2020/5) Clean buildの方法がない
- (2020/5) undeleteが動かない
- (2020/5) RoverC + USB/PCMode動かない
- (2020/5) ペン色スポイト色指定固まる
- (2020/5) 別のロボットのサンプルプログラムを開いたとき、非対応ブロックが多すぎてOKが押せない場合がある

## 今後の機能対応

- Arduino Mode 文字変数対応 (現在は数値変数のみ)
- thing speak対応
- port解放、宅外アクセス対応

## ごめんなさい不具合

- (ESP32版) [NTTルーター PR-400MI問題](PR400MI_issue.md)
- (ESP32版) C:￥以外で展開するとパスエラーになる
- (ESP32版) [USB接続でつくるっち接続中に本体RESETするとESP32がBOOTモードになる](RTS_DTR_Control.md)
