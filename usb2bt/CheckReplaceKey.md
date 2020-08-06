## USB2BTplus キー置換動作確認

USB2BTplusのキー置換機能の確認方法です。この例ではキー置換に **HHKBproForMac.csv** を設定しており、  
　無変換 (8B) → 英数 (91)  
　変換　 (8A) → かな (90)  
に置換しています。  

1. USB2BT設定アプリ上で **[このPC(USB接続)]** を選択 (USBパススルー)  

2. **[Debug Start]** を押す  
![CheckReplaceKey2](https://user-images.githubusercontent.com/43091864/89482696-66261880-d7d5-11ea-9b36-4834b60f56d1.png)  
**DebugView** というアプリが立ち上がる。  

3. USBキーボードの **無変換キー** を押す、**変換キー** を押す  
![CheckReplaceKey](https://user-images.githubusercontent.com/43091864/89482692-645c5500-d7d5-11ea-9ff5-b85e5d450ca3.png)  

**DebugView** 上にログが表示される。正しくキー置換されているか確認。h: 00..が変換前、H: 00..が変換後です。  
[25524] h:00008b0000000000 　置換前 (無変換 8b)  
[25524] H:0000910000000000 　置換後 (英数 91)  

4. USB2BT設定アプリの **[Debug Stop]** を押す  

キーコードについてはそーたメイサイトを参照して下さい。  
http://sohta02.web.fc2.com/usb2btp1_setup_j.html#key_remap  
