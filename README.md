# Scratch2.0-Chaser-base
# フォルダの説明
* Procon-Server       ゲームサーバ一式(プロコンサーバー)
* Scratchセーブデータ  スクリプト保存先
* logs                ゲームサーバによって利用されるフォルダ
* source code         procon.exeのソースコード
* マップ               ゲームサーバにで利用できるマップ
* IPアドレスをたしかめる.exe localhostのIPアドレスを表示
* NaganoProconClient.exe コンパイル済みのbot
* Procon-Server.exe.lnk ゲームサーバのショートカット
* Scratchサーバー起動.bat procon.exeを最小化で起動するスクリプト
* procon.exe http to Socket
* プロコン拡張パッチ日本語版 HTTP Extensions のブロック情報

# Scratchに追加されるブロック
## スタックブロック
* ゲームサーバーを起動する
* IPアドレスの設定をする
* ポート番号の設定をする
* チーム名の設定をする
* ゲームサーバーに接続する
* リセットをする
* 自分のターンを待つ
*  に移動する
*  の周りを見る
*  の遠くまで見る
*  にブロックを置く
## 値ブロック
* ゲームの状態   
* 1 マス目
* 2 マス目
* 3 マス目
* 4 マス目
* 5 マス目
* 6 マス目
* 7 マス目
* 8 マス目
* 9 マス目
* 全てのマス目

# プログラムについて
Chaser(プロコンサーバー)に準拠した順序でスタックブロックや値ブロックを組み合わせ通信を行います。
procon.exeは12345ポートでhttpリクエストをlistenします。起動できはい場合はポートが他のプログラムによってlistenされていないことを確認してください。
IPアドレスの初期値は127.0.0.1
ポートは2009です。
「IPアドレスの設定をする」「ポート番号の設定をする」を実行することで変更する事ができます。
# 対戦について
procon.exeはPC1台につき1プロセスしか動作しません。
よってScratchとScratchの対戦はPCが2台必要になることを注意してください。
その際接続がうまく行かない場合は、IP及びポート番号、windowsのファイアウォールの設定が正しくできているかを確認してください。
# 使い方
Scratchで書かれたbotとC#のbotの対戦は、以下の通りに動作します。
COOLとHOTの接続方法は、Chaserの仕様書を確認してください。
![demo](https://raw.githubusercontent.com/kayamalab/Scratch2.0-Chaser-base/master/image/howtouse.gif)
# リセットについて
procon.exeはゲームの状態を保持しています。そのため再度対戦を行う場合は、リセットブロックを実行し、内部状態を初期化する必要があります。

# スタックブロックについて
## ゲームサーバーを起動する
Procon-Server/Procon-Server.exeを起動します
## IPアドレスの設定をする
プロコンサーバーのIPアドレスを指定します。ローカルでは[127.0.0.1]です。対戦を行う場合は変更が必要になります
## ポート番号の設定をする
プロコンサーバーのポート番号を指定します。coolは2009 hotは2010 が初期値です。
## チーム名の設定をする]
プロコンサーバーに通知するチーム名を指定します。
## ゲームサーバーに接続する
設定されたIPとポートを使用し、プロコンサーバーに接続を行います。初期値が内部で設定されているため、IPとポートを設定しなくても、プロコンサーバーに接続できることがあります。
## リセットをする
プロコンサーバーとの接続を終了し、リセットを行います。基本的にはゲーム終了後に、この実行ファイルを再度起動する手間を省くためのものです。
## 自分のターンを待つ
プロコンサーバーに対して、「getready」を送信します。プロコンサーバーに接続されていなければ処理はスキップされます。ターン中に実行した場合、処理をスキップする保護機能があります。
## に移動する
プロコンサーバーに対して、「walk」を送信します。プロコンサーバーに接続されていなければ処理はスキップされます。ターン外に実行した場合、処理をスキップする保護機能があります。
## の周りを見る
プロコンサーバーに対して、「look」を送信します。プロコンサーバーに接続されていなければ処理はスキップされます。ターン外に実行した場合、処理をスキップする保護機能があります。
## の遠くまで見る
プロコンサーバーに対して、「search」を送信します。プロコンサーバーに接続されていなければ処理はスキップされます。ターン外に実行した場合、処理をスキップする保護機能があります。
## にブロックを置く
"プロコンサーバーに対して、「put」を送信します。プロコンサーバーに接続されていなければ処理はスキップされます。ターン外に実行した場合、処理をスキップする保護機能があります。
# 値ブロックについて
## ゲームの状態
[ゲーム前,ゲーム中,ゲーム終了]=[0,1,2]
の値を保持します。ただし、プロコンサーバーの実装上の不備により、COOL側にはゲーム終了のステータスレスポンスが送られずにゲームが終了するため、ゲーム終了判定の信頼性はあまりないでしょう。
## nマス目
プロコンサーバーから送られる配列がマス目に直されています。周辺情報、やLOOK searchの結果がここに反映されます。
すべて上書きの扱いになるので、値を保持する場合は変数を利用しましょう。
## 全てのマス目
配列を返します。
