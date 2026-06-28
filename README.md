# IELTS Coach — 使用手冊

---

## 每天要做什麼

### 🚗 早上開車（1.5h）

1. 播放昨晚準備的 Podcast 音檔（前 45 min）
2. 後 45 min 出聲練口說（見下方週節奏）
3. 不需要做任何筆記，到公司後不需要繼續

### 📖 晚上學習（90 min）

1. 打開今天的 Daily Sheet：`09_coach/daily/YYYY-MM-DD.md`
2. 照著 Daily Sheet 做完當天任務
3. 做完後把結果貼給我（格式見下方「做完後告訴我什麼」）

### 🎙️ 睡前準備（10 min）

對我說：**「幫我準備明天的 Podcast」**

我會：
- 填入明天的 Podcast 腳本（`08_ai/podcast/YYYY-MM-DD.md`）
- 建立明天的 Daily Sheet（`09_coach/daily/YYYY-MM-DD.md`）

你只需要：
- 用錄音 App 或 TTS 把 Podcast 轉成音檔
- 放到手機備用

---

## 每週節奏

| 天 | 開車後半段 | 晚上任務 |
|---|---|---|
| **週一** | Part 2 出聲 | Writing：問題類型辨識 + Skeleton |
| **週二** | Part 3 出聲 | Listening：Cambridge S4 + transcript analysis |
| **週三** | Shadowing | Writing：Body paragraph 或完整限時作文 |
| **週四** | Part 2 暖身（Joe 課前） | **Joe 口說課** + 課後記 1–2 個糾正 |
| **週五** | 輕鬆回顧 | **Matt 寫作課** 或 essay review + 準備問題 |
| **週六** | 自由 | Buffer（補課或 Sprint 回顧） |
| **週日** | 不需要開車練習 | **Full Mock**（L + R + W + S 自錄）+ error analysis |

---

## 做完後告訴我什麼

### 每次晚上練習結束後

**Writing 練習：**
```
貼上你寫的 Skeleton 或段落
＋ 哪題類型你不確定
＋ 有沒有出現過去錯過的 error（G001 / G010 / G011...）
```

**Listening 練習：**
```
S4 得幾分（X/10）
每道錯題的錯誤類型（qualifier trap / self-correction missed / concentration drop...）
```

**Joe 課後：**
```
貼上逐字稿或課堂筆記 → 我說「更新筆記」
```

**Matt 課後：**
```
貼上逐字稿或課堂筆記 → 我說「更新筆記」
```

### Sunday Full Mock 結束後

```
Listening: S1=X S2=X S3=X S4=X
S4 錯誤類型：[列出]
Writing Task 1：大概幾分
Writing Task 2：大概幾分，TR/CC/LR/GRA 感覺
Writing 出現的 error：[列出]
這次第二次出現的 error：[列出]
Speaking 自己觀察：[可選]
```

我會自動更新所有 DB 和 Dashboard。

---

## 常用指令

| 你說什麼 | 我做什麼 |
|---|---|
| `start today` | 輸出今天任務的簡潔格式 |
| `finish today` + 結果 | 更新所有 DB，必要時重新生成 Dashboard |
| `幫我準備明天的 Podcast` | 建 Podcast 腳本 + Daily Sheet |
| `批改 [草稿路徑]` | 評分 + 存 feedback + 更新 DB |
| `更新筆記` + 逐字稿 | 拆解到各筆記檔 + 更新 DB |
| `建草稿` + 題目 + 我的文章 | 存草稿到對應資料夾 |

---

## 重要文件在哪裡

| 文件 | 路徑 |
|---|---|
| 今天該做什麼 | `09_coach/daily/YYYY-MM-DD.md` |
| 目前 Sprint | `09_coach/sprints/sprint-001.md` |
| 整體狀態一覽 | `09_coach/dashboard.md` |
| 每日 Podcast 腳本 | `08_ai/podcast/YYYY-MM-DD.md` |
| Podcast 模板 | `08_ai/podcast/daily_template.md` |
| Writing 草稿 | `02_writing/task1/drafts/` · `02_writing/task2/drafts/` |
| Writing 批改回饋 | `02_writing/task1/feedback/` · `02_writing/task2/feedback/` |
| 文法錯誤 DB | `09_coach/errors/grammar_db.md` |
| 介系詞錯誤 DB | `09_coach/errors/preposition_db.md` |
| 聽力成績 DB | `09_coach/performance/listening_db.md` |
| 寫作成績 DB | `09_coach/performance/writing_db.md` |
| 錯誤總清單 | `06_error_database/error_log.md` |

---

## 我（Claude）會自動更新什麼

| 觸發事件 | 自動更新的檔案 |
|---|---|
| 你完成晚上 Writing 練習並回報 | `errors/grammar_db.md` · `connie_profile.md` Evidence Log |
| 你完成晚上 Listening 練習並回報 | `performance/listening_db.md` · `connie_profile.md` |
| Sunday Full Mock 完成並回報 | `listening_db.md` · `writing_db.md` · `connie_profile.md` · `dashboard.md` |
| 你說「更新筆記」+ 逐字稿 | `error_log.md` · `teacher.md` · `speaking_notes.md` / `writing_notes.md` · 各 error DB |
| 你說「批改」+ 路徑 | `writing_db.md` · `connie_profile.md` · Feedback 檔案 |
| Sprint 結束 / Retrospective 填完 | `sprints/INDEX.md` · `dashboard.md` |

---

## 你不需要做的事

- 不需要自己決定哪個 DB 要更新（我來判斷）
- 不需要自己開 sprint 文件（`start today` 就夠了）
- 不需要每次背所有錯誤（DB 會記著）
- 不需要追蹤自己進步了多少（Sunday mock + Dashboard 會追蹤）

---

---

## 資料夾結構

```
ielts-notes/
├── 01_lessons/                 # 課堂筆記
│   ├── speaking/               # Joe 的口說課
│   ├── writing/                # Matt 的寫作課
│   └── teacher.md              # 兩位老師的核心原則
├── 02_writing/                 # 寫作練習
│   ├── task1/ (drafts / feedback / models)
│   └── task2/ (drafts / feedback / models)
├── 03_speaking/                # 口說練習記錄
│   └── self-practice/          # Sunday mock 自錄音檔
├── 04_listening/               # 聽力練習記錄
├── 05_reading/                 # 閱讀練習記錄
├── 06_error_database/          # 原始錯誤清單（人類可讀）
├── 08_ai/                      # AI 設定層
│   ├── prompts/                # Coach prompt
│   ├── podcast/                # 每日 Podcast 腳本
│   │   ├── daily_template.md   # 填充模板
│   │   └── YYYY-MM-DD.md       # 每日腳本
│   ├── anki/                   # Anki 卡片
│   └── teachers/               # Matt / Joe persona
├── 09_coach/                   # AI Coach 核心系統
│   ├── dashboard.md            # 整體狀態（每次工作先讀這個）
│   ├── connie_profile.md       # 學習者完整背景
│   ├── daily/                  # 每日任務清單
│   │   └── YYYY-MM-DD.md
│   ├── sprints/                # Sprint 計畫
│   │   ├── INDEX.md
│   │   ├── sprint-001.md
│   │   └── TEMPLATE.md
│   ├── performance/            # 成績資料庫
│   │   ├── listening_db.md
│   │   ├── reading_db.md
│   │   ├── writing_db.md
│   │   └── speaking_db.md
│   └── errors/                 # 錯誤資料庫
│       ├── grammar_db.md
│       ├── preposition_db.md
│       └── word_form_db.md
└── knowledge/                  # 教練知識庫
    ├── coaches/ (simon / matt / joe)
    └── consensus/ (writing / speaking)
```

---

## AI 設定文件

| 文件 | 用途 |
|---|---|
| [CLAUDE.md](CLAUDE.md) | Claude Code 的行為規則（不需要修改） |
| [08_ai/prompts/coach_prompt.md](08_ai/prompts/coach_prompt.md) | Coach 的指導原則 |
