# ConnieVerse Podcast Template — 劇情型 IELTS Podcast

> **2026-07-04：完全取代**原本的 Rachel/Connie 教學對話型 Podcast（見 git 歷史）。
> **2026-07-05：改回全自動選材**——Claude 從 Knowledge Base（`sentence_patterns.md`
> 的 Podcast Candidates、`expressions.md` 的 Podcast Candidate 條目、
> `writing_patterns.md` §9 主題輪替）自動決定本集 5 個輸入，你不用每次手動填。
> 說「幫我準備明天的 Podcast」，Claude 生成整集腳本，存成
> `07_podcast/episodes/YYYY-MM-DD.md`。

---

## 核心設定

主角是平行宇宙的 Connie。她住在法國巴黎，在一間 AI / tech startup 擔任 Product
Manager，同時也是 fashion influencer，會參加 fashion party、startup event、café
gathering，也會和朋友討論生活、工作、時事、育兒、科技、職場與社會議題。

這不是一般英文教學 Podcast，而是透過故事、角色、情境劇和台詞，自然記住英文句型、
文法和字彙。

## 世界觀風格

參考氛圍：
- **Emily in Paris** — 巴黎、時尚、職場、社交場合
- **Friends** — 朋友之間的生活對話與幽默
- **Breaking Bad** — 邏輯推理、犀利分析、人生壓力
- **2 Broke Girls** — 吐槽、現實感、快節奏對話

可以有類似這些作品「風格」的角色，但不要直接複製原劇台詞。

## 每集學習限制

每一集只學：
- 1 個 target pattern / grammar structure
- 2–3 個 target vocabulary 或 collocations
- 1 句 key line
- 1 個 IELTS transfer sentence

不要塞太多內容。

## 語氣要求

- 像一集有劇情的 Podcast，不要像補習班講義
- 可以幽默，但不要廢話太多
- 故事要服務記憶，不是記憶服務故事
- 解說要短
- 重點是代入角色，最後能自然使用英文

---

## 使用流程

1. 說「幫我準備明天的 Podcast」——**不用附任何輸入**，Claude 自動決定本集 5 個欄位
2. Claude 生成完整腳本，存成 `07_podcast/episodes/YYYY-MM-DD.md`
3. 複製全文 → NotebookLM（或其他 TTS 工具）新 notebook → 貼入 **source**
4. 進 Studio > Podcast → 把「Podcast 生成指示」貼入 **prompt** 欄位
5. 按生成 → 下載音檔 → 存到手機，明天開車聽

如果你這次想指定某個輸入（例如想練特定句型），可以直接說，其餘欄位照下表自動選。

## 本集 5 個輸入怎麼選（2026-07-05 起全自動，Claude 執行，供參考）

| 輸入 | 來源 | 選法 |
|---|---|---|
| Target Pattern | `10_knowledge_base/writing/sentence_patterns.md` 底部「🎙️ Podcast Candidates」表格 | 挑一個 `Yes`，避免跟 Episode Archive 過去 2 週重複 |
| Target Vocabulary（2–3 個） | `10_knowledge_base/writing/expressions.md` | 挑 Podcast Candidate = `Yes` 的條目，避免跟過去 2 週重複 |
| IELTS Topic | `10_knowledge_base/writing/writing_patterns.md` §9（16 個常見 Task 2 主題） | 輪流選，不跟昨天重複 |
| Episode Setting | Claude 創作 | 貼合 ConnieVerse 世界觀，避免跟最近幾集場景重複 |
| Main Conflict | Claude 創作 | 貼合本集 Target Pattern/Vocabulary/Topic |

---

## Episode 格式（Claude 生成時使用）

```markdown
# ConnieVerse — [Episode Title]
# [DATE] [WEEKDAY]
# Target Pattern: [pattern] · Vocabulary: [2-3 items] · Topic: [IELTS topic]

---

## 使用說明

1. 複製本檔全文 → NotebookLM（或其他 TTS 工具）新 notebook → 貼入 source
2. 進 Studio > Podcast → 把下方「Podcast 生成指示」貼入 prompt 欄位
3. 按生成 → 下載音檔存到手機

---

## Podcast 生成指示（貼入 NotebookLM）

請根據以下故事腳本，製作一段有劇情的雙人/多人對話 Podcast，風格參考 Emily in
Paris / Friends 的生活劇氛圍——不是教學對話，是有場景、有衝突、有角色個性的短劇。
語氣自然、可以有笑聲和真實反應。旁白/角色對話用英文，如果腳本裡有繁體中文解說段落，
維持中文朗讀。

---

## Target Learning

- Target Pattern: [pattern]
- Target Vocabulary: [2-3 items]
- IELTS Function: [這個句型可以表達什麼觀點功能，例如 cause / contrast / solution / risk / opinion / concession]

---

## Opening Story

[30–60 秒英文故事開場，有畫面感、有角色、有衝突或小事件，不解釋英文]

---

## Mini Drama

[2–3 分鐘英文情境劇，角色自然對話，讓 target pattern 和 vocabulary 自然出現]

---

## First Listen

先完整聽一次，不需要背，只要理解故事。

---

## Explanation（繁體中文）

[簡短解說本集句型、文法、單字、片語，每個包含：意思 / 使用情境 / IELTS 怎麼用 / 1 個自然例句]

---

## Shadowing x3

Key line: [挑出的句子]

1. 慢速
2. 正常速度
3. 角色語氣版

---

## Role Play Gap

[重播 Mini Drama 其中一小段，挖空 Connie 的台詞，格式：]

```
Character A: ...
Connie: [PAUSE — you say the line]
Character A: ...
```

---

## Situation Swap

[換 2 個 IELTS 常見主題情境，不直接給完整答案，先讓我自己說，每個情境後才提供 sample answer]

---

## IELTS Transfer

[一題 IELTS Writing Task 2 或 Speaking Part 3 題目，示範如何把今天故事中的 key line 轉成正式但自然的 IELTS 答案]

---

## Chant Song

[30–45 秒 chant/rhythm song，簡單、重複、有節奏，目的是記住 key pattern，不要太幼稚]

---

## Related Ideas

[選填：若本集 IELTS Topic 在 `10_knowledge_base/ideas/<theme>/` 已有對應 idea note，列出連結；只放連結，不複製內容；沒有對應的就留白]
```

---

## Episode Archive

| Date | Target Pattern | Vocabulary | Topic | Setting |
|---|---|---|---|---|
