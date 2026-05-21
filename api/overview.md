---
scope: api
title: VRChat REST API — 概要・認証
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — 概要・認証

## 重要な前提

> **このAPIはVRChatによる公式サポートなし。**  
> コミュニティがリバースエンジニアリングで維持するドキュメントであり、予告なく変更・廃止される可能性があります。  
> **乱用するとアカウント停止のリスクがあります。**

ドキュメント: [vrchat.community](https://vrchat.community/)  
OpenAPI仕様: [github.com/vrchatapi/specification](https://github.com/vrchatapi/specification)

## ベースURL

```
https://api.vrchat.cloud/api/1
```

## セキュリティスキーム

| 名前 | 種別 | 説明 |
|---|---|---|
| `authCookie` | Cookie | `auth` Cookie によるセッション認証 |
| `authHeader` | HTTP Basic | `Authorization: Basic {base64}` によるログイン時認証 |
| `twoFactorAuthCookie` | Cookie | `twoFactorAuth` Cookie による2FA済み状態の維持 |

## 認証フロー

### 1. ログイン

```
GET /auth/user
Authorization: Basic {base64(urlencode(username):urlencode(password))}
```

- `{base64(...)}` は `username` と `password` を**それぞれURLエンコード**してコロンで結合し、Base64エンコードしたもの
- 成功すると `auth` Cookie と `twoFactorAuth` Cookie が Set-Cookie で返される
- **以降のリクエストは `auth` Cookie を送り続けることでセッションを維持**

> **WARNING**: ログインするたびに新しいセッションを消費します。同時セッション数には上限があります（上限値は非公開）。  
> **`auth` Cookie を保存・再利用してください。** 毎回ログインするとすぐにセッション上限に達します。

### 2. 2FAが必要な場合

ログインレスポンスで `requiresTwoFactorAuth` が返される場合、以下のいずれかで2FAを完了させます：

| エンドポイント | 用途 |
|---|---|
| `POST /auth/twofactorauth/totp/verify` | TOTP（認証アプリ）コード |
| `POST /auth/twofactorauth/emailotp/verify` | メールOTPコード |
| `POST /auth/twofactorauth/otp/verify` | リカバリーコード |

```json
{ "code": "123456" }
```

### 3. セッション確認

```
GET /auth
```

現在の `auth` Cookie が有効かどうかを検証します。

### 4. ログアウト

```
PUT /logout
Cookie: auth=...
```

セッションを無効化します。

## 共通ヘッダー

| ヘッダー | 値 | 説明 |
|---|---|---|
| `User-Agent` | `MyApp/1.0 contact@example.com` | 識別子として必須（空だとブロックされることあり） |
| `Content-Type` | `application/json` | POSTリクエスト時 |
| `Cookie` | `auth=authcookie_...` | 認証済みリクエスト時 |

## レート制限

- HTTP 429 が返された場合は**指数バックオフ**で再試行（初回1秒、以降倍増）
- レート制限のタイミングや閾値は一定ではなく予測不可能
- データは積極的にキャッシュして不要なAPIコールを減らすこと
- 429 を受け取ったら即座に停止すること

## エンドポイントカテゴリ

| カテゴリ | エンドポイント数 | 概要 |
|---|---|---|
| Authentication | 24 | ログイン・2FA・メール確認・セッション |
| Users | 24 | ユーザー情報・検索・更新 |
| Worlds | 13 | ワールド検索・作成・管理 |
| Avatars | 15 | アバター検索・作成・管理 |
| Friends | 6 | フレンド申請・管理 |
| Groups | 44 | グループ管理・ロール・メンバー |
| Instances | 6 | インスタンス作成・取得 |
| Notifications | 10 | 通知管理 |
| Favorites | 8 | お気に入り管理 |
| Files | 18 | ファイルアップロード・管理 |
| Economy | 23 | 購入・サブスクリプション・取引 |
| Miscellaneous | 8 | 設定・ヘルスチェック |

## 利用可能なSDK

| 言語 | リポジトリ |
|---|---|
| TypeScript / JavaScript | vrchatapi/vrchatapi-javascript |
| Python | vrchatapi/vrchatapi-python |
| Dart | vrchatapi/vrchatapi-dart |
| .NET (C#) | vrchatapi/vrchatapi-csharp |
| Java | vrchatapi/vrchatapi-java |
| Rust | vrchatapi/vrchatapi-rust |
