## microbit開発環境について(C言語、他）

### 開発環境比較
つくるっち開発用にいくつかの開発環境を試してみました。
- python環境(Mu&microbit公式)  
v1だと600行以上で「there is no storage space left」になる。
- Makecode/pxt(Javascript)  
hexにJavascriptソースコードを保存するためpython環境より厳しそう
- mbed(C言語)  
microbit v2非対応、v1.5でtiltがちゃんと取れない？
- nordic SDK(C言語)  
BLE関連のライブラリは充実しているがUARTやI2Cなどのライブラリを使うのが大変。Keil uVisionなど有償の開発環境＋ICE＋ライブラリを使うのが一般的。
- Lancaster CODAL(C言語)  
nordicSDKをベースとした無償のライブラリ。
https://tech.microbit.org/software/runtime/
![](https://tech.microbit.org/docs/software/assets/software-overview.svg)

### 数分でUSB/UART通信固まる
原因を探るとUSB/UART処理をしているmicro:bitのDAPLinkが固まっている、固まった状態でもnordicはUARTのRX&TXしている。UART portを閉じて開くと復活する。
- baudrate 115200でNG、公式でOKとなっている9600もNG
https://tech.microbit.org/software/daplink-interface/
- DAPLink 推奨ver253でNG, 最新ver254でNG
- Win10環境のみ確認。ドライバはOS標準のUSB CDC。アプリはchrome(webSerial)とSerialDebuggerで確認。
USB/UART接続はBLE接続と比較してPC側の相性問題や多人数のworkshopでの接続性でメリットがあるため、つくるっちではmicro:bitでのUSB/UART接続とBLE接続の両対応を目指していました。
もしmicro:bitのDAPLinkによるUSB/UART通信について何か情報や、実際にガンガン使いこなしている例をご存じでしたらぜひご教示いただけないでしょうか。上記動画のように500msから200ms周期でのUART通信が必要です。

まだv2だけですが、USB UART(USB CDC)以外の機能をdisableすることによりUART固まる問題は再現していません (現在 60分 = 36000cycle)
結局のところ「UART接続についてはPC依存あり」ということになりそうです。もしかすると「USBドライブの取り外し」でも対処可能かもしれません。
