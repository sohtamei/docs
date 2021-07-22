## microbit開発環境について(C言語、他）

### 開発環境比較
つくるっち開発用にいくつかのmicrobit開発環境を試してみました。
- **Makecode/pxt** (Javascript)  
hexにJavascriptソースコードを保存するため、コードサイズ面ではpython環境より厳しそう。
- **Lancaster CODAL** (C言語)  
nordicSDKをベースとした無償のライブラリ。使い方が良く分かりませんでした。。
- **python環境** (Mu&microbit公式)  
microbit v1だと600行以上で「there is no storage space left」になる。
- **mbed**(C言語)  
microbit v2非対応。
- **nordic SDK** (C言語)  
BLE関連のライブラリは充実しているがUARTやI2Cなどのライブラリを使うのが大変。Keil uVisionなど有償の開発環境＋ICE＋ライブラリを使うのが一般的のよう。
<img src="https://tech.microbit.org/docs/software/assets/software-overview.svg" width="300" />
https://tech.microbit.org/software/runtime/

### microbit用Arduino環境
microbitV2はNordic社nRF52833を搭載、現時点ではマイナーで(通常はnRF52840)、非対応の開発環境が多い。
- **nordicライブラリ**  
nordicがかなり以前にリリースしたArduinoライブラリ、更新されていない。sandeepmistryはこれをベースとしているようです。
- **sandeepmistry**  
nRF51,nRF52用として一般的なArduino環境。Sandeep氏が個人で実装されているようです。  
[arduino-nRF5](https://github.com/sandeepmistry/arduino-nRF5)　nRF用Board環境。nRF51とnRF52に対応、microbitV2(nRF52833)はSoftDevice非対応。  
[arduino-BLEPeripheral](https://github.com/sandeepmistry/arduino-BLEPeripheral)　nRF用BLEライブラリ。nRF51のみ対応。  
- **vladkozlov69**  
sandeepmistryを元に拡張したもの。  
[arduino-BLEPeripheral](https://github.com/vladkozlov69/arduino-BLEPeripheral)　nRF用BLEライブラリ。nRF52に対応、nRF52833は非対応  
- **そーたメイ**  
microbitV2(nRF52833)に対応。arduino-nRF5はsandeepmistryを拡張、arduino-BLEPeripheralはvladkozlov69を拡張  
[arduino-nRF5](https://github.com/sohtamei/arduino-nRF5)  
[arduino-BLEPeripheral](https://github.com/sohtamei/arduino-BLEPeripheral)  

### セットアップ方法
- sandeepmistryのboardmanagerで一式をインストール  
https://sandeepmistry.github.io/arduino-nRF5/package_nRF5_boards_index.json
- 私のarduino-nRF5をdownload - zip、zip展開してArduinoの下記フォルダに上書きコピー  
portable/packages/sandeepmistry/hardware/nRF5/0.7.0
- 私のarduino-BLEPeripheralをzipでライブラリ追加  

### microbit用ArduinoIDE情報
- [Deko氏サイト](https://ht-deko.com/arduino/microbit.html)  
非常にまとまっています、つくるっちのmicrobitFWはDeko氏のLEDライブラリを使用しています。
- https://learn.adafruit.com/use-micro-bit-with-arduino

