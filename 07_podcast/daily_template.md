# IELTS Podcast Template — NotebookLM Edition

> 這個 template 由 Claude 自動填入，不需要手動填寫。
> 說「幫我準備明天的 Podcast」→ Claude 自動選卡 + 生成 → 存為 `07_podcast/episodes/YYYY-MM-DD.md`

---

## 使用流程

1. Claude 生成明天的 Podcast 檔案
2. 打開 `07_podcast/episodes/YYYY-MM-DD.md`
3. 複製全文 → 貼入 NotebookLM 新 notebook 的 **source**
4. 進 Studio > Podcast → 把「Podcast 生成指示」區塊貼入 **prompt** 欄位
5. 按生成（約 5–10 分鐘）→ 下載雙人對話音檔
6. 音檔存到手機 → 明天開車聽

---

## Episode 格式（Claude 生成時使用）

```markdown
# IELTS Podcast — [DATE] [WEEKDAY]
# 焦點：[Grammar ID] · [Expression ID] · [Listening ID]
# 預估時長：34 min

---

## 使用說明

1. 複製本檔全文 → NotebookLM 新 notebook → 貼入 source
2. 進 Studio > Podcast → 把下方「Podcast 生成指示」貼入 prompt 欄位
3. 按生成（約 5–10 分鐘）

---

## Podcast 生成指示（貼入 NotebookLM）

請根據以下 IELTS 學習材料，製作一段大約 34 分鐘的雙人對話 Podcast。

角色設定：
- Rachel（IELTS 教練）：負責解說、提問、舉例、引導練習
- Connie（IELTS 考生）：程度約 Band 6–7，正在備考 General Training，有具體的錯誤模式

對話結構（請按順序進行）：
1. [2 min] 開場：Rachel 預告今天三個重點，說明為何重要
2. [5 min] 文法焦點：解說 Grammar card 的規則，給錯誤例子，讓 Connie 嘗試改正
3. [5 min] 表達式練習：帶 Connie 在句子裡用 Expression card 的片語，要求 Connie 造句
4. [10 min] Speaking 練習：Rachel 出今日主題，Connie 作答，Rachel 點評並示範一段好的回答
5. [7 min] 聽力技巧：解說 Listening card，用模擬的 Cambridge 風格例子說明陷阱
6. [5 min] Shadowing：Rachel 唸句子，Connie 重複，Rachel 糾正語調節奏

語氣：輕鬆自然，像真實一對一家教課，可以有笑聲和真實反應。
語言：解說和點評用繁體中文，英文練習和例子保留英文，shadowing 句子只用英文。

---

## 今日知識小卡

[由 Claude 貼入 3 張 card 全文]

---

## Speaking 練習主題

**類型：** [Part 2 或 Part 3]
**題目：** [一道具體題目]
**回答要點：**
- [要點 1]
- [要點 2]
- [要點 3]
**Sample Answer：**
[示範回答]

---

## Shadowing 句子

[8 句，每句 8–12 字]
```

---

## 選卡邏輯（Claude 執行，供參考）

| 類型 | 來源 | 選法 |
|---|---|---|
| Grammar | `02_knowledge_base/grammar/` 或 `prepositions/` 或 `word_form/` | 對應當前最高頻 Active error |
| Expression | `02_knowledge_base/expressions/` 或 `collocations/` | 輪流 E001 → E002 → E003 → E004 → C001 |
| Listening | `02_knowledge_base/listening/` | 輪流 L001 → L002 → L003 → L004 → L005 |

Speaking 主題依星期：
- 週一 / 週四 → Part 2（地方 / 人物 / 事件）
- 週二 / 週三 / 週五 → Part 3（社會觀點）

---

## Episode Archive

| Date | Grammar | Expression | Listening | Speaking |
|---|---|---|---|---|
| 2026-06-30 | G010 double conjunction | E004 Part 3 openers | L003 reversal signals | Part 3: individuals vs govt |
| 2026-07-01 | G001 past time markers | E001 concession | L003 reversal signals | Part 3: public transport |
