## つくるっちでのRTS/DTR制御について
つくるっちではロボットとのUSB接続/切断時（物理的な接続切断でなくアプリ上での接続切断）にロボットをRESETしている。これはAruduinoUnoやNanoがUSB-UART接続/切断時にHW的にRESETしていることに準じている。つくるっちが対応しているATmega328p / ESP32 / SAMD(Koov)はそれぞれDTR/RTSをRESET, BOOT モード切り替えに使っており、各プラットフォームごとに方法が異なる。

| |ATmega328p|ESP32|Koov/SAMD|
|---|---|---|---|
|I/F|3線式 (RxD,TxD,DTR)|4線式 (RxD,TxD,DTR,RTS)|2線式? (RxD,RxD)|
|RESET端子|DTRがC経由で接続,<br />DTR=H->Lの瞬間L|(DTR=H,RTS=L)でL, Cで遅延| |
|EN端子| |(DTR=L,RTS=H)でL| |
|BOOTモード|RESET直後に<br />特定のコマンドを送信|EN端子=LでRESET|1200bpsでUART接続|
|Bootloader書き込み|できない|できる|？|
|Teraterm<br />DTR=H->L, RTS=H->L|接続時RESET|切断時RESET<br /><font color="#ff0000">e: QuadC</font>※PC依存ありそう|なし|
|つくるっち<br />DTR=H->L, RTS=H固定|接続時RESET|なし(切断時SW RESET)<br />※接続中のRESETボタンで<br />BOOTモードになる|なし(切断時SW RESET)|
