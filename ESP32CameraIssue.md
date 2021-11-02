## ESP32 camera deviceでのWifi問題まとめ

ESP32カメラに共通するWifi接続性の問題です。WROOM-32で起きやすく、chip実装で起きにくいです。  
周辺デバイスやI2Sのmaster clockをESP32で生成したときに起きる問題で、カメラ以外でも起きます。

### 対策
- XCLKを20 → 8MHz等にする（20, 10, 5MHzはNG）  
　ov2640の動作clockが1/2.5になってしまうため、ov2640内部の逓倍PLLでx2動作させる  
 
### 試したこと＆考察
0. WROOM-32で起きやすく、chip実装で起きにくい。32/32D/32E間での有意差は確認できず
 
1. I2Sによる10MHz生成（元はLEDC≒PWM）  
　→ NG
 
2. DirectI/Oによる10MHz生成
　→ DevkitCはOKになったが、OKだったaitendo基板がNGになった。  
　　XCLKとWiFi不安定の原因の間でなんらかの同調関係になると問題が起きるらしく、周波数と位相関係の依存性がありそう。
 
3. 最終段のIO_MUXを10MHzから別のI/O(H又はL)にするとOKになる  
　→ IO_MUX、DigitalPads (出力I/Oセル) 周辺で問題が起きている
 
4. XCLK出力 open drain、drive stgrength 最低でもNG。XCLK=GND直結でもNG  
　→ 出力I/Oセル周辺の問題だが、XCLK信号の反射等によるものではない
 
![image](https://user-images.githubusercontent.com/43091864/139958515-1955829e-33e9-46d8-92dd-43f9bbea1107.png)
 
2のことからXCLKと「WiFi不安定原因」の周期との同調が小さい（最大公倍数が大きい）周波数を取ることである程度の対策が可能かも  
→ XCLK=8MにすることでOK
 
### XCLK=8M評価結果

試したデバイスで全てOK。数値は1回のキャプチャの時間ms

