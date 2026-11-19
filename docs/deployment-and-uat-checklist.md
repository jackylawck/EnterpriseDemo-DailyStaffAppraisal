# Deployment Guide & End-to-End UAT Verification Matrix
# 部署實施指引與端到端使用者驗收測試（UAT）清單

This guide outlines the standardized deployment sequence and User Acceptance Testing (UAT) scenarios required before releasing the workflow to frontline construction sites.  
本文件提供本工作流的標準化部署順序，以及正式推展至地盤前線使用前必須通過的使用者驗收測試（UAT）矩陣。

---

## 1. Deployment Sequence | 標準部署步驟

1. **Provision SharePoint Lists (建立 SharePoint 資料庫)**
   * Create `Supervisors` list and populate exact supervisor display names alongside corporate M365 emails.
   * Create `DailyStaffAppraisal` list with numeric columns (`Q01–Q15` for both self and supervisor ratings) and the 4 Calculated Columns (`TotalScore`, `Percentage`, `AverageScore_5Pt`, `Grade`).
2. **Configure Microsoft Forms & PICS Notice (設定雙問卷與私隱聲明)**
   * Embed the bilingual **Personal Information Collection Statement (PICS)** in the header description of both Form A and Form B.
   * Verify Form A is set to `Anyone can respond` and Form B is restricted to `Only people in my organization can respond`.
   * Generate Form B's pre-filled URL template to extract exact question GUIDs.
3. **Import & Bind Power Automate Flows (配置雙自動化流程)**
   * Configure `EnterpriseDemo_Appraisal_01_WorkerToSupervisor` with `Clean_StaffID`, `Auto_TemplateType`, null-safe `Q11–Q15` casting, and URI-encoded `Supervisor_Link`.
   * Configure `EnterpriseDemo_Appraisal_02_SupervisorToAdmin` with `Final_SupQ03_Score` zero-score substantiation enforcement and single-item `Get item` retrieval prior to sending the admin summary email.
4. **Access Control Hardening (權限收緊與隔離)**
   * Restrict `DailyStaffAppraisal` list permissions exclusively to HR Administrators and the Power Automate service connection account.

---

## 2. End-to-End UAT Verification Matrix | 端到端驗收測試矩陣

| Test ID | Test Scenario<br>測試場景 | Input Condition<br>測試輸入條件 | Expected System Behavior<br>預期系統執行結果 | Status |
| :--- | :--- | :--- | :--- | :---: |
| **UAT-01** | **W2 Supervisory Track**<br>工頭／助理工頭完整流程 | Job Role = `工頭`; completes Sections 1–4; Supervisor enters valid Q03 proof & scores | Template auto-set to `W2`; all 15 items ingested; `TotalScore` calculated out of `150`; Grade (`A–E`) assigned; admin notified | `[ ]` |
| **UAT-02** | **W1 General Worker Track**<br>一般工種分支跳過驗證 | Job Role = `雜工`; skips Section 3 (`Q11–Q15` blank) | Flow 1 casts `Q11–Q15` to `0` without runtime errors; Template auto-set to `W1`; `TotalScore` calculated out of `100` | `[ ]` |
| **UAT-03** | **Q03 Zero-Score Rule**<br>創造力「無實證即零分」防呆 | Supervisor rates Q03 = `5`, but enters `無` / `N/A` / whitespace in justification | Flow 2 overrides `上司評分Q03` to **`0`**; `TotalScore` deducts the unsubstantiated points; audit note preserved | `[ ]` |
| **UAT-04** | **Staff ID Normalization**<br>員工編號空格與大小寫容錯 | Worker enters `  test01  ` in Form A; Supervisor submits pre-filled Form B | `Clean_StaffID` normalizes to `TEST01`; OData query matches exact SharePoint record without duplicate creation | `[ ]` |
| **UAT-05** | **Unauthorized Form B Access**<br>未登入帳號嘗試開啟問卷 B | External / incognito browser opens Form B pre-filled URL | Blocked by Microsoft Entra ID authentication prompt (`Only people in my organization can respond`) | `[ ]` |
