# handoff.md — 交接檔（收工必寫，開工必讀）

## ⏯️ 目前做到哪

2026-09-21 收工。本次完成上次交接的三項下一步：
1. B 版加姓名／座號欄：第 0 站輸入，上傳 `player_name`＋證書具名（空白回退「B版玩家」）。
2. A 版英雄榜改讀 DB：結算抓 `game_version=A` 前 5 名即時排行；離線回退本機＋假人。
3. 新增 `classroom-dashboard.html`：課堂戰情儀表板，讀 sessions＋events 呈現人次／答對率／各站嘗試＋自動對比結論，教師投影用。
4. 修 bug：saveBoard 缺結尾括號（檢查攔下，已補，三檔 JS 複驗通過）。
5. 儀表板數據層用匿名查詢實測通過；糾正卡關數據：找錯 15 次、補零 13 次（上次誤報為探索／找錯）。

## 🚦 目前狀態

- 可運行：兩遊戲＋儀表板皆單檔，瀏覽器直開即玩（上傳／讀取需連網，離線有降級顯示）。
- DB 現況：sessions 2 列（A×1、B×1）、events 4 列，均為測試資料；進教室實測前可留可清。
- 儀表板只能用老師電腦開（需連網讀 anon REST）；遠端截圖驗證不可行，已改數據層驗證。

## ➡️ 下一步（1-3 項）

1. 進教室實測：學生先 A 後 B，投影儀表板做「答案 vs 過程」對比討論。
2. 視課堂情況決定是否清掉測試列、是否 `git init` 開版控。
3. 考慮：B 版錄音上傳（目前只留本機）要不要做（需 Storage bucket＋政策）。

## ⚠️ 注意事項

- Token／service-role key 只在全域 `opencode.json`，絕不在 repo 內；換電腦需重設。
- B 版錄音不上傳、只留本機播放（設計取捨）。
- 專案目錄非 git repo，無 L2 同步。
- 曾踩坑：`/database/query` 多敘述一次送一件；`Prefer: return=minimal` 回空 body 別當失敗；PowerShell 主控台印 emoji 會炸（cp950），改寫檔再讀；Playwright 遠端瀏覽器連不到本機 localhost。

## 🕐 最後更新

- 2026-09-21，Muse Spark @ DESKTOP-CCY，Git push：待推（無 repo，未推）。
