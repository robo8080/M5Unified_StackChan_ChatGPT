# M5Unified_StackChan_ChatGPT
「ChatGPT API搭載AIｽﾀｯｸﾁｬﾝ」です。

![画像1](images/image1.png)<br><br>

これは @mongonta555 さんの[ｽﾀｯｸﾁｬﾝ M5GoBottom版組み立てキット](https://raspberrypi.mongonta.com/about-products-stackchan-m5gobottom-version/ "Title")に対応したｽﾀｯｸﾁｬﾝファームです。<br>

HOYA社が提供する[VoiceText Web APIサービス](https://cloud.voicetext.jp/webapi "Title")を使った音声合成(TTS)を使用しています。<br>
VoiceText TTSは、kghrlaboさんのesp32_text_to_speechを参考にさせていただきました。<br>
オリジナルはこちら。<br>
esp32_text_to_speech <https://github.com/kghrlabo/esp32_text_to_speech><br>

---

### M5GoBottom版ｽﾀｯｸﾁｬﾝ本体を作るのに必要な物、及び作り方 ###
こちらを参照してください。<br>
* [ｽﾀｯｸﾁｬﾝ M5GoBottom版組み立てキット](https://raspberrypi.mongonta.com/about-products-stackchan-m5gobottom-version/ "Title")<br>

### プログラムをビルドするのに必要な物 ###
* [M5Stack Core2](http://www.m5stack.com/ "Title")<br>
* VSCode<br>
* PlatformIO<br>

使用しているライブラリ等は"platformio.ini"を参照してください。<br>

---

### サーボモーターを使用するGPIO番号の設定 ###
* M5Unified_StackChan_ChatGPT.inoの42行目付近、サーボモーターを使用するGPIO番号を設定してください。


### ChatGPTのAPIキーの取得 ###

ChatGPTのAPIキー取得方法は以下の通りです。(詳細はこのページ一番下のリンクを参照してください。)

* [OpenAIのウェブサイト](https://openai.com/ "Title")にアクセスして、アカウントを作成します。メールアドレスと携帯電話番号が必要です。
* アカウント作成後、APIキーを発行します。APIキーは有料ですが、無料期間やクレジットがあります。<br>


### VoiceText Wev API api キーの取得 ###
APIキーは、[ここ](https://cloud.voicetext.jp/webapi/ "Title")の「無料利用登録」から申請すれば、メールで送られて来ます。<br>
* TTSのパラメータの詳細はこちらを参照してください。<br>
[VoiceText Web API [API マニュアル](https://cloud.voicetext.jp/webapi/docs/api/ "Title")]
<br><br>

---

### 使い方 ###
* SDカードのルートに以下の2つのファイルを作成しておくと、使用できるようになります。<br>

1. wifi.txtファイル：ファイル名は"wifi.txt"で、中身は次の通りです。<br>
YOUR_WIFI_SSID<br>
YOUR_WIFI_PASS<br>

2. apikey.txtファイル：ファイル名は"apikey.txt"で、中身は次の通りです。<br>
YOUR_OPENAI_APIKEY<br>
YOUR_VOICETEXT_APIKEY<br>

* もしM5Stackが以前にWifiに接続していた場合、SDカードが必要なく自動的にWifiに接続されます。<br>
この場合、ブラウザで"http://XXX.XXX.XXX.XXX/apikey"にアクセスし、APIキーを設定できます。<br>
(xxxx.xxxx.xxxx.xxxxはAIスタックチャンの起動時に表示されるIPアドレスです。)<br>

* 声の変更には、voiceパラメータを指定できます。<br>
値は0〜4の範囲で指定できます。<br>
例えば、次のように指定します。<br><br>
http://192.168.11.20/chat?voice=4&text=こんにちは<br>
<br>

* ブラウザで"http://xxxx.xxxx.xxxx.xxxx/role"にアクセスすると、ロールを設定できます。<br>
(xxxx.xxxx.xxxx.xxxxはAIスタックチャンの起動時に表示されるIPアドレスです。)<br>
テキストエリアに何も入力せずに送信すると、以前に設定されたロールが削除されます。<br><br>
ロール情報は自動的にspiffsに保存されます。<br>
<br>

* ブラウザで"http://xxxx.xxxx.xxxx.xxxx/role_get"にアクセスすると、現在設定しているロールを取得できます。<br>

* AIスタックチャンの表情を会話内容に合わせて変更できます。<br>
ロール設定で以下の２行をそのまま入力してください。<br><br>
(Happy)のように、必ず括弧で囲んで感情の種類を表し、返答の先頭に付けてください。<br>
感情の種類には、Neutral、Happy、Sleepy、Doubt、Sad、Angryがあります。<br><br>
他にもロールを設定する際は、これらの2行を最後にしてください。<br>
出来ればこの2行のみでやってみてください。<br>
ロールを増やすと失敗しやすくなります。<br>
<br>

* 独り言モードを追加しました。ランダムな時間間隔で、ランダムに喋ります。<br>
感情表現機能と組み合わせると楽しいです。<br>
ボタンAで独り言モードをON/OFFできます。<br>
独り言モードでも従来通りスマホから会話できます。<br>
<br>

* 直近５回分の会話の履歴を保存する機能があります。<br>

* 音声認識プログラムは別途ユーザーが用意する必要があります。<br>
音声認識プログラムからこのようにhttpコマンドでテキスト(UTF-8)を渡します。<br>
(テキストはURLエンコードして渡してください。)<br><br>
http://XXX.XXX.XXX.XXX/chat?text=こんにちは<br><br>
XXX.XXX.XXX.XXXの部分は起動時に表示されるM5StackのIPアドレスに置き換えてください。<br><br>
* 上記と同様にしてブラウザを使ってアクセスすることも出来ます。<br><br>
![画像2](images/image2.png)<br>

* 私は音声認識にiPhoneのショートカット機能を使っています。<br>
このように簡単に音声認識が使えます。<br><br>
![画像3](images/image3.png)<br>

* M5Stack Core2の画面中央付近にタッチするとｽﾀｯｸﾁｬﾝの首振りを止められます。<br>

* M5Stack Core2のボタンCを押すと、音声合成のテストが出来ます。<br>

---

### ChatGPTのAPIキー取得の参考リンク ###

* [ChatGPT API利用方法の簡単解説](https://qiita.com/mikito/items/b69f38c54b362c20e9e6/ "Title")<br>

### VoiceText Wev API api キーのキー取得のリンク ###

* APIキーは、[ここ](https://cloud.voicetext.jp/webapi/ "Title")の「無料利用登録」から申請すれば、メールで送られて来ます。<br>


### ChatGPTのキャラクター設定の参考リンク ###

* [ChatGPTのAPIでキャラクター設定を試してみた](https://note.com/it_navi/n/nf5f702b36a75#8e42f887-fb07-4367-9f3f-ab7f119eb064/ "Title")<br>
<br><br>

