---
title: OSC Overview
scope: osc
source: https://docs.vrchat.com/docs/osc-overview
source_wiki: https://wiki.vrchat.com/wiki/Open_Sound_Control
status: verified
last_verified: 2026-05-21
---

# VRChat OSC — 概要

## このファイルでわかること
VRChat の OSC 機能の有効化方法、ポート設定、基本的な通信モデル。

## 概要

OSC（Open Sound Control）は音声機器間通信のために設計されたプロトコル。
VRChat では 2022年2月から OSC サポートを導入し、アバター制御・外部アプリ連携に利用できる。

## 有効化方法

Action Menu → OSC → Enabled

デバッグ確認: Action Menu → OSC → OSC Debug

## ポート設定

| 方向 | ポート | 説明 |
|---|---|---|
| 受信（外部→VRChat） | 9000 | 外部アプリから VRChat へ送信 |
| 送信（VRChat→外部） | 9001 | VRChat から外部アプリへ送信 |

## ポートの上書き（コマンドライン引数）

```
--osc=inPort:senderIP:outPort

# 例: デフォルト設定の明示
--osc=9000:127.0.0.1:9001

# 例: LAN 上の別デバイスに送信
--osc=9000:192.168.1.42:9001
```

ログファイルで実際のポート番号を確認可能：
```
2025.01.02 03:04:05 Debug - Advertising Service VRChat-Client-XXXXXX of type OSC on 9000
```

## 推奨ライブラリ

| 言語 | ライブラリ |
|---|---|
| C# | OscCore（all-in-one ブランチ）|
| Python | python-osc |

## 関連ファイル

- [Avatar Parameters](./avatar-parameters.md)
- [Avatar Scaling](./avatar-scaling.md)
- [Chatbox](./chatbox.md)
- [Input Controller](./input-controller.md)
- [Trackers](./trackers.md)
- [Eye Tracking](./eye-tracking.md)
- [Debugging](./debugging.md)
- [OSCQuery](./oscquery.md)
- [Resources](./resources.md)
