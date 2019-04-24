# stackdriver-line-notify
Stackdriver のからのAlerting通知をLine Notifyに送るための Webhook です。
Google Cloud Functions 関数として使用します。

## デプロイ手順
1. auth.json.sample を参考に、 auth.json を作成する  
```
【auth.json.sample】

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
