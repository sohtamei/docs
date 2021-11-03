## ESP32 camera deviceでのWifi問題まとめ

### 概要
ESP32のLEDCやI2Sで5, 10, 20MHzのmaster clock (連続したclock) を出力するとWifiスループットが低下します。  
ESP32カメラで一般的なCameraWebServerで発生します。WROOM-32で起きやすく、chip実装で起きにくいです。  
[https://www.facebook.com/100009187204902/videos/954929518394522/](https://www.facebook.com/100009187204902/videos/954929518394522/)

### 対策
- XCLK(master clock)を20 → 8MHz等にする  
　ov2640の場合動作clockが1/2.5になってしまうため、ov2640内部の逓倍PLLでx2動作させる  
 
### 試したこと＆考察
0. WROOM-32で起きやすく、chip実装で起きにくい。32/32D/32E間での有意差は確認できず
 
1. I2Sによる10MHz生成（元はLEDC≒PWM）  
　→ NG
 
2. DirectI/Oによる10MHz生成  
　→ DevkitCはOKになったが、OKだったaitendo基板がNGになった。  
　　XCLKとWiFi不安定の原因の間でなんらかの同調関係になると問題が起きるらしく、周波数と位相関係の依存性がありそう。
 
3. 最終段のIO_MUXを10MHzから別のI/O(H又はL)にするとOKになる  
　→ IO_MUX、DigitalPads (出力I/Oセル) 周辺で問題が起きている
 
4. XCLK出力 open drain、drive strength 最低でもNG。XCLK=GND直結でもNG  
　→ 出力I/Oセル周辺の問題だが、XCLK信号の反射等によるものではない
 
![image](https://user-images.githubusercontent.com/43091864/139958515-1955829e-33e9-46d8-92dd-43f9bbea1107.png)
 
2のことからXCLKと「WiFi不安定原因」の周期との同調が小さい（最大公倍数が大きい）周波数を取ることである程度の対策が可能かも  
→ XCLK=8MにすることでOK、未知の「WiFi不安定原因」が10MHzで動作している？  
　ノイズ源：不安定要因 ＝ 8MHz：10MHz？ ＝ 4：5 とあまり非同期化できていないため(XCLKから見て4周期に1回程度同期する)、  
　なぜここまで効果があるのか謎。

### テスト環境
この問題はESP32単体で発生。下記に再現環境をリリースします。

0. chromeブラウザで下記URLを開く  
　[https://sohta02.sakura.ne.jp/tukurutch/](https://sohta02.sakura.ne.jp/tukurutch/)

1. 拡張機能(左下ボタン) - [M5Camera,ESP32cam..] 選択

2. [xx 書き込み] - [testXclockIssue]を選択して[xx 書き込み]をクリック  
　FW書き込み開始

3. [接続 ssid ..] でSSID/PASS設定してクリック、[WiFi接続状態] でIP確認

<img src="https://user-images.githubusercontent.com/43091864/139959400-63dfa8a6-8645-49a1-835b-4aa013128257.png" width="300" />  

4. ブラウザからIPにアクセス、ダミー画像の[Get Still] [Start Stream] が可能、xclkの設定変更が可能  
　TeraTermで所要時間を確認することが出来る。

<img src="https://user-images.githubusercontent.com/43091864/139969710-083c0ccc-a817-49ac-b846-8fdb240f49c2.png" width="700" />  

ソースコード：[https://github.com/sohtamei/TuKuRutch.ext/tree/master/libraries/testCamWifi/src](https://github.com/sohtamei/TuKuRutch.ext/tree/master/libraries/testCamWifi/src)

### 評価結果

**XCLK=20MHz、カメラ不要、上記テスト環境**  
<img src="https://user-images.githubusercontent.com/43091864/139960909-c1bd90ec-0595-44d1-afe3-67e02874f64c.png" width="400" />  
chip実装は全てOK。WROOMではaitendoのみOK  
  
**XCLK=8MHz、カメラあり**  
<img src="https://user-images.githubusercontent.com/43091864/139968956-ddacb4a7-6586-4c5f-9791-48acfc9d95fe.png" width="400" />  
全てOK。ov2640 → ESP32転送が有効のため20MHz評価より時間が長くなっているが正常。

**共通**  
ESP32 - AP距離約5m、マンションのため他の世帯からの干渉は多い。

### 対策FW
unitCAM, ESP32CAM用FWをリリース中
1. burn firmware (customized CameraWebServer)  
[https://sohta02.sakura.ne.jp/tukurutch/](https://sohta02.sakura.ne.jp/tukurutch/)  
[Add extension]  
-- [M5Camera,ESP32cam,..]  
-- pulldown [burn (M5Camera)] to "unitCam" or "esp32cam"  
-- click [burn (unitCam)]  
2. enter SSID and pass to [connect ssid ..] and click it.
3. click [Wifi Status] and get IP address
4. access to IP address via web Browser

### LINK
M5Stack Community [https://community.m5stack.com/topic/3649/unitcam-hw-issue-cannot-stream-video](https://community.m5stack.com/topic/3649/unitcam-hw-issue-cannot-stream-video)
Official arduino-esp32 [https://github.com/espressif/arduino-esp32/issues/5834](https://github.com/espressif/arduino-esp32/issues/5834)
