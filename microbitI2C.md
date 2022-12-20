# micro:bitのI2C接続方法

## I2C接続OLED

* 使うもの

|||
|---|---|
|0.96インチ 128×64ドット有機ELディスプレイ(OLED) 白色|<a href="https://akizukidenshi.com/catalog/g/gP-12031/">https://akizukidenshi.com/catalog/g/gP-12031/</a>|  
|ピンソケット 1x5 リード長10mm|<a href="https://akizukidenshi.com/catalog/g/gC-06360/">https://akizukidenshi.com/catalog/g/gC-06360/</a>|  
|小型クリップ付コード 5色 45cm 5本入|<a href="https://akizukidenshi.com/catalog/g/gC-04351/">https://akizukidenshi.com/catalog/g/gC-04351/</a>|   

* OLEDの足は短いため、足の長いリードソケットを使う。<br />
4pinのピンソケットは販売してないので5pinのピンソケットを1本削って4pinにし、写真の通り足を曲げる。<br />  
<img src="images/microbitI2C1.jpg" width="500">  

* ピンソケットをOLEDに挿し、写真の通りOLEDとmicro:bitを接続。ワニ口同士がショートしないよう注意。<br />
<img src="images/microbitI2C2.jpg" width="500">  

* micro:bitへつくるっちFW書き込み。<br />下記hexファイルを「右クリック」「名前を付けてリンク先を保存」で保存し、micro:bitへダウンロード<br />
<a href="https://sohta02.sakura.ne.jp/tukurutch/static/extensions/Tukurutch.microbitV1.hex">micro:bit V1</a><br />
<a href="https://sohta02.sakura.ne.jp/tukurutch/static/extensions/Tukurutch.microbitV2.hex">micro:bit V2</a>

* chromeブラウザでつくるっちアプリを開く  
<a href="https://sohta02.sakura.ne.jp/tukurutch/#000000542">SSD1306アニメ表示</a>

* I2C= の部分で "d0 c1 microbit" を選択  
![image](https://user-images.githubusercontent.com/43091864/208553803-6c219e16-04c0-481a-9859-a73b2fad671f.png)

* 左端のmicrobitを選択、USBまたはBLEを選択して "接続/切断 .."をクリック。"mbed Serial Port(COM xx)" や "microbit xx" などそれっぽいのを選択して[OK]  
![image](https://user-images.githubusercontent.com/43091864/208554045-2fb50696-d4a7-40d0-98c7-532e6ea722c9.png)  
![image](https://user-images.githubusercontent.com/43091864/208554424-4b74c815-70df-4886-b6e0-d1111fff5e30.png)  
![image](https://user-images.githubusercontent.com/43091864/208554478-ab35fe27-020e-4ec1-a46c-86e5f9f28b38.png)

* 右上の [緑の旗] ![image](https://user-images.githubusercontent.com/43091864/208554668-733e79bd-e1c9-469d-ab49-dfb16c9cab0f.png) を押して実行

