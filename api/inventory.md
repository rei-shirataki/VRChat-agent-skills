---
scope: api
title: VRChat REST API — Inventory
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Inventory

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

ドロップバンドルなどのコレクタブルアイテムを管理するAPIです。

## エンドポイント一覧

### インベントリ全体

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/inventory` | getInventory | インベントリオブジェクトを取得 |
| GET | `/inventory/collections` | getInventoryCollections | コレクション名一覧 |
| GET | `/inventory/drops` | getInventoryDrops | ドロップ一覧 |

### アイテム操作

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/inventory/template/{templateId}` | getInventoryTemplate | インベントリテンプレートを取得 |
| GET | `/inventory/{inventoryId}/item/{itemId}` | getOwnInventoryItem | 自分のインベントリアイテムを取得 |
| PUT | `/inventory/{inventoryId}/item/{itemId}` | updateOwnInventoryItem | アイテムを更新 |
| DELETE | `/inventory/{inventoryId}/item/{itemId}` | deleteOwnInventoryItem | アイテムを削除 |
| POST | `/inventory/{inventoryId}/item/{itemId}/consume` | consumeOwnInventoryItem | アイテムを消費 |
| POST | `/inventory/{inventoryId}/item/{itemId}/equip` | equipOwnInventoryItem | アイテムを装備 |
| DELETE | `/inventory/{inventoryId}/slot/{slotId}` | unequipOwnInventorySlot | スロットのアイテムを装備解除 |
| GET | `/users/{userId}/inventory/{inventoryId}/item/{itemId}` | getUserInventoryItem | 他ユーザーのアイテムを取得 |

### 共有・スポーン

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| POST | `/inventory/cloning/direct` | shareInventoryItemDirect | 他ユーザーに直接共有 |
| POST | `/inventory/cloning/pedestal` | shareInventoryItemPedestal | ペデスタル経由で共有 |
| POST | `/inventory/spawn` | spawnInventoryItem | インスタンスにアイテムをスポーン |

### リワード

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| POST | `/reward/redeem` | redeemReward | リワードを引き換え |

## 注意事項

- インベントリはVRChatのコレクタブルアイテム（ドロップバンドル等）の管理機能です
- 他ユーザーのアイテムは `getUserInventoryItem` でのみ参照可能（変更不可）
