# VRChat Knowledge Base — SKILL

## このスキルを使うタイミング

以下のキーワードや状況が含まれる場合、このスキルを参照すること：

- VRChat OSC（送受信、Avatar Parameters、Chatbox、Input、Eye Tracking、トラッカー）
- VRChat API / REST API（ユーザー情報取得・更新、ワールド、認証、フレンド、グループ、招待、通知、インスタンス、お気に入り、プレイヤーモデレーション、Economy・クレジット、ファイルアップロード、カレンダー、インベントリ、Props、Jams、Prints、システム設定）
- VRChat WebSocket / Pipeline イベント
- OyasumiVR、Pulsoid、VRCX などの VRChat 連携ツール
- VRChat のボット・自動化スクリプト開発

## 構成ファイル

| ファイル | 内容 | 状態 |
|---|---|---|
| `_meta/index.md` | 全体サマリー・ソース一覧 | ✅ verified |
| `osc/overview.md` | OSC の基本・ポート設定 | ✅ verified |
| `osc/avatar-parameters.md` | Avatar Parameters の仕様・Built-in パラメータ一覧 | ✅ verified |
| `osc/avatar-scaling.md` | アバタースケール（アイハイト）の読み書き | ✅ verified |
| `osc/chatbox.md` | Chatbox API（テキスト送信・タイピング表示） | ✅ verified |
| `osc/input-controller.md` | Input API（Axes・Buttons 全一覧） | ✅ verified |
| `osc/trackers.md` | 外部トラッカー統合（位置・回転） | ✅ verified |
| `osc/eye-tracking.md` | アイトラッキングデータの送信 | ✅ verified |
| `osc/debugging.md` | OSC デバッグ画面の使い方 | ✅ verified |
| `osc/oscquery.md` | OSCQuery 自動検出プロトコル | ✅ verified |
| `osc/resources.md` | ツール・ライブラリ・プロジェクト一覧 | ✅ verified |
| `osc/diy.md` | OSCカスタム実装ガイド（構造・ライブラリ・Unityパターン） | ✅ verified |
| `api/overview.md` | REST API の概要・認証・注意事項 | ✅ community |
| `api/user.md` | ユーザー関連エンドポイント | ✅ community |
| `api/world.md` | ワールド関連エンドポイント | ✅ community |
| `api/avatar.md` | アバター関連エンドポイント | ✅ community |
| `api/friends.md` | フレンド申請・管理 | ✅ community |
| `api/notifications.md` | 通知管理・フレンド申請承認フロー | ✅ community |
| `api/instances.md` | インスタンス作成・取得・閉鎖 | ✅ community |
| `api/groups.md` | グループ管理（メンバー・ロール・招待等） | ✅ community |
| `api/favorites.md` | お気に入り（ワールド・アバター・フレンド）管理 | ✅ community |
| `api/invites.md` | 招待送受信・招待メッセージ管理 | ✅ community |
| `api/player-moderation.md` | ユーザーのミュート・ブロック管理 | ✅ community |
| `api/economy.md` | VRC+・クレジット・ストア・購入履歴 | ✅ community |
| `api/files.md` | アセットファイルアップロード・管理 | ✅ community |
| `api/calendar.md` | グループカレンダーイベント管理 | ✅ community |
| `api/inventory.md` | コレクタブルアイテム管理 | ✅ community |
| `api/props.md` | インスタンス内スポーンアイテム管理 | ✅ community |
| `api/jams.md` | 創作コンテスト（Jam）への投稿 | ✅ community |
| `api/prints.md` | VRChatカメラ写真（Print）管理 | ✅ community |
| `api/miscellaneous.md` | システム設定・ヘルスチェック・パーミッション | ✅ community |
| `websocket/pipeline.md` | WebSocket イベントストリーム | ✅ community |
| `_meta/changelog.md` | 仕様変更ログ | ✅ verified |

## 重要な前提知識

- **OSC** は VRChat 公式サポート（`docs.vrchat.com` / `wiki.vrchat.com`）
- **REST API** は非公式・コミュニティドキュメント（`vrchat.community`）
- REST API は予告なく変更される可能性があり、乱用するとアカウント停止のリスクがある
- ドキュメントの `status` フィールドで信頼度を確認すること

## AI エージェントへの指示

1. `_meta/index.md` が存在すれば最初に読む。なければ `osc/overview.md` などセクションの overview から読む
2. タスクに関連するセクションファイルを参照する
3. `status: unverified` または `status: community` の情報は実装前に確認を促す
4. コード例を提示するとき、そのコード例が属するスコープ（`scope: osc` / `scope: api` / `scope: websocket`）が今解こうとしている問題のスコープと一致していることを確認する。OSCのコード例をAPI実装に流用しないこと。`status: verified` のファイルのコード例を `status: community` より優先するのはスコープが一致する場合に限る
