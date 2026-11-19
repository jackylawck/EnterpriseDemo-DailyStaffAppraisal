# Regulatory Compliance, Information Security & AI Governance Assessment
# 法規合規、資訊安全、私隱保護及人工智能治理適用性評估報告

**Project / 專案名稱：** `EnterpriseDemo-DailyStaffAppraisal`  
**System Classification / 系統技術定性：** Deterministic Low-Code Workflow (Non-AI Rule-Based Automation) | 確定性低代碼自動化工作流（非人工智能規則引擎）  
**Governance Baseline / 治理基準：** Hong Kong SAR Jurisdiction with International ISO Alignment | 香港特別行政區法域為核心，對齊國際 ISO 管理體系標準

---

## 1. Executive Governance Statement | 治理與技術定性聲明

* **English:**  
  `EnterpriseDemo-DailyStaffAppraisal` is built strictly on deterministic conditional logic (`if`, `contains`, `int`, and deterministic SharePoint calculated formulas) with mandatory human-in-the-loop evaluation by authenticated supervisors. **The system does not utilize Machine Learning (ML), Deep Learning, Generative AI (GenAI), Large Language Models (LLMs), or automated profiling algorithms.** Consequently, AI-specific statutory regimes (such as the EU AI Act, PRC CAC algorithm regulations, and ISO/IEC 42001) are **not directly applicable** by architectural design. Instead, governance controls focus rigorously on personal data protection, access isolation, auditability, and information security under Hong Kong's **Personal Data (Privacy) Ordinance (PDPO, Cap. 486)**, **ISO/IEC 27001**, and **ISO/IEC 27701**.

* **繁體中文：**  
  `EnterpriseDemo-DailyStaffAppraisal` 完全建基於**確定性條件邏輯（Deterministic Conditional Logic）**（包括 `if`、`contains`、`int` 函數及 SharePoint 確定性計算公式），並以獲授權監工的實質人工評核為核心。**本系統並無採用任何機器學習（ML）、深度學習、生成式人工智能（GenAI）、大型語言模型（LLM）或自動化演算法畫像技術。** 因此，針對人工智能的專門監管法規（如《歐盟人工智能法案》、國家網信辦演算法／生成式 AI 規定及 ISO/IEC 42001）在本架構設計下**均不直接適用（Out-of-Scope by Design）**。本專案的合規治理重心精準聚焦於香港**《個人資料（私隱）條例》（第 486 章）**、**ISO/IEC 27001（資訊安全）**及 **ISO/IEC 27701（私隱資訊管理）**所要求之個人資料保護、權限隔離、可稽核性與資料安全控制。

---

## 2. Global Regulatory & Standards Applicability Matrix | 全球法規與國際標準適用性矩陣

| Framework / Regulation<br>法規或國際標準 | Applicability Status<br>適用性判定 | Technical & Legal Rationale<br>技術與法律依據說明 |
| :--- | :--- | :--- |
| **Hong Kong PDPO (Cap. 486)**<br>香港《個人資料（私隱）條例》 | **Directly Applicable**<br>**直接適用（核心合規基準）** | Governs the collection, accuracy, retention, security, and transparency (DPP1–DPP6) of employee names, Staff IDs, job roles, and appraisal records within Hong Kong. |
| **ISO/IEC 27001**<br>資訊安全管理體系標準 | **Aligned (Control Baseline)**<br>**直接對齊（資安控制基準）** | Enforces Role-Based Access Control (RBAC), separation of public intake vs. authenticated review, encrypted M365 transit/storage, and immutable audit logs. |
| **ISO/IEC 27701**<br>私隱資訊管理體系標準 | **Aligned (Control Baseline)**<br>**直接對齊（私隱控制基準）** | Establishes PII controller/processor accountability, data minimization (collecting only appraisal-necessary fields), and standardized PICS transparency notices. |
| **EU GDPR**<br>歐盟《通用數據保障條例》 | **Not Directly Applicable**<br>(Reference Best Practice)<br>**不直接適用（作最佳實踐參考）** | Only applies if processing EU residents' data. Notably, **Article 22 (Automated Individual Decision-Making)** is not triggered because scores are entered by human supervisors and weighted via transparent arithmetic rules. |
| **PRC PIPL**<br>中國《個人資訊保護法》 | **Not Directly Applicable**<br>(Cross-Border Note)<br>**不直接適用（跨境部署備註）** | Not applicable to local Hong Kong operations. If extended to Mainland China personnel, separate consent and cross-border transfer assessment (CAC / GBA Standard Contract) would be required. |
| **EU AI Act (Regulation (EU) 2024/1689)**<br>《歐盟人工智能法案》 | **Out-of-Scope (Non-AI)**<br>**不適用（非 AI 系統）** | While HR/employment evaluation tools using AI fall under Annex III (High-Risk AI), this workflow uses **zero AI inference**. Intentional deterministic design avoids High-Risk AI compliance overhead while preserving full algorithmic transparency. |
| **ISO/IEC 42001 (AIMS)**<br>人工智能管理體系標準 | **Out-of-Scope (Non-AI)**<br>**不適用（無 AI 模型生命週期）** | Governs AI model training, drift monitoring, and AI risk impact assessments. Not applicable as no AI models are developed, fine-tuned, or deployed. |
| **PRC CAC Regulations**<br>(Algorithm / GenAI Measures)<br>國家網信辦演算法及生成式 AI 規定 | **Out-of-Scope (Non-AI)**<br>**不適用（無演算法推薦或生成內容）** | Applies to algorithmic recommendation, deep synthesis, and generative AI services in Mainland China; irrelevant to deterministic internal HR workflows in Hong Kong. |

---

## 3. Hong Kong PDPO (Cap. 486) Six Data Protection Principles Mapping | 香港《私隱條例》六項保障資料原則對照表

| Data Protection Principle<br>保障資料原則 | System Control Implementation<br>系統架構落實措施 |
| :--- | :--- |
| **DPP1: Purpose & Manner of Collection**<br>收集目的及方式 | **Data Minimization & Transparency (資料最小化與透明度)：** Only essential appraisal fields (Staff ID, Name, Job Title, Supervisor, Ratings) are collected. A standardized **Personal Information Collection Statement (PICS)** is displayed prior to submission on both Form A and Form B. |
| **DPP2: Accuracy & Duration of Retention**<br>準確性及保留期間 | **Input Normalization & Retention Governance (輸入正規化與保留期管理)：** Staff IDs are normalized (`trim` + `toUpper`); pre-filled URLs prevent manual transcription mismatches. Records in SharePoint serve strictly as a temporary intake staging layer prior to core system entry and scheduled purging. |
| **DPP3: Use of Personal Data**<br>個人資料的使用 | **Strict Purpose Limitation (嚴格目的限制)：** Collected appraisal data is used exclusively for annual performance evaluation and core HR system reconciliation—never repurposed for unrelated profiling. |
| **DPP4: Security of Personal Data**<br>個人資料的保安 | **Identity & Storage Isolation (身份驗證與儲存隔離)：** Form A (`Anyone can respond`) acts solely as a write-only dropbox without read access to backend data. Form B requires M365 organizational authentication. Backend SharePoint lists restrict read/edit permissions strictly to authorized HR administrators and service accounts. |
| **DPP5: Information to be Generally Available**<br>資訊須在一般情況下可提供 | **Clear Policy Disclosure (明確政策披露)：** Employees and supervisors are informed of the evaluation criteria, scoring weights (`W1`/`W2`), and the substantiation rule for Criterion 3 ("Creativity & Innovation"). |
| **DPP6: Access to Personal Data**<br>查閱個人資料 | **Subject Access & Rectification Channel (查閱與更正渠道)：** Data subjects may submit data access or correction requests through the designated HR administration contact stated in the PICS notice. |

---

## 4. ISO/IEC 27001 & ISO/IEC 27701 Technical & Organizational Controls | 資訊安全與私隱技術控制措施

1. **Zero-Trust Ingress Separation (零信任入口隔離)：**  
   Frontline workers have zero direct access to SharePoint lists or Power Automate flows. Data flows strictly one-way from Microsoft Forms into SharePoint via service-account connectors.
2. **Deterministic Auditability & Non-Repudiation (確定性可稽核與不可否認性)：**  
   * Every supervisor evaluation requires M365 organizational login (`Only people in my organization can respond`), capturing authenticated user identity and UTC completion timestamps (`utcNow()`).
   * The *"No Substantiation = Zero Score"* rule (`Final_SupQ03_Score`) executes deterministically in code rather than subjective post-hoc adjustments, ensuring uniform governance across all site supervisors.
3. **Repository Sanitization & Credential Hygiene (程式碼庫脫敏與憑證隔離)：**  
   No API keys, passwords, tenant GUIDs, or production PII are hardcoded or committed to version control.

---

## 5. Standard Personal Information Collection Statement (PICS) Template | 標準《收集個人資料聲明》範本

*(Recommended to be pasted into the Form A & Form B description header to fulfill PDPO DPP1 & DPP5 requirements | 建議直接貼於問卷 A 及問卷 B 開頭說明欄，以符合香港《私隱條例》第 1 及第 5 原則之法定告知義務)*

```text
【Personal Information Collection Statement | 收集個人資料聲明】

1. Purpose of Collection (收集目的)：
The personal data provided in this form will be used solely by the Human Resources & Administration Department for annual performance appraisal, supervisory review, and updating records in the Company's core HR appraisal system.
本表格所收集之個人資料，僅供人力資源及行政部作年度工作表現評估、主管評核及錄入公司核心績效評估系統之用。

2. Classes of Transferees (資料轉移對象)：
Your data will be kept strictly confidential and disclosed only to your designated site supervisor(s), authorized HR/Administration personnel, and relevant management for evaluation processing, or where required by law.
閣下的個人資料將嚴格保密，僅會提供予閣下所屬地盤監工、獲授權之人力資源及行政人員、相關管理層作評核處理，或按法律規定作出披露。

3. Access & Correction of Personal Data (查閱及更正個人資料)：
Under the Personal Data (Privacy) Ordinance (Cap. 486), you have the right to request access to and correction of your personal data. Please contact the HR Administration Team (hr-admin@companydemo.com) for any such requests.
根據《個人資料（私隱）條例》（第486章），閣下有權要求查閱及更正所提供的個人資料。如有需要，請聯絡人力資源行政組（hr-admin@companydemo.com）。

