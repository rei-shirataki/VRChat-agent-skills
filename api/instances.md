---
scope: api
title: VRChat REST API — Instances
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Instances

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

## エンドポイント一覧

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| POST | `/instances` | createInstance | インスタンスを作成 |
| GET | `/instances/recent` | getRecentLocations | 最近訪問したインスタンス一覧 |
| GET | `/instances/s/{shortName}` | getInstanceByShortName | ショートネームでインスタンスを取得 |
| GET | `/instances/{worldId}:{instanceId}` | getInstance | IDでインスタンスを取得 |
| DELETE | `/instances/{worldId}:{instanceId}` | closeInstance | インスタンスを閉鎖 |
| GET | `/instances/{worldId}:{instanceId}/shortName` | getShortName | インスタンスのショートネームを取得 |

## インスタンスIDの形式

```
{worldId}:{instanceId}

例: wrld_12345678-abcd-...:12345~private(usr_...)~nonce(...)
```

## closeInstance クエリパラメータ

| パラメータ | 型 | 説明 |
|---|---|---|
| `hardClose` | boolean | ハードクローズするか（デフォルト: `false`） |
| `closedAt` | string (ISO 8601) | この時刻以降は入室不可にする。省略時は即時閉鎖 |

## Instance オブジェクトの主要フィールド

| フィールド | 型 | 説明 |
|---|---|---|
| `id` | string | インスタンスID |
| `worldId` | string | ワールドID |
| `instanceId` | string | インスタンス番号 + アクセス修飾子 |
| `shortName` | string | ショートリンク用の短縮名 |
| `ownerId` | string | オーナーのユーザーID |
| `type` | string | インスタンスタイプ（下記参照） |
| `userCount` | integer | 現在の人数 |
| `capacity` | integer | 最大収容人数 |
| `full` | boolean | 満員かどうか |
| `platforms` | object | プラットフォーム別の人数 |

## インスタンスタイプ（type）

| 値 | 説明 |
|---|---|
| `public` | 誰でも参加可能 |
| `hidden` | フレンド+（フレンドのフレンドも参加可） |
| `friends` | フレンドのみ |
| `private` | 招待のみ |
| `group` | グループメンバーのみ |
| `groupPublic` | グループ公開インスタンス |

## 注意事項

- `getInstance` に無効な `instanceId` を渡すと `null` が返ります（エラーではない）
- `closeInstance` はオーナー自身、またはグループインスタンスの場合は `group-instance-manage` 権限が必要
- `getRecentLocations` は自分が最近訪れたインスタンスのみ返します
