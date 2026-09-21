# AGENTS.md — 專案共用紀錄

> 規則：每一個完成的對話，都要把重要事項（決定、設定、狀態、待辦）記錄在這份文件，
> 讓本專案裡的每一個對話都能共用。機密（Token、金鑰）絕對不寫進本檔案或本 repo。

更新紀錄：
- 2026-09-20：建立檔案；記入 Supabase 連線、資料庫現況、遊戲化評量理念、八年級多項式除法規劃。
- 2026-09-21（收工）：A/B 版遊戲完成並接上 DB（匿名寫入實測通過）；`handoff.md` 建立，詳見交接檔。
- 2026-09-21（收工）：B 版具名＋A 版 DB 即時排行＋課堂戰情儀表板完成；修 saveBoard 缺括號 bug；儀表板數據層實測通過。

## 1. 專案目錄現況

- `housing-copy.html`：房仲 FB/IG 行銷文案生成器（單檔 HTML，與目前數學遊戲主題無關，暫留）。
- `AGENTS.md`：本檔案，共用知識庫。
- `polynomial-division-game-A.html`：A 版遊戲（巧克力花椰菜，單檔離線可玩，已接 DB 上傳）。
- `polynomial-division-game-B.html`：B 版遊戲（結構型，單檔，已接 DB 上傳）。
- `classroom-dashboard.html`：課堂戰情儀表板（讀 DB，即時呈現 A/B 證據對比，教師投影用）。
- `handoff.md`：跨對話／跨電腦交接檔（收工必寫，開工必讀）。
- 本目錄已是 git repo（2026-09-21 建，首 commit `c623855`，L2 生效；尚無遠端，push 待設 remote 後再推）。
- L3：Obsidian `my-classroom-tools/專案工作流程.md`（詳細紀錄：決策＋踩坑，收工寫、開工按需讀）。

## 2. Supabase 連線（已完成）

- 選定專案：`20260706`
- Project ref：`mbhdtwxmhxsaxwosjnrw`
- 區域：`ap-northeast-1`（Tokyo），Postgres 17
- 狀態：2026-09-20 確認 `ACTIVE_HEALTHY`（之前為 INACTIVE，已在 Dashboard 按 Restore 喚醒）
- MCP 設定位置（全域，非本 repo）：`C:\Users\ccy2025\.config\opencode\opencode.json` → `mcp.supabase`
  - 模式：local stdio，`@supabase/mcp-server-supabase@latest`，`--project-ref`（唯讀已於 2026-09-21 解除，目前可寫）。
  - Token 放在全域設定，不進 repo。`opencode mcp list` 顯示 `supabase connected`。
  - 改設定後要重啟 OpenCode 才生效。
- 同帳號另有兩個專案（皆曾為 INACTIVE，若使用者提到再查）：
  - `my-teaching-tools`（`gtwmmqfadvgsvqjmqrsu`，ap-south-1）
  - `live-word-cloud`（`lnczipmbcxtstgnbieyq`，ap-southeast-2）

## 3. 資料庫現況（2026-09-20 實查）

- 查法：Management API `POST /v1/projects/{ref}/database/query` 查 `pg_tables`。
- 結果：`public` schema **0 張表、0 個 view**。只有系統 schema：
  - `auth` 27 張、`storage` 8 張、`realtime` 3 張、`vault` 1 張。
- 結論：`20260706` 原為空專案。2026-09-21 已建 `public.game_sessions`、`public.game_events`（A/B 版遊戲紀錄用，見 §7），`public` 不再是空的。

## 4. 教學設計理念（使用者的主張，已整理）

### 4.1 「巧克力花椰菜」：第一種遊戲化（批判對象）
- 定義：評量本質仍是選擇題，只用遊戲包裝。學生吃到的是花椰菜，不是巧克力。
- 六個缺點：
  1. 學生很快識破，新鮮感一過參與度掉更快。
  2. 外在獎勵（點數、排名）擠出內在動機；拿掉遊戲就不學了。
  3. 效度變差：量到手速、遊戲熟練度，而非理解。
  4. 認知負荷雙重：學科難＋遊戲規則難，低成就學生負擔最大。
  5. 公開競爭傷害後段學生，與差異化教學相違。
  6. 老師製作成本高，但題目與回饋品質沒提升。

### 4.2 「結構型遊戲化」：第二種遊戲化（主張方向）
- 定義：改變「菜」本身。學習過程本身就是遊戲，評量內建在過程裡。
- 通用五環（跨科共用）：
  1. 真實任務：學習目標翻譯成待解決的問題／作品。句式：「在＿＿情境下，用＿＿方法，產出＿＿，解決＿＿。」
  2. 探索與建構：解鎖制，完成 A 才見 B；AI 給線索不給答案；資料庫記路徑與卡關點。
  3. 結構性挑戰：排序／分類、因果／預測、修正／除錯。評思考結構，不評記憶。
  4. 證據產出：每環留一件思考證據（草稿、語音解釋、圖表、操作紀錄）；老師定義「好」的標準＋常見迷思。
  5. 回饋迭代：失敗不扣分，退回重練可重交；AI 指具體缺口，老師處理迷思與動機。
- 跨科備課表欄位：環節｜本單元設計｜AI 做什麼｜資料庫記什麼｜老師判什麼。
- 對照口訣：舊＝先教完→包遊戲→考選擇→給排名；新＝給任務→玩中學→留證據→給回饋→再挑戰。

## 5. 單元：國中八年級「多項式的除法」（規劃完成，未開始製作）

- 課綱：學習內容 `A-8-3`（被除式為二次之多項式的除法運算）；學習表現 `a-IV-5`。
- 核心關係：被除式＝商式×除式＋餘式。方法：分配律拆分＋直式長除法。
- 範圍限制：被除式最高二次；不用分離係數法；餘式次數＜除式次數。
- 常見迷思：降冪未排、缺項未補 0、忘加餘式、商次數判錯、符號錯。
- 共同母題（A/B 版共用，比較才公平）：
  1. `(x²+3x+2)÷(x+1)`
  2. `(x²-4)÷(x-2)`（缺項補 0）
  3. `(2x²+5x+2)÷(x+2)`（驗算餘式）
- A 版（巧克力花椰菜）：教完→勇者打怪皮→10 題選擇題→限時＋排名＋扣血；只看對錯速度。
- B 版（結構型）：麵包盒面積任務→面積拼圖探索→三關結構挑戰（分配／補零除／找錯驗算）→留步驟＋語音證據→錯了退回重練＋AI 針對性提示。
- 使用者指令：先做 A 版，再做 B 版，好比較差異。
- A 版已完成（2026-09-21）：`polynomial-division-game-A.html`（單檔，離線可玩，JS 語法已驗證）。
  內容：出發前複習→勇者vs餘式魔王→10 題選擇題（3 母題＋變式＋驗算＋餘式次數各 1 觀念題）→每題 30 秒→答對怪扣 10 HP＋100 分起跳（連擊＋時間加成）→答錯/超時扣 20 HP→結算答對率＋本機英雄榜。結尾附註明淺層回饋，供與 B 版比較。
- B 版已完成（2026-09-21）：`polynomial-division-game-B.html`（單檔，離線可玩，JS 語法已驗證）。
  內容：麵包店訂單三選一（面積/寬各不同）→磁磚拼圖探索（調長的組成，即時展開比對）→三關挑戰（分配填空／補0x＋商填空／點選錯誤步驟＋正確商＋驗算三格）→解鎖制＋嘗試/提示次數自動記錄→心得文字或錄音證據→完工證書（四項學習表現＋歷程表）。全程無分數排名計時，失敗不扣分＋針對性提示。（2026-09-21 補：領證書按鈕上傳後鎖死，防重複寫入——此前實測曾因連點產生雙胞胎 session。）

## 6. 待辦

- [x] 用母題製作 A 版遊戲（巧克力花椰菜）。
- [x] 製作 B 版遊戲（結構型）。
- [x] 寫入 DB：2026-09-21 使用者確認後，已解除 MCP `--read-only`（改設定需重啟 OpenCode 才生效）；已建表，見 §7。
- [x] B 版具名：2026-09-21，第 0 站加姓名／座號欄，`player_name`＋證書具名（空白回退「B版玩家」）。
- [x] A 版英雄榜改讀 DB：2026-09-21，結算時抓 `game_version=A` 前 5 名即時排行；離線回退本機＋假人。
- [x] 課堂儀表板：2026-09-21，`classroom-dashboard.html` 讀 sessions＋events 呈現人次／答對率／各站嘗試，供課堂對比討論用。

## 7. 資料表結構（`20260706`．`public`）

- `game_sessions`：一局遊戲一列。`id` uuid、`game_version`（A/B）、`player_name`、`score`、`accuracy`、`max_combo`、`total_time_s`、`order_id`（B 版訂單）、`reflection_text`、`has_audio`、`created_at`。
- `game_events`：B 版各站歷程。`id`、`session_id`（FK 級聯刪除）、`station`、`attempts`、`hints`、`status`、`created_at`＋`session_id` 索引。
- RLS 已開（2026-09-21）：兩表各有 `anon_insert_*`（anon 可 INSERT）＋`anon_read_*`（anon 可 SELECT）共 4 政策；anon key 是 publishable 設計，嵌在遊戲檔屬正常做法。MCP 經 Management API 寫入不受 RLS 限制。
- 前端已接線（2026-09-21，匿名 REST 直寫＋離線降級顯示）：A 版結算時上傳 1 列 session（版本／名／分／答對率／連擊／用時）；B 版領證書時先建 session（訂單／心得文字）再批次建 4 列 events；錄音不上傳、只留本機播放（`has_audio` 記 false）；上傳失敗顯示「未上傳，紀錄只留本機」。匿名鏈路已用測試列實測（建→讀→刪，級聯刪除正常，測後 count 歸 0）。
