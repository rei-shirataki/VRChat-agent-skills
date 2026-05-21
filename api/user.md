---
scope: api
title: VRChat REST API — Users
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Users

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

## エンドポイント一覧

### 自分自身の情報

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/auth/user` | getCurrentUser | ログイン & 自分のCurrentUser情報取得 |
| PUT | `/users/{userId}` | updateUser | 自分のプロフィール更新（email, birthday等） |

### ユーザー検索・取得

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/users` | searchUsers | displayName でユーザーを検索 |
| GET | `/users/{userId}` | getUser | IDでユーザー情報を取得 |

#### searchUsers クエリパラメータ

| パラメータ | 型 | 説明 |
|---|---|---|
| `search` | string | displayName で検索（空だと空配列） |
| `developerType` | string | `none`=一般ユーザー, `internal`=モデレーター |
| `n` | integer | 取得件数 |
| `offset` | integer | ページングオフセット |

### ユーザーノート

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/userNotes` | getUserNotes | 最近更新したユーザーノート一覧 |
| POST | `/userNotes` | updateUserNote | ユーザーへのメモを更新 |
| GET | `/userNotes/{userNoteId}` | getUserNote | 特定のユーザーノートを取得 |

### タグ管理

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| POST | `/users/{userId}/addTags` | addTags | ユーザーにタグを追加 |

## 主要レスポンスフィールド（User オブジェクト）

| フィールド | 型 | 説明 |
|---|---|---|
| `id` | string | ユーザーID（例: `usr_xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx`） |
| `displayName` | string | 表示名 |
| `username` | string | ユーザー名（非推奨フィールド） |
| `avatarImageUrl` | string | アバター画像URL |
| `status` | string | オンライン状態（`active`, `join me`, `ask me`, `busy`, `offline`） |
| `statusDescription` | string | ステータスメッセージ |
| `bio` | string | 自己紹介文 |
| `location` | string | 現在地（インスタンスID） |
| `isFriend` | bool | 自分のフレンドかどうか |
| `tags` | string[] | タグ一覧（`system_trust_*` 等） |
| `last_login` | string | 最終ログイン日時（ISO 8601） |

## 注意事項

- `searchUsers` で他ユーザーを検索するには認証が必要
- `getUser` は認証なしでも公開情報を取得可能だが一部フィールドは `0` または空になる
- `updateUser` は自分のアカウントのみ更新可能。パスワード変更には `currentPassword` が必要
