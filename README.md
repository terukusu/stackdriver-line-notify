# stackdriver-line-notify
Stackdriver のからのAlerting通知をLine Notifyに送るための Webhook です。
Google Cloud Functions 関数として使用します。

## 前提
* Google Cloud Platform (GCP) へのの登録(無料)は完了している
    * GCP プロジェクトが作成済みでそのプロジェクトで課金が有効になっている
        * 無料枠を利用するだけでも課金の設定が必要
* [gcloud コマンド](https://cloud.google.com/sdk/downloads?hl=JA)がインストール済み
* gcloud コマンドが認証済で、使用するGCPプロジェクトがデフォルトプロジェクトになっている

## 手順
1. auth.json.sample を参考に、 auth.json を作成する
auth.json.sample
```
{
  "auth_token": "aaaaaaaaaaaaa", ← この関数へのアクセス認証用。アクセスするときに auth_token=.... としてクエリ文字列に含めないと 403 Forbidden になる
  "line_token": "bbbbbbbbbbbbbb" ← LINE Notify へのアクセストークン
}
```
※ LINE Notify のアクセストークン取得方法は[この辺り](../../auto-trading-support-tools/wiki/create_line_token)を参考に。


2. コマンドラインから以下を実行する
```
$ gcloud beta functions deploy stackdriverLineNotify --runtime=nodejs10 --entry-point=stackdriverLineNotify --region=asia-northeast1 --memory=128 --trigger-http
```


これで以下のURLを Stackdriver の Alert通知先Webhookとして登録すれば LINE Notify に通知が送られます。
```
https://asia-northeast1-<GCPプロジェクトID>.cloudfunctions.net/stackdriverLineNotify?auth_toke=<関数アクセス用トークン>
```
