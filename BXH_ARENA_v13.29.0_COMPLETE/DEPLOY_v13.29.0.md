# BXH ARENA v13.29.0 部署順序

此版本新增玩家稱號與每日簽到的可信後端。不要只上傳 `index.html`。

> Cloud Functions 正式部署需要 Firebase 專案使用 Blaze 隨用隨付方案。請先設定預算警示；本版沒有設定常駐 `minInstances`，避免產生固定閒置執行費用。

1. 安裝 Firebase CLI 並執行 `firebase login`。
2. 執行 `firebase use --add`，明確選擇 BXH ARENA 正式專案。
3. 在本目錄執行 `npm --prefix functions install`。
4. 先部署 `firebase deploy --only firestore:rules`。
5. 再部署 `firebase deploy --only functions`。
6. 最後部署或上傳 `index.html`。
7. 在最高管理員「帳號管理 → 稱號與每日簽到」按下「建立／同步第一批稱號」。
8. 先只開啟 `titlesEnabled` 與 `dailyCheckInEnabled` 進行封測；確認穩定後再開啟自動發放。

建議起始設定：

```json
{
  "titlesEnabled": true,
  "automaticTitleAwardsEnabled": false,
  "dailyCheckInEnabled": true,
  "checkInTitleAwardsEnabled": false,
  "timezone": "Asia/Taipei"
}
```

回復時可先將四個功能開關全部設為 `false`，再把網站退回 v13.28.9；不需要刪除任何新集合。
