---
scope: meta
title: 仕様変更ログ
source: internal
status: verified
last_verified: 2026-05-21
---

# 仕様変更ログ

VRChat OSC・API・WebSocketの仕様変更を記録するファイルです。
変更を確認したら `last_verified` とともにここに記録してください。

## 2026-05-21

- **初回作成**: ナレッジベース全体を構築
  - OSC: 11ファイル（overview, avatar-parameters, avatar-scaling, chatbox, input-controller, trackers, eye-tracking, debugging, oscquery, resources, diy）
  - REST API: 16ファイル（overview, user, world, avatar, friends, notifications, instances, groups, favorites, invites, player-moderation, economy, files, calendar, inventory, props, jams, prints, miscellaneous）
  - WebSocket: 1ファイル（pipeline）
  - メタ: 2ファイル（index, changelog）
- `osc/chatbox.md`: 対象URL `docs.vrchat.com/docs/osc-chatbox` が404のため、`osc-as-input-controller` ページの情報を元に構成
- REST API全ファイル: `vrchat.community` および `github.com/vrchatapi/specification` v1.20.7 を参照

## 記録フォーマット

```
## YYYY-MM-DD

- **変更内容**: 何が変わったか
- **影響ファイル**: 変更が必要なファイルとその対応
- **ソース**: 変更を確認した出典URL
```
