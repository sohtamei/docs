## Scratch3.0で独自extensionを使ったサンプルプログラムをリンククリックで開く方法

※[Scratch3.0フォーラムでの投稿](!https://scratch.mit.edu/discuss/topic/337226/?page=2#post-4236202) をまとめたものです

### 課題
ユーザー様にロボットのsb3サンプルプログラムを提供したいのですが、sb3ファイルを配布した場合  
<sb3ダウンロード> - <ローカルに保存> - scratch3.0から<コンピューターから読み込む>   
という手順になってしまい、特にスマフォでユーザー様操作の難易度が高くなってしまいます。  

そこで個人サイト上にsb3を置き、https://scratch.mit.edu/projects/102478814/ のようなリンクの  
クリックでscratch3.0でsb3サンプルプログラムを開きたいのですが、URL クエリパラメータなどの方法で  
任意のサンプルプログラムを開くことは出来ないでしょうか。  

### 保存方法と保存形式
scratch3.0はscratch.mit.eduへのクラウド保存が原則になります。保存形式はsb3に似てますが、ビミョーに異なります。

　共通：project.json(プログラム本体) とassets (wav, svg, png) で構成される

　ローカル保存：上記ファイルをzip圧縮 (.sb3)

　クラウド保存 (例：project ID=412506341、assets=f5cf1fc58bbc69bf8dd47f904e08cb91.pngのとき)：
　　project.json - https://projects.scratch.mit.edu/412506341
　　assets - https://assets.scratch.mit.edu/9230a0b1c1176bf5ce32b3a79f16405b.png

●project ID=412506341として下記２つのサーバーに別のsb3を登録してみました。
　scratch.mit.edu に “Scratch 3.0 is here!.sb3”
　sohta02.sakura.ne.jp/tukurutch に “オシロスコープ.sb3(独自ext入り)”

　それぞれのスクラッチ実行環境では、project IDが同じでもサーバー設定により読み込まれるprojectが異なります。
　1. 本家 https://scratch.mit.edu/projects/412506341/editor
　2. ユカイ工房さんカスタマイズ  https://kurikit.ux-xu.com/scratch/#412506341
　3. そーたメイカスタマイズ http://sohta02.sakura.ne.jp/tukurutch/#412506341

　1と2は “Scratch 3.0 is here!.sb3” になります。独自でscratchサーバーを立ててもprojectの参照先はscratch.mit.eduになります。
　3は “オシロスコープ.sb3” になります。project参照先を下記の通り変更しています。

# scratch-gui/src/lib/project-fetcher-hoc.jsx
    ProjectFetcherComponent.defaultProps = {
        //assetHost: 'https://assets.scratch.mit.edu',
        //projectHost: 'https://projects.scratch.mit.edu'
        assetHost: 'http://sohta02.sakura.ne.jp/tukurutch',
        projectHost: 'http://sohta02.sakura.ne.jp/tukurutch/internalapi'
    };

●まとめ
　- scratch3.0ではsb3を読み込むときあらかじめサーバ上でzip展開＆ファイル名変更 (project.json→9桁projectID) しておく必要がある。
　- 独自extを使ったsb3はscratch.mit.eduには置けないため自分のサーバーで公開する必要がある。
　またその場合参照先をscratch.mit.edu→自分のサーバーに変更しておく必要がある
　- サンプルのリンク方法は＜自分のscratch実行環境＞/#＜9桁projectID＞

