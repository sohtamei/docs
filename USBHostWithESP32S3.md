# ESP32S3でのαカメラ用USB host実装

## USBモード切り替え

ESP32S3はRESET直後USB deviceモードになりD+端子はESP32内部で1.5kΩでpullupされる。ESP32起動後にUSB device→hostに切り替えるとpullupは解除される。  
この状態だとLR1ではUSB接続できない。そのため8encoderではD+/D=にアナログスイッチを入れ、boot時はPC(power)側に接続されるようにしている。  

![image](https://github.com/user-attachments/assets/5e4298c7-152a-4f80-bd02-1f8586cb5029)

## CC端子制御


