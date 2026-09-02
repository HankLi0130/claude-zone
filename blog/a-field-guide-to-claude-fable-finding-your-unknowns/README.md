---
Source: https://claude.com/blog/a-field-guide-to-claude-fable-finding-your-unknowns
---

# Claude Fable 5 實戰指南：找出你的未知（Finding your unknowns）

**類別**：Claude Code

**產品**：Claude Code

**日期**：2026 年 7 月 6 日

**閱讀時間**：8 分鐘

使用 Claude Code 時，我經常想起「地圖」與「疆域」之間的差異。

地圖是待完成工作的表徵，包含我的 Prompt、Skill 和 Context，也就是我提供給 Claude 的內容。疆域則是工作實際發生的場域，也就是 Codebase、現實世界以及其真實存在的限制條件。

地圖與疆域之間的差異，就是我所謂的「未知」（unknowns）。當 Claude 遇到未知時，它必須根據自己對我需求的最佳猜測來做出決定。要執行的工作越多，Claude 可能遇到的未知也就越多。

Claude Fable 是第一個讓我發現工作品質的瓶頸在於我自己釐清其未知之能力的情境模型。

重要的是，光是提前規劃並不總是足夠。你可能會在深入實作時才發現未知，或者你的未知可能會引導你發現，你其實應該改用完全不同的方式來解決問題。

我發現與 Fable 合作是一個在實作前、實作中以及實作後不斷發現自身未知的反覆迭代過程。

---

## 了解你的未知（Knowing your unknowns）

什麼是你的未知？當我帶著問題來找 Claude 時，我通常會將其分解為 4 個面向：

* **Known Knowns（已知的已知）**：這本質上就是我 Prompt 裡的內容。我告訴了 Agent 我想要什麼？
* **Known Unknowns（已知的未知）**：我還沒弄清楚什麼，但我意識到自己還沒弄清楚？
* **Unknown Knowns（未知的已知）**：什麼是顯而易見到我永遠不會寫下來，但只要看到就會認得出來的事物？
* **Unknown Unknowns（未知的未知）**：什麼是我完全沒考慮到的？我不曉得哪些知識？我知道某件事物可以達到多好的境界嗎？

最優秀的 Agentic Coder 擁有的未知相對較少。看著像 Boris 或 Jarred 這樣的人下 Prompt，對我來說很明顯的是，他們非常清楚且詳細地知道自己想要什麼。他們與 Codebase 以及模型的行為模式都高度同步。

但他們也會假設未知的存在。在許多方面，減少並針對未知進行規劃，正是 Agentic Coding 的核心技能。但幸運的是，這是一項你可以透過與 Claude 合作來提升的技能。

## 幫助 Claude 幫助你（Help Claude help you）

指導 Claude 是一種微妙的平衡。如果你說得太具體，Claude 即使在轉向更為合適時也會照著你的指示執行。如果你說得太模糊，Claude 通常會根據業界的最佳實踐來做出選擇和假設，而這些可能並不適合你的任務。

當你沒有將未知考慮在內時，無論哪種方式都會失敗。你不知道何時道路會充滿阻礙，也不知道何時道路雖然暢通無阻，但你仍希望 Claude 轉向。

Claude 可以幫助你更快發現你的未知。它可以極其快速地搜尋你的 Codebase 和網際網路，而且它對一般主題的了解遠遠超過你。它也能更快地從失敗中迭代。

這個過程中最關鍵的部分是給予 Claude 關於你起點的 Context。例如，告訴它你目前處於思考過程的哪個階段；揭露你對該問題和 Codebase 的經驗；並讓它像思考夥伴一樣與你合作。

在本文中，我詳細介紹了我用來揭露這些未知的一些模式，包括：

**實作前（Pre-implementation）：**

* Blind spot pass（盲點檢視）
* Brainstorms and prototype（腦力激盪與原型製作）
* Interviews（訪談）
* References（參考範例）
* Implementation plan（實作計畫）

**實作中（During implementation）：**

* Implementation notes（實作筆記）

**實作後（Post implementation）：**

* Pitches and explainers（提案簡報與解說說明）
* Quizzes（測驗）

---

## 實作前（Pre-implementation）

### 盲點檢視（Blind Spot Pass）

在開始工作時，你能做的最有用的事情之一就是了解自己的盲點。例如，如果你正在 Codebase 的全新部分編寫功能，或者使用 Claude 協助你進行不熟悉的工作（例如迭代一項設計），你很可能會有大量的 Unknown Unknowns。

你可能不知道該問什麼問題、優秀的成果看起來是什麼樣子、過去做過哪些歷史工作，或者該避開哪些坑洞。

在這些情況下，你可以請 Claude 幫你找出你的 Unknown Unknowns 並解釋給你聽。我喜歡直接使用「blind spot pass」和「unknown unknowns」這些字眼。向它提供關於你是誰以及你了解什麼的 Context，通常對於 Claude 理解與你開始協作的最佳方式至關重要。

**範例 Prompt：**

> 「我正在加入一個新的 Auth Provider，但我對這個 Codebase 中的 Auth 模組一無所知。你能做一次 blind spot pass，幫我找出相關的 unknown unknowns，並協助我更好地向你下 Prompt 嗎？」

> 「我不知道什麼是 Color Grading，但我需要替這支影片調色。你能教我理解關於 Color Grading 的 unknown unknowns，好讓我能給出更好的 Prompt 嗎？」

### 腦力激盪與原型製作（Brainstorms and prototypes）

當我在一個存在大量 Unknown Knowns 的領域工作時——涉及那些我只有親眼看到才知道如何定義的標準——我喜歡請 Claude 與我一起進行腦力激盪和原型製作。

在原型製作階段及早識別並說出 Unknown Knowns 是非常有價值的，因為在實作期間才發現它們的代價（相對而言）可能非常高昂。Feature 或 Spec 的微小變更可能會導致程式碼中完全不同的實作方式，而且你的 Agent 也更難以復原先前的變更。

例如，你可能只是想看看在 Frame 中新增一個按鈕的外觀如何，而不需要串接後端 Route 或在前端維護額外的 State。

另一個例子是視覺設計，對我來說，這很難用言語表達，但當我看到它時，我就知道這是不是我想要的。在這些情況下，我會要求為一個產出物提供數種不同的設計切入方向。

我幾乎每次 Coding Session 也都會從探索或腦力激盪階段開始。這有助於我帶著定義專案範圍的意圖開始。Claude 經常會發現我遺漏的高價值方法，有時也會見樹不見林。腦力激盪能防止我將範圍設定得過窄或過寬。

**範例 Prompt：**

> 「我想為這組數據製作一個 Dashboard，但我沒有視覺品味，也不知道有哪些可能。請為我製作一個包含 4 種截然不同設計方向的 HTML 頁面，以便我能對它們做出反應並評估。」

> 「在串接任何東西之前，先製作一個包含假資料的單一 HTML 檔案來 Mock 新的編輯器工具列。我想在你改動真正的應用程式之前，先感受並評估這個 Layout。」

> 「這是我的粗略問題：使用者在 Onboarding 之後就流失了。請搜尋 Codebase 並腦力激盪 10 個我們可以介入的地方，從成本最低到最雄心勃勃的方案。我會告訴你哪些引起我的共鳴。」

### 訪談（Interviews）

當我完成了充分的腦力激盪後，我可能仍有未知。

在這種情況下，我會請 Claude 針對任何未知或模糊之處對我進行訪談。請 Claude 訪談你時，請試著為它提供關於問題的 Context，以引導它的提問方向。

**範例 Prompt：**

> 「針對任何模糊不清之處，一次問我一個問題進行訪談；如果我的回答會改變架構，請優先提出該問題。」

### 參考範例（References）

有時候你無法詳細描述你想要什麼。例如，你可能缺乏相應的術語，或者它太過複雜，需要耗費你相當多的時間。

在這種情況下，最佳做法就是提供 Reference。雖然你可以加入架構圖、文件或圖片，但絕對最好的參考範例是原始碼（source code）。

如果你有一個以特定方式實作某項功能的 Library，或者一個你非常喜歡的設計元件，只需將 Fable 指向該資料夾並告訴它要尋找什麼，即使它是使用不同的程式語言寫成的。與螢幕截圖等相比，這能為 Claude 提供圍繞 Markup 和結構的更豐富細節。

**範例 Prompt：**

> 「vendor/rate-limiter 中的這個 Rust crate 實作了我完全想要的 Backoff 行為。請閱讀它，並在我們的 TypeScript API Client 中重新實作相同的語意。」

### 實作計畫（Implementation Plans）

當我認為自己準備好實作時，我往往會請 Claude 擬定一份實作計畫供我審閱。該計畫會著重在最有可能變更的部分，例如 Data Model、Type Interface 或 UX Flow。這讓 Claude 能夠將我實際上可能需要修改的項目凸顯出來。

**範例 Prompt：**

> 「用 HTML 撰寫一份實作計畫，但請以我最有可能進行微調的決策為開頭：Data Model 變更、新的 Type Interface 以及任何面向使用者的部分。將機械式的 Refactoring 埋在最底層，那部分我信任你。」

---

## 實作中（During implementation）

### 實作筆記（Implementation notes）

一旦我對計畫感到滿意，我就會建立一個新的 Session，並將所有產出物傳遞給 Prompt。這給了 Claude 一個全新的 Context Window，但同時具備了從你的規劃中所彙整的所有資訊。例如，我可能會傳入一份 Spec 檔案和一個 Prototype，並要求 Agent 進行實作。

但事實是，無論你做了多少規劃，總會有潛藏的 Unknown Unknowns。Agent 在工作過程中可能會發現，由於它在程式碼中發現的 Edge Case，它必須採取不同的策略。

我會要求 Claude Code 維護一個暫時的 `implementation-notes.md`（或 `.html`）檔案，用來追蹤它所做的決策，以便我們能為下一次嘗試汲取經驗。

**範例 Prompt：**

> 「維護一份 implementation-notes.md 檔案。如果你遇到迫使你偏離計畫的 Edge Case，請選擇保守的選項，將其記錄在『Deviations』下方，然後繼續進行。」

---

## 實作後（Post implementation）

### 提案簡報與解說說明（Pitches and explainers）

發布某項成果最重要的部分之一就是獲得認同（buy-in）與核准。在最終文件中建構提案簡報（pitch）和解說說明（explainer）產出物有助於：

* 當審查者（Reviewer）一開始帶著與你相同的未知時，加速理解
* 當專家希望看到你已經考慮到他們所預期到的未知和常見失敗點時，加速獲得核准

**範例 Prompt：**

> 「將 Prototype、Spec 和 Implementation Notes 打包成一份單一文件，讓我能發到 Slack 上以獲得團隊認同。請以 Demo GIF 作為開頭。」

### 測驗（Quizzes）

經過漫長的工作 Session 後，Claude 完成的工作可能遠比我意識到的還要多。閱讀 Code Diff 只能讓我對發生的事情有初步的了解，因為許多行為將取決於現有的程式碼路徑。

在提供大量 Context 後要求 Claude 對我進行關於該變更的測驗，有助於我理解實際發生的情況。只有在完全通過測驗後，我才會進行 Merge。

**範例 Prompt：**

> 「我想確保自己理解這次變更中所發生的一切。請給我一份關於這些變更的 HTML 報告，包含 Context、直覺思考、做了什麼等，供我閱讀和理解；並在底部附上一份我必須通過的變更測驗。」

---

## 整合應用：推出 Fable（How this comes together: launching Fable）

Fable 的發布影片是全程使用 Claude Code 端到端剪輯完成的。這對我來說是一個全新的領域，我絕非這方面的專家。

因此，我從自己所知道的內容開始。我知道 Claude 可以使用程式碼來剪輯影片並產生轉錄稿（transcript），但我不確定它是否足夠準確。接著我請 Claude 向我解釋像 Whisper 這樣的語音轉錄是如何運作的，以及我是否能使用 ffmpeg 精確剪掉贅字（例如 um）或過長的停頓。

我希望 Claude 建立一個能與我所說的話同步時間軸的 UI，但我不確定這是否可行，所以我請 Claude 使用 Remotion 和轉錄稿製作一個原型影片，看看是否能正常運作。

最後，影片本身看起來有點平淡無光（muted），我知道這是 Color Grading（調色）造成的結果，但我並不知道 Color Grading 到底是什麼。我的第一次嘗試是想讓 Claude 做幾個不同版本讓我挑選，但我意識到在調色這件事上，我甚至不知道「好的效果」看起來是什麼樣子。因此，我轉而請 Claude 教我關於 Color Grading 的知識，以發現我的未知。

---

## 地圖與疆域的媒合（Matching the Map and Territory）

模型變得越強大，你在掌握正確方法的情況下所能實現的成果就越多。當一個長週期（long-horizon）任務的結果不如預期時，很可能是你需要花更多時間來定義你的未知，或是建立一份能讓你和 Claude 共同靈活適應這些未知的實作計畫。

每一次的解說說明、腦力激盪、訪談、原型製作與參考範例，都是一種低成本的方式，讓你在需要付出高昂代價去修正之前，搶先找出自己不知道的事情。

因此，在開始下一個專案時，不妨先請 Claude 協助你找出你的未知。

關於使用 Fable 世代模型時的 Context 面向，請參閱《Context Engineering 的新規則》（The new rules of context engineering for Claude 5 generation models）。

*本文由 Anthropic 技術人員 Thariq Shihipar 撰寫。*