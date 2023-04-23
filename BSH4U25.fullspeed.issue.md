## BUFFALO BSH4U25のFull Speed動作問題

### 背景

USB2BTplus＋BUFFALO BSH4U25(USB2.0 hub)＋USBキーボードの組み合わせで接続できない不具合指摘を頂戴し、解析を行った。  
原因を解析したところUSB2BTplusの動作に不具合はなく、一方でWindowsPCのUSBポートをFull Speedに制限することで  
WindowsPC＋BSH4U25＋USBキーボードの組み合わせでも不具合を再現できることが分かった。

### 結果

BUFFALO BSH4U25はUSB host機器がFull Speed動作の場合、USBキーボードなどのデバイスと安定して接続することができない。  
（WindowsPCとUSB2BTplusにて確認）

![DSC06659s](https://user-images.githubusercontent.com/43091864/233819327-fe18d066-9292-4a25-9e5e-6ffb0a6c5e94.JPG)

### 解析１：* USB hub、USBキーボード組み合わせ検証

* キーボードを固定してhubの動作をwindowsPCで確認

![image](https://user-images.githubusercontent.com/43091864/233819653-b03ce516-2d51-4beb-aaf0-9ce40c6cd2fb.png)
![DSC06657s](https://user-images.githubusercontent.com/43091864/233819689-f1bf9a63-73a9-4137-a032-8473dd11fc8f.JPG)


### 解析２：OK時とNG時のUSBキャプチャデータ比較
* 
