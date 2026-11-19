# Security & Data Privacy Policy | 資訊安全與私隱保護政策

## 1. Repository Sanitization Guarantee | 儲存庫脫敏合規聲明
* **English:** This repository serves strictly as a sanitized architectural Proof of Work (`EnterpriseDemo`). No production credentials, API tokens, Microsoft Entra ID Tenant GUIDs, internal SharePoint URLs, or personally identifiable information (PII) of real employees are stored or committed in this codebase.
* **繁體中文：** 本儲存庫僅作為企業架構之脫敏技術展示範例（`EnterpriseDemo`）。本專案之所有程式碼與文件中，均不包含任何真實系統憑證、API 金鑰、Microsoft Entra ID 租戶識別碼、內部 SharePoint 網址或真實員工個人資料（PII）。

---

## 2. Production Security Architecture Controls | 生產環境資安控制基準
When deploying this architecture in an enterprise environment, the following baseline controls (aligned with **ISO/IEC 27001**, **ISO/IEC 27701**, and **Hong Kong PDPO Cap. 486**) are enforced:
在企業生產環境部署本架構時，必須落實以下對齊 **ISO/IEC 27001**、**ISO/IEC 27701** 及 **香港《個人資料（私隱）條例》（第 486 章）** 的安全基線控制：

1. **Ingress / Storage Decoupling (入口與儲存隔離)：** Anonymous intake forms operate strictly as write-only interfaces; external respondents have zero read or query privileges on backend SharePoint lists.
2. **Authenticated Supervisory Sign-Off (監工強制身份驗證)：** Evaluation forms require corporate M365 authentication (`Only people in my organization can respond`) to ensure non-repudiation and audit logging.
3. **Least-Privilege List Governance (最小權限清單管理)：** SharePoint data repositories restrict read/write access solely to designated HR administrators and service accounts.
4. **Data Retention & Purging (資料保留與清理機制)：** Staging records in SharePoint are purged on a scheduled cycle once verified and reconciled into the core HR appraisal system.

---

## 3. Reporting a Vulnerability | 安全漏洞通報
If you identify any potential security flaw or documentation issue within this demo blueprint, please open a GitHub Issue or contact the repository maintainer at `security@companydemo.com`.  
如發現本範例架構存在任何潛在安全隱患或文件疏漏，請透過 GitHub Issue 回報或電郵至 `security@companydemo.com`。
