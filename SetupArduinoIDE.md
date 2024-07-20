## つくるっち用ArduinoIDE環境セットアップ

QuadCrawlerAIなどつくるっち用マイコンfirmwareのカスタマイズ環境です、以前TukurutchExeとして公開していたものです。

* ArduinoIDE 1.8.19  
* Arduino-ESP32 2.0.9  
* raspberryPI pico  

**windows10,11のみ対応です。**

### WSL, node.jsインストール
* windows10,11のPCでWSL(WSL2)とubuntuをインストール  
[https://www.google.com/search?q=wsl+ubuntu+install](https://www.google.com/search?q=wsl+ubuntu+install)
* WSLでnodejsをインストール  
```
sudo apt update
sudo apt install -y nodejs
```

### つくるっち用ArduinoIDEをダウンロード・展開

C:￥work フォルダを作成してください。（別の名前でもOK。半角英数、スペースなし、10文字以内、C:ドライブ直下）  
[https://sohta02.sakura.ne.jp/release/Arduino.20240720.zip](https://sohta02.sakura.ne.jp/release/Arduino.20240720.zip)   (3.1GB)  
上記zipファイルをダウンロード＆展開し、得られるArduinoフォルダを上記フォルダに移動してください（C:￥work￥Arduino）。  
<font color="#0000ff">
Windowsではファイルのパス長さが260文字以下という制限があるのですが、Arduino-ESP32に含まれるパスの長さが200文字以上あるためです。  
</font>

### TuKuEutch.extソース取得

githubからfirmwareのソースコードとライブラリ取得。  
[https://github.com/sohtamei/TuKuRutch.ext](https://github.com/sohtamei/TuKuRutch.ext)

上記をC:￥workにclone。下記のようなフォルダ構成にする。  
![image](https://github.com/user-attachments/assets/432cb611-b4cf-41ec-8df1-222194a4a90a)

### robot.json編集方法

robot.json → src.ino自動生成します。記述方法は下記ページを参照して下さい。  
[http://sohta02.web.fc2.com/familyday_extension.html#prepare](http://sohta02.web.fc2.com/familyday_extension.html#prepare)  

### build&書き込み
WSLコマンドラインで./build.shを実行。target=QuadCrawlerAI、UARTポート=COM20のとき
```
cd TuKuRutch.ext/libraries/
./build.sh
usage: build.sh <target> [COM1]
./build.sh QuadCrawlerAI COM20
```
robot.json → src/src.ino自動生成し、build＆FW書き込みします。
**src/src.inoを編集して./build.shを実行すると上書きされます。**

書き込みだけやり直すとき
```
./burn.sh QuadCrawlerAI COM20
```

robot.json → src/src.ino自動生成せず、build＆FW書き込みするとき
```
./build.sh QuadCrawlerAI COM20
```

### wslでnodejsでエラーになるとき
WSLコマンドラインでnodeを実行し、下記エラーになるとき
```
node
bash: /usr/bin/node: cannot execute binary file: Exec format error
```
下記コマンドを実行
```
sudo apt remove --purge nodejs npm
sudo apt autoremove
curl -fsSL https://deb.nodesource.com/setup_20.x | sudo -E bash -
sudo apt install -y nodejs
```
