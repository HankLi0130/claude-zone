---
paths:
  - "**/*_test.go"
---

# 測試慣例

## 共用原則

- 相同測試流程的多情境使用 table-driven tests，搭配 `t.Run`；名稱描述情境，不用編號。
- 不為覆蓋率測試單純的 getter / setter；優先測試驗證規則、錯誤分流、邊界條件與併發行為。
- 失敗訊息須指出預期值與實際值。
- 靜態測試資料放在測試所在目錄的 `testdata/`。

## 單元測試 (Unit tests)

- 與被測程式同目錄、同 package，檔名為 `<檔名>_test.go`。
- 不得依賴外部網路或真實資料庫。

## 整合測試 (Integration tests)

- 統一放在專案頂層 `tests/integration/`，使用 `package integration_test`，檔名為 `<功能>_test.go`。
- 使用真實資料庫的測試歸類於整合測試，僅使用獨立測試資料庫。
- 在 `testing.Short()` 時以 `t.Skip()` 跳過；正常執行時，必要依賴不可用應使測試失敗。
- 測試資料須隔離並清理，不得依賴其他測試的執行順序。