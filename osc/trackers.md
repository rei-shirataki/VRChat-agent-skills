---
scope: osc
title: OSC Trackers
source: https://docs.vrchat.com/docs/osc-trackers
status: verified
last_verified: 2026-05-21
---

# OSC Trackers

## 概要

OSCを使用して外部トラッカーの位置・回転データをVRChatに送信できます。
最大8つのトラッカー（ヒップ・チェスト・両足・両膝・両肘）と頭部のトラッキングをサポートしています。

## OSCアドレス

### トラッカー（番号指定）

| アドレス | 型 | 説明 |
|---|---|---|
| `/tracking/trackers/{1-8}/position` | Float × 3（X, Y, Z） | トラッカーの位置 |
| `/tracking/trackers/{1-8}/rotation` | Float × 3（X, Y, Z） | トラッカーの回転（オイラー角） |

### 頭部

| アドレス | 型 | 説明 |
|---|---|---|
| `/tracking/trackers/head/position` | Float × 3（X, Y, Z） | 頭部の位置 |
| `/tracking/trackers/head/rotation` | Float × 3（X, Y, Z） | 頭部の回転（オイラー角） |

## 座標系

| 項目 | 仕様 |
|---|---|
| 上方向 | +Y軸 |
| スケール | 1.0 = 1メートル（現実空間と対応） |
| 利き手 | 左手座標系 |
| 回転表現 | オイラー角（度数法） |
| 回転適用順 | Z → X → Y |

## 頭部データの動作

- **位置**: 毎フレーム完全に同期されます。
- **回転**: トラッキング空間の自動調整に使用され、徐々に調整されます。

## 推奨設定

- 全8トラッカーを常に送信することが最適とは限りません。
- まずは**足とヒップのみ**送信し、トラッキング精度が高い場合に段階的にトラッカー数を増やすことを推奨します。
