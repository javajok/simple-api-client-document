# 2015/11/15 Java女子部 説明資料

## Webアプリケーションについて (20分)
Webアプリケーションの基礎知識について説明

- サーバー/クライアントモデル
  - サーバーは提供する側。クライアントは提供される側。
  - Webアプリの世界にかぎらず、サーバー/クライアントという言葉はつかう
  - 今日説明するのは、あくまでWebアプリでのサーバーとクライアント
- クライアント
  - サーバーに必要な情報を要求し、返却された情報を利用するためのもの
  - Webアプリでいうところのクライアントはブラウザにあたる
    - これがスマホアプリならスマホ端末がクライアント
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
    - GET、POST、(PUT、DELETE)
    - ステータスコード

## ワークショップで作ってもらったプロジェクト説明 (20分)
Webアプリの基礎を説明したうえで、今日のプロジェクトがどうなっているか

- 今日のプロジェクトの構成
  - こういう感じの図を用意する
    - https://cacoo.com/diagrams/Ybvv5TuxOAGIHMsB
- フレームワークについて
  - 一般的に、フレームワークとは何をさすのか
  - Javaのフレームワークの種類
    - 今日使ったのはSpringBootだけど、他にもいろいろあるよ
- simple-api-sampleが何をしているか簡単に説明
  - ここでは、つぶやいた情報をデータベースに保存、それを取得することができる。程度の説明で。
- REST APIについて
  - curlでAPIを叩いてみせる？
  - TwitterのAPI仕様書を開いてみせてもよさそう
- タイムライン取得をしたときに何がおきているか(GET)
  - ブラウザでhttp://localhost:8080/sample にアクセス
    - メソッドはGET
  - https://github.com/javajok/simple-api-client-sample/blob/master/src/main/java/javajok/sample/TweetController.java#L46 が実行される
    - https://github.com/javajok/simple-api-client-sample/blob/master/src/main/java/javajok/sample/TweetController.java#L58
      - http://localhost:8090/timeline にGETでアクセス、タイムラインを取得
      - TimelineはTweetのリスト
      - デバッグで止めて、timelineに何が入ってるか見せるといいのかもしれない
    - https://github.com/javajok/simple-api-client-sample/blob/master/src/main/java/javajok/sample/TweetController.java#L69
      - 取得したtimelineをhtmlで使えるようにするための処理。詳しくはあとで。
    - https://github.com/javajok/simple-api-client-sample/blob/master/src/main/java/javajok/sample/TweetController.java#L76
      - templates/sample/timeline.html を呼び出す
    - テンプレートエンジンについて説明
    - https://github.com/javajok/simple-api-client-sample/blob/master/src/main/resources/templates/sample/timeline.html#L37
      - さっき、Controllerで ``` model.addAttribute(timeline); ``` って書いたから使えてる
    - Controllerから受け取った値を埋め込んだ結果のHTMLを生成、クライアントに返している
- tweetしたときに何がおきているか(POST)
  - https://github.com/javajok/simple-api-client-sample/blob/master/src/main/resources/templates/sample/timeline.html#L24
    -  ``` method="post" ```だからPOST実行される
  - あとはGET同様、処理の流れを説明

## Javaについて (20分)
処理の流れをわかってもらったところで、もう少しコア(Java)な部分を説明

- Javaとは
  - 歴史をさらっと
    - Sun Microsystems社が開発
    - 2010年 Oracleが買収
      - 【確認事項】Oracleの製品という表現をしてよい？？
    - 最新バージョンは8
  - オブジェクト指向言語である
    - オブジェクト指向自体の説明はしない
  - 参考URL：http://docs.oracle.com/javase/jp/8/docs/index.html
    - 簡略化した図を作る？
- 今日のアプリでサーバーを起動した際に何が起きているか
  - ```./gradlew bootRun```
    - Gradleというビルドツールを利用して起動
    - ビルドツールとは
  - コンパイル
    - 一般で言うコンパイルとは、ソースコードをコンピュータが実行できる機械語のプログラムに変換すること
    - Javaの場合、JVMが実行できるバイトコードのクラス・ファイルに変換される
    - Javaのコンパイラはjavac
      - javacコマンドでコンパイルできる
      - 今回はGradleがrunコマンド叩いたときに裏で実行してくれている
    - コンパイルするにはJDKが必要
      - JDK
        - Java SE Development Kit  の略
        - Java用開発者向けキット
          - アプリケーションを開発するのに必要または便利なコンパイラやデバッガなどの開発ツール (http://docs.oracle.com/javase/jp/8/docs/technotes/guides/index.html#jre-jdk)
          - JREも含んでいる
        - 一般的に、こういう開発者向けキットを「SDK (Software Development Kit)」という
  - JVM
    - Java仮想マシン
    - Javaで開発されたアプリケーションはこの仮想マシン上で実行される
    - 各OS版のJVMが存在する。OS差異はJVMにより吸収されるため、同じプログラムで各OS上で実行することができる。
      - 【確認事項】と言い切ってしまって大丈夫なのかどうか。
        - 「実行することを目指している」の方がいい？
    - 今回、runすると内蔵のTomcatが起動して、その上でコンパイルされたプログラムが動く
      - 今日はローカルで動かしてもらっている
      - これを公開したいなら、どっかのサーバーにデプロイすればいい

## (おまけ) データベースについて
  時間があればsimple-api-sampleを元に説明してもいいかも
