---
scope: api
title: VRChat REST API — Player Moderation
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Player Moderation

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

自分が行ったプレイヤーへのモデレーション（ミュート・ブロック等）を管理するAPIです。

## エンドポイント一覧

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/auth/user/playermoderations` | getPlayerModerations | 自分が行ったモデレーション一覧 |
| POST | `/auth/user/playermoderations` | moderateUser | ユーザーをモデレート |
| DELETE | `/auth/user/playermoderations` | clearAllPlayerModerations | 全モデレーションを削除 |
| PUT | `/auth/user/unplayermoderate` | unmoderateUser | 特定のモデレーションを解除 |

## getPlayerModerations クエリパラメータ

| パラメータ | 型 | 説明 |
|---|---|---|
| `type` | string | モデレーション種別（`PlayerModerationType`） |
| `targetUserId` | string | 対象ユーザーのID |
| `sourceUserId` | string | 自分のユーザーID（他人のモデレーションは取得不可） |

## PlayerModerationType（モデレーション種別）

| 値 | 説明 |
|---|---|
| `mute` | 音声ミュート |
| `unmute` | ミュート解除 |
| `block` | ブロック |
| `unblock` | ブロック解除 |
| `hideAvatar` | アバターを非表示 |
| `showAvatar` | アバターを表示 |
| `interactOff` | インタラクション無効 |
| `interactOn` | インタラクション有効 |

## 注意事項

- ⚠️ `clearAllPlayerModerations` は**これまで行った全てのモデレーションを削除します**。元に戻せません
- 他人のモデレーション一覧は取得できません（自分のものだけ）
- `unmoderateUser` は `moderateUser` で追加したモデレーションを元の状態に戻します（例：アバター表示をデフォルトに戻す）
