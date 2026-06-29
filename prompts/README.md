# Prompts

## 參考

- [Spec-Driven Development with Coding Agents](https://github.com/https-deeplearning-ai/sc-spec-driven-development-files)
- [Claude Code Tips: From Basics to Advanced](https://github.com/ykdojo/claude-code-tips)

## 學習

```
double check everything, every single claim in what you produced and at the end make a table of what you were able to verify
```

```
dig into this issue, try to find the root cause.
```

```
Slimming RootError to "client-relevant" variants
將 RootError 縮減至「與用戶端相關」的變體
```

```
Unified output struct
統一的輸出結構體
```

```
Skip unless you've adopted Cow patterns elsewhere.
除非你在其他地方也已經採用了 Cow（Copy-on-Write，寫時複製）模式，否則請直接跳過此項。
```

```
do the minimal compile-clean fix
最小化修改且保證編譯成功
```

### 一、你常用中文下的句子 → 英文句型

**「幫我安排計畫，問我問題直到你了解所有細節」**
→ `Help me plan this. Ask me questions until you have everything you need.`
→ 或更精確：`Before writing any code, interview me to clarify requirements. Ask one question at a time.`

**「幫我決定 [某事]」**
→ `Decide [X] for me and explain your reasoning.`
→ 例：`Decide the skill name for me and explain why.`

**「用 AskUserTool 問我問題」**（這句你在 Android SMS app 那個 prompt 用中文下）
→ `Use interactive questions to gather my preferences before proceeding.`

**「可以從一個全新的練習專案開始練習」**
→ `Feel free to use a fresh practice project if that helps.`

---

### 二、你表達不清楚的句子 → 改寫

**你寫過：** 「請根據 Claude code best practices 實現規格書」
這句混了中英文，Claude Code 讀起來也有歧義（「實現」是 implement？generate？enforce？）

→ `Implement the spec in SPEC.md following Claude Code best practices.`
→ 或更具體：`Read the spec, produce a gap analysis, then implement phase by phase.`

**你寫過（意圖是這樣的）：** 「讓 Claude Code 先做 gap analysis，再產生 implementation plan」
這個你當時用中文說，如果要下成 Claude Code prompt：

→ `First, run a gap analysis comparing the existing code against the spec. Then generate a phased implementation plan. Do not write any code yet.`

注意 "Do not write any code yet" 這句很重要——不加的話 Claude Code 會直接開始動手。

---

### 三、語法錯誤模式

根據你寫的英文句子，你有幾個一致的傾向：

**傾向一：漏掉 "the" 或 "a"**
- ❌ `Use Bruno collection as source of truth`
- ✅ `Use the Bruno collection as the source of truth`

**傾向二：動詞後面的介係詞選錯**
- ❌ `compare the code with spec` （這樣說也對，但技術文件裡通常用 against）
- ✅ `compare the code against the spec`

**傾向三：條件句語序**
- ❌ `If spec need to change, it is a separate commit`
- ✅ `If the spec needs to change, make it a separate commit.`

---

### 四、你說過但可以更好的句子

**你在 CLAUDE.md prompt 裡寫的：**
> "explore files first, propose a migration plan, await approval, then execute file-by-file"

這句很好，但在 Claude Code 裡可以更明確地用「停頓點」語言：

→ `Explore the codebase, then propose a migration plan and stop. Wait for my approval before making any changes.`

加 "and stop" 讓暫停點更清楚。

---

### 五種你最常用的句型模板（整理）

```
1. 任務起點
   "Read [file], then [action]. Do not [unwanted action] yet."

2. 分階段執行
   "Phase 1: [X]. Phase 2: [Y]. Complete each phase before moving to the next."

3. 設定停頓點
   "After [action], stop and show me the plan. Wait for my approval."

4. 設定邊界
   "Out of scope: [list]. Do not implement these."

5. 驗收標準
   "Acceptance criteria: [list]. The task is complete only when all items pass."
```