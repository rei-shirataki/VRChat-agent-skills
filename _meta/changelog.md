---
scope: meta
title: 仕様変更ログ
source: internal
status: verified
last_verified: 2026-10-02
---

# 仕様変更ログ

VRChat OSC・API・WebSocketの仕様変更を記録するファイルです。
変更を確認したら `last_verified` とともにここに記録してください。

## 2026-10-02

- **変更内容**: 情報の鮮度・誤り確認（再検証）
  - **REST API**: `vrchatapi/specification` v1.21.0（`main`、2026-09-30コミット）の全326操作と `api/*.md` 全表を method+path+operationId で機械照合。フィールド単位の再照合は未実施（2026-08-16以降、スキーマ変更が多数あり）
    - `api/world.md`: `removeWorldTags` のパスが誤り（`/worlds/{id}/removeTags` → 正しくは `/deleteTags`）
    - `api/economy.md`: `getSteamTransaction` に誤って付いていた非推奨注記を削除（仕様上 deprecated は `getAdminTransaction` と `getProductListingAlternate` のみ）
    - `api/overview.md`: カテゴリ別件数を v1.21.0 に更新（合計326）。未収録だった約45件（2FA管理・メール確認・モデレーション報告・グローバルアバターモデレーション・permissions・cosmetics・clientConfig・tutorial・instanceVibes 等）を補足表として追加
    - `_meta/index.md`: groups のエンドポイント数 53→51
  - **OSC**: `docs.vrchat.com` が本環境から到達不可（egress遮断）のため公式ドキュメントとは**再照合できず**、`last_verified` は更新していない。代わりに `vrchat-community/osc` wiki（最終更新2023-08）と照合し、以下を修正
    - `osc/input-controller.md`: `/input/Voice` のプッシュトゥミュート値が逆（正: 1=ミュート、0=解除）。LookLeft/LookRight のスナップターン条件（コンフォートターン有効時）を明記
    - `osc/oscquery.md`: 送信先として認識されるパス（`/avatar`、`/tracking/vrsystem`）とWindows版の同一マシン制限を追記
  - 未確認: Chatbox の144文字・9行・第3引数（公式docs由来で wiki より新しい情報のため維持。wiki記載の「ASCIIのみ」は古い可能性）、`avatar-parameters.md`/`diy.md`/`resources.md` の再照合
- **影響ファイル**: `api/*.md`（`last_verified` はエンドポイントレベル照合分）、`osc/input-controller.md`、`osc/oscquery.md`、`_meta/index.md`、`_meta/changelog.md`
- **ソース**: https://github.com/vrchatapi/specification（v1.21.0）、https://github.com/vrchat-community/osc/wiki

## 2026-08-16

- **変更内容**: `SKILL.md` に frontmatter（`name` / `description`）を追加。従来 frontmatter が存在せず、スキル一覧表示時に H1 見出しがフォールバック表示されており、トリガー精度が低下していた
  - `description` にOSC・REST API・WebSocketの主要キーワードを列挙し、スキル自動呼び出しの判定材料とした
  - `SKILL.md` の構成ファイル表（30行超）を `_meta/index.md` と重複させず、セクション単位の要約表に圧縮（内容の一次情報は `_meta/index.md` に一本化）
- **影響ファイル**: `SKILL.md`
- **ソース**: https://code.claude.com/docs/en/skills.md#frontmatter-reference（Claude Code Skills frontmatter仕様）

- **変更内容**: 全31コンテンツファイル（OSC 11・REST API 19・WebSocket 1）を一斉再検証。`last_verified` が2026-05-21で約3ヶ月停滞していたため、公式ドキュメント（`docs.vrchat.com`）および `vrchatapi/specification` の OpenAPI 定義（raw YAML）と全件照合した。主な修正点は以下の通り（軽微な文言修正は省略）：
  - **REST API（大きな乖離）**
    - `api/economy.md`: 収録エンドポイントが43件中15件のみだった（商品リスティング・購入履歴・残高・Tilia連携・サブスクリプション等を大幅追加、非推奨エンドポイントに `deprecated` 注記）
    - `api/user.md`: 21件のエンドポイント漏れ（プロフィール・バッジ・グループ関連・ミューチュアル・永続化データ）を追加
    - `api/world.md`: 8件のエンドポイント漏れ（tags操作・platform削除・publish系・getWorldInstance）を追加
    - `api/inventory.md`: パス構造が誤り（`/inventory/{inventoryId}/item/{itemId}` → 実際は `/inventory/{inventoryItemId}` のフラット構造）、複数エンドポイントのHTTPメソッドも誤っていたため全面修正
    - `api/groups.md`（53エンドポイント）: `addGroupMemberRole` のメソッド誤り(POST→PUT)、`declineGroupInvite`/`getGroupGalleryImages`/`getGroupTransferability` 等のパス誤りを修正
    - `api/calendar.md`: グループカレンダーのパスが誤り（`/groups/{groupId}/calendar/...` → 実際は `/calendar/{groupId}/...`）、`.ics` サフィックスの誤りも修正
    - `api/favorites.md`: `clearFavoriteGroup` のメソッド・パスが誤り（PUT+`/clear` → 実際は DELETE のみ）
    - `api/invites.md`: 写真付き招待3エンドポイントのパス構造誤りを修正
    - `api/player-moderation.md`: 存在しない `unblock` を削除し `muteChat`/`unmuteChat` を追加。`hideAvatar`/`showAvatar` が2022年10月以降ローカルストレージ管理に移行しAPIには反映されない点を注記
    - `api/files.md`: analysis系エンドポイントのパス誤り、`getFiles`/`uploadGalleryImage`/`uploadIcon`/`getAdminAssetBundle` の漏れを修正
    - `api/props.md` / `api/prints.md` / `api/jams.md` / `api/miscellaneous.md`: パスパラメータ名・HTTPメソッド・フィールド名の誤りを修正（詳細は各ファイル参照）
    - `api/overview.md`: エンドポイントカテゴリ表のカウントが全面的に陳腐化していたため実測値に更新し、欠落していた7カテゴリ（Calendar/Inventory/Invite/Jams/PlayerModeration/Prints/Props）を追加
  - **OSC（軽微〜中程度の修正）**
    - `osc/resources.md`: ツール・ライブラリ一覧に多数の漏れ・誤分類・言語表記ミスがあり大幅修正（ハートレート5件・IRL Control 4件・Misc 2件を新規追加等）
    - `osc/avatar-scaling.md`: `eyeheightmin`/`eyeheightmax` の方向が「読み書き」と誤記されていたが実際は読み取り専用
    - `osc/oscquery.md`: 公式のOSCQuery接続ガイドへの言及が丸ごと欠落していたため追加
    - `osc/eye-tracking.md` / `osc/trackers.md` / `osc/diy.md` / `osc/overview.md`: 説明の精緻化・欠落情報の追加
    - `osc/chatbox.md` / `osc/debugging.md` / `osc/input-controller.md` / `osc/avatar-parameters.md`: 内容は最新のソースと一致（`last_verified` のみ更新）
  - **WebSocket**
    - `websocket/pipeline.md`: 未文書化だった7件のUserイベント（`user-badge-assigned` 等）、`location` フィールドの `traveling` 状態、エラーメッセージ例を追加
  - 全ファイルで `status:` / `source:` フィールドは変更せず、内容確認結果のみ反映（`source:` が汎用URLの場合、実際の照合には `vrchatapi/specification` の該当YAMLファイルを使用）
  - `_meta/index.md`: 上記再検証結果を反映し、`api/groups.md` のエンドポイント数表記を44→53に修正、`api/economy.md` の概要説明にTilia決済連携・商品リスト管理を追記、`last_verified` を更新
- **影響ファイル**: `osc/*.md`（11件）、`api/*.md`（19件）、`websocket/pipeline.md`、`_meta/index.md`
- **ソース**: https://docs.vrchat.com/ 各ページ、https://github.com/vrchatapi/specification（`main`ブランチ、`openapi/components/paths/*.yaml`）

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
