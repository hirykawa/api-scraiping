
# api-scraiping

#### Slackから最新のサッカーニュースをスクレイピングから取得することのできるアプリケーションです。

## 使い方

.envでipアドレスを指定してください
<code>

    'dev' => env('IP_DEV'),
    'heroku' => env('IP_HEROKU'),
    'home' => env('IP_HOME'),
    'slack'  => env('SLACK_TOKEN'),
    
</code>

## 現状

一応使うことができるのですが、herokuはcronがクレジット登録必須でつかえないのでAzureへの移行を検討

## APIリファレンス

HerokuのURL
https://slack-soccer.herokuapp.com

## API一覧

|NO.|RequestType|機能概要|
|:---|:---|:---|
|1|POST|URLを登録しトークンを返す|
|2|GET|トークンをもらったらHTMLを返す|
|3|GET|日時とタイプをもらって適応するレコードのリストを返す|

### NO.1
#### ルート

|入力||
|:---|:---|
|アクセスURL|/api/store/url|

#### POSTデータ

|name|型|サイズ|必須|暗号化|検索結果|値の説明|
|:---|:---|:---|:---|:---|:---|:---|
|url|string|255|○|なし|完全一致|有効なURLであること|

#### 出力

|JSON Key|型|サイズ|必須|値の説明|
|:---|:---|:---|:---|:---|
|token|string|255|○|HTMLを引き出す時に必要な値|
|url|string|255|○|入力されたURLを返却する|
|status|string|255|○|成功時 success  失敗時 error:メッセージ|

### NO.2
#### ルート

|入力||
|:---|:---|
|アクセスURL|/api/get/data|

#### POSTデータ

|name|型|サイズ|必須|暗号化|検索結果|値の説明|
|:---|:---|:---|:---|:---|:---|:---|
|token|string|255|○|なし|完全一致|すでに登録されたトークンであること|

#### 出力

|JSON Key|型|サイズ|必須|値の説明|
|:---|:---|:---|:---|:---|
|token|string|255|○|受け取ったトークンを返す|
|html|string|65535|○|スクレイピングしたHTML|
|status|string|255|○|成功時 success  失敗時 error:メッセージ|

### NO.3
#### ルート

|入力||
|:---|:---|
|アクセスURL|/api/get/list|

#### GETデータ

|name|型|サイズ|必須|暗号化|検索条件|値の説明|
|:---|:---|:---|:---|:---|:---|:---|
|start_date|date|不明|○|なし|end_dateよりも前の日付であること|検索をかけるスタートの日付|
|start_date|date|不明|○|なし|start_dateよりも後の日付であること|検索をかける最後の日付|
|start_date|string|255|○|なし|updated_atかもしくはcreated_atであること|どちらのタイプで検索をかけるか|

#### 出力

|JSON Key|型|サイズ|必須|値の説明|
|:---|:---|:---|:---|:---|
|token|string|255|○|それぞれのトークン|
|html|string|65535|○|スクレイピングしたHTML|
|updated_at	|string|不明|○|いつスクレイピングしたか|
|created_at	|string|不明|○|いつURLを登録したか|
|status|string|255|○|成功時 success  失敗時 error:メッセージ|

