## つくるっちexe の ArduinoIDE 1.8.11→1.8.19, ESP32 lib 1.0.4→2.0.4更新メモ (2022/8/1)

#### 0. ESP32 Arduino 2.0.4 更新内容

* ESP32 S2/S3/C3対応
* CameraWebServer機能更新

#### 1. ユーザーディレクトリをuser\AppData, user\DocumentsからArduino\portableに移動

* ArduinoIDEを起動し、AppData\Arduino15\* が生成されるので Arduino\portableに移動
* Documents\Arduino\librariesを参照するので、Arduino\portable\librariesに移動

#### 2. ESP32 Arduino 2.0.4インストール

環境-board managerに https://raw.githubusercontent.com/espressif/arduino-esp32/gh-pages/package_esp32_dev_index.json を追加してboard managerでESP32 2.0.4追加

#### 3. ESP32にbitrate 750000, 1500000追加

つくるっちexeではM5Atomなどもboard=ESP32でbuildするため、下記定義をArduino\portable\packages\esp32\hardware\esp32\2.0.4\boards.local.txtに追加

~~~boards.local.txt
esp32.menu.UploadSpeed.750000=750000
esp32.menu.UploadSpeed.750000.upload.speed=750000
esp32.menu.UploadSpeed.1500000=1500000
esp32.menu.UploadSpeed.1500000.upload.speed=1500000
~~~

#### 4. CameraWebServerソースコード取得&build

新しいCameraWebServerのサンプルソースとprebuild libraryが2.0.4に含まれている。headerファイルの互換性がある下記ソースコードをgithub取得。  
https://github.com/espressif/esp32-camera/tree/8575d75b91c0387037b68b3a864ac6696f6e0a2e  (2022/6/30)

localでビルドするとエラーになるため下記headerファイルをディレクトリ間でコピー
~~~
Arduino\portable\packages\esp32\tools\xtensa-esp32-elf-gcc\gcc8_4_0-esp-2021r2-patch3\xtensa-esp32-elf\include\c++\8.4.0\xtensa-esp32-elf\esp32-psram\bits
Arduino\portable\packages\esp32\tools\xtensa-esp32-elf-gcc\gcc8_4_0-esp-2021r2-patch3\xtensa-esp32-elf\include\c++\8.4.0\bits
c++allocator.h
gthr-default.h
~~~

#### 5. I2Cエラーが出る(M5TimerCam)

2.0.4でi2c_config_tにパラメータが追加され、0初期化されてないとエラーになる  
memset(&conf, 0, sizeof(i2c_config_t)); 追加  

https://github.com/sohtamei/TuKuRutch.ext/blob/df0d06ca305b36a7e82eb4026f34a15e4fa1c62c/libraries/M5TimerCam/src/bmm8563.c#L12

#### 6. PWM問題

ledcSetupのlow speedとhigh speedが入れ替わっている？  
1.0.4ではpwm0-7がlow speed, 8-15がhidh speed。  
2.0.4ではpwm0-7がhigh speed, 8-15がlow speed。  
CameraWebServerはtiemr0を使用  

~~~
/*
 * LEDC Chan to Group/Channel/Timer Mapping
** ledc: 0  => Group: 0, Channel: 0, Timer: 0
** ledc: 1  => Group: 0, Channel: 1, Timer: 0
** ledc: 2  => Group: 0, Channel: 2, Timer: 1
** ledc: 3  => Group: 0, Channel: 3, Timer: 1
** ledc: 4  => Group: 0, Channel: 4, Timer: 2
** ledc: 5  => Group: 0, Channel: 5, Timer: 2
** ledc: 6  => Group: 0, Channel: 6, Timer: 3
** ledc: 7  => Group: 0, Channel: 7, Timer: 3
** ledc: 8  => Group: 1, Channel: 0, Timer: 0
** ledc: 9  => Group: 1, Channel: 1, Timer: 0
** ledc: 10 => Group: 1, Channel: 2, Timer: 1
** ledc: 11 => Group: 1, Channel: 3, Timer: 1
** ledc: 12 => Group: 1, Channel: 4, Timer: 2
** ledc: 13 => Group: 1, Channel: 5, Timer: 2
** ledc: 14 => Group: 1, Channel: 6, Timer: 3
** ledc: 15 => Group: 1, Channel: 7, Timer: 3
*/
~~~

#### 7. Staticなclassのコンストラクタ内でattachInterruptするとexception

私のanalogRemoteではコンストラクタ内でattachInterruptしており、globalで analogRemote remote(MODE_NORMAL, /*port*/2, NULL) 宣言して使用するがESP32 2.0.4だとexceptionで落ちる。

~~~
rst:0xc (SW_CPU_RESET),boot:0x13 (SPI_FAST_FLASH_BOOT)
configsip: 0, SPIWP:0xee
clk_drv:0x00,q_drv:0x00,d_drv:0x00,cs0_drv:0x00,hd_drv:0x00,wp_drv:0x00
mode:DIO, clock div:1
load:0x3fff0030,len:1344
load:0x40078000,len:13864
load:0x40080400,len:3608
entry 0x400805f0
E (300) gpio: esp_ipc_call_blocking failed (0x103)
E (589) gpio: gpio_install_isr_service(449): GPIO isr service already installed
Guru Meditation Error: Core  1 panic'ed (LoadProhibited). Exception was unhandled.
Core  1 register dump:
~~~

analogRemote::probeを追加し、setupからattachInterrupuに変更  
https://github.com/sohtamei/analogRemote/commit/3f01835efe01b25e28acfa8b924e79c1dd5be625

#### 8. "GPIO isr service already installed" が出る

既知の問題で、動作上は問題ないらしい  
E (792) gpio: gpio_install_isr_service(449): GPIO isr service already installed  
https://esp32.com/viewtopic.php?f=41&t=23104
