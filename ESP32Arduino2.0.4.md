## つくるっちexe の ArduinoIDE 1.8.11→1.8.19, ESP32 lib 1.0.4→2.0.4更新メモ (2022/8/1)

### 1. ユーザーディレクトリをuser\AppData, user\DocumentsからArduino\portableに移動

* ArduinoIDEを起動し、AppData\Arduino15\* が生成されるので Arduino\portableに移動
* Documents\Arduino\librariesを参照するので、Arduino\portable\librariesに移動

### 2. ESP32 Arduino 2.0.4インストール

環境-board managerに https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json を追加してboard managerでESP32 2.0.4追加

### 3. ESP32にbitrate 750000, 1500000追加

つくるっちexeではM5Atomなどもboard=ESP32でbuildするため、下記定義をArduino\portable\packages\esp32\hardware\esp32\2.0.4\boards.local.txtに追加

~~~boards.local.txt
esp32.menu.UploadSpeed.750000=750000
esp32.menu.UploadSpeed.750000.upload.speed=750000
esp32.menu.UploadSpeed.1500000=1500000
esp32.menu.UploadSpeed.1500000.upload.speed=1500000
~~~

### 4. CameraWebServerソースコード取得&build

新しいCameraWebServerのサンプルソースとprebuild libraryが2.0.4に含まれている。headerファイルの互換性がある下記ソースコードをgithub取得。  
https://github.com/espressif/esp32-camera/tree/8575d75b91c0387037b68b3a864ac6696f6e0a2e  (2022/6/30)

localでビルドするとエラーになるため下記headerファイルをディレクトリ間でコピー
~~~
Arduino\portable\packages\esp32\tools\xtensa-esp32-elf-gcc\gcc8_4_0-esp-2021r2-patch3\xtensa-esp32-elf\include\c++\8.4.0\xtensa-esp32-elf\esp32-psram\bits
Arduino\portable\packages\esp32\tools\xtensa-esp32-elf-gcc\gcc8_4_0-esp-2021r2-patch3\xtensa-esp32-elf\include\c++\8.4.0\bits
c++allocator.h
gthr-default.h
~~~

### 5. M5TimerCamでI2Cエラーが出る

2.0.4でi2c_config_tにパラメータが追加され、0初期化されてないとエラーになる  
memset(&conf, 0, sizeof(i2c_config_t)); 追加

### 6. 

