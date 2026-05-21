# VRChat Agent Skills

VRChat の外部連携仕様（OSC・REST API・WebSocket）をまとめた、AIエージェント向けナレッジベースです。

## 概要

Claude Code のスキル機能と連携し、VRChat 連携ツール・ボット・自動化スクリプトの開発を支援します。
`SKILL.md` がエントリーポイントとなり、AIエージェントが適切なファイルを参照して回答します。

## ディレクトリ構成

```
VRChat-agent-skills/
├── SKILL.md                 # スキル定義・トリガー条件・AIエージェント指示
├── _meta/
│   ├── index.md             # 全ファイルの索引
│   └── changelog.md         # 仕様変更ログ
├── osc/                     # OSC（公式サポート）
│   ├── overview.md
│   ├── avatar-parameters.md
│   ├── avatar-scaling.md
│   ├── chatbox.md
│   ├── input-controller.md
│   ├── trackers.md
│   ├── eye-tracking.md
│   ├── debugging.md
│   ├── oscquery.md
│   ├── resources.md
│   └── diy.md
├── api/                     # REST API（非公式・コミュニティ）
│   ├── overview.md
│   ├── user.md
│   ├── world.md
│   ├── avatar.md
│   ├── friends.md
│   ├── notifications.md
│   ├── instances.md
│   ├── groups.md
│   ├── favorites.md
│   ├── invites.md
│   ├── player-moderation.md
│   ├── economy.md
│   ├── files.md
│   ├── calendar.md
│   ├── inventory.md
│   ├── props.md
│   ├── jams.md
│   ├── prints.md
│   └── miscellaneous.md
└── websocket/               # WebSocket（非公式・コミュニティ）
    └── pipeline.md
```

## 各セクションについて

### OSC（Open Sound Control）

VRChat 公式サポートの外部連携プロトコル。Avatar Parameters の制御・Chatbox へのテキスト送信・コントローラー入力のエミュレート・トラッカー統合などに使用します。

- 受信ポート: `9000`（VRChat が受け取る）
- 送信ポート: `9001`（VRChat から送り出す）
- ソース: `docs.vrchat.com` / `wiki.vrchat.com`

### REST API

コミュニティが文書化した非公式 API。ユーザー・ワールド・グループ・フレンド・Economy など幅広い操作が可能です。

- ベース URL: `https://api.vrchat.cloud/api/1`
- 認証: Cookie ベース（`auth=authcookie_...`）
- ソース: `vrchat.community` / `github.com/vrchatapi/specification`

> **注意**: 非公式 API のため予告なく変更される可能性があります。乱用するとアカウント停止のリスクがあります。

### WebSocket

`wss://pipeline.vrchat.cloud` への接続でフレンドのオンライン状態変化・通知・グループイベントをリアルタイム受信できます。

## status フィールド

各ファイルの frontmatter に記載されている信頼度を示します。

| 値 | 意味 |
|---|---|
| `verified` | 公式ドキュメントと照合済み |
| `community` | コミュニティドキュメント。非公式・変更リスクあり |
| `unverified` | 未検証。実装前に要確認 |

## 更新方法

仕様変更を確認した場合は以下の手順で更新してください。

1. 対象ファイルの内容を修正する
2. frontmatter の `last_verified` を更新する
3. `_meta/changelog.md` に変更内容・影響ファイル・ソース URL を記録する

```markdown
## YYYY-MM-DD

- **変更内容**: 何が変わったか
- **影響ファイル**: 変更したファイルとその対応
- **ソース**: 変更を確認した出典 URL
```

## 関連リンク

| リソース | URL |
|---|---|
| VRChat OSC 公式ドキュメント | https://docs.vrchat.com/docs/osc-overview |
| VRChat Wiki | https://wiki.vrchat.com/wiki/Open_Sound_Control |
| vrchat.community API ドキュメント | https://vrchat.community/ |
| OpenAPI Specification | https://github.com/vrchatapi/specification |
