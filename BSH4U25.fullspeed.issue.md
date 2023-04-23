## BUFFALO BSH4U25のFull Speed動作問題

### 背景

USB2BTplus＋BUFFALO BSH4U25(USB2.0 hub)＋USBキーボードの組み合わせで接続できない不具合指摘を頂戴し、解析を行った。  
原因を解析したところ、USB2BTplusの動作に不具合はなく、一方でWindowsPCのUSBポートをFull Speedに制限することで  
WindowsPC＋BSH4U25＋USBキーボードの組み合わせでも不具合を再現できることが分かった。  
（USB2BTplusはfull speedとlow speed接続に対応）

### 結果

BUFFALO BSH4U25はUSB host機器がFull Speed動作の場合、USBキーボードなどのデバイスと安定して接続することができない。  
（WindowsPCとUSB2BTplusにて確認）

<img src="https://user-images.githubusercontent.com/43091864/233819327-fe18d066-9292-4a25-9e5e-6ffb0a6c5e94.JPG" width="400" />

### 解析１：USB hub、USBキーボード組み合わせ検証

* キーボードを固定してUSB hubの動作をwindowsPCで確認、Full Speedに制限するためPC側にFull Speed Hubを接続。

<table border="0">
<tbody>
  <tr>
    <td valign="top">接続失敗回数/テスト回数<br /><img src="https://user-images.githubusercontent.com/43091864/233819653-b03ce516-2d51-4beb-aaf0-9ce40c6cd2fb.png" /></td>
    <td><img src="https://user-images.githubusercontent.com/43091864/233819689-f1bf9a63-73a9-4137-a032-8473dd11fc8f.JPG" width="400" /></td>
  </tr>
</tbody>
</table>


BSH4U25はPCと直接接続(Hi Speed)であれば正しく動作するが、full speed hub経由だと接続できない。このような不具合は他のUSB hubでは確認することが出来なかった。

* full speed接続のBSH4U25について複数のUSB入力デバイスの動作をwindowsPCで確認。

接続失敗回数/テスト回数  

![image](https://user-images.githubusercontent.com/43091864/233820066-4cb45340-8615-49b7-a2da-b8c50699c5ee.png)
<img src="https://user-images.githubusercontent.com/43091864/233820632-a66d8266-e413-4d3f-9df4-6a05ee8727fe.JPG" width="400" />  

full speed接続のBSH4U25との組み合わせで、確認したUSBキーボードは動作せず、USBマウスは動作した。

### 解析２：OK時とNG時のUSBキャプチャデータ比較

* 
