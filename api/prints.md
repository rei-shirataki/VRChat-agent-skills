---
scope: api
title: VRChat REST API — Prints
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Prints

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

PrintはVRChatカメラから直接印刷した写真機能です。

## エンドポイント一覧

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| POST | `/prints` | uploadPrint | 写真をアップロードして作成 |
| GET | `/prints/user/{userId}` | getUserPrints | ユーザーのPrint一覧 |
| GET | `/prints/{printId}` | getPrint | 特定のPrintを取得 |
| PUT | `/prints/{printId}` | editPrint | Printを編集 |
| DELETE | `/prints/{printId}` | deletePrint | Printを削除 |

## uploadPrint / editPrint のフィールド

| フィールド | 型 | 必須 | 説明 |
|---|---|---|---|
| `file` | binary (PNG) | 必須 | 画像データ（multipart/form-data） |
| `caption` | string | 任意 | キャプション |
| `capturedAt` | string (ISO 8601) | 任意（upload時） | 撮影日時 |
| `worldId` | string | 任意（upload時） | 撮影したワールドのID |
| `worldName` | string | 任意（upload時） | 撮影したワールドの名前 |

## 注意事項

- `getUserPrints` は**自分のUserIDのみ**指定可能。他ユーザーのPrintは取得できません
