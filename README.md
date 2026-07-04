# IELTS Repo Operator Manual

> This file tells you what to type, what Claude Code reads, and what it updates.
> It only documents behaviour that actually exists in this repo today. Anything not
> yet implemented is labelled **Proposed** — it will not silently happen just
> because it's written here.
>
> Source of truth for behaviour rules: [`CLAUDE.md`](CLAUDE.md). This file is the
> human-facing index into that behaviour, not a replacement for it.
> Last verified against repo state: 2026-07-04.

---

## 1. Quick Start

| 情境 | 我輸入什麼 | Claude Code 會做什麼 | 會更新哪些檔案 | Status |
|---|---|---|---|---|
| 開始今天 | `start today` | 讀 `dashboard.md` + 目前 Active Skill Sprint（+ Active Theme Sprint，如果有）→ 輸出今天任務、焦點技能、今日主題（僅在任務需要時） | 不寫入任何檔案 — 純讀取 + 對話輸出 | **Existing** |
| 結束今天 | `finish today` + 練習結果 | 依練習類型更新對應 DB，判斷是否需要重新生成 dashboard | `performance/*.md` · `errors/*.md` · `connie_profile.md` Evidence Log · `dashboard.md`（視情況）· sprint 進度（視情況） | **Existing** |
| 準備明天 Podcast | `幫我準備明天的 Podcast`（不用附輸入，全自動） | 從 `sentence_patterns.md`/`expressions.md` 的 Podcast Candidate 條目 + `writing_patterns.md` §9 主題輪替，自動決定 5 個輸入，生成「ConnieVerse」劇情型腳本 | 新建 `07_podcast/episodes/YYYY-MM-DD.md`；`daily_template.md` 的 Episode Archive 表追加一行 | **Existing**（2026-07-04 取代舊版 Rachel/Connie 格式，2026-07-05 改回全自動選材；英文說法 "prepare tomorrow podcast" 我能理解同樣意圖） |
| 貼老師課堂 feedback | `更新筆記` + 逐字稿 | 拆解逐字稿到對應筆記檔（只追加，不覆寫），更新錯誤 DB | `06_error_database/error_log.md` · `01_lessons/teacher.md` · `02_writing/writing_notes.md` / `03_speaking/speaking_notes.md` · `09_coach/errors/*.md`（視錯誤是否達到建 entry 門檻） | **Existing**（英文說法 "update lesson" 同義，觸發句本身是中文） |
| 貼 Simon / 官方 / 教學內容 | `萃取知識` | 判斷可重複使用知識，歸入 6 種類型之一，去重後新增 | `10_knowledge_base/writing/*.md` · `10_knowledge_base/ideas/<theme>/*.md` · `01_lessons/teacher.md` · `09_coach/errors/*.md`（依類型而定） | **Existing**（英文說法 "extract knowledge" 同義） |
| 貼範文 | `存範本`（= `learn model essay`） | 判斷題型存檔、估 Band、抽取可借用表達與句型、**萃取 Reusable Ideas / Mental Model 到 `10_knowledge_base/ideas/`**、更新 Anki | `02_writing/task1或2/models/*.md` · `models_index.md` · `sentence_patterns.md` · `expressions.md` · `skeleton_*.md` · `10_knowledge_base/ideas/<theme>/*.md` · `10_knowledge_base/ideas/INDEX.md` · `08_ai/anki/writing/*.md` | **Existing**（2026-07-04 合併，見下方說明） |
| 練完 Listening | 目前沒有獨立指令 | 走 `finish today`（如果今天任務就是 listening）或 Sunday Mock 回報格式 | `performance/listening_db.md` · `connie_profile.md` | **Proposed** — 獨立命令未定義，見 §4 |
| 每週回顧 | `weekly review` | 統整本週完成/未完成任務、Sprint 進度、新增的 Active Weakness，必要時引導填 Retrospective | `dashboard.md`（視情況重新生成）· Active Sprint 檔案的 §10（若當天是 Retrospective 日） | **Existing**（2026-07-04 新增） |
| 開下一個 Sprint | `start next sprint` | 讀 dashboard/DB/Retrospective → 決定下一個 Primary/Secondary 目標 → 建立新 sprint 檔 | 新建 `sprints/sprint-00N.md` · `sprints/INDEX.md` · `dashboard.md` | **Existing**（2026-07-04 新增） |
| （bonus）批改草稿 | `批改` + 草稿路徑 | 依老師標準評分、寫評語檔、更新 DB | `02_writing/task1或2/feedback/*.md` · `performance/writing_db.md` · `connie_profile.md` | **Existing** |
| （bonus）建草稿 | `建草稿` + 題目圖檔/文字 + 我的文章 | 存成統一格式草稿檔 | `02_writing/task1或2/drafts/*.md` | **Existing** |

### `存範本` / `learn model essay` 現況（2026-07-04 已合併）

你貼一篇範文並說「存範本」或「learn model essay」，現在**一個指令**就會做完：
Band 估計、值得學的表達、連接詞/句型片語、Anki，**加上**新的一步——判斷這篇裡哪些
論點通過「半年後還能用在別題」的標準，寫成 Mental Model（Claim → Reason →
Mechanism → Impact → Example），依 `10_knowledge_base/ideas/<theme>/` 現有筆記去重後
新建或延伸 atomic idea note（Learning Status 預設 New）。

`萃取知識` 仍然是獨立指令，用在範文以外的內容（老師逐字稿、Simon 文章、官方教材）——
這次合併不影響它，只是讓「存範本」處理範文時順便執行同一段 Reusable Ideas 邏輯。

---

## 2. Daily Workflow

### Morning / Start Session

我輸入：
```
start today
```

Claude Code 會讀（不寫入）：
- `CLAUDE.md`
- `09_coach/dashboard.md`
- `09_coach/sprints/INDEX.md`
- 目前 Active 的 Skill Sprint（目前是 [`09_coach/sprints/sprint-001.md`](09_coach/sprints/sprint-001.md)）
- Active 的 Theme Sprint，如果 `09_coach/sprints/THEME_SPRINT_TEMPLATE.md` 複製出來的
  `theme-*.md` 檔案 Status 為 Active（**目前沒有 Active 的 Theme Sprint** —
  `sprints/INDEX.md` 的 Theme Sprint 表格是空的）

Claude Code 會輸出：
- 今日任務（來自 Active Skill Sprint 當天的 session）
- 今日能力焦點
- 今日主題 — **只有** Active Theme Sprint 存在、且今天任務需要一個主題時才會出現
- Podcast / Daily Sheet 連結 — **目前沒有**自動生成每日 Sheet。舊的每日 Sheet 工作流程
  （`09_coach/daily/2026-06-29.md`、`2026-07-01.md`）已於 2026-07-04 封存到
  `09_coach/archive/old_daily/`；現在的 `start today` 不讀也不寫這個路徑

**這一步不更新任何檔案** — 純讀取 + 對話輸出。

### Evening / Finish Session

我輸入：
```
finish today
```
（附上今天練習的結果——草稿、分數、錯誤觀察）

Claude Code 會依今天練習類型更新：

| DB | 什麼情況下更新 |
|---|---|
| `09_coach/performance/writing_db.md` | 今天做了 writing 練習 |
| `09_coach/performance/listening_db.md` | 今天做了 listening 練習 |
| `09_coach/performance/speaking_db.md` | 今天有口說課或口說練習記錄 |
| `09_coach/errors/grammar_db.md` / `preposition_db.md` / `word_form_db.md` | 出現符合 confidence policy 門檻的錯誤（第二次以上才建 entry） |
| `09_coach/connie_profile.md` | Evidence Log 一定追加一行 |
| `09_coach/dashboard.md` | 只有觸發 Regeneration Triggers 才重新生成（見 dashboard.md 底部表格） |
| 目前 Active Sprint 檔案（`sprint-001.md`） | 該天的任務標記完成/進度 |
| Active Theme Sprint 的 `Output Links` | **只有**今天用了 Theme Sprint 的 idea 才更新 —— 目前無 Active Theme Sprint，不適用 |

---

## 3. Weekly Workflow

### Weekly Review — **Existing**（2026-07-04 新增進 `CLAUDE.md`）

我輸入：
```
weekly review
```

Claude Code 會讀 `dashboard.md`（本週目標）、Active Skill Sprint 本週每日 session、
`errors/*.md`、`performance/*.md`，判斷本週完成/未完成的任務與新增的弱點。如果今天
是 Active Sprint 排定的 Retrospective 日，會引導我一起填 §10 的三個表格。輸出本週
回顧 + 下週建議，**但不會自動開下一個 Sprint**——那是 `start next sprint` 的工作。
會更新：`dashboard.md`（視情況重新生成）、Active Sprint 檔案的 §10（若當場填了）。

### Start Next Sprint — **Existing**（2026-07-04 新增進 `CLAUDE.md`）

我輸入：
```
start next sprint
```

Claude Code 會讀 `dashboard.md` → `performance/*.md` → `errors/*.md`（只取 High
confidence）→ `connie_profile.md` → 目前 Active Sprint 的 §10 Retrospective（如果還
沒填，會先提醒我填，不會跳過）。依證據決定下一個 Sprint 的 Primary/Secondary 目標
（一次一個主要弱點，遵守 Simon 的規則），複製 `sprints/TEMPLATE.md` 建立新的
`sprints/sprint-00N.md`，把舊 sprint 狀態改 Completed、新 sprint 設為 Active。
會更新：新建 `sprints/sprint-00N.md`、`sprints/INDEX.md`、`dashboard.md`。

---

## 4. Knowledge Intake Workflow

三種輸入，分開處理，不要混在一起：

### A. `萃取知識`（extract knowledge）— **Existing**

使用情境：老師教材、Simon 分析、官方教材、IELTS 教學文章、課堂逐字稿裡可重複使用的知識。

判斷標準：半年後看到，仍然可以直接拿來寫另一篇作文或回答另一題 IELTS。

依實際存在的檔案，會更新：

| 知識類型 | 存放位置 |
|---|---|
| Writing Patterns | `10_knowledge_base/writing/essay_patterns.md` 等（**注意**：`CLAUDE.md` 文件裡列的檔名如 `essay_patterns.md` / `question_types.md` / `planning.md` / `paragraph_patterns.md` / `introductions.md` / `conclusions.md` 實際上不存在——目前這些內容全部合併在 `10_knowledge_base/writing/writing_patterns.md` 一個檔案裡，見 §5） |
| Reusable Expressions | `10_knowledge_base/writing/expressions.md` |
| Sentence Patterns | `10_knowledge_base/writing/sentence_patterns.md` |
| Reusable Ideas | `10_knowledge_base/ideas/<theme>/<claim>.md`（atomic note，含 `Skeleton` 與 `Learning Status`） |
| Teacher Principles | `01_lessons/teacher.md` |
| Error Patterns | `09_coach/errors/grammar_db.md` 等（依 confidence policy） |

### B. `存範本`（= `learn model essay`）— **Existing**（2026-07-04 合併）

使用情境：貼一篇範文。

重要原則（你的規則，已生效）：
- 不要把範文變成收藏
- 不要鼓勵背整段
- 不要儲存整篇 body paragraph

會萃取（存在 `02_writing/task*/models/*.md` 的分析區塊裡）：
- Band 估計
- 這篇好在哪（結構/手法）
- 值得學的表達
- 連接詞/句型片語
- **Reusable Ideas / Mental Model**（Claim → Reason → Mechanism → Impact → Example）——
  只收通過「半年後還能用在別題」標準的論點

Learning Status（New/Practised/Internalised）存在於：
- `10_knowledge_base/ideas/TEMPLATE.md`（每個 idea note，`存範本` 新建/延伸時預設 New）
- `10_knowledge_base/writing/expressions.md`
- `10_knowledge_base/writing/writing_patterns.md` §8b Reasoning Patterns

`存範本` 現在會自動把範文裡合格的論點，依 `10_knowledge_base/ideas/<theme>/` 現有筆記去重後
新建或延伸 atomic idea note——不用再另外喊「萃取知識」。`萃取知識` 仍是獨立指令，
只是專門處理範文以外的內容（老師逐字稿、Simon 文章、官方教材）。

### C. `更新筆記`（update lesson）— **Existing**

使用情境：貼老師 feedback / 上課逐字稿。

會更新：
- `06_error_database/error_log.md`（原句 → 正確句格式，只追加）
- `01_lessons/teacher.md`（新原則）
- `03_speaking/speaking_notes.md` / `02_writing/writing_notes.md`（新重點）
- `09_coach/errors/*.md`（只有錯誤達到 confidence policy 門檻才建 entry）
- `09_coach/connie_profile.md` Evidence Log

---

## 5. File Update Policy

### A. Regularly Updated Files（每天/每週可能更新）

- `09_coach/dashboard.md`
- `09_coach/connie_profile.md`
- `09_coach/performance/listening_db.md` · `reading_db.md` · `writing_db.md` · `speaking_db.md`
- `09_coach/errors/grammar_db.md` · `preposition_db.md` · `word_form_db.md`
- `09_coach/sprints/sprint-001.md`（目前 Active Skill Sprint，逐日進度）
- `09_coach/sprints/INDEX.md`（Sprint 狀態變動時）
- `06_error_database/error_log.md`
- `01_lessons/teacher.md` · `02_writing/writing_notes.md` · `03_speaking/speaking_notes.md`
- `10_knowledge_base/ideas/<theme>/*.md`（Learning Status 更新）
- `10_knowledge_base/writing/expressions.md` · `sentence_patterns.md` · `writing_patterns.md`

### B. Passive Reference Files（通常只讀取，很少更新）

- `CLAUDE.md`
- `08_ai/prompts/coach_prompt.md`
- `08_ai/teachers/matt.md` · `joe.md`
- `10_knowledge_base/ARCHITECTURE.md`
- `10_knowledge_base/coaches/*/distilled.md` · `index.md`（只有 `新增教練文章` 指令觸發時更新）
- `10_knowledge_base/consensus/*.md`
- `10_knowledge_base/conflicts.md` · `10_knowledge_base/coaches/conflicts.md`
- `10_knowledge_base/vocabulary/*.md` · `10_knowledge_base/listening/*.md` · `10_knowledge_base/speaking/*.md`
  （讀取頻率跟 coaches/consensus 差不多）
- `09_coach/sprints/TEMPLATE.md` · `THEME_SPRINT_TEMPLATE.md` · `CHANGELOG.md`（Sprint 版型定義，只有重新設計時才動）
- `DECISIONS.md` · `PRD.md` · `09_coach/PLAN.md`（專案層級文件，非日常教練流程會動到的）
- `10_knowledge_base/`（**2026-07-06 統一為單一頂層知識庫**——`ideas/`、`coaches/`、
  `consensus/`、`vocabulary/`、`listening/`、`speaking/`、`writing/`（含 WR/expressions/
  collocations 合併後的內容）與原本就在這裡的 `grammar/`、`prepositions/`、`word_form/`
  （G/P/W 卡片）現在都在同一個資料夾底下，不再分散成頂層 `knowledge` 資料夾和
  `02_writing` 底下的 `knowledge` 子資料夾兩個獨立位置。G/P/W 卡片跟 `09_coach/errors/*.md` 內容重疊（例如 G001 兩邊都有）——
  **維持分開，不合併**：`10_knowledge_base/` 是教學卡片格式，`09_coach/errors/*.md`
  是 confidence-tracked 的錯誤證據資料庫，用途不同。

### C. Generated Files（由指令產生的新檔）

- `02_writing/task1/drafts/*.md` · `task2/drafts/*.md` — `建草稿`
- `02_writing/task1/feedback/*.md` · `task2/feedback/*.md` — `批改`
- `02_writing/task1/models/*.md` · `task2/models/*.md` — `存範本`
- `07_podcast/episodes/YYYY-MM-DD.md` — `幫我準備明天的 Podcast`
- `08_ai/anki/writing/*.md` · `speaking/*.md` — 「幫我做 Anki 卡」
- `10_knowledge_base/ideas/<theme>/<idea>.md` — `萃取知識` 或 `存範本`（新 idea 才建檔，延伸用 Related Notes）
- `10_knowledge_base/coaches/<coach>/originals/*.md` — `存文章`
- `09_coach/sprints/sprint-00N.md` — `start next sprint`

### Archived（已封存，不再是 Active 工作流程的一部分）

- `09_coach/archive/old_daily/2026-06-29.md` · `2026-07-01.md` — 2026-07-04 從
  `09_coach/daily/` 移出封存。這是重新設計 Sprint 系統前的「每日 Sheet」工作流程，
  現在的 `start today` / `finish today` 直接讀 dashboard + sprint 檔案，不再需要
  逐日生成的 Sheet。`09_coach/daily/` 資料夾已不存在。

### Passive / 空模板（存在但目前沒有指令讀寫）

- `04_listening/review_queue.md` · `05_reading/review_queue.md` — 空模板
- `07_podcast/commute_plan.md` — 空模板

---

## 6. Sprint Rules

- **Skill Sprint 是主線**（`09_coach/sprints/TEMPLATE.md` / `sprint-001.md`），決定今天練什麼能力、D1→D3 難度。
- **Theme Sprint 是輔助**（`09_coach/sprints/THEME_SPRINT_TEMPLATE.md`），只有在今天任務需要一個主題時才提供題材。
- Theme Sprint **不能**新增任務，也**不能**覆蓋 Skill Sprint 排定的內容。
- Theme Sprint 的目的**不是**收藏好句，而是建立主題的 Mental Model（Core Arguments → Skeleton → Reasoning Patterns → Functional Language → Natural Collocations）。
- Knowledge Base 的目的**不是**收藏，而是建立可重複輸出的能力——每筆知識都有 Learning Status（New → Practised → Internalised），系統應該推動舊知識往 Internalised 前進，而不是一直堆新的 New。

詳細設計原則見 [`10_knowledge_base/ARCHITECTURE.md`](10_knowledge_base/ARCHITECTURE.md)。

---

## 7. Definition of Done

**`start today`**
- [ ] 已讀 `dashboard.md`
- [ ] 已確認 Active Skill Sprint 與今天對應的 session
- [ ] 已檢查是否有 Active Theme Sprint，並依此決定要不要附加主題
- [ ] 已輸出今日任務、焦點技能，並標示是否使用了 Theme Sprint 的 idea

**`finish today`**
- [ ] 已根據回報內容判斷今天練習類型
- [ ] 已更新相對應的 performance/error DB，或明確說明「這次不需要更新哪個 DB」
- [ ] 已在 `connie_profile.md` Evidence Log 追加一行
- [ ] 已判斷 dashboard 是否需要重新生成，並執行或說明為何不需要
- [ ] 若今天用了 Theme Sprint 的 idea，已更新該 Theme Sprint 的 Output Links

**`幫我準備明天的 Podcast`（ConnieVerse）**
- [ ] 已從 `sentence_patterns.md` Podcast Candidates + `expressions.md` Podcast Candidate=Yes 條目自動選出 Pattern/Vocabulary，且沒有跟過去 2 週的 Episode Archive 重複
- [ ] 已從 `writing_patterns.md` §9 選出不跟昨天重複的 IELTS Topic
- [ ] 已創作貼合 ConnieVerse 世界觀的 Setting/Conflict
- [ ] 已依 `07_podcast/daily_template.md` 的固定結構生成完整腳本
- [ ] 已產生 `07_podcast/episodes/YYYY-MM-DD.md`（明天日期），並在 Episode Archive 表追加一行
- [ ] 已回報這集自動選了什麼、每項為什麼選它

**`更新筆記`**
- [ ] 已比對逐字稿與現有筆記，避免重複
- [ ] 已用「原句 → 正確句」格式記錄新錯誤
- [ ] 已只用「追加」方式更新筆記，沒有刪除或改寫既有內容
- [ ] 已條列這次新增了什麼給我確認

**`萃取知識`**
- [ ] 已用「半年後還能用嗎」的標準篩選內容
- [ ] 已依 6 種類型分類，並檢查是否與現有知識重複
- [ ] 已回報：新增了什麼、更新了什麼、哪些內容沒有保存（原因）

**`存範本`（= `learn model essay`）**
- [ ] 已判斷題型並存到對應資料夾
- [ ] 已產生 Band 估計、結構分析、值得學的表達、連接詞/句型片語
- [ ] 已產生 Reusable Ideas / Mental Model 區塊，只收通過「半年後還能用」標準的論點
- [ ] 已依 `10_knowledge_base/ideas/<theme>/` 現有筆記去重，新建或延伸 atomic idea note
- [ ] 已更新 `models_index.md`、`sentence_patterns.md`、`expressions.md`（如適用）、對應 `skeleton_*.md`
- [ ] 已檢查同題是否已有範本，若有則提醒

**`weekly review`**
- [ ] 已讀 dashboard 確認本週目標
- [ ] 已比對本週實際完成 vs 排定任務
- [ ] 已檢查本週是否有新增/升級的 Active Weakness
- [ ] 若當天是 Retrospective 日，已引導填寫或明確說明還沒到日子
- [ ] 已輸出下週建議（基於證據，不是憑空建議）

**`start next sprint`**
- [ ] 已確認上一個 Sprint 的 Retrospective 已填（沒填先提醒，不跳過）
- [ ] 已依證據決定 Primary/Secondary 目標（各最多一個）
- [ ] 已建立新的 `sprints/sprint-00N.md`，並把舊 sprint 狀態改 Completed
- [ ] 已更新 `sprints/INDEX.md`、`dashboard.md`

---

## 8. Safety Rules

- 不要建立不存在的檔案路徑，除非標註 Proposed。
- 不要重寫整份 Knowledge Base。
- 不要刪除既有學習紀錄。
- 所有更新以 append-first 為原則（`更新筆記` 尤其明確：只加不刪）。
- 如果不確定檔案是否存在，先查檔案樹，不要用猜的路徑。
- 如果某個流程會影響多個檔案（例如 Sprint 重設、Knowledge Base 改版），先列出計畫再修改，
  不要一次性靜默改完。

---

## Repo Structure（實際存在的資料夾，2026-07-06 驗證）

```
ielts-notes/
├── 01_lessons/                  # 課堂筆記（原始證據）
├── 10_knowledge_base/           # 單一頂層知識庫（2026-07-06 統一，見下方明細）
│   ├── ideas/<theme>/           # Reusable Ideas SSOT
│   ├── coaches/(simon/matt/joe)
│   ├── consensus/
│   ├── vocabulary/ · listening/ · speaking/
│   ├── grammar/ · prepositions/ · word_form/   # G/P/W 教學卡片
│   ├── writing/                 # writing_patterns.md（含 §10 Task 1）· sentence_patterns.md · expressions.md · skeleton_*.md
│   ├── practice_method.md
│   ├── ARCHITECTURE.md
│   └── index.md
├── 02_writing/
│   ├── task1/ (drafts/feedback/models)
│   └── task2/ (drafts/feedback/models)
├── 03_speaking/ (practice/chat, practice/situation)
├── 04_listening/ · 05_reading/  # review_queue.md 目前是空模板
├── 06_error_database/
├── 07_podcast/ (episodes/)
├── 08_ai/ (anki/ · prompts/ · teachers/)
├── 09_coach/
│   ├── dashboard.md
│   ├── connie_profile.md
│   ├── sprints/ (INDEX.md · TEMPLATE.md · THEME_SPRINT_TEMPLATE.md · CHANGELOG.md · sprint-001.md)
│   ├── performance/ · errors/
│   └── archive/ (old_dashboard/ · old_daily/)
├── CLAUDE.md                    # 行為規則的唯一權威來源
├── DECISIONS.md · PRD.md        # 專案層級文件
└── README.md                    # 這份文件
```

---

## Summary — 這次改了什麼（2026-07-04，含決策後續更新）

1. **README.md 全面改寫**成 Operator Manual 格式：Quick Start 表 + Daily/Weekly
   Workflow + Knowledge Intake + File Policy + Sprint Rules + Definition of Done +
   Safety Rules。
2. **Existing**：`start today` · `finish today` · `幫我準備明天的 Podcast` ·
   `更新筆記` · `萃取知識` · `存範本`(=`learn model essay`) · `批改` · `建草稿` ·
   **`weekly review`**（新增）· **`start next sprint`**（新增）。
3. **決策已執行**：
   - `存範本` + `萃取知識` 合併 → `CLAUDE.md` 存範本行為新增 Reusable Ideas /
     Mental Model 步驟（見該檔案「存範本行為」章節）；`萃取知識` 保留為獨立指令，
     處理範文以外的內容。
   - `weekly review` / `start next sprint` → 已寫進 `CLAUDE.md`「每週互動模式」章節，
     含完整步驟與回報格式。
   - `09_coach/daily/` → 兩個舊檔已用 `git mv` 移到 `09_coach/archive/old_daily/`，
     `09_coach/daily/` 資料夾已不存在。
   - `10_knowledge_base/` vs `09_coach/errors/*.md` → 維持分開，不合併（用途不同：
     教學卡片 vs confidence-tracked 錯誤證據庫）。
   - **Podcast 格式完全換掉（2026-07-04）**：舊版 Rachel/Connie 教學對話格式 →
     ConnieVerse 劇情型格式（巴黎平行宇宙 Connie，Emily in Paris/Friends 風格）。
     `10_knowledge_base/` 因此變成 **Orphaned**——內容還在，但沒有指令會再自動讀寫它。
   - **Podcast 選材改回全自動（2026-07-05）**：一度改成「你每次自己填 5 個輸入」，
     但很快發現這樣切斷了跟 Knowledge Base 的連結。現在 `sentence_patterns.md` 和
     `expressions.md` 的每筆條目多了 **Podcast Candidate**（Yes/No）欄位，Podcast
     自動從標 Yes 的條目選 Target Pattern/Vocabulary（避免兩週內重複），IELTS Topic
     從 `writing_patterns.md` §9 輪替，Setting/Conflict 由 Claude 創作。你不用附任何
     輸入，想指定某個輸入時可以直接說，其餘照舊自動選。
   - **`10_knowledge_base/` 內部重複問題解決（2026-07-05）**：發現舊的
     `writing`（WR001-008）、`expressions`（E001-003）、`collocations`（C001）卡片
     跟新寫的 Writing Patterns 內容重複——已比對合併，舊卡片刪除
     （merge 過程中順便補了一個真正的缺口：Task 1 letter 規則之前完全沒進
     Writing Patterns，現在是 `writing_patterns.md` §10）。`vocabulary`、
     `listening`、`speaking`（+ 誤放在 expressions 底下的 E004）其實**沒有重複**，只是
     Podcast 改用 ConnieVerse 後變成孤兒——搬進獨立的 `vocabulary/`/`listening/`/
     `speaking/` 子資料夾，不再是孤兒。
   - **單一頂層知識庫整併（2026-07-06）**：2026-07-05 那次重構一度把內容拆成三處
     （`10_knowledge_base/` 只留 grammar/prepositions/word_form、頂層 `knowledge`
     資料夾放 ideas/coaches/consensus/vocabulary/listening/speaking、`02_writing`
     底下的 `knowledge` 子資料夾放 writing patterns），造成「知識庫」名不副實地散落
     在三個資料夾。已用 `git mv` 把那兩個資料夾的全部內容併回 `10_knowledge_base/`，
     現在只有一個頂層知識庫資料夾；上述兩個舊資料夾都已不存在。
4. **仍是 Proposed**（未決策，維持現狀）：獨立的「練完 Listening」指令——目前仍靠
   `finish today` 或 Sunday Mock 回報帶過。
