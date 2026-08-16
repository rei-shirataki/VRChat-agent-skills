---
scope: api
title: VRChat REST API — Economy
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-08-16
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
| GET | `/subscriptions` | getSubscriptions | 存在する全サブスクリプションプラン一覧（`vrchatplus-monthly` 等） |
| GET | `/user/subscription/recent` | getRecentSubscription | 直近のサブスクリプションを取得 |
| GET | `/users/{userId}/subscription/eligible` | getUserSubscriptionEligible | サブスクリプションの利用資格を確認 |
| GET | `/users/{userId}/credits/eligible` | getUserCreditsEligible | クレジット残高に基づくサブスクリプション利用資格を確認 |
| GET | `/economy/licenses/active` | getActiveLicenses | 有効なライセンス一覧 |
| GET | `/licenseGroups/{licenseGroupId}` | getLicenseGroup | ライセンスグループを取得 |
| GET | `/economy/seller/eligibility` | getSellerEligibility | 販売者になれるか確認 |

### ストア

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/economy/stores` | listStores | ストア一覧 |
| GET | `/economy/store` | getStore | ストア情報を取得 |
| GET | `/economy/store/shelves` | getStoreShelves | ストアの棚一覧 |
| GET | `/tokenBundles` | getTokenBundles | トークンバンドル一覧 |

### 商品・リスティング

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| POST | `/products` | createProduct | 商品を作成 |
| GET | `/products/{productId}` | getProductListingAlternate | 商品リストを取得（⚠️非推奨。`getProductListing` を使用） |
| PUT | `/products/{productId}` | updateProduct | 商品を更新 |
| DELETE | `/products/{productId}` | deleteProduct | 商品を削除 |
| POST | `/listing` | createProductListingDirect | 商品リストを作成 |
| GET | `/listing/{productId}` | getProductListing | 商品リストを取得 |
| PUT | `/listing/{productId}` | updateProductListingDirect | 商品リストを更新（`active` で公開/非公開を切替） |
| DELETE | `/listing/{productId}` | deleteProductListingDirect | 商品リストを削除 |
| GET | `/user/{userId}/listings` | getProductListings | 指定ユーザーの商品リスト一覧 |
| GET | `/user/{userId}/products` | listUserProducts | 指定ユーザーの商品一覧 |

### 購入

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| POST | `/economy/purchase/listing` | purchaseProductListing | 商品リストを購入 |
| GET | `/economy/purchases` | getProductPurchases | 購入履歴一覧 |
| GET | `/economy/purchases/{productPurchaseId}` | getProductPurchase | 特定の購入履歴 |
| GET | `/economy/purchases/{productPurchaseId}/stacks` | getProductPurchaseStacks | 購入スタック情報 |
| GET | `/user/bulk/gift/purchases` | getBulkGiftPurchases | 一括ギフト購入履歴 |
| GET | `/user/{userId}/economy/transactions` | getProductPurchaseHistory | 商品購入履歴 |

### 残高・収益

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/economy/metrics/earnings` | getEarningsMetrics | 収益の合計と内訳 |
| GET | `/user/{userId}/balance` | getBalance | ユーザーの残高を取得 |
| GET | `/user/{userId}/balance/earnings` | getBalanceEarnings | ユーザーの収益残高を取得 |
| GET | `/user/{userId}/economy/account` | getEconomyAccount | エコノミーアカウント情報を取得 |
| GET | `/user/{userId}/economy/balances` | getEconomyBalances | 統合残高情報を取得 |
| GET | `/user/{userId}/economy/payouts/list` | getEconomyPayouts | 支払い履歴を取得 |
| GET | `/user/{userId}/economy/payouts/status` | getEconomyPayoutStatus | 支払いステータス・資格情報を取得 |

### Tilia連携（決済・KYC）

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/tilia/status` | getTiliaStatus | Tilia連携ステータスを取得 |
| GET | `/user/{userId}/tilia/kyc` | getUserTiliaKyc | Tiliaアカウントの本人確認（KYC）ステータス |
| GET | `/user/{userId}/tilia/tos` | getTiliaTos | Tilia利用規約の同意状況を取得 |
| PUT | `/user/{userId}/tilia/tos` | updateTiliaTos | Tilia利用規約の同意状況を更新 |

### トランザクション（管理者・Steam）

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/Steam/transactions` | getSteamTransactions | Steam トランザクション一覧 |
| GET | `/Steam/transactions/{transactionId}` | getSteamTransaction | 特定の Steam トランザクション（⚠️非推奨） |
| GET | `/Admin/transactions` | getAdminTransactions | 管理者トランザクション一覧（内部用） |
| GET | `/Admin/transactions/{transactionId}` | getAdminTransaction | 特定の管理者トランザクション（⚠️非推奨・内部用） |

## 注意事項

- `getSteamTransaction` / `getAdminTransaction` / `getProductListingAlternate` は OpenAPI 仕様上 `deprecated: true` が付与されている。前者2つは `getSteamTransactions` / `getAdminTransactions` と全く同じ情報を返すため実用性は低く、後者は `getProductListing` を使うこと
- `/Admin/transactions` 系のエンドポイントは `x-internal: true` が付与されており、VRChat内部での利用を想定したもの
- `getEarningsMetrics` は VRChat Creator Economy の収益者向け
- このカテゴリは VRChat Creator Economy（クレジット・商品販売機能）の追加以降に大幅に拡充されており、商品（Product）・商品リスト（Listing）・ストア（Store）・Tilia決済連携など多数のエンドポイントが存在する
