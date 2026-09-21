# handoff.md — 交接檔（收工必寫，開工必讀）

## ⏯️ 目前做到哪

2026-09-21 收工。本次把三層同步全部補齊：
1. `git init`＋兩 commits（`c623855` 初始版控、`4a86b31` 同步文件，含一次 amend 錯字修正）。
2. L3 建檔：`my-classroom-tools/專案工作流程.md`（進度＋更動表＋7 坑＋6 決策），已登記進 AGENTS.md。
3. DB 測試列清空：sessions／events 歸零，教室拿到乾淨 DB。
4. GitHub 公開 repo `jychun2005/polynomial-division-games` 已建＋push（追蹤 `origin/master`）。

## 🚦 目前狀態

- 可運行：兩遊戲＋儀表板單檔直開即玩（上傳／讀取需連網）。
- DB 是空的：第一個玩的學生就是第一列正式資料。
- repo 乾淨 push 完成（收工時僅剩 AGENTS.md 遠端行修改待 commit，見下一步）。

## ➡️ 下一步（1-3 項）

1. 進教室實測：學生先 A 後 B，投影儀表板做「答案 vs 過程」對比討論。
2. 考慮：B 版錄音上傳（需 Storage bucket＋政策）、課堂討論單＋教師講稿。
3. 剩餘三條路（錄音上傳／討論單／總體檢）上次問過，使用者選收工，下次可再問。

## ⚠️ 注意事項

- Token／service-role key 只在全域 `opencode.json`，絕不在 repo 內；換電腦需重設。
- 公開 repo 含 anon key（publishable＋RLS 最小權限，風險可控；PAT 等絕不在內）。
- B 版錄音不上傳、只留本機播放（設計取捨）。
- 曾踩坑：詳見 Obsidian 專案工作流程.md（7 坑：單敘述查詢、空 body、cp950、遠端瀏覽器、連點重複、缺括號、數據誤報）。

## 🕐 最後更新

- 2026-09-21，Muse Spark @ DESKTOP-CCY，Git push：✅ 已推（AGENTS.md 遠端行修改待下一輪 commit）。
