---
Source: https://claude.com/blog/the-ai-native-sdlc-playbook
Course: https://academy.claude.com/courses/ai-native-sdlc-playbook
---

# AI-Native SDLC 實戰手冊

如何透過 AI，逐階段轉型你的 software development lifecycle。

- Date

  2026 年 8 月 21 日

- Reading time

  46 分鐘

## Code 不再是瓶頸

組織已經開始使用 AI，以一年前難以想像的速度撰寫 code，但 code 周邊的流程並沒有以相同速度改變。

許多工程團隊仍然維持相同的 approval gates、reviews、handoffs 與 policies，使得使用像 [Claude Code](https://claude.com/product/claude-code) 這類 agentic coding solutions 所帶來的生產力提升受到阻礙。

software development lifecycle（SDLC）是讓軟體從構想到進入 production 的流程。大多數組織執行的都是相同六個階段的某種版本，涵蓋 planning、design、building、testing、deploying 與 maintaining software。傳統上，每個階段都是由不同角色負責的獨立 phase。Product managers 撰寫 requirements，technical architects 將其轉換成 designs，engineers 實作 designs，受監管企業中的 QA teams 負責驗證，release teams 負責發布，而 operations 則監控正在執行的系統。工作透過 documents、tickets 與 sign-offs 在各個 phases 之間流轉。

傳統 software development lifecycle（SDLC）為了確保每一步都有 accountability 與 control，因此流程十分繁重。然而，傳統 SDLC 的設計目標，是在「撰寫與實作 code 是最耗時且最昂貴階段」的時代最大化效率，而現在已經不是如此。PRDs、estimation rituals 與 product security reviews 的存在，都是為了在可能長達數週、數月甚至數季的 development work 中強制建立共識。

傳統 SDLC 也包含一些 controls，而這些 controls 假設每一個步驟都是由人類執行。能夠從中創造最大價值的組織，已經根據 agentic AI 現在能做到的事情重新打造流程，同時確保 humans stay in the loop。在本指南中，我們會介紹 Applied AI team 在與客戶合作時得到的經驗，說明如何在 SDLC 的每個階段內部整合 Claude，以加速 development 並讓流程運作得更快。

當 code 不再是瓶頸，而且 build phase 的執行速度快過傳統 SDLC 所允許的速度時，會出現三件事情：

- 瓶頸會移到 build phase 左右兩側的步驟。主要是 plan、review/test 與 deploy，因為這些仍然以人類速度運作。
- Controls 不再符合現實，因此變得難以執行。當 code 是人類撰寫時，逐行手動 review 很合理，但當 agents 撰寫了大部分 diff 後，這種方式就無法跟上。
- Governance 成本上升，因為 exceptions 仍然必須經由每週或每月召開一次的 meetings 與 committees 處理。



Build 已經不再是限制條件——真正的限制是它周圍以人類速度運作的步驟。以人類速度運作的 stages 長度保持不變，而 build 已縮短到數小時。

我們可以用 security bottleneck 當作例子。Security teams 的人力配置是按照人類產出速度設計的，因此當 agents 讓 code output 成倍增加時，不是 review queue 越積越多，就是 code 在未充分 review 的情況下被發布。受監管的組織無法接受任何一種結果，因此它的 security 與 policy checks 必須能跟上 agents 的速度。

為了更充分實現 agentic AI 的生產力提升，同時確保其安全性，傳統 SDLC lifecycle 必須經歷與 implementation phase 相同程度的轉型。

## 什麼是 AI-native SDLC？

AI-native SDLC 是一套重新構想的流程，它結合了舊有的 control objectives 與新的 enforcement。流程不再是線性的，而是變成 loop，並且 AI 被嵌入每一個節點。AI-native SDLC 推動自動化 handover，以及自動觸發後續 plays，藉此處理傳統 SDLC 各個 phases 之間手動且笨重的 handoff 問題。

你也可能會聽到這種轉變被稱為 agentic SDLC、AI SDLC，或簡單稱為 agentic software development——名稱不同，但描述的是同一件事情。



### AI-native SDLC 六個階段的轉變

下表呈現由 Claude 支援的 traditional SDLC 與 AI-native SDLC 兩端的差異。大多數組織會落在兩者之間的某個位置。

右側欄位中貫穿所有 stages 的核心，是 committed artifact。每個 stage 都會以寫入 version control 的 artifact 作為結尾（包括 `intent.md`、`spec.md`、`plan.md`、diff 與其 tests、包含 review findings 的 PR，以及 incident record），而下一個 stage 則從讀取這個 artifact 開始。對早期 stages 而言，.md files 是主要 artifact，因為 product owner 與 agent 都能閱讀並根據相同 file 採取行動。從 Build 開始之後，artifact 就變成 code 與相關 records。整個 commits chain 同時也是 audit trail：誰要求了什麼、agent 產生了什麼，以及誰批准了它。

所有需要 judgment 的決策仍由 humans 負責。在 agentic SDLC 的世界中，human attention 會隨著需要被 review 的 artifacts 一起轉移。

## Plays

Plays 是這份 playbook 的核心，並被分組到六個非線性的 stages（Plan、Design、Build、Test、Deploy、Maintain）中，這六個 stages 合起來涵蓋完整 lifecycle。

每個 play 都包含：

- 有什麼改變；
- 如何開始；
- 具體的 implementation steps；
- Governance considerations；以及
- 如何衡量是否有效。

這些 steps 是模組化的，不同組織可以根據自己的需求，選擇優先轉型不同 stages。每個 play 都會在「Prerequisites」中列出 dependencies，而 dependency graph 會進一步將其視覺化。

一個 stage 會以 commit 一個 artifact 作為結束，該 commit 同時啟動下一個 stage。被接受的 `intent.md` 會觸發 requirements 與 design pass，獲批准的 `spec.md` 會觸發 plan mode，被 merged 的 PR 會觸發 pipeline，而 production 中超出 control band 的事件則會寫出下一個 `intent.md`，讓 loop 繼續。

一開始，你可以手動 prompt 每一個 step，最終狀態則是一個 loop：每一個被接受的 artifact 都會觸發下一個 gate。Human attention 會集中在 gates 上，review agent 標記出的內容，而不是每個 stage 都由人類從零開始。



Plays 會列出其所屬 stage；箭頭則表示應採用它們的順序。兩者並不相同。你可以從任何 clay play 開始——沒有箭頭指向它，因此它不需要任何前置條件。對其他任何 play 而言，所有指向它的箭頭，代表你應該先採用的 plays。

### Capture as intent.md

啟動 software development process 的 `intent.md` 可以透過不同途徑進入流程。可能是一個人產生想法、一張 ticket 被建立，或 incident 透過 alert 被發現（請參閱 Stage 6: Maintenance）。

當一個人有想法時，他們會與 Claude brainstorm，並產生一份 markdown proto-spec。在傳統 SDLC 中，同一個人還必須說服 product team 的成員，請對方與自己一起撰寫這個想法，或代為撰寫。

Claude 產生的 proto-spec 是 human readable、version-controlled，並且可以立刻被下一個 stage 使用。這份 proto-spec 會被儲存為 `intent.md`。

無論 intent 是由 event trigger 還是 agent 產生，都適用相同 steps：product owner 會在 agent-written `intent.md` 被 committed 之前，先 review 並修正它。

建立這套機制是 platform 或 engineering team 的一次性工作。technical team member 需要建立 intent home，並決定誰具有 write 權限，因為 contributors 會來自組織中的不同部門。

Repository 建立之後，即使 contributors 沒有 git 經驗，也不需要直接使用 git。相反地，可以透過與 version-control system（例如 GitHub）連接的 connector，讓 Claude 從 claude.ai 或 Cowork 代表他們 commit markdown files。

#### 如何執行

1. Originator 用自己的話向 Claude 描述問題。Originator 可以描述目前做不到什麼、哪些人受到影響、改善後應該是什麼樣子，或哪些事情超出 scope。不需要使用正式語言。
2. 持續 brainstorm，直到想法具體化。Claude 會提出 analyst 會問的問題：scope、users、constraints，以及 success 應該長什麼樣子。
3. 請 Claude 使用組織的 template 將結果寫成 `intent.md`。這個 template 可以編碼成由 technical team member 設定、並經 lead 核准的 skill。內容可以涵蓋 problem、proposed outcome、affected users and systems、constraints，以及 open questions。
4. Originator 修正 Claude 誤解的任何地方。
5. 將 `intent.md` commit 到 shared home。Author 與 timestamp 也會進入紀錄，而 product owner 會從這裡接手這個 idea。

```markdown
# Intent: claims status self-service
Author: J. Ortiz (claims operations). Status: draft.

## Problem
Customers phone the contact center to ask where their claim is.
Handlers spend roughly a third of call time on status-only queries.

## Proposed outcome
Customers see claim status, next step and expected date in the portal.

## Affected users and systems
Claims handlers, portal team, claims-core API.

## Constraints
No new PII in the portal session. Existing authentication only.

## Open questions
Do third-party loss adjusters need access too?
```

#### Governance considerations

Evidence 就是 committed `intent.md`，其中列出了 author、timestamp 與完整 revision history。它會記錄在 intent home 的 git history 中。Product owner 負責 approval，而將 intent 送入 Stage 2: Design 的 accept 或 reject decision，則記錄為 merge 或 closing review。

### Requirements and design

一旦 product owner 批准後，Claude 就會取得 accepted `intent.md`，並產生 requirements and design spec。這個過程會受到組織的 [skills](https://code.claude.com/docs/en/skills) 引導，包括 brand、security、compliance 與 UX。

Product owner 會 review 該 spec，但不需要自己撰寫。這個流程的目標，是建立一份 engineering team 能夠據此 planning 的 spec，同時標出有疑慮的區域。

Front-end work 是最清楚的例子。當 `intent.md` 被接受後，product owner 可以從 `intent.md` 在 [Claude Design](https://claude.com/product/design)（beta）中建立 design mock，對 mock 進行迭代，最後匯出至 Claude Code 進行 build。

#### 如何執行

1. Product owner 在可使用組織 skills 的環境下開啟一個 session，並附上 `intent.md`。
2. Product owner 的 prompt 指向 `intent.md`、列出 constraints，並要求標記 concerns。一開始手動執行，之後再將其 codify 成 organization-level slash command。接著，讓 intent home 中 `intent.md` 的 acceptance 成為 trigger：在 merge 時觸發 non-interactive job，載入 organization skills 執行 pass，並將 `spec.md` commit 成 pull request（Stage 5: Deploy 中的 CI/CD play 會介紹這些 plumbing）。從那之後，product owner 第一次介入就直接是 review。
3. 同一位 product owner 對照原始 idea review spec。Spec 是否解決了已描述的 problem？`intent.md` 中的 open questions 是否已被回答，或被保留下來？
4. 優先處理被標記的 concerns，因為這些正是 analyst 會 escalate 的地方。Product owner 在 engineering 看到 spec 之前，先與相對應的 policy owner 解決每一個 concern。
5. 將 `spec.md` 與 `intent.md` 一起 commit。這組 files 會記錄原本提出了什麼，以及最後做了什麼 decision。
6. Product owner 決定 spec 與 intent 是否進入 build，若屬於組織定義的 higher risk 類型，則諮詢 technical lead。這個決定永遠由 human team mate 做出，而接受 spec 的動作，就是啟動 Stage 3: Build 中 plan mode play 的 trigger。

#### 實際長什麼樣子（prompt）

```markdown
Read the attached intent.md and produce a requirements and design spec for integrating it into our existing codebase. Apply the skills available to you so the plan conforms to our brand guidelines, security policies and UX standards. Document the spec fully as spec.md, ready to hand to the engineering team. Describe clearly any areas of concern, especially where you cannot satisfy contradicting policies.
```

#### Governance considerations

Live policy 不再是數週後才在 review 中被發現，而是在 spec 被撰寫時就被讀取與套用。組織的 skills 會作為 spec 的 constraints。Spec、產生 spec 的 prompt，以及當時生效的 skill versions，都會被記錄在 version control 中。Product owner 對 spec sign off，並將被標記的 concerns 路由給指定的 policy owners。

### 將 Claude Code plan mode 作為預設起點

Engineers 會以 [plan mode](https://code.claude.com/docs/en/permission-modes) 開始 Claude Code sessions，將 Stage 2: Design 核准的 `spec.md` 提供給 Claude，並讓它訪談 engineers，持續對 plan 進行迭代，直到 engineer 滿意。

#### 如何執行

1. Engineer 使用 Claude 的 plan mode 開始 session。
2. Engineer 將 `intent.md` 與 `spec.md` 提供給 Claude，要求產生 implementation plan，其中需列出會變更的 files、工作的執行順序，以及用來證明完成結果的 tests。
3. 質疑這份 plan：詢問這個 change 可能會破壞什麼、哪個 step 風險最高，以及 Claude 曾考慮但最後沒有採用哪些其他 options。
4. 持續迭代，直到一名完全沒看過對話內容的 engineer，也能只靠這份 plan 完成 implementation。
5. 將 approved plan commit 成 `plan.md`。這份 plan 會加入 audit trail，而 PR review play（Stage 5: Deploy）會檢查最終 diff 是否符合它。
6. 接受 plan，並讓 Claude 開始 implementation。如果 plan 夠扎實，implementation 通常可以一次完成。
7. 當 implementation 偏離 plan 時，在同一個 commit 中更新 `plan.md`。可以考慮使用 hook 強制確保兩者同步。

#### 實際長什麼樣子（plan.md）

```markdown
# Plan: claims status self-service (from intent.md 2026-06-02)

## Files that change
portal/src/claims/StatusPanel.tsx (new), claims-api/routes/status.py,
claims-api/tests/test_status.py

## Order of work
1. Add the status endpoint behind existing auth.
2. Panel against the endpoint.
3. Wire into the portal nav.

## Risks
The claims-core API rate-limits at 50 rps; the panel must cache.

## Proof
test_status.py covers the four claim states; screenshot matches the
approved mock.
```

#### Governance considerations

Design review 會發生在任何 code 被產生之前，此時改變方向還只需要修改一份 document。Plan mode 本身就會強制執行這件事情，因為在 engineer 接受 plan 以前，Claude 無法編輯 files。Plan 與其 revisions 都會被記錄，同時也會記錄誰接受了它。Routine changes 由 engineer 核准，而任何組織定義為 higher risk 的事情，則交由 tech lead 或 architect。

### Claude Code auto mode

Claude Code 也可以使用 auto mode。Engineer 核准 plan，並在對 plan 滿意且完成迭代之後，Claude 會自動套用每一個 change，不需要每次 edit 都出現 prompt。隨著後續 plays 中的 guardrails 逐漸成熟（調整良好的 `CLAUDE.md`、將 policy 編碼進去的 skills、封鎖 unsafe actions 的 hooks，以及 Claude 可以自行執行的 test suite），對 routine work 而言，auto-accept 會成為預設：嚴謹的 `spec.md`、小範圍的 blast radius，以及已被 tests 覆蓋的 code。

重心現在會從 user 看著 agent 每一次 edit 並 review actions，轉變成在較長的 autonomous sessions 結束後 review artifacts。Auto-accept mode 配合 worktrees 使用時，也能進一步支援個人與團隊的 parallelism，並且是讓 SDLC autonomous 運作、以及如 Stage 6: Maintenance 所述 closing the loop 的基礎。

### CLAUDE.md

[`CLAUDE.md`](https://code.claude.com/docs/en/memory) 提供 Claude 一名新進成員需要知道的 context，包括 conventions、commands、architecture，以及 team 最常遇到的 mistakes。過去存在人們腦中與 wikis 裡的 knowledge，現在變成 agent 每個 session 開始時都會讀取的 file，由整個 team 維護，並在每次錯誤發生後持續迭代。

#### 如何執行

1. 在 repo 中執行 `/init`。Claude 會根據找到的內容產生初始版 `CLAUDE.md`。
2. 將產生的 file 精簡成一名 new joiner 第一天需要知道的內容。保留 build、test 與 lint commands、真正重要的 conventions，以及 Claude 一直犯錯的項目。
3. 將 `CLAUDE.md` check into git，放在 repo root，讓整個 team 共用同一個 version，並像 code 一樣 review 其 changes。
4. 一條實用規則是：當 Claude 同一個錯誤犯兩次時，就把 correction 寫進 `CLAUDE.md`。
5. 控制在一頁以內，因為 Claude 每個 session 開始時都會讀取全部內容，任何 stale 資訊都只會占用 context 而沒有任何益處。

#### 實際長什麼樣子（CLAUDE.md）

```javascript
# Payments service

## Commands
- Build: make build
- Test: make test (unit), make itest (integration, needs docker)
- Lint: make lint (runs in CI; fix before pushing)

## Conventions
- Java 21, Spring Boot 3. No new Lombok.
- Money is always BigDecimal, never double.
- Every endpoint needs an integration test in src/itest.

## Architecture
- api/ holds REST controllers, core/ holds domain logic,
  adapters/ talks to external systems.
- Kafka events are defined in schemas/; never edit generated classes.

## Things Claude gets wrong
- Do not bump dependency versions; the platform team owns them.
- The legacy v1/ package is frozen; changes go in v2/.
```

#### Governance considerations

`CLAUDE.md` 是 version controlled，因此 agent 執行工作時依循的 instructions 都可以被 review 與 audit。Team conventions 會透過這個 file 被套用，所有 changes 都記錄在 git history 中，而 code owners 會在 PR review 中核准這些 changes。

### Skills 作為 institutional knowledge

Skills 是組織讓 institutional knowledge 具備可操作性的方式。Instructions 是明確的、version-controlled、可廣泛套用，並在 policy 改變時由中央更新。經驗法則是：需要一致套用的 institutional knowledge，寫成 skill；屬於 `CLAUDE.md` 或 prompt 的 components，就不要寫成 skill。

#### 如何執行

1. 選擇一項目前執行不一致的 knowledge。這可以是 security standard、API design convention，或 brand rule。
2. 將它寫成 skill，也就是一個包含 `SKILL.md` 的 folder，其中 frontmatter 說明何時 trigger，而 body 說明該做什麼。Engineer 從 policy owner 的 source of truth 撰寫它，並使用 Claude 協助。
3. 將 skill 放進 repo 的 `.claude/skills/<name>/`，讓它隨 code 一起發布，或透過 [plugin](https://code.claude.com/docs/en/plugin-marketplaces) 在 organization-wide 範圍散布。
4. 測試 skill 是否會 trigger。用不同方式要求 Claude 執行相關 task，並確認每次都會載入 skill。
5. Policy 改變時，更新 skill，並由 policy owner sign off 該 change。
6. Engineers 在下一個 session 中會自動取得新 version。

#### 實際長什麼樣子（.claude/skills/secure-api-review/SKILL.md）

```markdown
---
name: secure-api-review
description: Apply the API security standard. Use whenever creating or
  modifying an external-facing endpoint, reviewing API code, or
  generating an OpenAPI spec.
---
# Secure API review

When you create or change an API endpoint:
1. Authentication: every endpoint requires the gateway JWT;
   no anonymous routes outside /health.
2. Input validation: validate request bodies against the OpenAPI
   schema and reject unknown fields.
3. Audit: every state-changing endpoint emits an audit event with
   actor, action, entity and timestamp.
4. Data classification: fields tagged pii in the schema must never
   appear in logs or error messages.

Run scripts/check-endpoints.sh and include its output in your summary.
```

#### Governance considerations

Skill 是一種 control，但屬於 advisory control。它讓 Claude 在寫 code 時很可能套用 policy，但沒有任何東西強制 session 一定 comply。必須永遠成立的 policy，需要在 skill 背後再加上一個 deterministic 機制，例如 block action 的 hook，或在 PR 階段重新檢查 policy 的 review pass。Skill 讓 violations 變得罕見，而 hook 則讓 violations 幾乎不可能發生。Skill invocations 會記錄在 session traces 中，而 policy owner 會像 review code 一樣 review skill changes。

### Hooks 作為 build-time guardrails

Skill 是 advisory control，而 [hook](https://code.claude.com/docs/en/hooks) 則是背後的 deterministic layer。Claude 在 implementation 過程中的大部分 actions 都是 file edits 與 shell commands，因此 build phase 往往也是 hooks 最常觸發的地方。

Build-phase hooks 可以：

- Block 對 protected paths 的 edits，例如 generated classes 或 frozen package；
- 在 file edits 後執行 formatter 與 linter，讓 drift 永遠不會累積；
- 防止 credentials 進入 diff。

任何必須無條件成立的 skill policy，都應該用 hook 支撐。Hook 會在每個符合條件的 action 上執行，因此 build-phase hooks 應該快速，且 scope 限定於 changed file。較重的 checks，例如完整 test suite，應該放在 commit 或 PR 階段。

如果 hook 會要求 human approval，它就應該屬於 Stage 5: Deploy 的 gates，因為 build 過程中的 approval prompt 會重新把人放回所有 parallel sessions 的 critical path 上。

### Parallel sessions 與 subagents

一名 engineer 可以同時推動多個 work streams。

Parallel session 是另一個完整的 Claude Code instance，在自己的 [git worktree](https://code.claude.com/docs/en/worktrees) 中執行不同 task。每一個獨立 session 彼此完全不知道對方的存在，它們唯一共用的就是負責 steering 它們的 engineer。

[Subagent](https://code.claude.com/docs/en/sub-agents) 則是在單一 session 內執行的 scoped helper，擁有自己的 context window 與 tool limits，適合那些會在多個 tasks 中重複出現的 jobs，例如驗證 app 是否如預期運作。

Parallel sessions 提高一名 engineer 可以同時進行的 tasks 數量，而 subagents 則讓每個 session 能專注在自己的 task。Engineer 的工作，是 steering 並 reviewing 所有這些 sessions。

#### 如何執行

1. Engineer 利用 plan mode play（Stage 3: Build）所產生的 plan，將工作拆成會碰觸不同 files 的 tasks，藉此找出哪些工作是獨立的。會修改相同 files 的 tasks 則放在同一 session 中，依序執行。
2. 每個 parallel task 都建立自己的 worktree，例如在一個 terminal 執行 `claude --worktree feature-auth`，另一個則執行 `claude --worktree fix-rate-limit`。Worktree 是位於獨立 branch 上的 separate checkout，可避免 sessions 在 files 上互相衝突。
3. 一開始使用兩到三個 sessions 是合理的。實際上限取決於一個人能夠妥善 review 幾條 streams，因此只有在 review 還跟得上的情況下才增加 sessions。
4. 將重複 jobs 轉成 subagents，定義於 `.claude/agents/` 中的 markdown files。每個 subagent 都有 name、何時使用的 description，以及它可以使用的 tools。例如：在 main agent 完成後移除不必要 complexity 的 code simplifier、啟動 app 並檢查 behavior 的 verifier、探索 codebase 並回報結果而不讓 main context 被塞滿的 researcher。將 definitions check into git，讓整個 team 共用。

#### 實際長什麼樣子（.claude/agents/verifier.md）

```javascript
---
name: verifier
description: Runs the app and checks the change works before the session
  reports done
tools: Bash, Read
---
Start the app with make run. Exercise the changed behavior and the two
nearest neighboring flows. Report what you ran, what you saw, and any
behavior that does not match plan.md. Do not fix anything; report only.
```

#### Governance considerations

更多 sessions 意味著更多 output，因此 controls 必須來自 repo 中的 configuration。Hooks 與 permission settings 會套用到所有 sessions，而 session 做過的事情都會被記錄，並歸屬到執行它的 engineer。

### 給 Claude 一個 feedback loop

永遠提供 Claude 一種驗證自己工作的方式，無論是 tests、build，或 screenshot diff。Session 應該先自行檢查工作並修正錯誤，再讓 engineer 看到結果。

Feedback loop 不應該與 verifier subagent（Stage 3: Build）混淆。Feedback loop 會在整個 task 執行期間反覆運作，次數可能和工作的迭代次數一樣多。另一方面，verifier subagent 則是一種將 final check 包裝成獨立步驟的方法：當 session 認為工作已完成時，以 fresh context window 執行一次檢查。這樣 verdict 就不會受到產生 code 時那些 assumptions 的影響。

#### 如何執行

1. 如果今天檢查工作的方式需要執行一連串 commands 加上一些 environment knowledge，就把它包裝成單一 target，例如 `make test` 或 `npm test`，且失敗時必須以 non-zero exit。
2. 在 `CLAUDE.md` 的 Commands section 中列出每一個 command，並附上一個 healthy output 範例。
3. 設定一個可量化的 target，讓 Claude 可以不用詢問你就自行驗證，例如：「`test_status.py` 中所有 tests 都通過」、「screenshot 與 attached mock 一致」，或「endpoint 使用 new field 回傳 200」。
4. 對 bug fixes 而言，先寫 failing test。要求 Claude 將 bug 重現成 test，執行它，並確認它是因為你預期的原因失敗。Commit 該 test。只有在那之後，才要求 Claude 在不能修改 test 的情況下讓它通過，而 final step 中的 test-file hook 會強制這個限制。一個在 fix 前就已經存在、而且 agent 無法重寫的 test，就是 bug 已被修正的證明。
5. UI work 則使用 visual check 關閉 loop。提供 Claude browser 或 screenshot tool，提供 mock，並讓它反覆迭代：implement、screenshot、compare、adjust。兩到三輪很常見，而且每一輪結果都應該變得更好。
6. 讓 verification 成為「done」的一部分。Instruction 放在 `CLAUDE.md` 中。在回報 task 完成之前執行 tests，並顯示 output。
7. 最後，loop 本身也需要被保護，因為修 code 的 agent 不能有能力弱化用來檢查該 code 的機制。可以用 hook 在 fix task 中 block 對 test files 的 edits。另一個方法是在 review 時檢查 diff，並拒絕任何修改 test 的 change。

#### 實際長什麼樣子（CLAUDE.md verification block）

```javascript
## Verifying your work

- Build: make build (must finish with "Build succeeded")
- Test: make test (all green; never skip or delete a failing test)
- Lint: make lint (zero warnings)

Run all three before reporting any task complete, and paste the output.
If a test fails, fix the code, not the test.
```

### CI 中的 Continuous evals

Evals 是 AI-native 版本的 stage-gate QA。實際上，它是一套每當 agent configuration 改變時就會執行的 suite。當切換新 model 或重新撰寫 prompt 時，eval suite 會指出 agent 是否仍然能以相同標準完成工作。

Evals 應被視為一套持續更新的 live suite。隨著 models 改善，過去能區分品質的 cases 會失去辨識力，因此必須根據持續 monitoring 中發生的新情況加入新的 cases。

根據 use case，有些 teams 可能偏好依固定 cadence offline 執行 evals，而不是每次 change 都執行。以下 steps 針對 continuous evaluations。

#### 如何執行

1. Platform engineer 從最近的工作中收集 20 到 50 個 real tasks，以及它們預期／被接受的 outcome。
2. 將每個 task 寫成 eval，也就是 prompt 加上定義 acceptable 的 checks（tests pass、lint clean、behavior unchanged、policy followed）。
3. Suite 會以 non-interactive 方式在 CI 中依 schedule 執行，同時任何 `CLAUDE.md`、skills 或 hooks 的 change 也會觸發它，因為這些 configuration 會 steering agent，因此理應獲得和 code 相同的 regression testing。
4. 使用結果作為 configuration changes 的 gate。若 skill change 導致 pass rate 下降，就必須在 merge 前 review。
5. 每個 production incident 都應新增一個 eval，由負責該 incident 的 team 撰寫，並永久保留在 suite 中作為 regression test。

#### 實際長什麼樣子（.github/workflows/agent-evals.yml）

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
      - name: Run eval suite
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

#### Governance considerations

Evals 給 QA 一個可以跟上 agent output 的 gate。Pass-rate threshold 會被強制為 merge check，runs 會被記錄，因此 results 可以隨時間比較，而 configuration change 所屬的 team 負責核准它。

### PR review loop 中的 AI

Claude 同時會給出 review，也會接收 review。它會根據組織的 policies review incoming PRs，並自行處理自己 PR 上的 review comments。如此一來，engineers 可以把 PR review 重點放在 behavior 上，本質上就是判斷 intent 與 risk。

#### 如何執行

1. Managed Code Review service 是最快的起點。Admin 啟用它並選擇 repositories。當你需要控制 pipeline，或希望 API calls 經由自己的 cloud agreement 路由時，則透過 claude-code-action 在自己的 CI 中執行 review（CI/CD play 會介紹這些 plumbing）。
2. Tech lead 在 repo root 建立 `REVIEW.md` 作為 review policy，依照組織關心的 passes 分類：bugs 與 logical errors；security 與 vulnerabilities；與 spec（requirements play 的 `spec.md`）、implementation plan（plan mode play 的 `plan.md`）以及 design principles 的 compliance。`REVIEW.md` 也定義什麼算 Important、什麼只是 Nit，以及哪些內容應該 skip。
3. Tech lead 設定 human threshold。Findings 本身不會 approve 或 block PR，branch protection 仍然要求 code owner approval。如果 platform engineer 希望依據 findings gate merges，可以讀取 check run 發布的 severity counts，這是一份 machine-readable tally。
4. 當 reviewer 或 author 在 review comment 中 tag `@claude`，Claude 會處理 comment 並 push fix。PR thread 會同時記錄 request 與 change。這個 fix loop 透過 claude-code-action 運作。在 managed service 中，comment `@claude review` 則會要求重新執行 review。對 Claude 自己開啟的 PR，可以再往前一步，讓 Claude babysit PR 直到 merge。Teams 會將這個 loop 包裝成 custom slash command，掃描 PR 上 unresolved review comments 與 failing checks，處理它們並 push fixes，直到 PR 變成 green，只剩下等待 code owner approval。
5. Review findings 回饋到 `CLAUDE.md`。當 review 第二次標記同樣的錯誤時，就在該 review 中將 correction 加入 `CLAUDE.md`，而因為 review 也會讀取 `CLAUDE.md`，所以從下一個 PR 開始就會抓到這個錯誤。Review 也會在 change 造成 `CLAUDE.md` outdated 時提出警告。
6. 每個月 tech lead 調整一次 setup：評分 findings 以改善 reviewer，並在 `REVIEW.md` 中限制 Nit 數量。Generated paths 與任何 CI 已經 enforce 的項目都會被排除。

#### 實際長什麼樣子（REVIEW\.md）

```markdown
# Review instructions

## Passes
Run three passes and tag each finding with its pass:
- Bugs: logic errors, broken edge cases, subtle regressions
- Security: injection risks, authentication gaps, PII in logs
- Compliance: the change matches spec.md, plan.md and our design principles

## What Important means here
Reserve Important for findings that would break behavior, leak data
or breach a policy. Style and naming are nits.

## Cap the nits
Report at most five nits per review; summarize the rest as a count.

## Do not report
Generated files under src/gen/ and anything CI already enforces.
```

#### Governance considerations

Separation of duties 會被保留，因為撰寫 code 的 agent 無法 approve 自己的 code。`REVIEW.md` 中的 review policy 會套用到所有 PRs，而且 findings、fixes、ratings 與 approvals 都會記錄在 PR history 中，因此 PR 本身就是 audit record。Approval 由 human 透過 branch protection 提供，並參考 findings 做出決策。

如要了解這些 controls 在 production scale 下如何組合，請參閱 [securing an AI-native SDLC at Anthropic](https://claude.com/blog/how-anthropic-secures-its-ai-native-software-development-lifecycle)。

### Hooks 作為 approval gates

Build phase 使用 hooks 作為 guardrails，在沒有人類介入的情況下 allow 或 block actions（Stage 3: Build）。Hook 也可以要求 approval，在特定 person 核准之前暫停 action，而這正是 release gating 所需要的功能。

這個 play 被放在 Stage 5: Deploy，因為 release gate 是最清楚的案例，但 hooks 並不限於 deploy：Claude 在任何地方執行 action 時都能觸發。例如，在 Stage 3: Build，hooks 可以 block 沒有 change ticket 的 migration 與 infra edits；在 Stage 4: Test，則能在 fix task 中阻止 agent 修改 test files。

#### 如何執行

1. Engineering leadership 與 change management、compliance 一起列出必須保留的 human approval gates，例如 change management sign-off、release authorization，以及 protected paths 的 edits。
2. Platform engineer 將每個 gate 表達為 hook，也就是 Claude action 執行前會觸發的 script，並可以 allow、ask 或 block。
3. Team hooks 放在 git 中的 `.claude/settings.json`，不可妥協的 hooks 則放進由 platform 或 IT admin 管理的 managed settings，individual engineers 無法將其關閉。
4. Block 應該能解釋原因，因此當 hook 阻止 action 時，Claude output 中會同時顯示原因與取得 approval 的途徑。

#### 實際長什麼樣子（.claude/settings.json）

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

#### Gate 本身（.claude/hooks/production-gate.sh）

```bash
#!/bin/bash
# Production deploys require a named release authorization
cmd=$(jq -r '.tool_input.command' < /dev/stdin)
if [[ "$cmd" == *"deploy"* && "$cmd" == *"production"* ]]; then
   if [ -z "$RELEASE_APPROVAL" ]; then
     echo "Production deploys need a release authorization." >&2
     exit 2 # exit 2 blocks the action; the message goes to Claude
   fi
fi
exit 0
```

#### Governance considerations

Hooks 就是 approval gates。Gate condition 每一次、對每一個人都會被 enforce。Allow 與 block decisions 會和 timestamp 一起被記錄。Gate 也定義了什麼算 approval，無論是 approved change ticket，或 release manager 的 sign-off。

### CI/CD integration 與 deployment

在 CI/CD pipeline 內以 non-interactive 方式執行 Claude Code，將 execution sandbox 化，讓 long-running agents 能安全執行，透過 MCP integrations 暴露 deployment，並在 agent 真正需要使用 rollback path 之前先演練它。

#### 如何執行

1. Platform engineer 從 read-only judgment steps 開始。在 pipeline job 中使用 `claude -p`，處理 failed build triage、summarize flaky test，或草擬 changelog。
2. 在現有 gates 之後加入 write steps，用來處理例如 fix lint、update generated docs，或透過 `@claude` mentions 處理 review comments 等 jobs。任何 agent 寫入的內容都必須透過 branch protection 以 PR 方式進入，而 agent 沒有任何直接 push 到 main 的路徑。
3. Execution 必須 sandboxed。Agent jobs 在受 network policy 管理的 containers 中執行，使用 short-lived scoped tokens，且預設不持有 production credentials。
4. 透過 MCP 暴露 deployment。Deploy、status 與 rollback 會成為 tools，並依 environment 限定 scope，因此 agent 的 deployment powers 會是 allowlist，而不是一支帶 credentials 的 shell script。
5. 根據 environment 分級 autonomy。在 development，agent 可以自由 deploy。在 production，agent 準備 release，而 release manager 負責 authorize，並由 hook enforce production gate。Staging 則位於兩者之間。
6. Rollback 應該是 pipeline 中演練最多的 path，一條 agent 可以執行的 single command，並定期在 staging 中 exercise。Closing the loop play（Stage 6: Maintenance）會在 control band breach 時呼叫這個 rollback，因此必須事先證明它能正常工作。

#### 實際長什麼樣子（pipeline step）

```markdown
- name: Triage failed build
  if: failure()
  run: >
    claude -p "Read the build log at out/build.log. Identify the most
    likely cause, say whether the failure looks flaky or real, and write a
    three-line summary for the PR thread." >> triage.md
```

#### Governance considerations

核心治理原則是：agent 可以一路行動到 production gate，但無法跨過它。以下 controls 會 enforce 這項原則。

- Branch protection 會把 agent 寫入的任何東西都轉成 PR，不存在直接進入 main 的路徑。
- Production deploy hook 會 block release，直到指定的 release manager authorize。每個 non-interactive run 都以 agent 自己的 identity 執行，因此 pipeline log 能清楚區分 agent 做了什麼，以及觸發它的 engineer 做了什麼。
- Per-environment permission tiers 會設定 agent 在抵達 gate 前能執行到什麼程度。

### Maintenance 與 closing the loop

到目前為止，我們討論的是如何將 Claude 加入 SDLC process 的每一個 stage，每個 stage 都需要由 human 啟動初始 steps。不過這個 stage 會將焦點轉向 Claude 的 autonomous running，用來 closing the loop。

例如，一個 continuously running monitoring agent 可以在 bug ticket 被建立後，自動建立 `intent.md`，接著依序流經 requirements、plan、build、test 與 review phases。Stage 6: Maintenance 以 headless 模式執行，各 stages 之間有 independent confidence gate，由 deterministic check 或 adversarial reviewing agent 判斷上一個 stage 的 output 是否可以繼續，還是需要 escalate 給 human。

### Closing the loop

Deterministic script 會監看 production，並在 control band 被突破時 invoke Claude。監控 breach 是 autonomous loop pattern 的一個有用範例，而本 stage 最後的 [Claude Tag](https://claude.com/product/tag)（public beta）section，則會介紹透過不同 channels 進入的工作。

#### 如何執行

1. Service owner 或 platform engineer 選擇一個具有穩定 rolling baseline 的 metric，例如 CI test failure rate、post-deploy 5xx rate，或 PR cycle time。
2. 他們撰寫 detection script，通常是 rolling window 的 mean 與 standard deviation，加上 rules（Western Electric 或類似規則），讓 bands 不只能抓 spikes，也能抓 slow drift。Script 必須 version controlled 且 unit tested，而 detection 全程保持 deterministic，不涉及任何 model。
3. 在 version-controlled config（如下方 `bands.yaml`）中定義 response tiers。1σ 時 script 只 log；2σ 時 invoke Claude 進行 read-only diagnosis；3σ 時 Claude 可以採取 action，但只能透過開啟 PR 進入 review gate，或觸發 pre-approved runbook。
4. Trigger layer 可以是 GitHub 或 GitLab 的 scheduled workflow、來自現有 monitoring stack 的 webhook，或 network 內部的 Cron Job。Claude 以 stateless 方式執行，可以是 CI runner 上的 non-interactive step，也可以是 sandboxed container 中的 Agent SDK service，而 CI/CD play 會涵蓋 deployment 與 model-access options。因為 run 是 stateless 且 non-interactive，因此 loop 可以在沒有人啟動的情況下開始與結束。
5. Agent 會依照 Stage 1: Plan format 將 diagnosis 寫成 `intent.md`，涵蓋 anomaly 與其 evidence、proposed outcome、affected systems，以及任何 open questions。從這裡開始，finding 會像其他任何事情一樣進入 pipeline。
6. Service owner 或 on-call engineer triage queue，並將 product-facing findings 路由給 product owner。Fix now、schedule 或 dismiss。Dismissals 會用來調整 bands，並協助降低 noise。
7. Fix ship 後，為該 incident 新增一個 eval（continuous evals play），確保這類問題未來受到保護。

#### 實際長什麼樣子（例如監控 CI test failure rate 的 bands.yaml）

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

#### Governance considerations

Tier boundaries 由 version-controlled config enforce，並透過 permissions 與 managed settings 拒絕 production access。Invocations、findings 與 triage decisions 都會加上 timestamp 記錄。Service owner 負責 triage 與 approve findings，產生的 changes 仍然會通過正常 PR review gate，而 agent 可以觸發的 runbooks 都已事先批准。

#### 範例

- 當 CI test failure rate 突破 3σ，agent 會 quarantine flaky test 或開啟 revert PR，並由 review gate 決定。
- 當 post-deploy 5xx rate 在 deployment 發生的時間 window 內突破 3σ，agent 會觸發既有 rollback pipeline。
- 當 PR cycle time 觸發 drift rule，agent 會替 engineering leadership 寫一份 report，證明這套 harness 同樣可以處理 process metrics，而不只是 production metrics。

### Recurring codebase scans

Security scan 是在某個特定 model 與某個時間點，針對 codebase 做出的判斷，而兩邊都會過時：code 每週都在變，新一代 model 也會發現上一代 model 找不到的 vulnerabilities。AI-native 的答案，是按照 schedule 自動執行 scan，讓 human 不必位於 invocation path 中，並將發現的內容透過與其他 codebase changes 相同的 gates 處理。

[Claude Security](https://claude.com/product/claude-security) 是 scheduled scanning 的 hosted 形式。連接 GitHub repository 後，scans 會在 Anthropic infrastructure 上使用 Claude Mythos 5 執行，每一個 finding 都會在回報前被驗證，並附上 confidence rating。Suggested patches 會在 Claude Code on the web 中 review 與套用。Organization 不需要自行存取 model，也能取得 findings。

#### 如何執行

1. Security lead 連接 repositories，並依 repo、service 或 team 將它們組織成 projects，讓 finding ownership 一開始就清楚。
2. 對最 critical repositories 執行第一次 full scan，包括過去曾被其他 tools 或較早 models 掃描過的 repositories。把 first scan 當作 baseline。第一次 scan 很可能會在原本被視為 clean 的 code 中找到 findings。
3. 依 project 設定 schedule。對持續開發中的 services 而言，每週一次是合理的預設。如果 repository 很大或內容混合，則將 scans scope 限制在某個 directory 或 branch。
4. 在知道 confidence rating 的情況下 triage findings。Dismiss 時附上 reason，讓 dismissal 被記錄，並確保相同 finding 下一次 scan 時不會再次被當成 new finding。
5. 對 bounded finding，在 Claude Code on the Web 中開啟 suggested patch，review 後透過 PR review gate 處理，和其他 change 一樣。提出 fix 的 agent 沒有任何方式 approve 自己的 fix。
6. 對任何超出單一 patch 範圍的事情，例如 architectural weakness，或跨 services 重複出現的 pattern，依照 Stage 1 format 寫成 `intent.md`，並從 Plan 開始。
7. Fix release 到 production 後，為該 vulnerability class 新增一個 eval 到 continuous evals play 的 suite 中，讓 steering agent 的 configuration 從此會針對該 vulnerability class 接受測試。
8. 將 findings 匯出成 CSV 或 Markdown，或使用 webhooks，讓組織既有 tracker 與 audit systems 繼續作為 system of record，因為那是 auditors 原本就預期資料所在的位置。

#### Governance considerations

Scan 在 organization 的 admin controls 下執行，也就是 connected repositories、誰擁有 scan seat，以及 spend limit 都由中央設定。每個 finding 都有 validation result 與 confidence rating，每個 dismissal 都會有 reason，因此 scan history 本身就是一份 audit record，記錄哪些問題被找到、哪些被修正，以及哪些是經過有意識的判斷後接受的。

Fixes 會透過 PR review gate 與 branch protection 進入 production，而不是由 scan 本身直接發布。Claude Security 是 existing static analysis 與 dependency scanning 的補強。Deterministic checks 繼續留在 CI，而 model-driven scan 則負責那些 deterministic checks 本來就不擅長找到的 context-dependent vulnerabilities。

### 使用 Claude Tag 讓 Claude on call

Incidents 也可能透過其他方式進入，例如 Slack 或 Teams 等 workplace communication apps。一個 incident 可能長得像晚上 10 點 incident channel 中的一則緊急 fix Slack message，而現在它可以立即被處理。Claude Tag（目前 public beta 可在 Slack 使用）會讓 Claude 以自己的 identity 成為這些 channels 的成員，因此每個新 incident 都會立刻獲得 first responder，而 response 本身也會成為未來 incidents 的 loop 與 memory 一部分。

Conversation 與 institutional knowledge 都會留在 channel 中，channel 內任何人都能引導並採取 action。任何 team member 都可以即時測試 hypotheses、探索新 options 與進行 investigation，而 channel history 則讓整個流程更具 auditability。Claude 可以透過 MCP 驗證 metric 已恢復 baseline，並在 thread 中確認，接著將 post-mortem 寫進 version-controlled lessons file，讓未來 investigations 可以讀取。

Incidents 並不是 Claude Tag 唯一會處理的工作。當它透過 MCP 在 ticket 中被 tagged，或在 channel 中收到要求時，Claude 會以相同方式 triage work。小型且邊界明確的 fix 會透過 review gate 以 PR 進入，而較大的工作則會寫成 Stage 1: Plan 的 `intent.md`，此時 loop 就開始自我 feeding。請參閱：[how Claude Tag runs on-call for CI/CD at Anthropic](https://claude.com/blog/ai-ci-cd-on-call)。



Channel 就是 audit trail：request、diagnosis、human authorization 與 fix 都會保留在 incident 被處理的地方。

## 結語

Models 與 harnesses 已經變得更加先進，讓組織不只能改變產生 code 的方式，也能改變整個 software development lifecycle。

這樣的 transformation 讓 human judgement 仍然位於流程核心，同時也納入大型 enterprise organizations 所需要的 governance 與 regulation requirements。

這份指南整合了 Applied AI team 每天替客戶實際執行的許多 best practices，希望你會覺得它是一份實用且能直接採取行動的資源。