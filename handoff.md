# handoff.md — 交接檔（收工必寫，開工必讀）

## ⏯️ 目前做到哪

2026-09-21 收工。本次只有開工檢查，無實質進度：
- 遠端同步（落後 0）、全域 Supabase 設定無變動（Token 在、唯讀已解除）。
- 輕量同步：AGENTS 更新紀錄＋本交接檔刷新。

## 🚦 目前狀態

- 可運行：兩遊戲＋儀表板單檔直開即玩（上傳／讀取需連網）。
- DB 是空的：第一個玩的學生就是第一列正式資料。
- repo 4 commits 已 push，工作區僅剩本次收工紀錄待 commit（見下一步回填）。

## ➡️ 下一步（1-3 項）

1. 進教室實測：學生先 A 後 B，投影儀表板做「答案 vs 過程」對比討論。
2. 考慮：B 版錄音上傳（需 Storage bucket＋政策）、課堂討論單＋教師講稿。

## ⚠️ 注意事項

- Token／service-role key 只在全域 `opencode.json`，絕不在 repo 內；換電腦需重設。
- 公開 repo 含 anon key（publishable＋RLS 最小權限，風險可控；PAT 等絕不在內）。
- B 版錄音不上傳、只留本機播放（設計取捨）。

## 🕐 最後更新

- 2026-09-21，Muse Spark @ DESKTOP-CCY，Git push：✅ 已推（`7ea15a2`）。
