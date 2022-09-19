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

