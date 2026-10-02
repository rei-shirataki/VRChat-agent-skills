---
scope: osc
title: OSCQuery
source: https://docs.vrchat.com/docs/oscquery
status: verified
last_verified: 2026-08-16
---

# OSCQuery

## 概要

OSCQueryはOSCアプリケーション同士が互いを自動的に検出・設定できるようにするプロトコルです。
VRChatは **2023.3.1** リリース以降、OSCQuery仕様を実装しています。

## 主な利点

- アプリケーション同士が**IPアドレスやポートを手動設定なしに**互いを発見できます。
- 相手のアプリケーションの能力（利用可能なOSCアドレス等）を自動的に把握できます。
- ユーザーが設定ファイルを手動編集する手間を省きます。

## 開発者向け情報

| リソース | 説明 |
|---|---|
| [OSCQuery仕様リポジトリ](https://github.com/Vidvox/OSCQueryProposal) | OSCQueryプロトコルの詳細仕様 |
| [VRChat OSCQuery接続ガイド](https://github.com/vrchat-community/osc/wiki/OSCQuery) | VRChatとOSCQueryを連携させるための実装ガイド |
| [VRChat向けC#ライブラリ (vrc-oscquery-lib)](https://github.com/vrchat-community/vrc-oscquery-lib) | OSCQuery統合のためのオープンソースライブラリ |

詳細な技術仕様については [OSCQuery仕様リポジトリ](https://github.com/Vidvox/OSCQueryProposal) を参照してください。

## 対応アプリケーション

OSCQuery対応アプリケーションはVRChatと自動的に接続・設定が行われます。
各アプリケーションのドキュメントでOSCQuery対応状況と必要なセットアップ手順を確認してください。

## 注意事項・送信先として認識されるパス

- Windows 版 VRChat は、HTTPライブラリの制限により、OSCアドレス・値の情報を**同一マシン上のアプリにしか提供できない**（Android 版は制限なし）。
- 複数の受信アプリへ自動送信されるには、アプリが OSC/OSCQuery サービスを広告し、OSCQuery のアドレスツリーに以下のパスのいずれかを含める必要がある（出典: vrchat-community/osc wiki「OSCQuery」）:
  - `/avatar` — `/avatar/change` と `/avatar/parameters/*` を受信
  - `/tracking/vrsystem` — `/tracking/vrsystem/head`・`leftwrist`・`rightwrist`・`pose` を受信（ユーザーが追加の法的通知に同意した後）
- 認識されると、VRChat は HUD 通知で送信先アプリ名を表示する。
- ユーザーが起動引数でポートを指定している場合は、従来どおりそのポートへ全 OSC メッセージが送られる。
