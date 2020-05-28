## つくるっちでのRTS/DTR制御について
つくるっちではロボットとのUSB接続/切断時（物理的な接続切断でなくアプリ上での接続切断）にロボットをRESETしている。これはAruduinoUnoやNanoがUSB-UART接続/切断時にHW的にRESETしていることに準じている。つくるっちが対応しているATmega328p / ESP32 / SAMD(Koov)はそれぞれDTR/RTSをRESET, BOOT モード切り替えに使っており、各プラットフォームごとに方法が異なる。

#### ATmega328p  
I/F : 3線式 (RxD,TxD,DTR)  
　　RESET端子：DTRがC経由で接続, DTRがH->LのときRESET  
BOOTモード : RESET直後に特定のコマンドを送信  
Bootloader書き込み : できない  

#### ESP32 
I/F : 4線式 (RxD,TxD,DTR,RTS)  
　　RESET端子：(DTR=H,RTS=L)でL, Cで遅延  
  　EN端子：(DTR=L,RTS=H)でL  
BOOTモード : EN端子=LでRESET  
Bootloader書き込み : できる  

#### Koov/SAMD 
I/F : 2線式? (RxD,RxD)　マイコンがUSB-UARTを内蔵  
BOOTモード : 1200bpsでUART接続  
Bootloader書き込み : ？  

#### アプリでのDTR/RTS制御とデバイスの挙動
Teratermなど通常のWindows UARTコンソールアプリではUART接続でDTR=H->L, RTS=H->Lになる。  
私の環境ではESP32はUART切断時にRESET=Lとなった。PC依存がありそう。  

つくるっちではUART接続でDTR=H->L, RTS=H固定になる。  
UART接続切断ではRESETはかからない、UART接続中にRESETボタン押しするとBOOTモードになってしまう。  
