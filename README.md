# 2015/11/15 Java女子部 説明資料

## はじめに
- 今日のプロジェクトの構成
  - こういう感じの図を用意する
    - https://cacoo.com/diagrams/Ybvv5TuxOAGIHMsB
- フレームワークについて
  - 一般的に、フレームワークとは何をさすのか
  - Javaのフレームワークの種類
    - 今日使ったのはSpringBootだけど、他にもいろいろあるよ
- simple-api-sampleが何をしているか簡単に説明
  - TwitterAPIつかうの手間なので用意しました
  - ここでは、つぶやいた情報をデータベースに保存、それを取得することができる。程度の説明で。

## Webアプリケーションについて (目安：20分)
Webアプリケーションの基礎知識について説明

- サーバー/クライアントモデル
  - サーバーは提供する側。クライアントは提供される側。
  - Webアプリの世界にかぎらず、サーバー/クライアントという言葉はつかう
  - 今日説明するのは、あくまでWebアプリでのサーバーとクライアント
- クライアント
  - サーバーに必要な情報を要求し、返却された情報を利用するためのもの
  - WebアプリでいうところのクライアントはWebブラウザ
    - スマホアプリならスマホ端末がクライアント
  - Webブラウザについて
  - HTML・JavaScript・CSS
    - JavaScriptとJavaは違うものなんやで
- サーバー
  - サーバーとは
    - クライアントの要求に応じて、情報を返却するもの
    - サーバー機能を提供するサーバーソフトを使用
      - サーバーソフトは色々な種類がある
        - Apache、nginxなどなど色々種類がある
        - Javaの場合、TomcatとかJettyとか
        - 今日はSpringBootに内蔵されているTomcatを使用している
      - サーバーマシンは何も特殊なPCがいるわけではない
        - みんなのPCもサーバーにできるんやで
          - 時間がありそうなら、発表に使っているマシンでサーバー立ち上げて、そこにみんなでアクセスしてもらう
          - 自前でサーバー立てるとめっちゃたいへんやし今はあんまりみんなやらない
            - 今はそこそこ安くで借りれる
            - 今日のsimple-api-sampleはHerokuってとこに置いていて、ただで使ってる。
- サーバーとクライアントのやり取り
  - 図を作る
  - リクエストとレスポンス
    - リクエスト
    - レスポンス
  - HTTPプロトコル
    - サーバー・クライアント間の通信の取り決め。
    - URL(URI)
    - GET、POST、(PUT、DELETE)
    - ステータスコード

## ワークショップで作ってもらったプロジェクト補足説明
Webアプリの基礎を説明したうえで、今日のプロジェクトがどうなっているか
- HelloWorld! + 名前表示
  - テンプレートエンジンについて説明


- REST APIについて
  - curlでAPIを叩いてみせる？
  - TwitterのAPI仕様書を開いてみせてもよさそう

- リダイレクトについて

## Javaについて (目安：20分)
処理の流れをわかってもらったところで、もう少しコア(Java)な部分を説明

- Javaとは
  - 参考URL：http://docs.oracle.com/javase/jp/8/docs/index.html
    - 簡略化した図を作る？
- 今日のアプリでサーバーを起動した際に何が起きているか
  - コンパイル
    - 一般で言うコンパイルとは、ソースコードをコンピュータが実行できる機械語のプログラムに変換すること
    - Javaの場合、JVMが実行できるバイトコードのクラス・ファイルに変換される
    - Javaのコンパイラはjavac
      - javacコマンドでコンパイルできる
      - IDEのrunボタン叩いたときに裏で実行してくれている
    - コンパイルするにはJDKが必要
      - JDK
        - Java SE Development Kit  の略
        - Java用開発者向けキット
          - アプリケーションを開発するのに必要または便利なコンパイラやデバッガなどの開発ツール (http://docs.oracle.com/javase/jp/8/docs/technotes/guides/index.html#jre-jdk)
        - 一般的に、こういう開発者向けキットを「SDK (Software Development Kit)」という
  - JVM
    - Java仮想マシン
    - Javaで開発されたアプリケーションはこの仮想マシン上で実行される
    - 各OS版のJVMが存在する。OS差異はJVMにより吸収されるため、同じプログラムで各OS上で実行することができる。

    - (こっからは口頭)
    - 今回、runすると内蔵のTomcatが起動して、その上でコンパイルされたプログラムが動く
      - 今日はローカルで動かしてもらっている
      - これを公開したいなら、どっかのサーバーにデプロイすればいい
