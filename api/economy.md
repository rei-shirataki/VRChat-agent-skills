---
scope: api
title: VRChat REST API — Economy
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Economy

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

VRC+・クレジット・サブスクリプション・ストアに関するAPIです。

## エンドポイント一覧

### サブスクリプション・ライセンス

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/auth/user/subscription` | getCurrentSubscriptions | 現在有効なサブスクリプション一覧 |
| GET | `/economy/licenses/active` | getActiveLicenses | 有効なライセンス一覧 |
| GET | `/economy/seller/eligibility` | getSellerEligibility | 販売者になれるか確認 |

### ストア・購入

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/economy/stores` | listStores | ストア一覧 |
| GET | `/economy/store` | getStore | ストア情報を取得 |
| GET | `/economy/store/shelves` | getStoreShelves | ストアの棚一覧 |
| POST | `/economy/purchase/listing` | purchaseProductListing | 商品リストを購入 |
| GET | `/economy/purchases` | getProductPurchases | 購入履歴一覧 |
| GET | `/economy/purchases/{purchaseId}` | getProductPurchase | 特定の購入履歴 |
| GET | `/economy/purchases/{purchaseId}/stacks` | getProductPurchaseStacks | 購入スタック情報 |

### 収益・メトリクス

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/economy/metrics/earnings` | getEarningsMetrics | 収益の合計と内訳 |

### トランザクション（管理者・Steam）

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/Steam/transactions` | getSteamTransactions | Steam トランザクション一覧 |
| GET | `/Steam/transactions/{transactionId}` | getSteamTransaction | 特定の Steam トランザクション |
| GET | `/Admin/transactions` | getAdminTransactions | 管理者トランザクション一覧 |
| GET | `/Admin/transactions/{transactionId}` | getAdminTransaction | 特定の管理者トランザクション |

## 注意事項

- `getSteamTransaction` / `getAdminTransaction` は `getSteamTransactions` / `getAdminTransactions` と全く同じ情報を返すため実用性は低い
- `getEarningsMetrics` は VRChat Creator Economy の収益者向け
- このカテゴリは VRChat Creator Economy（クレジット販売機能）の追加以降に大幅に拡充されている
