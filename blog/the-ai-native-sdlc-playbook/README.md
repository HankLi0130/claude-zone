---
Source: https://claude.com/blog/the-ai-native-sdlc-playbook
Course: https://academy.claude.com/courses/ai-native-sdlc-playbook
---

# AI-Native SDLC 實戰手冊

如何運用 AI，逐階段改造你的軟體開發生命週期。

- **日期：** 2026 年 8 月 21 日
- **閱讀時間：** 46 分鐘
- **作者：** Louis Claxton

## 程式碼不再是瓶頸

組織已開始運用 AI，以一年前難以想像的速度撰寫程式碼，然而，圍繞程式碼的流程卻沒有以同樣的速度改變。

許多工程團隊仍沿用相同的核准關卡、審查、交接與政策，使得使用 [Claude Code](https://claude.com/product/claude-code) 等 agentic coding 解決方案所帶來的生產力提升停滯不前。

軟體開發生命週期（SDLC）是讓軟體從構想走向正式環境的流程。大多數組織採行的流程，都是相同六個階段的某種版本，涵蓋軟體的規劃、設計、建置、測試、部署與維護。傳統上，每個階段都是由不同角色負責的獨立階段。產品經理撰寫需求，技術架構師將需求轉換為設計，工程師實作設計，受監管企業的 QA 團隊負責驗證，發布團隊負責交付，維運團隊則監控正在執行的系統。工作透過文件、工作單與簽核，在各階段之間流轉。

傳統的軟體開發生命週期（SDLC）有繁重的流程，以確保每個步驟的責任歸屬與控管。然而，傳統 SDLC 的設計，是為了在撰寫與實作程式碼仍是最耗時、最昂貴階段的年代，將效率最大化；如今已不再如此。PRD、估算流程與產品安全審查，都是為了在可能長達數週、數月或數季的開發工作期間，強制達成共識。

傳統 SDLC 的控管措施，也是假設每個步驟都由人類執行。創造最多價值的組織，已根據 agentic AI 現在能做到的事情重建流程，同時確保人類持續參與。本指南受到我們與客戶合作經驗的啟發，將介紹 Applied AI 團隊在 SDLC 各階段於內部整合 Claude 的多項最佳實務，以加速開發並讓流程運作得更快。

當程式碼不再是瓶頸，而且建置階段的速度超過傳統 SDLC 所能配合的程度時，以下三件事便會成為現實：

- 瓶頸會移到建置階段前後的步驟。主要是規劃、審查／測試與部署，這些步驟仍以人類的速度運作。
- 控管措施不再符合現實，並變得難以落實。當程式碼是由人撰寫時，逐行手動審查是合理的；但當 agent 撰寫了大部分 diff，這種方式就跟不上了。
- 治理成本增加，因為例外情況仍要經由每週或每月召開的會議與委員會處理。

![](https://cdn.prod.website-files.com/68a44d4040f98a4adf2207b6/6a8739a1b934ffe55bfc9715_44592f18.png)

建置不再是限制，周圍那些以人類速度運作的步驟才是。以人類速度運作的階段維持原有長度，而建置則縮短為數小時。

以安全瓶頸為例。安全團隊的規模是依照人類的產出量配置的，因此，當 agent 讓程式碼產出倍增時，不是審查佇列開始堆積，就是程式碼在審查不足的情況下發布。受監管的組織無法接受其中任何一種結果，因此，安全與政策檢查必須跟上 agent 的速度。

為了更充分實現 agentic AI 帶來的生產力提升，並確保其安全性，傳統 SDLC 生命週期需要經歷與實作階段同等程度的轉型。

**目錄**

1. 程式碼不再是瓶頸
2. 實踐方法
3. 第 1 階段——規劃
4. 第 2 階段——設計
5. 第 3 階段——建置
6. 第 4 階段——測試
7. 第 5 階段——部署
8. 第 6 階段——維護
9. 結語

## 什麼是 AI-native SDLC？

AI-native SDLC 是重新構思的流程，將原有的控管目標與新的執行方式結合。流程從線性流動轉為循環，並在每個環節嵌入 AI。AI-native SDLC 推動自動化交接與後續實踐方法的觸發，有助於解決傳統 SDLC 各階段之間交接仰賴人工且繁瑣的問題。

你也會聽到這項轉變被稱為 agentic SDLC、AI SDLC，或直接稱為 agentic software development——名稱不同，但描述的是同一件事。

![](https://cdn.prod.website-files.com/68a44d4040f98a4adf2207b6/6a8858c2eccce183e7553cf2_53b010df.png)

### AI-native SDLC 六個階段的轉變

下表呈現傳統 SDLC 與 Claude 支援的 AI-native SDLC 之間，光譜兩端的差異。大多數組織位於兩欄之間。

| 階段 | 傳統 SDLC | AI-native SDLC |
|---|---|---|
| 規劃 | 由委員會蒐集需求，經過工作坊與簽核加以整理，再由人工撰寫。 | Claude 直接從來源彙整痛點，並記錄於 `intent.md`，讓人類可以閱讀，機器也能據以行動。 |
| 設計 | 分析師撰寫規格，再由設計師解讀。 | 需求與設計濃縮為一次與 agent 協作的工作階段，以編寫成 skills 的標準引導，並在 git 中進行版本管理。 |
| 建置 | 測試與程式碼由人工撰寫，文件則在主要開發工作完成後才撰寫。 | 測試與程式碼由 AI 產生，組織知識則維護為可供機器讀取、具版本管理的 `CLAUDE.md` 檔案與 skills。 |
| 測試 | 在階段交界設置 QA 關卡。 | 持續性 evals 貫穿實作過程。 |
| 部署 | 人類逐行審查程式碼，治理發生於審查週期中，而且往往不一致。 | 多層 agentic review，人類審查保留給受監管與關鍵程式碼。治理在 AI 行動時落實，並以 hooks 作為核准關卡。 |
| 維護 | 人類監看正式環境，尋找 bug。 | Agents 監控已上線的部署。任何突破控制區間的情況都會被診斷，並以新的 `intent.md` 寫回循環。 |

貫穿右欄的主線，是已提交的產出物。每個階段都以將一份產出物寫入版本控制作結，包括 `intent.md`、`spec.md`、`plan.md`、diff 與其測試、包含審查發現的 PR，以及事件紀錄；下一個階段則從讀取該產出物開始。在早期階段，`.md` 檔案是主要產出物，因為 product owner 與 agent 都能讀取同一份檔案並據以行動。從建置階段開始，產出物則是程式碼與其紀錄。這一連串 commit 也是稽核軌跡：誰提出了什麼要求、agent 產出了什麼，以及誰核准了它。

凡是需要判斷的決策，仍由人類負責。在 agentic SDLC 的世界裡，人類的注意力會隨著必須審查的產出物而轉移。

> 每個階段都會提交下一個階段能讀取的產出物。意圖、規格、計畫、diff 與審查發現，共同構成稽核軌跡。

## 實踐方法

這些實踐方法是本手冊的核心，分為六個非線性階段：規劃、設計、建置、測試、部署與維護，共同涵蓋完整的生命週期。

每項實踐方法都涵蓋：

- 有哪些改變；
- 如何開始；
- 具體實作步驟；
- 治理考量；以及
- 如何衡量是否奏效。

這些步驟採模組化設計，組織可依自身需求，選擇在不同時間優先改造不同階段。每項實踐方法都在「前置條件」中列出相依項目，相依關係圖則進一步加以呈現。

一個階段以提交產出物作結，而該 commit 會啟動下一個階段。接受 `intent.md` 會觸發需求與設計作業，核准 `spec.md` 會觸發 plan mode，合併 PR 會觸發 pipeline，而正式環境突破控制區間時，則會寫出下一份 `intent.md`，循環如此持續。

一開始，你會手動下 prompt 啟動每個步驟；最終狀態則是一個循環，每份獲接受的產出物都會觸發下一個關卡。人類的注意力集中在關卡上，審查 agent 標記的內容，而不是每個階段都從頭啟動。

![](https://cdn.prod.website-files.com/68a44d4040f98a4adf2207b6/6a8855c75344623fc81efcb8_5d5a3c05.png)

各項實踐方法標示了所屬階段；箭頭則表示導入順序。兩者並不相同。可以從任何陶土色的實踐方法開始——沒有箭頭指向它，因此不需要先完成其他項目。對其他實踐方法而言，指向它的箭頭，代表應先導入的項目。

## 第 1 階段——規劃

構想不再等待有人將它寫下來。以提出者自己的話，一次記錄意圖，形成具版本管理、可供下一階段據以行動的產出物。

### 記錄為 intent.md

啟動軟體開發流程的 `intent.md`，可以來自不同途徑。有人提出構想、有人建立工作單，或透過警示浮現事件，詳見第 6 階段：維護。

當一個人有了構想，可以與 Claude 腦力激盪，產出一份 Markdown 初步規格。在傳統 SDLC 中，同一個人接著必須說服產品團隊成員，與自己一起或代替自己將構想寫下來。

Claude 產生的初步規格可供人類閱讀、受到版本控制，而且能立即由下一階段使用。這份初步規格會儲存為 `intent.md`。

無論意圖來自事件觸發還是 agent，都適用相同步驟：在提交之前，product owner 必須審查並修正 agent 撰寫的 `intent.md`。

| 傳統 | AI-native |
|---|---|
| 一個構想在任何人能採取行動之前，必須經過 backlog 項目、user stories、story points 與細化會議。每次交接都會轉移責任歸屬，因此，最後抵達工程團隊的內容，已與提出者原本的意思相隔好幾層。 | 提出者與 Claude 腦力激盪，並將結果寫成 `intent.md`，這是一份以提出者自己的話撰寫的初步規格。產出物包含想要什麼、為什麼，以及受到哪些限制。重複性流程透過 skills 編寫。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 無。 |
| 基礎設施 | 讓非工程人員能使用 Claude（claude.ai 或 Cowork）；一份已達成共識的 `intent.md` 範本；一個共享、具版本管理且由 product owner 關注的意圖存放處。對單一產品而言，最簡單的存放處是產品 repo 中的 `intent/` 資料夾。這種設置讓產出物鏈與由其衍生的程式碼放在一起。只有當意圖橫跨許多 repositories 時，獨立的意圖 repo 才值得額外的管理成本；在 monorepo 中，它就是一個目錄。第 3 階段：建置的側欄，會說明這個存放處與已持有紀錄的 Jira 或需求工具之間的關係。 |

這項設置是平台或工程團隊的一次性工作。技術團隊成員需要建立意圖存放處，並決定誰可以寫入，因為許多貢獻者會來自組織內不同部門。

Repository 建立後，沒有 git 經驗的貢獻者不需要直接使用 git。透過版本控制系統的 connector，例如 GitHub，Claude 就能從 claude.ai 或 Cowork 代替他們提交 Markdown 檔案。

#### 如何執行

1. 提出者以自己的話向 Claude 描述問題。可以描述目前做不到什麼、這個構想會影響誰、更好的狀態是什麼，或哪些內容不在範圍內。不需要正式用語。
2. 持續腦力激盪，直到構想具體化。Claude 會提出分析師會問的問題：範圍、使用者、限制，以及成功的樣貌。
3. 請 Claude 使用組織的範本，將結果寫成 `intent.md`。範本可編寫成 skill，由技術團隊成員建立，並經主管簽核。內容可以涵蓋問題、預期成果、受影響的使用者與系統、限制，以及待釐清問題。
4. 提出者修正 Claude 誤解的任何內容。
5. 將 `intent.md` 提交至共享存放處。作者與時間戳記會納入紀錄，product owner 則從這裡接手構想。

```markdown
# 意圖：理賠狀態自助查詢
作者：J. Ortiz（理賠作業）。狀態：草稿。

## 問題
客戶致電客服中心，詢問理賠進度。
處理人員約有三分之一的通話時間，用於只詢問狀態的問題。

## 預期成果
客戶能在入口網站查看理賠狀態、下一步與預計日期。

## 受影響的使用者與系統
理賠處理人員、入口網站團隊、claims-core API。

## 限制
入口網站 session 中不得新增 PII。僅使用既有的身分驗證。

## 待釐清問題
第三方理賠公證人是否也需要存取？
```

#### 治理考量

證據是已提交的 `intent.md`，其中列出作者、時間戳記與完整修訂歷史。這些資訊記錄於意圖存放處的 git 歷史中。由 product owner 核准，而決定意圖是否進入第 2 階段：設計的接受或拒絕決策，則以合併或結案審查的形式記錄。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 從第一次對話到提交 `intent.md` 的時間，可從意圖存放處的 git 歷史讀取，其中記錄了作者與時間戳記。預期會從長達數週的需求訪談與細化週期，縮短為數小時。 |
| 落後指標 | 存活率，也就是 product owner 接受進入第 2 階段：設計，而非直接關閉的 `intent.md` 檔案比例。接受或拒絕的決策，記錄為產出物的合併或已結束的審查。此外，也要計算同一項變更在第一次提交 `spec.md` 之後，對 `intent.md` 所做的修改次數。 |

## 第 2 階段——設計

需求與設計濃縮為一次工作階段。政策在撰寫規格時就套用，而不是幾週後才在審查中發現。

### 需求與設計

在 product owner 核准後，Claude 會取得已接受的 `intent.md`，產出需求與設計規格。這項工作會由組織針對品牌、安全、合規與 UX 的 [skills](https://code.claude.com/docs/en/skills) 引導。

Product owner 審查這份規格，但不負責撰寫。這個流程的目標，是產出工程團隊可以據以規劃的規格，並標記需要關注的問題。

前端工作是最清楚的例子。`intent.md` 一經接受，product owner 就可以根據它，在 [Claude Design](https://claude.com/product/design)（beta）中製作設計 mockup，反覆調整，再匯出至 Claude Code 進行建置。

| 傳統 | AI-native |
|---|---|
| 需求與設計是由不同團隊執行的獨立階段。分析師將構想正式整理為需求，設計師再將需求解讀為設計。這種區分是為了釐清責任，但速度緩慢，而且容易遺失資訊。 | 兩個階段在同一次由 prompt 啟動的工作階段中完成。Claude 取得 `intent.md`，產出受組織 skills 約束的需求與設計規格，並標記需要關注的問題。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 撰寫一份 `intent.md`，並將品牌、安全、合規與 UX 政策寫成 skills。 |
| 基礎設施 | 一位能使用 Claude 的 product owner。不需要工程技能。 |

#### 如何執行

1. Product owner 開啟一個可使用組織 skills 的工作階段，並附上 `intent.md`。
2. Product owner 的 prompt 指向 `intent.md`、列出限制，並要求標記疑慮。一開始手動執行，再將其編寫成組織層級的 slash command。接著，將意圖存放處接受 `intent.md` 設為觸發條件：在合併時啟動非互動式工作，載入組織的 skills 執行作業，並以 pull request 提交 `spec.md`。第 5 階段：部署中的 CI/CD 實踐方法會說明相關串接。從此，product owner 首次介入的時點就是審查。
3. 同一位 product owner 對照構想審查規格。規格是否解決了原本陳述的問題？`intent.md` 中的待釐清問題是否已得到回答，或被延續至下一步？
4. 優先處理標記的疑慮，因為這些正是分析師會向上呈報的問題。Product owner 在工程團隊看到規格之前，先與各項政策的負責人逐一解決。
5. 將 `spec.md` 與 `intent.md` 一起提交。這一對檔案記錄了提出什麼要求，以及做出什麼決定。
6. Product owner 決定規格與意圖是否進入建置；凡是組織歸類為較高風險的事項，都應諮詢技術主管。這項決定一律由人類團隊成員做出，而接受規格，正是啟動第 3 階段：建置中 plan mode 實踐方法的條件。

#### 實際樣貌（prompt）

```markdown
閱讀附上的 intent.md，並產出將其整合到既有 codebase 的需求與設計規格。套用你可使用的 skills，讓計畫符合我們的品牌指南、安全政策與 UX 標準。將規格完整記錄為 spec.md，準備交付工程團隊。清楚描述任何需要關注的問題，尤其是無法同時滿足互相矛盾政策的地方。
```

#### 治理考量

現行政策會在撰寫規格時被讀取並套用，而不是幾週後才在審查中發現。組織的 skills 會作為規格的限制條件。規格、產生規格的 prompt，以及當時生效的 skill 版本，都會記錄在版本控制中。Product owner 簽核規格，並將標記的疑慮交給指定的政策負責人。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 同一项變更從提交 `intent.md` 到提交 `spec.md` 的經過時間，也就是兩個 git 時間戳記的差值，並與原本的需求加設計週期比較。 |
| 落後指標 | 建置開始後的需求返工。計算同一項變更第一次提交 `plan.md` 之後，`spec.md` 的 commit 次數。Git log 可直接提供這項資訊。 |

## 第 3 階段——建置

沒有已接受的計畫，就不進行任何實作。組織知識成為 agent 讀取的檔案，防護措施則以程式碼執行，而非依賴習慣。

### 以 Claude Code plan mode 作為預設起點

工程師以 [plan mode](https://code.claude.com/docs/en/permission-modes) 啟動 Claude Code 工作階段，提供第 2 階段：設計中已核准的 `spec.md`，並讓 Claude 訪談自己，反覆調整計畫，直到工程師滿意為止。

| 傳統 | AI-native |
|---|---|
| 工程師讀取設計後，就開始撰寫程式碼。如何進行變更，包括要修改哪些檔案、撰寫哪些測試，都留在工程師腦中，頂多寫成工作單留言。其他人無法審查。審查者第一眼看到的就是完成的 diff，而此時返工已相當緩慢。 | 工作從 Claude 在 plan mode 中產生的書面計畫開始；在這個模式下，Claude 可以讀取 codebase，但不能修改任何內容。工程師在程式碼撰寫前修正計畫，核准後的版本則提交為 `plan.md`，供後續階段核對。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 如果已有意圖產出物，提供 `intent.md` 或 `spec.md`；`CLAUDE.md` 也會有所幫助。 |
| 基礎設施 | 可存取 repository 的 Claude Code。 |

#### 如何執行

1. 工程師以 plan mode 開始與 Claude 的工作階段。
2. 工程師提供 `intent.md` 與 `spec.md`，要求 Claude 提出實作計畫，列明要修改的檔案、工作順序，以及能證明成果的測試。
3. 深入追問計畫：這項變更可能破壞什麼、哪個步驟風險最高，以及 Claude 放棄了哪些其他方案。
4. 持續迭代，直到一位從未看過這段對話的工程師，也能只憑計畫完成這項變更。
5. 將核准的計畫提交為 `plan.md`。計畫會加入稽核軌跡，而第 5 階段：部署中的 PR 審查實踐方法，會將最終 diff 與它核對。
6. 接受計畫，讓 Claude 實作。有了扎實的計畫，實作往往一輪就能完成。
7. 當實作偏離計畫時，在同一個 commit 中更新 `plan.md`。可考慮使用 hook 強制兩者保持同步。

#### 實際樣貌（plan.md）

```markdown
# 計畫：理賠狀態自助查詢（源自 intent.md 2026-06-02）

## 要修改的檔案
portal/src/claims/StatusPanel.tsx（新增）、claims-api/routes/status.py、
claims-api/tests/test_status.py

## 工作順序
1. 在既有身分驗證機制下新增狀態 endpoint。
2. 建立串接該 endpoint 的面板。
3. 整合至入口網站導覽。

## 風險
claims-core API 的速率限制為 50 rps；面板必須使用快取。

## 證明
test_status.py 涵蓋四種理賠狀態；螢幕截圖符合已核准的 mockup。
```

#### 治理考量

設計審查在任何程式碼產生之前進行，此時改變方向仍只是修改文件的問題。Plan mode 本身就會強制落實這一點，因為在工程師接受計畫之前，Claude 無法編輯檔案。計畫、修訂內容，以及接受計畫的人，都會一併記錄。例行變更由工程師核准，而組織歸類為較高風險的事項，則交由技術主管或架構師處理。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 第一輪實作後就能合併的變更比例，以及從計畫核准到 PR 合併的時間；所需資料都在 PR metadata 中。 |
| 落後指標 | 每項變更的返工次數，同樣來自 PR metadata；以及合併後的 diff 仍符合已提交 `plan.md` 的頻率。 |

### 以 auto mode 執行 Claude Code

Claude Code 也能以 auto mode 執行：工程師反覆調整計畫並確認滿意後予以核准，接著 Claude 套用每項變更時，就不會逐次提示確認。隨著後續實踐方法中的防護措施逐漸成熟——經過調校的 `CLAUDE.md`、將政策編寫成指示的 skills、阻擋不安全動作的 hooks，以及 Claude 能執行的測試套件——自動接受便成為例行工作的預設方式：一份嚴謹的 `spec.md`、有限的影響範圍，以及已受測試涵蓋的程式碼。

重心因此從使用者看著 agent 編輯並審查動作，轉向在較長的自主工作階段結束後審查產出物。搭配 worktrees 使用時，自動接受模式還能支援個人與團隊的平行作業，也是自主執行 SDLC，以及完成第 6 階段：維護所述閉環的基礎。

#### 側欄：既有系統與權威來源

*適用於流程產生的每一項產出物。*

既有 SDLC 流程很可能已經在追蹤產出物，只是沒有使用 Markdown 檔案。工作項目可能在 Jira，需求可能存放於內建法規追溯能力的工具，設計在 Figma，變更核准則由變更委員會處理。這些系統很難被取代，因為稽核人員與監管機關已經接受它們，其他團隊也仰賴它們，因此 AI-native SDLC 必須配合現有系統。

轉向 AI-native SDLC 時，對流程產生的每一項產出物，都要指定一個系統作為權威來源，其他地方則持有副本或連向原始內容的連結。以下配置都可以設定為只有一個權威來源，而且不同產出物可以採用不同選擇：

**以 repo 作為權威來源。** Markdown 產出物是權威紀錄，既有系統則參照 commit 中的檔案。對工程主導的組織而言，這可能是最簡潔的配置之一，因為所有紀錄都存在同一個工具中，並由同一個來源提供權威時間戳記。

**以既有系統作為權威來源。** Jira、ServiceNow 或需求工具持有權威紀錄，Markdown 產出物則是工作副本。Claude 在工作階段開始時讀取紀錄，並在產出規格或計畫的同一個工作階段中，透過 MCP connector 將結果寫回。

**以建立連結作為最低要求。** 所有產出物都註明紀錄 ID，所有既有紀錄也都包含 Markdown 檔案的 commit SHA。轉向 AI-native SDLC 時，建立連結是很好的起點，同時接受存在兩個權威來源的情況。

既有系統與 Markdown 優先的系統可以共存，只要兩者之間有連結，或明確宣告其中一個為權威來源。

### CLAUDE.md

[`CLAUDE.md`](https://code.claude.com/docs/en/memory) 提供 Claude 新進成員所需的背景資訊，涵蓋慣例、命令、架構，以及團隊最常遇到的錯誤。過去存在人們腦中與 wiki 上的知識，會成為 agent 在每次工作階段開始時讀取的檔案，由整個團隊維護，並在每次發生錯誤時持續修訂。

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 無。 |
| 基礎設施 | 一個 repo、已安裝的 Claude Code，以及一位熟悉 codebase 的工程師。 |

#### 如何執行

1. 在 repo 中執行 `/init`。Claude 會根據找到的內容，產生初始的 `CLAUDE.md`。
2. 將產生的檔案精簡到新進成員第一天所需的內容。保留 build、test 與 lint 命令、重要慣例，以及 Claude 持續犯錯的事項。
3. 將 `CLAUDE.md` 放在 repo 根目錄並提交至 git，讓整個團隊共用同一個版本，且變更像程式碼一樣接受審查。
4. 這裡有一條實用規則：當 Claude 同一個錯誤犯了兩次，就將修正指示寫進 `CLAUDE.md`。
5. 將長度控制在一頁以內，因為 Claude 會在工作階段開始時讀取全部內容；任何過時資訊都只會占用 context，卻沒有好處。

#### 實際樣貌（CLAUDE.md）

```markdown
# 付款服務

## 命令
- Build：make build
- Test：make test（unit）、make itest（integration，需要 docker）
- Lint：make lint（會在 CI 中執行；push 前先修正）

## 慣例
- Java 21、Spring Boot 3。不得新增 Lombok。
- 金額一律使用 BigDecimal，絕不使用 double。
- 每個 endpoint 都需要在 src/itest 中有 integration test。

## 架構
- api/ 放置 REST controllers，core/ 放置 domain logic，
  adapters/ 與外部系統通訊。
- Kafka events 定義於 schemas/；絕不編輯產生的 classes。

## Claude 容易犯的錯誤
- 不要調升相依套件版本；版本由平台團隊負責。
- 舊版 v1/ package 已凍結；變更請放在 v2/。
```

#### 治理考量

`CLAUDE.md` 受到版本控制，因此 agent 遵循的指示可以審查與稽核。團隊慣例透過這份檔案套用，變更記錄於 git 歷史中，並由 code owners 在 PR 審查時核准。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | Claude 重複犯下原本應由 `CLAUDE.md` 防止的錯誤之頻率。對 `CLAUDE.md` 的修正或變更應在 git 歷史中追蹤。 |
| 落後指標 | 新團隊成員從加入到第一個 PR 合併的時間，資料來自 PR 歷史。 |

### 以 Skills 承載組織知識

Skills 是組織讓自身知識實際運作的方式。指示明確、受到版本控制、廣泛套用，並在政策變動時集中更新。經驗法則是：為必須一致套用的組織知識撰寫 skill；不要為應該放在 `CLAUDE.md` 或 prompt 裡的內容撰寫 skill。

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 不需要。擁有 `CLAUDE.md` 會有幫助，因為它讓 agent 的工作知識保留在 repo 中，但 skill 並不依賴它。 |
| 基礎設施 | 一項具有明確負責人與書面權威來源的政策。 |

#### 如何執行

1. 選擇一項目前執行不一致的知識。可以是安全標準、API 設計慣例，或品牌規範。
2. 將它寫成 skill，也就是一個包含 `SKILL.md` 的資料夾；其 frontmatter 說明何時觸發，內文則說明要做什麼。工程師以政策負責人的權威來源為依據，借助 Claude 撰寫。
3. 將 skill 放在 repo 的 `.claude/skills/<name>/`，使其隨程式碼一起交付，或透過 [plugin](https://code.claude.com/docs/en/plugin-marketplaces) 發布至整個組織。
4. 測試 skill 是否會觸發。以不同方式請 Claude 執行相關任務，確認每次都會載入 skill。
5. 政策變更時，同步修改 skill，並請政策負責人簽核。
6. 工程師會在下一次工作階段中自動取得新版本。

#### 實際樣貌（.claude/skills/secure-api-review/SKILL.md）

```markdown
---
name: secure-api-review
description: 套用 API 安全標準。建立或修改對外 endpoint、
  審查 API 程式碼，或產生 OpenAPI 規格時使用。
---
# API 安全審查

建立或修改 API endpoint 時：
1. 身分驗證：每個 endpoint 都需要 gateway JWT；
   除了 /health 之外，不得有匿名 routes。
2. 輸入驗證：依照 OpenAPI schema 驗證 request bodies，
   並拒絕未知欄位。
3. 稽核：每個會改變狀態的 endpoint，都必須發出包含
   actor、action、entity 與 timestamp 的 audit event。
4. 資料分類：schema 中標記為 pii 的欄位，絕不得出現在
   logs 或錯誤訊息中。

執行 scripts/check-endpoints.sh，並將輸出納入摘要。
```

#### 治理考量

Skill 是一種控管措施，不過屬於建議性質。它提高 Claude 在撰寫程式碼時套用政策的可能性，但沒有任何機制強迫工作階段遵守。必須始終成立的政策，需要 skill 背後有確定性的機制支撐，例如阻擋動作的 hook，或在 PR 中重新檢查政策的審查程序。Skill 讓違規變得少見，hook 則讓違規接近不可能。Skill 的呼叫會記錄於工作階段追蹤紀錄中，政策負責人則像審查程式碼一樣審查 skill 變更。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 從政策負責人核准政策變更，到更新後的 skill 合併所需的時間，資料來自 skill 資料夾的 PR。 |
| 落後指標 | PR 審查中引用該政策的問題發現數量；當 skill 已在撰寫程式碼時套用政策，這個數字應逐漸趨近零。若沒有趨近零，可能是 skill 沒有觸發，或其文字已偏離正式政策。 |

### 以 Hooks 作為建置時的防護措施

Skill 是建議性的控管措施，而 [hook](https://code.claude.com/docs/en/hooks) 是其背後的確定性層。Claude 的大多數動作，是實作期間的檔案編輯與 shell 命令，因此建置階段往往是 hooks 最常觸發的地方。

建置階段的 hooks 可以：

- 阻擋對受保護路徑的編輯，例如產生的 classes 或已凍結的 package；
- 在檔案編輯後執行 formatter 與 linter，避免偏差持續累積；
- 防止憑證進入 diff。

任何政策必須毫無例外地成立的 skill，都應有 hook 支撐。Hook 會在每個符合條件的動作上執行，因此建置階段的 hooks 應該快速，並將範圍限定在變更的檔案。完整測試套件等較重的檢查，應放在 commit 或 PR 時執行。

需要向人類請求核准的 hook，應歸入第 5 階段：部署的關卡，因為在建置期間要求核准，會讓人類重新成為所有平行工作階段關鍵路徑上的必要環節。

### 平行工作階段與 subagents

一位工程師可以同時推進多條工作線。

平行工作階段是另一個完整的 Claude Code instance，在自己的 [git worktree](https://code.claude.com/docs/en/worktrees) 中處理獨立任務。每個獨立工作階段都不知道其他工作階段的情況，唯一的共同點就是引導它們的工程師。

[Subagent](https://code.claude.com/docs/en/sub-agents) 在單一工作階段內執行，作為限定範圍的助手，擁有自己的 context window 與工具限制，適合在多項任務中重複出現的工作，例如驗證應用程式是否如預期執行。

平行工作階段提高工程師能同時推進的任務數量，而 subagents 則讓每個工作階段專注於自己的任務。工程師的工作是引導並審查所有工作。

| 傳統 | AI-native |
|---|---|
| 一位工程師一次處理一項任務，每天或每週有很大一部分時間花在 build、test 與等待審查者。等待時雖然可以切換任務，但切換 context 相當耗神，因此很少有人選擇這麼做。 | 一位工程師同時執行多個 Claude 工作階段，每個階段在自己的 worktree 中處理各自的任務。重複性工作則成為擁有獨立 context 與工具限制的 subagents。工程師的工作轉向協調，最終轉向建立與監控循環。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | `CLAUDE.md`，因為所有工作階段都會讀取它。第 4 階段：測試中的回饋循環也有幫助，因為當工作階段能驗證自己的工作時，工程師所需的監督就更少。 |
| 基礎設施 | 一個 git repository，因為隔離來自 worktrees；以及經過調整的權限設定，讓工作階段不必為組織認定安全的命令等待核准提示。 |

#### 如何執行

1. 工程師將工作拆成會修改不同檔案的任務，並利用第 3 階段：建置中 plan mode 實踐方法產出的計畫，判斷哪些工作彼此獨立。會共用檔案的任務，則在同一個工作階段中依序執行。
2. 每項平行任務都有自己的 worktree，例如在一個 terminal 中執行 `claude --worktree feature-auth`，在另一個 terminal 中執行 `claude --worktree fix-rate-limit`。Worktree 是位於自己 branch 上的獨立 checkout，能避免工作階段在檔案上互相衝突。
3. 以兩到三個工作階段作為起點是合理的。實際上限取決於一個人能妥善審查多少條工作線，因此，只有在審查跟得上的情況下，才增加工作階段。
4. 將重複性工作轉為 subagents，透過 `.claude/agents/` 中的 Markdown 檔案定義。每個 subagent 都包含名稱、使用時機描述，以及允許使用的工具。例如：在主要 agent 完成後移除不必要複雜度的 code simplifier、執行應用程式並檢查行為的 verifier，以及探索 codebase 並回報、卻不塞滿主要 context 的 researcher。將定義提交至 git，讓整個團隊共用。

#### 實際樣貌（.claude/agents/verifier.md）

```markdown
---
name: verifier
description: 在工作階段回報完成之前，執行應用程式並檢查變更是否有效
tools: Bash, Read
---
使用 make run 啟動應用程式。實際操作變更後的行為，以及兩個最接近的相鄰流程。
回報你執行了什麼、看到了什麼，以及任何不符合 plan.md 的行為。
不要修正任何內容；只回報。
```

#### 治理考量

更多工作階段意味著更多產出，因此控管措施必須來自 repo 中的設定。那裡的 hooks 與權限設定會套用至所有工作階段，而工作階段所做的事情都會記錄，並歸屬於執行它的工程師。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 在維持審查品質的前提下，每位工程師的同時執行工作階段數量，從 OpenTelemetry 匯出資料計算；以及一天中花在引導而非等待的時間比例。 |
| 落後指標 | 每位工程師每週合併的變更數量，並搭配 PR 歷史所呈現的返工率一起觀察。 |

## 第 4 階段——測試

每個工作階段都在人類看到之前，先檢查自己的工作；引導 agent 的設定，也像它撰寫的程式碼一樣接受 regression testing。

### 給 Claude 一個回饋循環

始終提供 Claude 一種驗證自身工作的方法，無論是測試、build，還是螢幕截圖 diff。工作階段會在工程師看到之前，先檢查自己的工作並修正錯誤。

不要將回饋循環與 verifier subagent 混為一談，後者見第 3 階段：建置。回饋循環貫穿整項任務，隨工作需要反覆執行。相較之下，verifier subagent 是封裝最終檢查的一種方式：當工作階段認為工作完成後，以全新的 context window 執行一次檢查。如此一來，判定結果就不會受到產生程式碼時所採用的假設影響。

| 傳統 | AI-native |
|---|---|
| 程式碼是否能正常運作的訊號來得很晚。CI 在幾分鐘後、測試人員在幾天後、正式環境則在幾週後才提供訊號。當程式碼由 agent 產生時，訊號延遲意味著某個人必須檢查所有產出，而這個人就成了瓶頸。 | 工作階段被賦予方法，在人類看到之前檢查自己的工作。執行測試、執行 build、擷取螢幕截圖。Claude 持續迭代直到檢查通過，因此交到工程師手上的內容已通過檢查。建立循環是執行該工作階段的工程師的責任，以下步驟就是為他們撰寫的。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 無。 |
| 基礎設施 | 一套測試與 build，兩者各自都能以單一命令在本機執行。對 UI 工作而言，讓 Claude 能看見結果非常重要，可以是 browser tool，或透過 MCP 串接的螢幕截圖工具。 |

#### 如何執行

1. 如果目前檢查成果需要一連串命令與一些環境知識，就將它封裝成單一 target，例如 `make test` 或 `npm test`，並在失敗時以非零狀態碼結束。
2. 在 `CLAUDE.md` 的 Commands 區段中，列出每個命令，以及正常輸出的範例。
3. 明確提出可量化的目標，讓 Claude 不必詢問你也能檢查成果，例如：「`test_status.py` 中的所有測試都通過」、「螢幕截圖符合附上的 mockup」，或「endpoint 回傳 200，且包含新欄位」。
4. 修復 bug 時，先撰寫會失敗的測試。請 Claude 將 bug 重現為測試、執行它，並確認它是因為你預期的原因而失敗。提交該測試。只有在這之後，才要求 Claude 在不編輯測試的情況下讓它通過，並由最後一步提到的測試檔案 hook 強制執行限制。一個在修復前就存在、而且 agent 無法改寫的測試，就是 bug 已消失的證據。
5. 對 UI 工作，以視覺檢查完成閉環。提供 Claude browser 或螢幕截圖工具、提供 mockup，然後讓它反覆調整。實作、截圖、比較、調整。兩到三輪很正常，而且每一輪的結果都應有所改善。
6. 將驗證納入「完成」的定義。指示存放於 `CLAUDE.md`。在回報任務完成之前，先執行測試並展示輸出。
7. 最後，循環本身也需要保護，因為修正程式碼的 agent 不應能削弱對該程式碼的檢查。可透過 hook，在修復任務期間阻擋測試檔案編輯。另一種方式是在審查時檢查 diff，並拒絕任何修改測試的變更。

#### 實際樣貌（CLAUDE.md 驗證區塊）

```markdown
## 驗證你的工作

- Build：make build（必須以 "Build succeeded" 結束）
- Test：make test（全部通過；絕不跳過或刪除失敗的測試）
- Lint：make lint（零警告）

在回報任何任務完成之前，執行以上三項並貼上輸出。
如果測試失敗，修正程式碼，不要修改測試。
```

#### 治理考量

| 項目 | 內容 |
|---|---|
| 強制執行什麼 | 在回報任務完成之前進行驗證，以及在修復期間禁止 agent 編輯測試檔案。當組織需要保證這兩點時，都以 hooks 實作。 |
| 證據是什麼 | Claude 實際執行並貼上的 `make test` 原始輸出、build log，或螢幕截圖 diff，因此證據來自工具鏈。 |
| 記錄在哪裡 | 工作階段逐字紀錄中，OpenTelemetry 匯出會將其轉送至組織的可觀測性系統；也會記錄於 PR 的 check run，讓審查者與日後的稽核人員都能看到。 |
| 誰核准 | 審查 PR 的 code owner。由於機械性檢查的證據已附上，他們可以專注於意圖與風險。 |

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | Agent 撰寫的變更首次執行 CI 的成功率，CI 系統已支援這項資料。 |
| 落後指標 | 每個 PR 的審查時間，資料來自 PR metadata；當測試能捕捉過去由審查者發現的問題時，審查時間應下降。另追蹤事件追蹤系統中的變更失敗率。 |

### 在 CI 中持續執行 evals

Evals 是 AI-native 版本的階段關卡式 QA。實務上，這代表一套會在 agent 設定變更時執行的評估套件。替換新模型或改寫 prompt 時，eval suite 會判斷 agent 是否仍以相同標準完成工作。

應將 evals 視為持續演進的套件。隨著模型改善，過去能區分表現的案例將不再具有區辨力，必須加入從持續監控中產生的新案例。

視使用情境而定，有些團隊可能更傾向以固定頻率離線執行這些 evals，而不是每次變更都執行。以下步驟適用於持續評估。

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | `CLAUDE.md` 與回饋循環，見第 4 階段：測試。 |
| 基礎設施 | 能以非互動方式執行 Claude Code 的 CI，以及具備 eval 執行預算的 API key。 |

#### 如何執行

1. 平台工程師從近期工作中蒐集 20 到 50 項真實任務，以及其預期／已接受的結果。
2. 將每項任務寫成 eval，也就是 prompt 加上定義可接受結果的檢查：測試通過、lint 無問題、行為不變，以及遵循政策。
3. 這套評估會以非互動方式在 CI 中定期執行，並在 `CLAUDE.md`、skills 或 hooks 有任何變更時執行，因為這些設定引導 agent，也應像程式碼一樣接受 regression testing。
4. 根據結果把關設定變更。會降低通過率的 skill 變更，必須在合併之前接受審查。
5. 每起正式環境事件都由負責該事件的團隊撰寫一項 eval，並留在套件中作為 regression test。

#### 實際樣貌（.github/workflows/agent-evals.yml）

```yaml
name: Agent evals
on:
  pull_request:
    paths: ['CLAUDE.md', '.claude/**']
  schedule:
    - cron: '0 2 * * *'
jobs:
  evals:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - run: npm install -g @anthropic-ai/claude-code
      - name: 執行 eval suite
        env:
          ANTHROPIC_API_KEY: ${{ secrets.ANTHROPIC_API_KEY }}
        run: |
          for eval in evals/*.json; do
            claude -p "$(jq -r '.prompt' $eval)" \
              --allowedTools "Read,Edit,Bash(make test)" \
              --output-format json > result.json
            ./evals/check.sh "$eval" result.json
          done
```

#### 治理考量

Evals 為 QA 提供能跟上 agent 產出的關卡。通過率門檻以合併檢查強制執行，執行紀錄會保留，以便比較不同時間的結果，並由負責該設定變更的團隊核准。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | Eval 通過率隨時間的變化，由套件在每次執行時回報；以及正式環境事件轉為永久 eval 所需的時間。 |
| 落後指標 | CI 捕捉到的 regressions，與事件追蹤系統所記錄、在正式環境才發現的 regressions 之比較。 |

## 第 5 階段——部署

審查雙向進行，治理在 agent 行動時落實。Agent 可以完成正式環境關卡之前的所有事情，但不能越過它。

### PR 審查循環中的 AI

Claude 既提供審查，也接受審查。它會根據組織政策審查送來的 PR，也會處理自己 PR 上的審查留言。這讓工程師在 PR 審查中能專注於行為，歸根究柢就是判斷意圖與風險。

| 傳統 | AI-native |
|---|---|
| 審查量能依照人類產出規劃。PR 等待審查者讀完整份內容，審查品質隨審查者負荷而變動，而作者隨著 backlog 增長不斷催促。 | 所有 PR 都接受相同的一組審查程序，並依嚴重程度排列發現的問題。人類的注意力提升一個層次，關注變更是否實現計畫意圖，以及風險是否可接受。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 第 3 階段：建置中已更新的 `CLAUDE.md`；若審查程序需要落實書面政策，則需要 skills；以及已定義的 subagents。 |
| 基礎設施 | 已安裝 Claude 整合的 repo，可以是由管理員啟用的代管 Code Review 服務（research preview），或在自己的 CI 中執行 claude-code-action，並視需要透過 AWS Bedrock、Google Vertex 或 Microsoft Foundry 呼叫模型。CI/CD 實踐方法會涵蓋部署選項。要求 code owner 核准的 branch protection 政策也很值得採用。 |

#### 如何執行

1. 代管 Code Review 服務是最快的起點。管理員啟用服務並選擇 repositories。若需要控制 pipeline，或希望 API 呼叫透過自己的雲端合約進行，就使用 claude-code-action 在自己的 CI 中執行審查；CI/CD 實踐方法會說明相關串接。
2. 技術主管在 repo 根目錄撰寫 `REVIEW.md` 作為審查政策，並依組織關注的項目分成不同審查程序：bug 與邏輯錯誤；安全與漏洞；是否符合規格，也就是需求實踐方法中的 `spec.md`、實作計畫，也就是 plan mode 實踐方法中的 `plan.md`，以及設計原則。`REVIEW.md` 也定義哪些問題屬於 Important、哪些屬於 Nit，以及哪些內容應略過。
3. 技術主管設定人類介入的門檻。審查發現本身不會核准或阻擋 PR，branch protection 仍要求 code owner 核准。若平台工程師希望根據審查發現把關合併，可以讀取 check run 發布的各嚴重程度數量，這些資料以機器可讀格式提供。
4. 當審查者或作者在審查留言中標記 `@claude`，Claude 會處理留言並 push 修正。PR 討論串會同時記錄請求與變更。這個修正循環透過 claude-code-action 執行。在代管服務中，留言 `@claude review` 則是要求重新審查。對 Claude 建立的 PR，可以更進一步，讓 Claude 持續照看直到合併。團隊會以自訂 slash command 封裝這個循環，掃描 PR 上尚未解決的審查留言與失敗檢查，處理後 push 修正，直到 PR 全部通過，只剩等待 code owner 核准。
5. 審查發現會回饋至 `CLAUDE.md`。当某個錯誤第二次在審查中被指出，就將修正指示納入 `CLAUDE.md`，作為該次審查的一部分；由於審查會讀取 `CLAUDE.md`，從下一個 PR 開始就能捕捉這個錯誤。審查也會標記哪些變更已使 `CLAUDE.md` 過時。
6. 技術主管每月調校一次設定，透過評分審查發現來改善審查者表現，並在 `REVIEW.md` 中限制 Nit 數量。產生的檔案路徑，以及 CI 已強制執行的事項，均排除在外。

#### 實際樣貌（REVIEW.md）

```markdown
# 審查指示

## 審查程序
執行三輪審查，並為每項發現標記所屬程序：
- Bugs：邏輯錯誤、失效的邊界情況、細微的 regressions
- Security：injection 風險、身分驗證缺口、logs 中的 PII
- Compliance：變更符合 spec.md、plan.md 與我們的設計原則

## 這裡的 Important 代表什麼
Important 僅用於會破壞行為、洩漏資料或違反政策的問題。
風格與命名屬於 nits。

## 限制 nits
每次審查最多回報五個 nits；其餘以數量摘要呈現。

## 不要回報
src/gen/ 下的產生檔案，以及任何 CI 已強制執行的事項。
```

#### 治理考量

職責分離得以保留，因為撰寫程式碼的 agent 無法核准自己的程式碼。`REVIEW.md` 中的審查政策套用至所有 PR，而審查發現、修正、評分與核准都記錄在 PR 歷史中，因此 PR 就是稽核紀錄。核准由人類依據審查發現，透過 branch protection 給予。

若要了解這些控管措施如何在正式環境規模下共同運作，請參閱 [Anthropic 如何確保 AI-native SDLC 的安全](https://claude.com/blog/how-anthropic-secures-its-ai-native-software-development-lifecycle)。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 首次審查所需時間，應縮短至數分鐘；以及未經人類修改 branch 就解決的審查留言比例，資料直接儲存在 Git 中。 |
| 落後指標 | 合併前捕捉到的缺陷與漏洞，與漏至正式環境的缺陷與漏洞之比較，資料來自 PR 歷史與事件追蹤系統。 |

### 以 Hooks 作為核准關卡

建置階段使用 hooks 作為防護措施，在沒有人類介入的情況下允許或阻擋動作，見第 3 階段：建置。Hook 也可以提出核准請求，在特定人員核准之前暫停動作，這正是發布關卡所需的能力。

這項實踐方法位於第 5 階段：部署，因為發布關卡是最清楚的案例，但 hooks 並非部署專用：只要 Claude 行動，就能執行。例如，在第 3 階段：建置中，hooks 可以在缺少變更工作單時阻擋 migrations 與基礎設施的編輯；在第 4 階段：測試中，則能阻止 agent 在修復任務期間編輯測試檔案。

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | 無。 |
| 基礎設施 | 一份書面清單，列出變更流程所要求的核准。 |

#### 如何執行

1. 工程主管與變更管理、合規人員共同列出必須保留的人類核准關卡，例如變更管理簽核、發布授權，以及受保護路徑的編輯。
2. 平台工程師將每個關卡表達為 hook，也就是在 Claude 行動前執行、可允許、詢問或阻擋動作的 script。
3. 團隊 hooks 放在 git 中的 `.claude/settings.json`，不可妥協的 hooks 則放在平台或 IT 管理員持有的 managed settings 中，個別工程師無法將其關閉。
4. 阻擋應該能說明自身原因，因此，當 hook 停止一項動作時，原因與取得核准的途徑都會出現在 Claude 的輸出中。

#### 實際樣貌（.claude/settings.json）

```json
{
    "hooks": {
      "PreToolUse": [
        {
          "matcher": "Bash",
          "hooks": [
            { "type": "command",
              "command": "${CLAUDE_PROJECT_DIR}/.claude/hooks/production-gate.sh" }
          ]
        }
      ]
    }
}
```

#### 關卡本身（.claude/hooks/production-gate.sh）

```bash
#!/bin/bash
# 正式環境部署需要具名的發布授權
cmd=$(jq -r '.tool_input.command' < /dev/stdin)
if [[ "$cmd" == *"deploy"* && "$cmd" == *"production"* ]]; then
   if [ -z "$RELEASE_APPROVAL" ]; then
     echo "正式環境部署需要發布授權。" >&2
     exit 2 # exit 2 會阻擋動作；訊息會傳給 Claude
   fi
fi
exit 0
```

#### 治理考量

Hooks 就是核准關卡。關卡條件每次都會執行，對所有人都適用。允許與阻擋的決策會附帶時間戳記記錄。關卡也定義什麼才算核准，無論是已核准的變更工作單，或發布經理的簽核。

#### 實作範例：受監管企業的 managed settings

由平台團隊透過 MDM 或管理主控台部署；工程師無法編輯或覆寫其中任何設定。

```json
{
  "permissions": {
    "deny": [
      "Read(.env*)", "Read(./secrets/**)",
      "WebFetch", "Bash(curl *)", "Bash(wget *)"
    ],
    "allow": [
      "Bash(git *)", "Bash(make build)",
      "Bash(make test)", "Bash(make lint)"
    ],
    "disableBypassPermissionsMode": "disable"
  },
  "allowManagedPermissionRulesOnly": true,
  "sandbox": {
    "enabled": true,
    "failIfUnavailable": true,
    "allowUnsandboxedCommands": false,
    "network": {
      "allowedDomains": [
        "git.internal.example.com",
        "registry.npmjs.org"
      ]
    },
    "credentials": {
      "files": [
        { "path": "~/.ssh", "mode": "deny" },
        { "path": "~/.aws/credentials", "mode": "deny" }
      ],
      "envVars": [
        { "name": "GITHUB_TOKEN", "mode": "deny" }
      ]
    }
  },
  "allowManagedHooksOnly": true,
  "disableSideloadFlags": true,
  "allowManagedMcpServersOnly": true,
  "strictKnownMarketplaces": [
    {
      "source": "github",
      "repo": "example-corp/approved-plugins"
    }
  ],
  "requiredMinimumVersion": "2.1.193"
}
```

**每一行提供了哪些控管能力**

`permissions.deny` 防止 secrets 進入 agent 的 context，並阻擋透過工具任意對外連線；`permissions.allow` 預先核准安全的內部工作循環，避免 deny 清單造成反覆核准提示的疲勞。

`disableBypassPermissionsMode` 加上 `allowManagedPermissionRulesOnly`，表示任何工程師、專案檔案或 command-line flag 都無法放寬規則。

`sandbox` 補上 permissions 無法涵蓋的缺口。在工具層級禁止 WebFetch，無法阻止 shell 命令存取網路；OS 層級的網域 allowlist 則直接阻擋對外連線。

`failIfUnavailable` 與 `allowUnsandboxedCommands` 讓 sandbox 成為一道關卡：當 sandbox 無法初始化時，Claude Code 會拒絕啟動；在 sandbox 內失敗的命令，也無法在其外部重試。

`credentials` 補上 deny 規則留下的缺口。`permissions.deny` 管控的是 Claude 的檔案工具，但在預設情況下，sandbox 中的 shell 命令仍可能讀取 `~/.ssh` 或 `~/.aws/credentials`；這個區塊會拒絕這些讀取，並從每個 sandbox 命令的環境中移除指定的 secrets。

`allowManagedHooksOnly` 表示這項實踐方法中的核准關卡，是唯一會執行的 hooks；本機的任何設定都無法新增或取代它們。

`disableSideloadFlags` 與 `strictKnownMarketplaces` 表示，工程師機器上的每個 skill、agent、hook 與 MCP server，都必須透過組織核准的 plugin marketplace 取得，絕不來自家目錄。

`allowManagedMcpServersOnly` 讓 agent 可使用的工具集合，成為由平台團隊管理的 allowlist。

`requiredMinimumVersion` 會拒絕在低於核准最低版本的版本上啟動，確保控管措施由組織實際評估過的 build 強制執行。

請將以上內容視為可供調整的起點，而非建議直接複製的設定。每一項 deny 都會犧牲部分能力，而適當的平衡取決於 repo 的資料分類。設定參考文件說明了每個 key，包括僅限 managed settings 使用的項目：[code.claude.com/docs/en/settings](https://code.claude.com/docs/en/settings)。

#### 如何衡量（針對 hooks 本身）

| 指標 | 內容 |
|---|---|
| 領先指標 | 每個核准關卡的等待時間。每項 hook 決策都會寫入 OpenTelemetry 匯出資料，附帶時間戳記，以及允許或阻擋的判定，因此可以看見各關卡的等待時間。 |
| 落後指標 | 導入 hooks 前後，違反關卡規則卻仍進入正式環境的情況，資料來自事件追蹤系統。 |

### CI/CD 整合與部署

在 CI/CD pipeline 中以非互動方式執行 Claude Code，將執行環境置於 sandbox，讓長時間執行的 agents 能安全運作，透過 MCP 整合提供部署能力，並在 agent 真正需要之前，先演練 rollback 路徑。

| 傳統 | AI-native |
|---|---|
| Pipelines 執行確定性的 scripts，凡是需要判斷的事情，都等待人類處理。例如，研判不穩定測試、撰寫 changelog，或查明 build 為何失敗。部署與 rollback 是人類在壓力下遵循的 runbooks。 | Claude 在 pipeline 中，以非互動方式執行需要判斷的步驟，並在 sandbox 中使用限定範圍的憑證。部署工具透過 MCP 提供給 agent，因此撰寫並測試變更的同一套 workflow，也能在組織依環境定義的關卡內發布與 rollback。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | PR 審查循環中的 Claude，以及作為核准關卡的 hooks，因為在自動化加速任何工作通過關卡之前，關卡必須先存在。 |
| 基礎設施 | 已安裝 claude-code-action 的 CI 平台，或任何能呼叫 `claude -p` 的 runner；透過 API 存取模型，或當流量必須納入組織雲端合約時，使用 Bedrock、Foundry 或 Vertex；部署目標的 MCP servers；以及不持有常駐正式環境憑證的 agent 工作 sandbox 設定。 |

#### 如何執行

1. 平台工程師從唯讀的判斷步驟開始。在 pipeline 工作中使用 `claude -p`，研判失敗的 build、摘要不穩定測試，或草擬 changelog。
2. 在既有關卡後方加入寫入步驟，例如修正 lint、更新產生的文件，或透過 `@claude` 標記處理審查留言。Agent 寫入的任何內容，都會透過 branch protection 以 PR 形式進入流程，agent 沒有任何途徑直接 push 至 main。
3. 執行環境置於 sandbox。Agent 工作在受網路政策約束的 containers 中執行，使用短效且限定範圍的 tokens，預設不持有正式環境憑證。
4. 透過 MCP 提供部署能力。部署、狀態查詢與 rollback 都成為工具，並依環境限定範圍，使 agent 的部署權限成為 allowlist，而非一份帶有憑證的 shell script。
5. 依環境劃分自主程度。在開發環境，agent 可自由部署。在正式環境，agent 準備發布，由發布經理授權，再由 hook 強制執行正式環境關卡。Staging 則位於兩者之間。
6. Rollback 應是 pipeline 中演練最充分的路徑：一個 agent 能執行的單一命令，且會定期在 staging 中演練。第 6 階段：維護中的完成閉環實踐方法，會在突破控制區間時呼叫這個 rollback，因此必須事先證實可用。

#### 實際樣貌（pipeline 步驟）

```yaml
- name: 研判失敗的 build
  if: failure()
  run: >
    claude -p "閱讀 out/build.log 中的 build log。找出最可能的原因，
    說明這次失敗看起來是不穩定問題還是真正的故障，
    並為 PR 討論串撰寫三行摘要。" >> triage.md
```

#### 治理考量

治理原則是：agent 可以執行到正式環境關卡之前，但不能越過它。以下控管措施會強制落實這項原則。

- Branch protection 讓 agent 寫入的任何內容都成為 PR，沒有直接進入 main 的途徑。
- 正式環境部署 hook 會阻擋發布，直到具名的發布經理授權。每次非互動式執行都使用 agent 自己的身分，因此 pipeline log 能區分哪些動作由 agent 執行，哪些由觸發它的工程師執行。
- 各環境的權限分級，決定 agent 在抵達關卡之前能做多少事情。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 不需呼叫人類處理，就能完成初步研判的 pipeline 失敗比例，資料來自 CI/CD pipeline logs。 |
| 落後指標 | DevOps Research and Assessment（DORA）指標，CI 系統與部署工具已會輸出這些資料。 |

## 第 6 階段——維護

循環完成閉合。觸發機制呼叫 Claude，呼叫路徑中不需要任何人介入，而其發現會以 `intent.md` 重新進入 pipeline。

### 維護與完成閉環

到目前為止，我們討論了如何在 SDLC 流程的每個階段加入 Claude，而且每個階段都需要人類啟動最初的步驟。然而，這個階段會將焦點轉向讓 Claude 自主執行，以完成閉環。

例如，一個持續執行的監控 agent，可以在 bug 工作單建立後，產生 `intent.md`，接著通過需求、規劃、建置、測試與審查階段。第 6 階段：維護採 headless 方式執行，並在階段之間設置獨立的信心關卡，由確定性檢查或對抗式審查 agent，決定上一階段的產出是繼續往下走，還是上報給人類。

| 傳統 | AI-native |
|---|---|
| 維護是被動回應的階段。所有工作單或事件都等待人類採取行動並重新啟動流程。凌晨 3 點觸發的警示可能被錯過，工作單可能留在 backlog 中直到有人接手，而如果另一個緊急狀況先發生，事後檢討的行動項目可能根本不會反映到 codebase。 | 控制區間突破、工作單、頻道訊息或排程等觸發條件，可以在無人介入的情況下呼叫 Claude。Claude 進行診斷，只透過設有關卡的途徑採取行動，並將發現寫成 `intent.md`，接著通過前述各階段。人類負責分流與審查工作，不再需要負責啟動它。 |

### 完成閉環

確定性 script 監看正式環境，並在突破控制區間時呼叫 Claude。監控區間突破，是說明循環如何自主運作的實用範例；本階段結尾的 [Claude Tag](https://claude.com/product/tag)（public beta）小節，則涵蓋從不同管道進來的工作。

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | `intent.md`，讓循環有可用於重新啟動的結構化輸出；由 Claude 加速的 PR 審查；作為行動邊界的 hooks；以及 CI/CD 的 rollback 路徑，最高自主層級會呼叫它。 |
| 基礎設施 | 可供偵測 script 查詢的指標儲存系統，例如 Prometheus、CI 系統的 API 或同等工具；repository 的讀取權限；在 CI 中以非互動方式執行 Claude Code 的方法，或使用 Agent SDK 建立接收 webhooks 的服務。 |

#### 如何執行

1. 服務負責人或平台工程師選擇一項具有穩定滾動基準的指標，例如 CI 測試失敗率、部署後的 5xx 比率，或 PR 週期時間。
2. 撰寫偵測 script，通常使用滾動視窗中的平均值與標準差，搭配 Western Electric 或類似規則，讓控制區間既能捕捉緩慢漂移，也能捕捉突增。Script 受到版本控制並有 unit tests；偵測完全保持確定性，不涉及模型。
3. 在受到版本控制的設定中定義回應層級，見下方 `bands.yaml`。在 1σ 時，script 只記錄；在 2σ 時，以唯讀方式呼叫 Claude 進行診斷；在 3σ 時，Claude 可以採取行動，但只能建立 PR 送入審查關卡，或觸發事先核准的 runbook。
4. 觸發層可以是 GitHub 或 GitLab 的 scheduled workflow、既有監控系統發出的 webhook，或網路內的 Cron Job。Claude 以無狀態方式執行，可以是 CI runner 上的非互動步驟，或 sandbox container 中的 Agent SDK 服務；CI/CD 實踐方法會涵蓋部署與模型存取選項。由於執行是無狀態且非互動式的，循環可以在無人啟動的情況下開始並結束。
5. Agent 依照第 1 階段：規劃的格式，將診斷寫成 `intent.md`，涵蓋異常及其證據、預期成果、受影響系統，以及任何待釐清問題。接著，這項發現就像其他工作一樣進入 pipeline。
6. 服務負責人或 on-call 工程師對佇列進行分流，將面向產品的發現交給 product owner。立即修復、排入時程，或不予處理。不予處理的決定有助於調整控制區間，並減少雜訊。
7. 修復發布後，為該事件新增 eval，參照持續執行 evals 的實踐方法，確保未來能防範此類問題。

#### 實際樣貌（例如，監控 CI 測試失敗率的 bands.yaml）

```yaml
metric: ci_test_failure_rate
baseline: rolling_30d
rules: western_electric
tiers:
  1sigma: { action: log }
  2sigma: { action: diagnose,
            tools: "Read,Grep,Bash(gh run view *)" }
  3sigma: { action: propose,
            routes: [pull_request, runbook:rollback-deploy] }
```

#### 治理考量

各層級邊界由受到版本控制的設定強制執行，並透過 permissions 與 managed settings 拒絕正式環境存取。呼叫、發現與分流決策都附帶時間戳記記錄。服務負責人負責分流與核准發現，由此產生的變更通過一般 PR 審查關卡，而 agent 可觸發的 runbooks 都已事先核准。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 從突破控制區間，到分流佇列中出現 `intent.md` 的時間，與過去從事件發生到採取事後檢討行動的時間比較。偵測 script 的 log 包含突破時間戳記與事件層級。 |
| 落後指標 | 發現轉為已合併修復的比例，將分流佇列與實際 PR 歷史比較；以及同類事件重複發生的情況。隨著修復將案例加入 eval suite，重複事件應減少。 |

#### 範例

- 當 CI 測試失敗率突破 3σ，agent 隔離不穩定測試，或建立 revert PR，再由審查關卡決定。
- 當部署後的 5xx 比率突破 3σ，且觀察視窗內有部署發生，agent 觸發既有 rollback pipeline。
- 當 PR 週期時間觸發漂移規則，agent 為工程主管撰寫報告，這顯示 harness 同樣適用於流程指標與正式環境指標。

> 偵測維持確定性。一旦突破控制區間，才呼叫 Claude，而層級決定它可以做什麼。

### 定期掃描 codebase

安全掃描是在某個時間點，使用特定模型，對 codebase 做出的判定；兩者都會過時：程式碼每週都在改變，而每一代模型都會找到前一代遺漏的漏洞。AI-native 的做法是依排程執行掃描，讓呼叫路徑中不需要人類，並將發現送入與其他 codebase 變更相同的關卡。

[Claude Security](https://claude.com/product/claude-security) 是排程掃描的代管形式。連接 GitHub repository 後，掃描會在 Anthropic 的基礎設施上使用 Claude Mythos 5 執行；每項發現都會在回報前經過驗證，並附上信心評級。建議的修補程式會在網頁版 Claude Code 中審查與套用。組織無須取得模型本身的存取權，就能獲得掃描發現。

| 傳統 | AI-native |
|---|---|
| 安全掃描是一項特定活動，在發布或稽核之前啟動。報告送入追蹤系統，接著由人類逐步處理 backlog，直到下一次掃描活動。兩次掃描之間撰寫的程式碼，只受到 PR 審查所捕捉問題的涵蓋。 | 對每個已連接的 repository，依排程使用可用的最強模型執行掃描，並在任何人讀取之前驗證發現。每項發現的處理方式與突破控制區間相同：能在一個 PR 內完成的修復，通過審查關卡；更大的項目則成為 `intent.md`。涵蓋範圍的時間基準是最近一次執行，而非第一次。 |

#### 如何開始

| 項目 | 內容 |
|---|---|
| 前置條件 | PR 審查關卡與作為核准關卡的 hooks，見第 5 階段：部署，讓發現像其他變更一樣接受審查。對超出單一 PR 範圍的發現，使用第 1 階段：規劃的 `intent.md` 格式。 |
| 基礎設施 | Claude Security 以 public beta 形式提供給 Claude Enterprise 組織。需要在目標 repositories 上安裝 Anthropic GitHub App，且使用雲端代管的 github.com；啟用 Claude Code on the Web；開啟 Extra Usage 並設定支出上限；為執行掃描的人員提供 premium seats；並由管理員在 `claude.ai/admin-settings/claude-code` 啟用功能。掃描依 Mythos 5 費率按用量計費，因此支出上限應配合 repositories 的大小與數量。 |

#### 如何執行

1. 安全主管連接 repositories，並依 repo、服務或團隊將它們組織為 projects，讓發現的責任歸屬從一開始就清楚。
2. 對最關鍵的 repositories 執行首次完整掃描，包括先前已由其他工具或較早模型掃描過的 repositories。將首次掃描視為基準。首次掃描很可能會在過去認為沒有問題的程式碼中找出問題。
3. 為每個 project 設定排程。對積極開發中的服務，每週一次是合理的預設值；若 repository 規模較大或混合多種內容，可將掃描範圍限定在某個目錄或 branch。
4. 參考信心評級對發現進行分流。不予處理時提供原因，讓決定留下紀錄，避免同一項發現在下一次執行時又被當成新問題。
5. 對範圍明確的發現，在 Claude Code on the Web 中開啟建議的修補程式、審查它，並像其他變更一樣送入 PR 審查關卡。提出修復的 agent 沒有任何途徑核准它。
6. 對超過單一修補程式範圍的問題，例如架構弱點，或跨服務重複出現的模式，依第 1 階段格式寫成 `intent.md`，從規劃開始。
7. 修復發布至正式環境後，將該漏洞類別的 eval 加入持續執行 evals 實踐方法的套件，讓引導 agent 的設定從此接受針對該類問題的測試。
8. 將發現匯出為 CSV 或 Markdown，或使用 webhooks，讓組織既有的追蹤與稽核系統繼續作為正式紀錄系統，保留在稽核人員原本預期的位置。

#### 治理考量

掃描在組織的管理控管下執行，代表要連接哪些 repositories、誰持有掃描席次，以及支出上限，都由中央統一設定。每項發現都有驗證結果與信心評級，每項不予處理的決定也都有原因，因此掃描歷史就是稽核紀錄，記載發現了什麼、修復了什麼，以及有意識地接受了什麼。

修復透過 PR 審查關卡與 branch protection 進入正式環境，而不是由掃描本身直接送入。Claude Security 補強既有的 static analysis 與相依套件掃描。確定性檢查保留在 CI 中，而模型驅動的掃描則涵蓋依賴 context、原本不在這些檢查設計範圍內的漏洞。

#### 如何衡量

| 指標 | 內容 |
|---|---|
| 領先指標 | 已連接 repositories 中設有排程的比例，以及從發現回報到修補程式進入 PR 審查關卡的時間，資料來自掃描歷史與 PR metadata。 |
| 落後指標 | 排程掃描找到的漏洞，與正式環境中發現或外部回報的漏洞之比較，資料來自事件追蹤系統；以及已經歷多次掃描的 repositories，每次掃描發現數量的趨勢。隨著修復與 evals 累積，該數量應下降。 |

### 透過 Claude Tag 讓 Claude 值班

事件也可能透過其他方式進來，例如 Slack 或 Teams 等工作通訊應用程式。事件可能是晚上 10 點出現在事件頻道、要求緊急修復的 Slack 訊息，而現在可以立即採取行動。Claude Tag 目前以 public beta 形式在 Slack 提供，讓 Claude 以自己的身分成為這些頻道的成員，因此每起新事件都有第一位回應者，而回應本身也成為循環與未來事件記憶的一部分。

對話與組織知識保留在頻道中，任何頻道成員都能引導回應並採取行動。任何團隊成員都可以即時測試假設、探索新選項與調查，而頻道歷史也提升了可稽核性。透過 MCP 存取，Claude 會驗證指標已回到基準，並在討論串中確認，再將事後檢討寫入受到版本控制的經驗紀錄檔案，供未來調查讀取。

事件並非 Claude Tag 唯一會接手的工作。無論是透過 MCP 在工作單中被標記，或在頻道中收到請求，Claude 都會以相同方式分流。小型且範圍明確的修復，以 PR 形式通過審查關卡；更大的工作則寫成第 1 階段：規劃的 `intent.md`，從此循環開始自行產生後續輸入。請參閱：[Claude Tag 如何在 Anthropic 為 CI/CD 值班](https://claude.com/blog/ai-ci-cd-on-call)。

![](https://cdn.prod.website-files.com/68a44d4040f98a4adf2207b6/6a8760aded54a2a8319cd5b9_fe6d780d.png)

頻道就是稽核軌跡：請求、診斷、人類授權與修復，都保留在處理事件的地方。

## 結語

模型與 harnesses 已變得更加先進，讓組織不僅能改造產出程式碼的方式，也能改造整個軟體開發生命週期。

這項轉型讓人類判斷持續位於流程核心，同時考量大型企業組織的治理與法規要求。

本指南彙整了 Applied AI 團隊每天為客戶實際執行的許多最佳實務，希望你覺得它是一份實用且可付諸行動的資源。

> 循環持續運作。人類判斷始終位於其上。
