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
→ XCLK=8MにすることでOK。なぜ8MHzだとOKなのかよくわからない、「WiFi不安定原因」が10MHzで動作している？

### テスト環境
この問題はESP32単体で発生。下記に再現環境をリリースします。

0. chromeブラウザで下記URLを開く  
　https://sohta02.sakura.ne.jp/tukurutch/

1. 拡張機能(左下ボタン) - [M5Camera,ESP32cam..] 選択

2. [xx 書き込み] - [testXclockIssue]を選択して[xx 書き込み]をクリック  
　FW書き込み開始

3. [接続 ssid ..] でSSID/PASS設定してクリック

4. [WiFi接続状態] でIP確認、ブラウザからIPにアクセス

![image](https://user-images.githubusercontent.com/43091864/139959400-63dfa8a6-8645-49a1-835b-4aa013128257.png)
 
### 評価結果

XCLK=20MHz、カメラ不要、上記テスト環境  
![image](https://user-images.githubusercontent.com/43091864/139960909-c1bd90ec-0595-44d1-afe3-67e02874f64c.png)    
chip実装は全てOK。WROOMではaitendoのみOK

XCLK=8MHz、カメラあり  
![image](https://user-images.githubusercontent.com/43091864/139968956-ddacb4a7-6586-4c5f-9791-48acfc9d95fe.png)  
全てOK

共通
ESP32 - AP距離約5m、マンションのため他の世帯からの干渉は多い。

### LINK
M5Stack Community https://community.m5stack.com/topic/3649/unitcam-hw-issue-cannot-stream-video
