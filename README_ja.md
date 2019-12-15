# Bolt ⚡️ を使った開発を始めよう

このリポジトリは、[Slack の Bolt⚡️ フレームワーク](https://slack.dev/bolt/)を使ったアプリのテンプレートです。この README は以下のような Slack アプリを作る手順をカバーしています。

* [CodeSandbox](https://codesandbox.io/)を使う: ステップ 1 -> ステップ 2A
* [Glitch](https://glitch.com/)を使う: ステップ 1 -> ステップ 2B
* ローカルマシン(Linux/macOS/Windows)を使う: ステップ 1 -> ステップ 2C

---

## (ステップ 1) Slack App の初期設定

### Slack App を新規作成

まずは Slack App を https://api.slack.com/apps でつくりましょう。

<img src="https://github.com/seratch/bolt-starter/raw/master/images/create_slack_app.png" width=400 />

### bot ユーザを追加

bot token を取得するために bot user を追加します。

`https://api.slack.com/apps/{APP_ID}/bots`

### Slack App をワークスペースにインストール

さらにいくつかの設定を後ほど行いますが、まずは bot token (`xoxb-***`) を入手するためにワークスペースにインストールしてみてください。

`https://api.slack.com/apps/{APP_ID}/install-on-team`

<img src="https://github.com/seratch/bolt-starter/raw/master/images/oauth.png" width=400 />

---

## (ステップ 2A) CodeSandbox のセットアップ

### GitHub アカウントでログイン

https://codesandbox.io/

2019 年 12 月時点で CodeSandbox は GitHub アカウントのみのログインをサポートしています。GitHub アカウントが必要となりますので、ご準備ください。

### Sandbox を作成

この手順はとても簡単です。この GitHub リポジトリを import 対象として指定して、新規の Sandbox を作ってください。

* `Create Sandbox` をクリック
* `IMPORT` タブへ遷移
* `https://github.com/seratch/bolt-starter` を入力
* `Open Sandbox` をクリック

<img src="https://github.com/seratch/bolt-starter/raw/master/images/codesandbox_github_import.png" width=400 />

すると、テンプレートの Sandbox が作成されますので、これを fork して作業用の Sandbox を作ります。

<img src="https://github.com/seratch/bolt-starter/raw/master/images/codesandbox_fork_template.png" width=400 />

この Sandbox プロジェクトで secrets の値を設定します。

<img src="https://github.com/seratch/bolt-starter/raw/master/images/codesandbox_secrets.png" width=400 />

* SLACK_SIGNING_SECRET: `https://api.slack.com/apps/{APP_ID}/general` Basic Information > App Credentials > Signing Secret
* SLACK_BOT_TOKEN: `https://api.slack.com/apps/{APP_ID}/install-on-team` にある `xoxb-` で始まる Bot User OAuth Access Token

<img src="https://github.com/seratch/bolt-starter/raw/master/images/codesandbox_edit_secrets.png" width=400 />

たった、これだけで完了です！もし変更しても反映されないときは同じ画面の Restart Sandbox ボタンを押してください。

### Request URL (Slack App) を設定

CodeSandbox の右側のペインを見ると `https://{random}.sse.codesandbox.io/` のような URL が表示され、そのアクセス結果が表示されているはずです。

<img src="https://github.com/seratch/bolt-starter/raw/master/images/codesandbox_url.png" width=400 />

この URL に `/slack/events` というパスを加えた `https://{random}.sse.codesandbox.io/slack/events` を Slack App 内の Request URL の項目に設定します。全て同じ URL で OK です。

* `https://api.slack.com/apps/{APP_ID}/event-subscriptions`
* `https://api.slack.com/apps/{APP_ID}/slash-commands`
* `https://api.slack.com/apps/{APP_ID}/interactive-messages`

### Slack App をワークスペースに再インストール

設定が変更されて、再インストールを促されていると思います。もう一度インストールし直してください。

`https://api.slack.com/apps/{APP_ID}/install-on-team`

<img src="https://github.com/seratch/bolt-starter/raw/master/images/oauth.png" width=400 />

---

## (Step 2B) Glitch のセットアップ

https://glitch.com/

### Glitch プロジェクトの作成

手順は CodeSandbox にかなり似ています。

<img src="https://github.com/seratch/bolt-starter/raw/master/images/glitch_clone_repo.png" width=400 />
<img src="https://github.com/seratch/bolt-starter/raw/master/images/glitch_paste_url.png" width=400 />

プロジェクトを作成したら、 `_env` ファイルを複製して `.env` という名前をつけて保存します。`.env` という名前のファイルは特殊なファイルとして認識され、Glitch は自動的に秘匿すべき情報の書かれたファイルとして、あなた以外のユーザには閲覧できないように制御してくれます。

<img src="https://github.com/seratch/bolt-starter/raw/master/images/glitch_duplicate_env.png" width=400 />
<img src="https://github.com/seratch/bolt-starter/raw/master/images/glitch_env_file.png" width=400 />

`.env` の編集が終わったら、アプリが正常に起動できているかログを確認してください。特にエラーのトレースが出ていなければ問題ないでしょう。

<img src="https://github.com/seratch/bolt-starter/raw/master/images/glitch_tools.png" width=400 />
<img src="https://github.com/seratch/bolt-starter/raw/master/images/glitch_logs.png" width=400 />

### Request URL (Slack App) を設定

<img src="https://github.com/seratch/bolt-starter/raw/master/images/glitch_live_app.png" width=400 />

Glitch 上で上記のような手順でアクセスすると Live App の設定のところで `https://{some-fancy-name}.glitch.me/` のような URL を入手できます。

この `https://{some-fancy-name}.glitch.me/slack/events` を Slack App の設定に何箇所か出てくる Request URL として指定します。全て同じ URL で OK です。

* `https://api.slack.com/apps/{APP_ID}/event-subscriptions`
* `https://api.slack.com/apps/{APP_ID}/slash-commands`
* `https://api.slack.com/apps/{APP_ID}/interactive-messages`

### Slack App をワークスペースに再インストール

設定が変更されて、再インストールを促されていると思います。もう一度インストールし直してください。

`https://api.slack.com/apps/{APP_ID}/install-on-team`

<img src="https://github.com/seratch/bolt-starter/raw/master/images/oauth.png" width=400 />

---

## (Step 2C) ローカルマシンをセットアップ

### ngrok をセットアップ

https://ngrok.com/ を使ってインターネットに公開された URL を生成し、ローカルで動いているアプリにリクエストを流します。

```bash
ngrok http 3000
```

もし有償プランに入っている場合は、サブドメインを固定のものに指定することができます。

```bash
ngrok http 3000 --subdomain your-awesome-subdomain
```

<img src="https://github.com/seratch/bolt-starter/raw/master/images/ngrok.png" width=400 />

### Request URL (Slack App) を設定

<img src="https://github.com/seratch/bolt-starter/raw/master/images/request_url.png" width=400 />

`https://{your-awesome-subdomain}.ngrok.io/slack/events` のような URL を以下の Request URL の項目に設定します。全て同じ URL で OK です。

* `https://api.slack.com/apps/{APP_ID}/event-subscriptions`
* `https://api.slack.com/apps/{APP_ID}/slash-commands`
* `https://api.slack.com/apps/{APP_ID}/interactive-messages`

### Slack App をワークスペースに再インストール

設定が変更されて、再インストールを促されていると思います。もう一度インストールし直してください。

`https://api.slack.com/apps/{APP_ID}/install-on-team`

<img src="https://github.com/seratch/bolt-starter/raw/master/images/oauth.png" width=400 />

### Node Version Manager (nvm) のセットアップ

#### Linux / macOS

* [Node Version Manager (nvm)](https://github.com/nvm-sh/nvm#installation-and-update) をインストール
* `nvm install --lts` (最新の LTS バージョンをインストール)

#### Windows

* [nvm-windows](https://github.com/coreybutler/nvm-windows) from [here](https://github.com/coreybutler/nvm-windows/releases) をインストール
* `mvn list available` を実行してダウンロード可能なバージョンを調べる
* `nvm install {最新の LTS バージョン}` (最新の LTS バージョンをインストール)

もし Install Windows Subsystem for Linux (WSL) を使っている場合は `Linux / macOS` と全く同じステップでいけるはずです。

### このテンプレートを使って開発を始める

<img src="https://github.com/seratch/bolt-starter/raw/master/images/use_template.png" width=400 />

あるいは、以下の方法でこのテンプレートをローカルにダウンロードしてください。

`git clone git@github.com:seratch/bolt-starter.git` or https://github.com/seratch/bolt-starter/archive/master.zip

### アプリを起動

```bash
cd bolt-starter
cp _env .env
# edit .env
npm i
npm run local
```

<img src="https://github.com/seratch/bolt-starter/raw/master/images/npm_run_local.png" width=400 />

# ライセンス

The MIT License
