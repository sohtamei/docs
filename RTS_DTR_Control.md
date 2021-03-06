## つくるっちでのDTR/RTS制御について
つくるっちではロボットとの接続/切断時（物理的な接続切断でなくアプリ上での接続切断）にロボットをRESETしてます。つくるっちが対応しているATmega328p / ESP32 / SAMD(Koov)はそれぞれUARTのDTR/RTS信号をRESET, BOOT モード切り替えに使っており、各プラットフォームごとに方法が異なります。

| |ATmega328p|ESP32|Koov/SAMD|
|---|---|---|---|
|I/F|3線式 (RxD,TxD,DTR)|4線式 (RxD,TxD,DTR,RTS)|2線式? (RxD,TxD)<br />マイコン内蔵|
|RESET端子(EN端子)|DTRがC経由で接続,<br />DTR=H->Lの瞬間L|(DTR=H,RTS=L)でL, Cで遅延| |
|MODE端子(IO0)| |(DTR=L,RTS=H)でL| |
|BOOTモード|RESET直後に<br />特定のコマンドを送信|MODE端子=LでRESET<br />(DTR=H->L, RTS=L->H)|1200bpsでUART接続|
|Bootloader書き込み|できない|できる|？|
|Teraterm<br />接続=(DTR=H->L,RTS=H->L)|接続時RESET|切断時RESET `※PC依存ありそう`|なし|
|つくるっち<br />接続=(DTR=H->L,RTS=H固定)|接続時RESET|なし(切断時ソフトRESET)<br />`※接続中のRESETボタンで`<br />`BOOTモードになる`|なし(切断時ソフトRESET)|
|serialWeb<br />接続=(DTR=H->L,RTS=H->L)|接続時RESET|なし| - |

DevkitCの回路図より  
![image8](images/image8.png)  
