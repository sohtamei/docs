## Scratch3.0で独自extensionを使ったサンプルプログラムをリンククリックで開く方法

※ [Scratch3.0フォーラムでの投稿](https://scratch.mit.edu/discuss/topic/337226/?page=2#post-4236202) をまとめたものです

### 課題
ユーザー様にロボットのsb3サンプルプログラムを提供したいのですが、sb3ファイルを配布した場合  
**<sb3ダウンロード> - <ローカルに保存> - scratch3.0から<コンピューターから読み込む>**   
という手順になってしまい、特にスマフォでユーザー様操作の難易度が高くなってしまいます。  

そこで個人サイト上にsb3を置き、https://projects.scratch.mit.edu/412506341 のようなリンクの  
クリックでscratch3.0でsb3サンプルプログラムを開きたいのですが、URL クエリパラメータなどの方法で  
任意のサンプルプログラムを開くことは出来ないでしょうか。  

### 解決方法
- scratch3.0ではsb3を読み込むときあらかじめサーバー上でzip展開＆ファイル名変更 (project.json→9桁projectID) しておく必要がある。  
参照先サーバーはデフォルトでscratch.mit.eduになっている。  
- 独自extを使ったsb3はscratch.mit.eduには置けないため自分のサーバーで公開する必要がある。  
またその場合scratch実行環境の設定(プログラム参照先)をscratch.mit.edu→自分のサーバーに変更しておく必要がある  
- サンプルのリンク方法は  
editor : ＜自分のscratch実行環境＞/#＜9桁projectID＞  
player : ＜自分のscratch実行環境＞/player.html#＜9桁projectID＞  

以下詳細

### 保存方法と保存形式
scratch3.0はscratch.mit.eduへのクラウド保存が原則になります。保存形式はsb3に似てますが、ビミョーに異なります。

　共通：project.json(プログラム本体) とassets (wav, svg, png) で構成される

　ローカル保存：上記ファイルをzip圧縮 (.sb3)

　クラウド保存 (例：project ID=412506341、assets=f5cf1fc58bbc69bf8dd47f904e08cb91.pngのとき)：  
　　project.json - https://projects.scratch.mit.edu/412506341  
　　assets - https://assets.scratch.mit.edu/internalapi/asset/9230a0b1c1176bf5ce32b3a79f16405b.png/get/  

### 実験
下記２つのサーバーに同じproject ID=412506341で２つのsb3を登録してみました。  
　scratch.mit.edu に “Scratch 3.0 is here!.sb3”  
　sohta02.sakura.ne.jp/tukurutch に “オシロスコープ.sb3(独自ext入り)”  

下記３つのスクラッチ実行環境では、project IDが同じでも実行環境の設定により読み込まれるsb3が異なります。  
　1. 本家実行環境 https://scratch.mit.edu/projects/412506341/editor  
　2. ユカイ工房さん実行環境 https://kurikit.ux-xu.com/scratch/#412506341  
　3. そーたメイ実行環境 http://sohta02.sakura.ne.jp/tukurutch/#412506341  

1と2は “Scratch 3.0 is here!.sb3” になります。独自で実行環境を用意してもprojectの参照先はscratch.mit.eduになります。  
scratch.mit.eduには独自extを使ったプログラムを置くことは出来ません。  
 
3は “オシロスコープ.sb3” になります。実行環境のproject参照先を下記の通り変更しています。  

    # scratch-gui/src/lib/project-fetcher-hoc.jsx
    ProjectFetcherComponent.defaultProps = {  
        //assetHost: 'https://assets.scratch.mit.edu',  
        //projectHost: 'https://projects.scratch.mit.edu'  
        assetHost: 'http://sohta02.sakura.ne.jp/tukurutch',  
        projectHost: 'http://sohta02.sakura.ne.jp/tukurutch/internalapi'  
    };  

### 実装例：そーたメイサイトでのサンプルプログラム配置状態とリンク先
**配置**  
http://sohta02.sakura.ne.jp/tukurutch/internalapi/412506341 (sb3のproject.json)
http://sohta02.sakura.ne.jp/tukurutch/internalapi/asset/83a9787d4cb6f3b7632b4ddfebf74367.wav
http://sohta02.sakura.ne.jp/tukurutch/internalapi/asset/83c36d806dc92327b9e7049a565c6bff.wav
http://sohta02.sakura.ne.jp/tukurutch/internalapi/asset/b7853f557e4426412e64bb3da6531a99.svg
http://sohta02.sakura.ne.jp/tukurutch/internalapi/asset/cd21514d0531fdffb22204e0ec5ed84a.svg
http://sohta02.sakura.ne.jp/tukurutch/internalapi/asset/e6ddc55a6ddd9cc9d84fe0b4c21e016f.svg
http://sohta02.sakura.ne.jp/tukurutch/internalapi/asset/f5cf1fc58bbc69bf8dd47f904e08cb91.png

**リンク先**  
http://sohta02.sakura.ne.jp/tukurutch/#412506341

**実行環境設定**  
assetHost: 'http://sohta02.sakura.ne.jp/tukurutch',  
projectHost: 'http://sohta02.sakura.ne.jp/tukurutch/internalapi'  

### 備考
> - 独自extを使ったsb3はscratch.mit.eduには置けないため自分のサーバーで公開する必要がある。  

scratchの規定4.4に「 "a modified version of the Scratch editor" で作成されたprojectはscratchサーバーにupできない」と規定されています。上記制約はこの規定と関連があるかもしれません。    
https://scratch.mit.edu/terms_of_use  
4.4 You may only submit user-generated projects that were created with (1) the Scratch website editor or (2) an unmodified copy of the Scratch editor compiled from the source code described in Section 5.3. You may not upload any projects that were created, by you or by anyone else, with a modified version of the Scratch editor.  
