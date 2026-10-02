---
scope: api
title: VRChat REST API — Users
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-10-02
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
| POST | `/users/{userId}/removeTags` | removeTags | ユーザーからタグを削除 |

### プロフィール・バッジ

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/profile/{userId}` | getPublicProfile | 公開プロフィール情報を取得 |
| GET | `/profile/{userId}/private` | getPrivateProfile | 認証済みユーザーに見えるプロフィール情報を取得 |
| PUT | `/users/{userId}/badges/{badgeId}` | updateBadge | ユーザーバッジを更新 |
| GET | `/users/{userId}/tutorial` | getUserTutorialStatus | チュートリアルの完了状況を取得 |
| GET | `/users/{userId}/feedback` | getUserFeedback | **非推奨**。ユーザーが送信したフィードバックを取得 |
| GET | `/users/{username}/name` | getUserByName | **非推奨**（管理者権限が必要）。ユーザー名でユーザー情報を取得 |
| GET | `/users/active` | searchActiveUsers | **非推奨**（管理者権限が必要）。アクティブユーザーをテキスト検索 |

### グループ関連

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/users/{userId}/groups` | getUserGroups | ユーザーの公開グループ一覧を取得 |
| GET | `/users/{userId}/groups/invited` | getInvitedGroups | 招待されているグループ一覧を取得 |
| GET | `/users/{userId}/groups/permissions` | getUserAllGroupPermissions | 参加中の全グループの権限一覧を取得 |
| GET | `/users/{userId}/groups/represented` | getUserRepresentedGroup | 現在代表しているグループを取得 |
| GET | `/users/{userId}/groups/requested` | getUserGroupRequests | 参加リクエスト中のグループ一覧を取得 |
| GET | `/users/{userId}/groups/userblocked` | getBlockedGroups | ブロックしているグループ一覧を取得 |
| GET | `/users/{userId}/instances/groups` | getUserGroupInstances | ユーザーのグループインスタンス一覧を取得 |
| GET | `/users/{userId}/instances/groups/{groupId}` | getUserGroupInstancesForGroup | 特定グループのインスタンス一覧を取得 |

### ミューチュアル

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/users/{userId}/mutuals` | getMutuals | 自分と指定ユーザーのミューチュアル数を取得 |
| GET | `/users/{userId}/mutuals/friends` | getMutualFriends | 自分と指定ユーザーの共通フレンド一覧を取得 |
| GET | `/users/{userId}/mutuals/groups` | getMutualGroups | 自分と指定ユーザーの共通グループ一覧を取得 |

### 永続化データ（World Persistence）

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| DELETE | `/users/{userId}/persist` | deleteAllUserPersistenceData | ユーザーの全ワールド分の永続化データを削除 |
| DELETE | `/users/{userId}/{worldId}/persist` | deleteUserPersistence | 指定ワールドの永続化データを削除 |
| GET | `/users/{userId}/{worldId}/persist/exists` | checkUserPersistenceExists | 指定ワールドの永続化データの有無を確認 |

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
- `getUserFeedback`・`getUserByName`・`searchActiveUsers` は非推奨。`searchActiveUsers` と `getUserByName` は管理者権限が必要
