## つくるっちbuildメモ (自分用)

2022/09/19 作成

### 1.環境

WSL2, ubuntu18.04で作成。node18だとエラーになるためnode16を使用。

~~~
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash

# update
* https://deb.nodesource.com/setup_14.x — Node.js 14 LTS "Fermium" (recommended)
* https://deb.nodesource.com/setup_16.x — Node.js 16 "Gallium"

sudo curl -sL https://deb.nodesource.com/setup_16.x | sudo bash -
sudo curl -sL https://deb.nodesource.com/setup_14.x | sudo bash -
sudo apt-get update
sudo apt-get install nodejs

  npm: '8.15.0',
  node: '16.17.0',
~~~

### 2.ソース取得

~~~
git clone https://github.com/sohtamei/scratch-vm.git
git clone https://github.com/sohtamei/scratch-gui.git
git clone https://github.com/sohtamei/scratch-render.git
~~~

### 3. build

* scratch-render  
~~~
cd scratch-render
npm install
npm link
~~~

* scratch-vm  
~~~
cd scratch-vm
npm install

# 依存性エラーになるためver指定でinstall
npm install @tensorflow/tfjs-core@"^2.8.6"
npm install @tensorflow/tfjs-converter@"^2.8.6"
npm install @tensorflow/tfjs-backend-webgl@"^2.8.6"
npm install @tensorflow-models/facemesh
npm install @tensorflow-models/handpose@"^0.0.6"   # 最新0.0.7だとエラー
# 未使用 (ML2Scratch)
npm install ml5@"^0.5.0"  # 最新0.12.2だとエラー

npm link
npm run build   # guiがdistを参照するため。toioなどうまくいったりいかなかったり
~~~

* scratch-gui  
~~~
npm install
npm install react-responsive@"^4"

rm -rf node_modules/scratch-render node_modules/scratch-vm
npm link scratch-render scratch-vm
npm start

# エラーになるとき - render,vm側でエラーになるとリンクが外れてmoduleになるため確認。
ls -l node_modules/scratch-render node_modules/scratch-vm
~~~
