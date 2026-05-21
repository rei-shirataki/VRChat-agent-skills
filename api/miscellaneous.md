---
scope: api
title: VRChat REST API — Miscellaneous
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Miscellaneous

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

他のカテゴリに分類されない汎用エンドポイントです。

## エンドポイント一覧

| メソッド | パス | operationId | 認証 | 説明 |
|---|---|---|---|---|
| GET | `/config` | getConfig | 不要 | APIの設定情報を取得 |
| GET | `/health` | getHealth | 不要 | APIの稼働状態を確認 |
| GET | `/time` | getSystemTime | 不要 | サーバーの現在時刻を取得 |
| GET | `/visits` | getCurrentOnlineUsers | 不要 | 現在のオンラインユーザー数を取得 |
| GET | `/infoPush` | getInfoPush | 不要 | インフォメーション通知を取得 |
| GET | `/auth/permissions` | getAssignedPermissions | 必須 | 自分に付与されているパーミッション一覧 |
| GET | `/css/app.css` | getCSS | 不要 | フロントエンドのCSSを取得（302リダイレクト） |
| GET | `/js/app.js` | getJavaScript | 不要 | フロントエンドのJSを取得（302リダイレクト） |

## 主な用途

### `GET /config`

APIの動作設定（利用規約バージョン・機能フラグ・制限値等）を含むオブジェクトを返します。
アプリ起動時のヘルスチェックや設定取得に使用されます。

### `GET /health`

```json
{ "ok": true, "serverName": "...", "buildVersionTag": "..." }
```

APIが正常稼働しているかを確認します。

### `GET /time`

サーバーの現在時刻（UTC）を返します。クライアントとサーバーの時刻同期に使用できます。

### `GET /visits`

現在オンラインのユーザー数を整数で返します。

### `GET /auth/permissions`

VRC+ 等のサブスクリプションによって付与されているパーミッション情報を返します。

## 注意事項

- `/css/app.css` と `/js/app.js` は Cloudfront への 302 リダイレクトを返します。HTTPライブラリがリダイレクト追従に対応している必要があります
- `/permissions`（管理者向け）と `/auth/permissions`（一般ユーザー向け）は別のエンドポイントです
