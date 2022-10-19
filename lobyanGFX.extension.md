## つくるっち - lovyanGFX拡張対応デバイス

### I2C LCDデバイス

|config|LCD名称|controller|size|
|:---|:---|:---|:---:|
|SSD1306|I2Cモノクロ|SSD1306|128x64|
|SSD1306|I2Cモノクロ|SSD1315|128x64|
|SSD1306_32|I2Cモノクロ|SSD1306|128x32|

デフォルトポート: sda=21,scl=22

### SPI LCDデバイス

|config|LCD名称|controller|size|sclk|mosi|miso|dc|cs|rst|busy|bl|
|:---|:---|:---|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|:---:|
|SSD1331| |SSD1331|96x64|32|33| |26|27|25| | |
|3248S035|3248S035|GC9A01|320x480|14|13|12|2|15| | |27|
|RoundLCD|RoundLCD(クラッカー)|GC9A01|240x240|14|12| |16|17|15| |13|
|RoundLCD|RoundLCD(stampC3)|GC9A01|240x240|4|6| |1|7|0| |10|
|RoundLCD|RoundLCD(pico)|GC9A01|240x240|18|19| |11|13|12| |10|
|MSP2807|MSP2807|ILI9341|240x320|25|26|32|27|12|14| |33|

### lovyanGFX自動認識デバイス

|config|LCD名称|controller|size|
|:---|:---|:---|:---:|
|AUTO|M5Stack| |320x240|
|AUTO|Core2| |320x240|
|AUTO_ROLL|M5StickC|ST7735S|80x160|
|AUTO_ROLL|M5StickCplus|ST7789|135x240|
|AUTO|CoreInk| | |
|AUTO_ROLL|M5Paper| | |
|AUTO|M5Tough| | |
|AUTO|ODROID-GO| | |
|AUTO|TTGO TS| | |
|AUTO|TTGO T-Watch| | |
|AUTO|DSTIKE D-duino-32 XS| | |
|AUTO|LoLinD32 PRO| | |
|AUTO|ESP32_WROVER_KIT| | |
