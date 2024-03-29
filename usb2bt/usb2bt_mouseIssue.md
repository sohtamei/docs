### USB2BT/plusでUSBマウスの挙動がおかしい不具合について

USB2BTplusと手元のUSBマウス4台で確認を行い結果をまとめてみました。  
マウスによってスムーズなもの(HP)と軌跡がとぶもの(dell)があります。原因はUSB→Bluetooth変換時のpacketの取りこぼしが原因です。  

|  | 型番 | 結果 |
|---|---|---|
| MS1 | Microsoft Optical Mouse 200 | 全く正常に動作せず（マウス軌跡が暴れる） |
| MS2 | Microsoft LaserMouse 6000 | ぶれる |
| HP | HP MOFYUO | ぶれない |
| Dell | Dell MS111-L | 引っかかる |
| (参考)X5 | 市販BTマウス | |

USBの規格上は最短で1ms周期でのデータ読み取りが規定されており、一般的なマウスでは1ms周期でのデータ読み取りに対応しています。  
一方でBluetoothは通信上の制約により最短でも数ms周期でしかデータ読み取りができません。1ms周期でのデータ読み取りが出来ないとき、  

* データが化けてしまうマウス (MS1)
* その間のデータを破棄するマウス (MS2, Dell)
* その間のデータを蓄積するマウス (HP)

の3タイプがあるようです。 
BluetoothとUSBの通信方式の違いから発生する問題で、対応は困難です、非常に申し訳ありません。。  
<img src="https://user-images.githubusercontent.com/43091864/157574129-0143100d-1b48-4588-a6ac-48e154490388.png" width="400" />
