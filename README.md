# IELTS Repo Operator Manual

> This file tells you what to type, what Claude Code reads, and what it updates.
> It only documents behaviour that actually exists in this repo today. Anything not
> yet implemented is labelled **Proposed** — it will not silently happen just
> because it's written here.
>
> Source of truth for behaviour rules: [`CLAUDE.md`](CLAUDE.md). This file is the
> human-facing index into that behaviour, not a replacement for it.
> Last verified against repo state: 2026-07-05.

---

## 1. Quick Start

| 情境 | 我輸入什麼 | Claude Code 會做什麼 | 會更新哪些檔案 | Status |
|---|---|---|---|---|
| 開始今天 | `start today` | 讀 `dashboard.md` + 目前 Active Skill Sprint（+ Active Theme Sprint，如果有）→ 輸出今天任務、焦點技能、今日主題（僅在任務需要時） | 不寫入任何檔案 — 純讀取 + 對話輸出 | **Existing** |
| 結束今天 | `finish today` + 練習結果 | 依練習類型更新對應 DB，判斷是否需要重新生成 dashboard | `performance/*.md` · `errors/*.md` · `connie_profile.md` Evidence Log · `dashboard.md`（視情況）· sprint 進度（視情況） | **Existing** |
| 生成 Podcast | `生成 Podcast` / `產生 Podcast` / `generate podcast` + Stage 1、2 或 3 input | 先由 gated router 判斷 input 類型，再只執行一個 stage；資料不足就停止 | Stage 1 → `source_briefs/`；Stage 2 → `output_drills/`；Stage 3 → `chants/` | **Existing — gated** |
| 產生 NotebookLM source brief | `根據這些資料產生 NotebookLM source brief` / `Generate NotebookLM source brief` + 使用者來源 | 預設 Research-Assisted Mode，以使用者材料為主並用可信來源補充；生成 Source Log、Source Briefing Article 與 NotebookLM Generation Prompt | 新建 `07_podcast/source_briefs/YYYY-MM-DD_notebooklm_source_brief_<topic-slug>.md`；不更新 Knowledge Base | **Existing — Phase 1** |
| 產生 Output Drill Script | `產生 Output Drill Script` + `# Output Drill Input` | 驗證使用者指定的 Pattern/Sentence/Vocabulary，解析 context，生成 ElevenLabs-ready script | `07_podcast/output_drills/YYYY-MM-DD_output_drill_<topic-slug>.md` | **Existing — Stage 2** |
| 產生 Chant | `生成 Podcast` / `產生 Chant` + `# Chant Input` 或 `Target sentence pattern:` | 用使用者提供的單一句型產生重複 chant lyrics 與 Suno prompt | `07_podcast/chants/YYYY-MM-DD_chant_<pattern-slug>.md` | **Existing — Stage 3** |
| 貼老師課堂 feedback | `更新筆記` + 逐字稿 | 拆解逐字稿到對應筆記檔（只追加，不覆寫），更新錯誤 DB | `06_error_database/error_log.md` · `01_lessons/teacher.md` · `02_writing/writing_notes.md` / `03_speaking/speaking_notes.md` · `09_coach/errors/*.md`（視錯誤是否達到建 entry 門檻） | **Existing**（英文說法 "update lesson" 同義，觸發句本身是中文） |
| 貼英文或教學內容 | `萃取知識`／`收錄 Knowledge Base`／`加入知識庫`／`學這句`／`這句不錯`／`值得收錄` | 萃取真正可重用的知識，先搜尋全庫，預設更新或合併既有條目；概念全新才建立 | `10_knowledge_base/` 對應分類（錯誤另依 policy 更新 `09_coach/errors/`） | **Existing** |
| 收錄單字 | `收錄單字 excavate` / `學單字 excavate` / 單獨提供一個 headword | 優先查 Vocabulary.com，建立英英 Front 與含 IPA、詞性、frequency、例句的 Back；先進 Knowledge Base，不直接產 Anki | `10_knowledge_base/vocabulary/<word>.md` · `knowledge_review_queue.md` | **Existing** |
| 記錄造句錯誤 | `記錄造句錯誤` + 原句／修正版／分析 | Front 保留完整錯誤原句；Back 保存修正版與 AI 分析。先進 review inbox，不拆成新詞或其他卡 | `10_knowledge_base/error_corrections/YYYY-MM-DD_<slug>.md` · `knowledge_review_queue.md` | **Existing** |
| 貼範文 | `存範本`（= `learn model essay`） | 判斷題型存檔、估 Band、抽取可借用表達與句型、**萃取 Reusable Ideas / Mental Model 到 `10_knowledge_base/ideas/`**、更新 Anki | `02_writing/task1或2/models/*.md` · `models_index.md` · `sentence_patterns/` · `expressions/` · `skeleton_*.md` · `10_knowledge_base/ideas/<theme>/*.md` · `10_knowledge_base/ideas/INDEX.md` · `08_ai/anki/writing/*.md` | **Existing**（2026-07-04 合併，見下方說明） |
| 練完 Listening | 目前沒有獨立指令 | 走 `finish today`（如果今天任務就是 listening）或 Sunday Mock 回報格式 | `performance/listening_db.md` · `connie_profile.md` | **Proposed** — 獨立命令未定義，見 §4 |
| 整理 Anki | `整理 anki` / `整理 Anki` | 將 active Vocabulary、Expressions、Sentence Patterns 與已看過的 Error Corrections 轉成 Front/Back；成功產卡後移至各自 archive | `08_ai/anki/weekly/knowledge-review_YYYY-MM-DD.md` · Knowledge archives · `knowledge_review_queue.md` | **Existing** |
| 每週回顧 | `weekly review` | 統整任務、Sprint 與 Weakness，執行 Vocabulary / Expressions / Sentence Patterns → Anki，並列出待確認的 Error Corrections | `knowledge_review_queue.md` · `08_ai/anki/weekly/knowledge-review_YYYY-MM-DD.md` · Knowledge archives · dashboard／Sprint（視情況） | **Existing** |
| 開下一個 Sprint | `start next sprint` | 讀 dashboard/DB/Retrospective → 決定下一個 Primary/Secondary 目標 → 建立新 sprint 檔 | 新建 `sprints/sprint-00N.md` · `sprints/INDEX.md` · `dashboard.md` | **Existing**（2026-07-04 新增） |
| （bonus）批改草稿 | `批改` + 草稿路徑 | 依老師標準評分、寫評語檔、更新 DB | `02_writing/task1或2/feedback/*.md` · `performance/writing_db.md` · `connie_profile.md` | **Existing** |
| （bonus）建草稿 | `建草稿` + 題目圖檔/文字 + 我的文章 | 存成統一格式草稿檔 | `02_writing/task1或2/drafts/*.md` | **Existing** |

## 生成 Podcast

這是一個三階段 gated workflow。`生成 Podcast`、`產生 Podcast` 或
`generate podcast` 不會直接製作一份未經驗證的完整 Podcast；系統先判斷 input
類型，而且每次只執行一個 stage。

### 如果我提供 NotebookLM Source Input

系統執行 Stage 1，產生 NotebookLM source brief，存到：

```text
07_podcast/source_briefs/
```

### 如果我提供 Output Drill Input

系統執行 Stage 2，產生 ElevenLabs output drill script，存到：

```text
07_podcast/output_drills/
```

### 如果我提供 Chant Input

系統執行 Stage 3，使用我指定的 Target Sentence Pattern 產生 chant lyrics 與 Suno
prompt，存到：

```text
07_podcast/chants/
```

### 如果資料不足

系統會停止並要求補資料，不會自動選句型、補 Model Sentence、挑 Vocabulary 或猜測
多個 context 候選。

### Generate NotebookLM Source Brief — Phase 1

先提供 IELTS question、model essay、article、source notes、NotebookLM notes 或自己
整理的 viewpoints，再輸入指令。推薦直接複製
[`07_podcast/templates/source_input_template.md`](07_podcast/templates/source_input_template.md)。

輸入模板預設 `Research-Assisted Mode`，以使用者材料為主，外部可信來源只能補充、
對照或提供背景；也可明確切換成 `Strict Source Mode`，完全不查外部資料。Topic 名稱
本身不是足夠來源；若內容無法支持至少三個 viewpoints，系統回覆
`Source is insufficient.` 且不建檔。

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
- Daily Sheet 連結 — **目前沒有**自動生成每日 Sheet。舊的每日 Sheet 工作流程
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
同時會執行下方 `整理 anki` workflow。會更新：weekly Anki、Knowledge archives、
queue、`dashboard.md`（視情況重新生成）、Active Sprint 檔案的 §10（若當場填了）。

### Organize Anki — **Existing**

我只想整理 Knowledge，不做完整 weekly review 時，輸入：

```text
整理 anki
```

`整理 Anki`、`整理anki` 也可以。系統會：

1. 讀取 `10_knowledge_base/vocabulary/`、`expressions/` 與 `sentence_patterns/`
   根目錄中的 active notes；
2. 搜尋所有既有 Anki 卡，避免相同 target 重複；
3. 依英文情境 Front / 正確 target + example Back 產卡；
4. 存到 `08_ai/anki/weekly/knowledge-review_YYYY-MM-DD.md`；
5. 卡片成功寫入或已確認存在後，才把來源 note 移到該類別的 `archive/`；
6. 更新 Knowledge Review Queue 的 link、Status、Last Review 與 Practice Evidence。

Archive 仍是 Knowledge Base，不是垃圾桶。未成功產卡或資料不完整的 note 會留在 active
folder；未來新增知識時也必須搜尋 archive，避免重新建立同一項。

Error Corrections 多一個人工確認 gate：直接輸入 `整理 anki` 代表已看過並批准；
`weekly review` 只列出 Pending Error Corrections，不會自動產卡或封存。

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

五種輸入，分開處理，不要混在一起：

### A. Vocabulary Intake — **Existing**

輸入 `收錄單字 excavate`、`學單字 excavate`、`excavate 做成單字卡`，或在單字 workflow
脈絡中只貼一個英文 headword。系統會優先讀 Vocabulary.com，建立：

- Front：不出現答案的精簡英英解釋
- Back：word、IPA、part of speech、frequency、兩個 domain-labelled examples、word forms
- Source：dictionary、直接 URL、access date，以及哪些欄位由使用者提供

Frequency 若來源頁沒有顯示、使用者也沒提供，就寫 `Not available`，不能估算。網站
長篇說明會改寫，例句預設原創，不整段複製第三方 example corpus。

新 note 存到 `10_knowledge_base/vocabulary/<word-slug>.md`，queue 標 `Pending`。
Intake 階段不建立 Anki；等之後輸入 `整理 anki` 才一起產卡與搬 archive。

### B. Error Correction Intake — **Existing**

輸入 `記錄造句錯誤`、`收錄造句錯誤` 或 `記錄這個錯誤`，並附原句與 AI／老師的修正
分析。每一筆只建立一張簡單卡：

- Front：完整保留你原本寫的句子，不修正
- Back：英文 Corrected Version、繁體中文 Error Analysis、繁體中文 Key Reminder

新 note 存到 `10_knowledge_base/error_corrections/`，queue 標 `Pending`。不會從同一筆
錯誤自動新增 Vocabulary、Expression、Sentence Pattern 或 Idea。你看過後直接輸入
`整理 anki`，才會產卡並移到 `error_corrections/archive/`。

### C. `萃取知識`（extract knowledge）— **Existing**

觸發語包含：「萃取知識」、「收錄 Knowledge Base」、「加入知識庫」、「學這句」、
「這句不錯」、「值得收錄」。適用於英文句子、段落、單字、collocation、expression、
老師教材、Simon 分析、官方教材與課堂逐字稿。

判斷標準：半年後看到，仍然可以直接拿來寫另一篇作文或回答另一題 IELTS。
不要預設保存整句；先抽出真正可重複使用的部分。建立前搜尋整個 Knowledge Base，
預設更新、補例句、改善解釋或合併重複條目，只有概念確實全新才建立新檔。

依實際存在的檔案，會更新：

| 知識類型 | 存放位置 |
|---|---|
| Writing methodology / structure | `10_knowledge_base/writing/` |
| User-selected Vocabulary | `10_knowledge_base/vocabulary/` |
| Reusable Expressions / chunks | `10_knowledge_base/expressions/` |
| Sentence Patterns | `10_knowledge_base/sentence_patterns/` |
| Error Corrections | `10_knowledge_base/error_corrections/` |
| Grammar Notes | `10_knowledge_base/grammar_notes/` |
| Reusable Ideas | `10_knowledge_base/ideas/<theme>/<claim>.md`（atomic note，含 `Skeleton` 與 `Learning Status`） |
| Listening / Speaking strategies | `10_knowledge_base/listening/` · `10_knowledge_base/speaking/` |
| Individual Coach Principles | `10_knowledge_base/coaches/<coach>/` |
| Cross-coach Consensus | `10_knowledge_base/consensus/` |

自然、可跨情境使用的 Expression 或 Sentence Pattern 留在相應知識資料夾。收錄知識
時不會自動生成 NotebookLM source brief，也不會把新 Knowledge 自動當成 source。
Source Briefing Article 與 NotebookLM Generation Prompt 不進知識庫。

### D. `存範本`（= `learn model essay`）— **Existing**（2026-07-04 合併）

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
- `10_knowledge_base/expressions/`
- `10_knowledge_base/writing/writing_patterns.md` §8b Reasoning Patterns

`存範本` 現在會自動把範文裡合格的論點，依 `10_knowledge_base/ideas/<theme>/` 現有筆記去重後
新建或延伸 atomic idea note——不用再另外喊「萃取知識」。`萃取知識` 仍是獨立指令，
只是專門處理範文以外的內容（老師逐字稿、Simon 文章、官方教材）。

### E. `更新筆記`（update lesson）— **Existing**

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
- `10_knowledge_base/vocabulary/` · `expressions/` · `sentence_patterns/` · `writing/writing_patterns.md`
- `10_knowledge_base/error_corrections/`（使用者尚未批准送 Anki 的修正卡）

### B. Passive Reference Files（通常只讀取，很少更新）

- `CLAUDE.md`
- `08_ai/prompts/coach_prompt.md`
- `08_ai/teachers/matt.md` · `joe.md`
- `10_knowledge_base/ARCHITECTURE.md`
- `10_knowledge_base/coaches/*/distilled.md` · `index.md`（只有 `新增教練文章` 指令觸發時更新）
- `10_knowledge_base/consensus/*.md`
- `10_knowledge_base/conflicts.md` · `10_knowledge_base/coaches/conflicts.md`
- `10_knowledge_base/listening/*.md` · `10_knowledge_base/speaking/*.md`
  （讀取頻率跟 coaches/consensus 差不多）
- `09_coach/sprints/TEMPLATE.md` · `THEME_SPRINT_TEMPLATE.md` · `CHANGELOG.md`（Sprint 版型定義，只有重新設計時才動）
- `DECISIONS.md` · `PRD.md` · `09_coach/PLAN.md`（專案層級文件，非日常教練流程會動到的）
- `10_knowledge_base/`（**2026-07-06 統一為單一頂層知識庫**——`vocabulary/`、
  `ideas/`、`coaches/`、
  `consensus/`、`listening/`、`speaking/`、`writing/`（現在只剩 essay/skeleton 結構性
  內容）、`expressions/`、`sentence_patterns/`，以及原本就在這裡的
  `grammar_notes/grammar/`、`grammar_notes/prepositions/`、
  `grammar_notes/word_form/`（G/P/W 卡片，2026-07-06 起統一收進 `grammar_notes/` 這個
  父資料夾）現在都在同一個資料夾底下，不再分散成頂層 `knowledge` 資料夾和
  `02_writing` 底下的 `knowledge` 子資料夾兩個獨立位置。G/P/W 卡片跟 `09_coach/errors/*.md` 內容重疊（例如 G001 兩邊都有）——
  **維持分開，不合併**：`10_knowledge_base/` 是教學卡片格式，`09_coach/errors/*.md`
  是 confidence-tracked 的錯誤證據資料庫，用途不同。
- **現行分類規則**：使用者明確選的單一 headword → `vocabulary/`；能塞進很多句子
  幾乎不用改的 multi-word chunk → `expressions/`；有空格可替換的 frame →
  `sentence_patterns/`；完整錯誤原句與修正分析 → `error_corrections/`；觀點而非語言
  → `ideas/<theme>/`。
  文法規則另外走 `grammar_notes/`，只在犯錯時查，不用主動複習。`expressions/` 與
  `sentence_patterns/` 現在是 `10_knowledge_base/` 的直接子項，不再嵌在
  `writing/` 底下（`writing/` 現在只放 essay 結構：
  `writing_patterns.md` + `skeleton_*.md`）。

### C. Generated Files（由指令產生的新檔）

- `02_writing/task1/drafts/*.md` · `task2/drafts/*.md` — `建草稿`
- `02_writing/task1/feedback/*.md` · `task2/feedback/*.md` — `批改`
- `02_writing/task1/models/*.md` · `task2/models/*.md` — `存範本`
- `07_podcast/source_briefs/YYYY-MM-DD_notebooklm_source_brief_<topic-slug>.md` — `根據這些資料產生 NotebookLM source brief`
- `07_podcast/output_drills/YYYY-MM-DD_output_drill_<topic-slug>.md` — `產生 Output Drill Script`
- `07_podcast/chants/YYYY-MM-DD_chant_<pattern-slug>.md` — `產生 Chant`
- `08_ai/anki/writing/*.md` · `speaking/*.md` — 「幫我做 Anki 卡」
- `08_ai/anki/weekly/knowledge-review_YYYY-MM-DD.md` — `整理 anki` 或 `weekly review`
- `10_knowledge_base/vocabulary/<word-slug>.md` — Vocabulary Intake；只建立 Knowledge note
- `10_knowledge_base/error_corrections/YYYY-MM-DD_<slug>.md` — Error Correction Intake；只建立 review note
- `10_knowledge_base/ideas/<theme>/<idea>.md` — `萃取知識` 或 `存範本`（新 idea 才建檔，延伸用 Related Notes）
- `10_knowledge_base/coaches/<coach>/originals/*.md` — `存文章`
- `09_coach/sprints/sprint-00N.md` — `start next sprint`

### Archived（已封存，不再是 Active 工作流程的一部分）

- `10_knowledge_base/vocabulary/archive/*.md`、
  `10_knowledge_base/expressions/archive/*.md` 與
  `10_knowledge_base/sentence_patterns/archive/*.md`、
  `10_knowledge_base/error_corrections/archive/*.md` — 已有 Anki coverage 的 canonical
  Knowledge notes；不再重複產卡，但萃取知識與去重時仍會搜尋
- `09_coach/archive/old_daily/2026-06-29.md` · `2026-07-01.md` — 2026-07-04 從
  `09_coach/daily/` 移出封存。這是重新設計 Sprint 系統前的「每日 Sheet」工作流程，
  現在的 `start today` / `finish today` 直接讀 dashboard + sprint 檔案，不再需要
  逐日生成的 Sheet。`09_coach/daily/` 資料夾已不存在。
- `09_coach/archive/pre-connieverse-podcast/2026-06-30.md` 與
  `07_podcast/episodes/season_01/` — 舊 Podcast workflow 歷史材料，不是 Phase 1
  source brief workflow 的輸入或輸出。

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

**`根據這些資料產生 NotebookLM source brief` / `Generate NotebookLM source brief`**
- [ ] 使用者已提供至少一種實質來源，不是只有 topic 名稱
- [ ] 沒有自動選題；topic 來自使用者或由明確來源做中性標記
- [ ] Strict Source Mode 未加入外部事實、數據、研究或具名案例
- [ ] Research-Assisted Mode 已先產生含 publisher、用途與 reliability note 的完整 Source Log
- [ ] Question Type 已標示並用一句話說明判斷理由
- [ ] 至少三個 viewpoints 都能追溯到允許的來源
- [ ] 每個 viewpoint 都有 Source basis 與 Natural IELTS sentence
- [ ] Solutions 只有在適用時出現，且包含 what / why / limitation
- [ ] 已產生 Source Briefing Article 與 NotebookLM Generation Prompt
- [ ] NotebookLM prompt 明確禁止加入 source 以外的 factual claims
- [ ] 資料不足時回覆 `Source is insufficient.` 並要求補充，沒有建立檔案
- [ ] 沒有產生完整 Podcast、TTS、Teacher Mode、Shadowing 或 output drill
- [ ] 成功檔案已存到 `07_podcast/source_briefs/YYYY-MM-DD_notebooklm_source_brief_<topic-slug>.md`

**Stage 2 Output Drill**
- [ ] Topic、Core Pattern、Model Sentence、3–5 個 Vocabulary / Expressions 都由使用者提供
- [ ] Practice Topics 視需要由使用者提供；空白時留在主要 Topic，沒有自動另選題目
- [ ] 缺少 required input 時已停止，沒有自行補 Pattern、Sentence 或 Vocabulary
- [ ] Context 已依 user recap → explicit source brief → unique topic match → only/latest 的順序解析
- [ ] 多個候選檔案時已列出路徑請使用者選，沒有猜測
- [ ] 找不到 context 時已回覆 `Stage 2 context is missing.`
- [ ] Source brief 只用於銜接、切題檢查、教學說明與貼近主題的 examples
- [ ] 沒有重新生成 NotebookLM discussion、重新 research 或更新 Knowledge Base
- [ ] Pattern Teaching 先播放完整 Model Sentence，再用短而口語的英文解釋兩部分功能，沒有朗讀難懂的 bracket labels
- [ ] Script 依 Opening Transition → Pattern Teaching → Vocabulary Focus → Shadowing → Interactive Output → Final Turn 產生
- [ ] 開頭有輕快自然的 welcome，結尾感謝收聽並銜接下一首歌或 today's chant
- [ ] 沒有 `[TEACHER]` 或其他 speaker labels；pause marker 只使用 3 秒的倍數
- [ ] 已存到 `07_podcast/output_drills/YYYY-MM-DD_output_drill_<topic-slug>.md`
- [ ] 完成回報已標示 `Context used:`

**Stage 3 Chant**
- [ ] Target Sentence Pattern 由使用者提供，沒有從 Stage 1/2、Knowledge Base 或歷史對話自動挑選
- [ ] Lyrics 約 1–1.5 分鐘、短句、強重複、有 chorus，且只練一個 pattern
- [ ] 已提供 5–8 個 substitutions 與最多 4 個 IELTS topic links
- [ ] Suno prompt 以 `Use my saved voice profile.` 開頭
- [ ] 已依 Nursery-rhyme chant 或 Light bossa nova chant 產生單一 prompt
- [ ] 沒有模仿真實 artist、做 external research 或更新 Knowledge Base
- [ ] 已存到 `07_podcast/chants/YYYY-MM-DD_chant_<pattern-slug>.md`

**`更新筆記`**
- [ ] 已比對逐字稿與現有筆記，避免重複
- [ ] 已用「原句 → 正確句」格式記錄新錯誤
- [ ] 已只用「追加」方式更新筆記，沒有刪除或改寫既有內容
- [ ] 已條列這次新增了什麼給我確認

**`萃取知識`**
- [ ] 已用「半年後還能用嗎」的標準篩選內容
- [ ] 已先搜尋整個 Knowledge Base，優先更新或合併既有條目
- [ ] 只有真正全新的概念才建立新檔，且已歸入十一類之一
- [ ] Expression/Pattern 已放在正確資料夾，未自動生成 NotebookLM source brief
- [ ] 已檢查相關連結與 README／ARCHITECTURE／CLAUDE 一致性
- [ ] 已回報：更新或新增了什麼、存放位置、哪些內容沒有保存（原因）

**Vocabulary Intake**
- [ ] 單字由使用者選，沒有自動推薦或收集
- [ ] 已先搜尋 active Vocabulary、archive 與全部既有 Anki
- [ ] Front 是不含答案的英英解釋；Back 包含 word、IPA、詞性、frequency 與兩個標籤例句
- [ ] Frequency 有明確來源；沒有資料時標 `Not available`
- [ ] 已記錄 dictionary URL、access date 與 user-provided fields
- [ ] 只建立 active Knowledge note 和 Pending queue row，沒有直接建立 Anki

**Error Correction Intake**
- [ ] Front 完整保留使用者原句，沒有偷偷修正
- [ ] Back 依序包含英文 Corrected Version、繁體中文 Error Analysis 與 Key Reminder
- [ ] 一個原句只建立一張卡，沒有拆成 Vocabulary／Expression／Pattern
- [ ] 只建立 active review note 和 Pending queue row，沒有直接建立 Anki
- [ ] 沒有繞過 Error DB recurrence/confidence policy

**`存範本`（= `learn model essay`）**
- [ ] 已判斷題型並存到對應資料夾
- [ ] 已產生 Band 估計、結構分析、值得學的表達、連接詞/句型片語
- [ ] 已產生 Reusable Ideas / Mental Model 區塊，只收通過「半年後還能用」標準的論點
- [ ] 已依 `10_knowledge_base/ideas/<theme>/` 現有筆記去重，新建或延伸 atomic idea note
- [ ] 已更新 `models_index.md`、`sentence_patterns/`、`expressions/`（如適用）、對應 `skeleton_*.md`
- [ ] 已檢查同題是否已有範本，若有則提醒

**`weekly review`**
- [ ] 已讀 dashboard 確認本週目標
- [ ] 已比對本週實際完成 vs 排定任務
- [ ] 已檢查本週是否有新增/升級的 Active Weakness
- [ ] 已搜尋全部既有 Anki 卡，避免重複 target
- [ ] 已依 `organize_anki_workflow.md` 產卡，確認 Anki coverage 後才移動 source notes
- [ ] 已更新 queue 的 archive link、Anki status、Last Review 與 Practice Evidence
- [ ] 如有合格項目，已生成 `08_ai/anki/weekly/knowledge-review_YYYY-MM-DD.md`
- [ ] 若當天是 Retrospective 日，已引導填寫或明確說明還沒到日子
- [ ] 已輸出下週建議（基於證據，不是憑空建議）

**`整理 anki` / `整理 Anki`**
- [ ] 只掃描 Vocabulary / Expressions / Sentence Patterns / Error Corrections active root，排除 templates、README 與 archive
- [ ] 已搜尋整個 `08_ai/anki/`，相同 target 沒有重複建卡
- [ ] Front 是不洩漏答案的英文使用情境；Back 保留 exact target、source example 與必要資訊
- [ ] 只有成功寫入或驗證既有卡片的 source note 才移到同類別 `archive/`
- [ ] 不完整、失敗或 path conflict 的 note 保留在 active folder 並回報
- [ ] 已更新所有受影響連結與 Knowledge Review Queue
- [ ] Error Corrections 只有在直接 `整理 anki` 時處理；`weekly review` 沒有自動輸出

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

## Repo Structure（實際存在的資料夾，2026-07-06 ConnieVerse 移出知識庫後驗證）

```
ielts-notes/
├── 01_lessons/                  # 課堂筆記（原始證據）
├── 10_knowledge_base/           # 十一類 Knowledge / correction records
│   ├── vocabulary/            # 使用者選字的 active Anki inbox；archive/ 存已產卡 notes
│   ├── expressions/           # active Anki inbox；archive/ 存已產卡的 canonical notes
│   ├── sentence_patterns/     # active Anki inbox；archive/ 存已產卡的 canonical notes
│   ├── error_corrections/     # 錯誤原句 → 修正版與分析；archive/ 存已批准 cards
│   ├── grammar_notes/           # 2026-07-06 新增的父資料夾，文法參考卡（犯錯時查，不主動複習）
│   │   ├── grammar/             # G001-G011
│   │   ├── prepositions/        # P001-P004
│   │   └── word_form/           # W001-W003
│   ├── ideas/<theme>/           # Reusable Ideas SSOT（不變）
│   ├── coaches/(simon/matt/joe)
│   ├── consensus/
│   ├── listening/ · speaking/
│   ├── writing/                 # 現在只放 essay 結構：writing_patterns.md（含 §10 Task 1）· skeleton_*.md
│   ├── ARCHITECTURE.md
│   └── index.md
├── 02_writing/
│   ├── task1/ (drafts/feedback/models)
│   └── task2/ (drafts/feedback/models)
├── 03_speaking/ (practice/chat, practice/situation)
├── 04_listening/ · 05_reading/  # review_queue.md 目前是空模板
├── 06_error_database/
├── 07_podcast/                  # Gated Stage 1 source briefs + Stage 2 drills + Stage 3 chants
│   ├── templates/ (gated router · Stage 1 · Stage 2 · Stage 3 workflows)
│   ├── source_briefs/           # YYYY-MM-DD_notebooklm_source_brief_<topic-slug>.md
│   ├── output_drills/           # YYYY-MM-DD_output_drill_<topic-slug>.md
│   ├── chants/                  # YYYY-MM-DD_chant_<pattern-slug>.md
│   ├── episodes/season_01/      # legacy；不再讀寫
│   ├── world/ · characters/ · songs/ · commute_plan.md  # legacy
│   └── README.md
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

目前 repo 中沒有 `00_dashboard/`、`10_knowledge_base/memory_triggers.md` 或
`10_knowledge_base/practice_method.md`。現行狀態入口是 `09_coach/dashboard.md`；
舊的 progress / weekly review / study plan 只存在 `09_coach/archive/old_dashboard/`。

---

## Change History（目前狀態優先；下方舊 Podcast 決策已 superseded）

1. **2026-07-05 gated workflow**：正式加入 `生成 Podcast` / `產生 Podcast` /
   `generate podcast` router。Stage 1 產生 source brief；Stage 2 經 input/context gate
   後產生 ElevenLabs-ready Output Drill；Stage 3 用使用者指定 pattern 產生 chant 與
   Suno prompt。Pattern、Model Sentence、Vocabulary 仍完全由使用者提供。舊
   `episodes/`、`characters/`、`world/`、`songs/` 保留為 legacy。
2. **README.md 全面改寫**成 Operator Manual 格式：Quick Start 表 + Daily/Weekly
   Workflow + Knowledge Intake + File Policy + Sprint Rules + Definition of Done +
   Safety Rules。
3. **Existing**：`start today` · `finish today` · `生成 Podcast` / `產生 Podcast` ·
   `根據這些資料產生 NotebookLM source brief` · `產生 Output Drill Script` ·
   `產生 Chant` ·
   `更新筆記` · `萃取知識` · `整理 anki` · `存範本`(=`learn model essay`) · `批改` · `建草稿` ·
   **`weekly review`**（新增）· **`start next sprint`**（新增）。
4. **歷史決策（Podcast 項目僅供追蹤，已被 Phase 1 reset 取代）**：
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
   - **Podcast 選材改回全自動（2026-07-05）**：Podcast 掃描
     `sentence_patterns/` 和 `expressions/` 的合規條目，選自然、可口說而且近兩週
     未使用的素材。現在 Topic 優先取自近期練習／弱點，並建立可討論的核心兩難。
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
   - **分類規則定案 + 單字併入 expressions/（2026-07-06）**：確立「三問分類法」
     （能塞進很多句子不用改→Expressions；有空格可替換→Sentence Patterns；是觀點→
     Ideas；文法規則另計，參考用不主動複習）。單字本身通過第一問測試，不需要獨立的
     `vocabulary/` 資料夾——`V001`/`V002` 已併入 `writing/expressions.md` § Vocabulary
     並刪除，`vocabulary/` 資料夾不再存在。另外新增 `writing/memory_triggers.md`：
     情境式記憶卡（畫面/情境/任務/句型/輸出句，照 `practice_method.md` 的方法），
     跟 `sentence_patterns/`/`expressions/` 的抽象句型分開存，互相連結不重複。
   - **四分類定案 + 實際資料夾搬遷（2026-07-06）**：正式定案知識庫四分類
     ——`expressions/`、`sentence_patterns/`、`grammar_notes/`、`ideas/`
     ——並把資料夾結構搬成跟分類一致：`expressions/`、`sentence_patterns/`、
     `memory_triggers.md` 從 `writing/` 底下搬到 `10_knowledge_base/` 直接子項
     （`writing/` 現在只剩 essay 結構：`writing_patterns.md` + `skeleton_*.md`）；
     `grammar/`、`prepositions/`、`word_form/` 三個卡片資料夾統一收進新的父資料夾
     `grammar_notes/`。這一輪也把 `07_podcast/episodes/*.md` 短暫搬進
     `10_knowledge_base/stories/`（當時的判斷：反正都是知識庫的一部分，不如收進
     同一個根目錄）。
   - **Vocabulary intake 重新加入（2026-07-05，本次，supersedes 單字併入
     Expressions）**：新增 `vocabulary/` active inbox 與 archive，只收使用者明確選擇的
     single headword。Intake 優先查 Vocabulary.com，先建立 source-backed Knowledge
     note，不直接產 Anki；`整理 anki` 再與 Expressions / Sentence Patterns 一起處理。
   - **Error Correction review inbox（2026-07-05）**：新增 `error_corrections/`，一張卡
     保存完整錯誤原句、修正版與 AI 分析，不拆成額外語言知識。Intake 不直接進 Anki；
     使用者看過後直接說 `整理 anki` 才輸出並封存。
   - **ConnieVerse 移出知識庫，回到 07_podcast/（2026-07-06，本次，推翻上一步）**：
     發現把 Podcast 劇本放進知識庫資料夾，反而讓「素材庫 vs 練習場」這條界線變模糊，
     不是變清楚。`07_podcast/` 重新設計成完整的獨立系統：
     `templates/`（`connieverse_template.md` 放 Episode 格式規則、`daily_template.md`
     放使用流程+自動選材邏輯+Episode Archive）、`episodes/season_01/`（現為
     NotebookLM source/prompt + ElevenLabs Speaking Practice，epNN 命名，不用日期）、
     `world/connieverse.md`（主持人背景）、`characters/`（新增
     `connie.md`、`emily.md`、`walter.md`、`friends_style_characters.md` 四個角色檔）。
     新增 `07_podcast/README.md` 說明整個系統，並解釋為什麼 ConnieVerse 不算
     knowledge base 本體（`10_knowledge_base/ARCHITECTURE.md` §11 也同步改版到
     v2.6）。舊版 Rachel/Connie 格式僅存的一集不是目前的 ConnieVerse Episode Package，
     封存到 `09_coach/archive/pre-connieverse-podcast/`，沒有放進
     `episodes/season_01/`。`10_knowledge_base/stories/` 資料夾已不存在。
5. **仍是 Proposed**（未決策，維持現狀）：獨立的「練完 Listening」指令——目前仍靠
   `finish today` 或 Sunday Mock 回報帶過。
