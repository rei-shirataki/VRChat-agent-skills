---
scope: api
title: VRChat REST API — Calendar
source: https://vrchat.community/docs/api/
status: community
last_verified: 2026-05-21
---

# VRChat REST API — Calendar

ベースURL: `https://api.vrchat.cloud/api/1`  
認証: `authCookie` (Cookie: `auth=...`)

VRChat コミュニティのカレンダーイベント（グループイベント等）を管理するAPIです。

## エンドポイント一覧

### イベント閲覧

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/calendar` | getCalendarEvents | 自分のカレンダーイベント一覧（月単位） |
| GET | `/calendar/featured` | getFeaturedCalendarEvents | フィーチャードイベント一覧（月単位） |
| GET | `/calendar/following` | getFollowedCalendarEvents | フォロー中のイベント一覧（月単位） |
| GET | `/calendar/discover` | discoverCalendarEvents | イベントを探索 |
| GET | `/calendar/search` | searchCalendarEvents | キーワードでイベントを検索 |

### グループイベント管理

| メソッド | パス | operationId | 説明 |
|---|---|---|---|
| GET | `/groups/{groupId}/calendar` | getGroupCalendarEvents | グループのイベント一覧 |
| POST | `/groups/{groupId}/calendar` | createGroupCalendarEvent | グループにイベントを作成 |
| GET | `/groups/{groupId}/calendar/{calendarEventId}` | getGroupCalendarEvent | 特定のグループイベントを取得 |
| PUT | `/groups/{groupId}/calendar/{calendarEventId}` | updateGroupCalendarEvent | グループイベントを更新 |
| DELETE | `/groups/{groupId}/calendar/{calendarEventId}` | deleteGroupCalendarEvent | グループイベントを削除 |
| GET | `/groups/{groupId}/calendar/{calendarEventId}/ics` | getGroupCalendarEventICS | ICS形式でダウンロード |
| GET | `/groups/{groupId}/calendar/next` | getGroupNextCalendarEvent | グループの次のイベントを取得 |
| POST | `/groups/{groupId}/calendar/{calendarEventId}/follow` | followGroupCalendarEvent | イベントをフォロー/アンフォロー |

## クエリパラメータ（月指定）

| パラメータ | 型 | 説明 |
|---|---|---|
| `date` | string | 対象月を指定（例: `2026-05`）。省略時は当月 |

## 注意事項

- ICS形式（`getGroupCalendarEventICS`）はカレンダーアプリ（Google Calendar, Outlook等）にインポートできます
- グループイベントの作成・編集にはグループ内のイベント管理権限が必要です
