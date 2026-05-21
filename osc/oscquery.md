---
scope: osc
title: OSCQuery
source: https://docs.vrchat.com/docs/oscquery
status: verified
last_verified: 2026-05-21
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
| OSCQuery仕様リポジトリ | OSCQueryプロトコルの詳細仕様 |
| VRChat向けC#ライブラリ | OSCQuery統合のためのオープンソースライブラリ |

詳細な技術仕様については [OSCQuery仕様リポジトリ](https://github.com/Vidvox/OSCQueryProposal) を参照してください。

## 対応アプリケーション

OSCQuery対応アプリケーションはVRChatと自動的に接続・設定が行われます。
各アプリケーションのドキュメントでOSCQuery対応状況と必要なセットアップ手順を確認してください。
