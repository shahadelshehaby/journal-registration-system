# 🎓 University of Dubai — Journal Papers Registration System (JPRS)
## Product Requirements Document · v1.0

---

> **Document Status:** Draft — For Review  
> **Version:** 1.0  
> **Date:** July 2026  
> **Prepared by:** Research Affairs  
> **Audience:** IT Dept  
> **Classification:** Confidential — Internal Use Only  
> **Companion System:** Conference Registration System (CRS) PRD v2.0 — JPRS is designed as a sibling system, sharing the same platform architecture, role model, and approval philosophy.

---

## 📋 Table of Contents

1. [Executive Summary](#1-executive-summary)
2. [Problem Statement & Current-State Analysis](#2-problem-statement--current-state-analysis)
3. [Goals & Success Metrics](#3-goals--success-metrics)
4. [Stakeholders & User Roles](#4-stakeholders--user-roles)
5. [System Architecture Overview](#5-system-architecture-overview)
6. [Functional Requirements](#6-functional-requirements)
   - 6.1 [Module 1: Authentication & Profile Management](#61-module-1-user-authentication--profile-management)
   - 6.2 [Module 2: Journal Paper (APC) Application Form](#62-module-2-journal-paper-apc-application-form)
   - 6.3 [Module 3: Application Approval Workflow](#63-module-3-application-approval-workflow)
   - 6.4 [Module 4: PRF Auto-Generation (Article Processing Charges)](#64-module-4-purchase-requisition-form-prf-auto-generation-article-processing-charges)
   - 6.5 [Module 5: Dean's Budget Management & Tracking](#65-module-5-deans-budget-management--tracking)
   - 6.6 [Module 6: Dashboard & Analytics](#66-module-6-dashboard--analytics)
7. [Post-Publication Compliance Module](#7-post-publication-compliance-module)
8. [Non-Functional Requirements](#8-non-functional-requirements)
9. [GitHub Repository Structure](#9-github-repository-structure)
10. [Implementation Roadmap](#10-implementation-roadmap)
11. [Core Data Model](#11-core-data-model-entity-overview)
12. [UI/UX Design Guidelines](#12-uiux-design-guidelines)
13. [Creative & AI Enhancement Suggestions](#13-creative--ai-enhancement-suggestions)
14. [Risks & Mitigations](#14-risks--mitigations)
15. [Acceptance Criteria for Go-Live](#15-acceptance-criteria-for-go-live)
16. [Glossary](#16-glossary)
17. [Document Sign-Off](#17-document-sign-off)

---

## 1. Executive Summary

The University of Dubai (UD) currently manages faculty journal paper Article Processing Charges (APC) — the fees publishers charge to publish an accepted paper (typically open-access, Scopus-indexed journals) — through a fully **manual, paper-based process**. Faculty members complete a Word-based request, which is routed through multiple approvers over email before manual data entry into Excel spreadsheets and a separate, manually prepared Purchase Requisition Form (PRF). Because APC funding is drawn from each **College Dean's own budget allocation** rather than a centralised research fund, there is currently no reliable, real-time way to see how much of a Dean's budget has been committed or spent at any point in the academic year.

The **Journal Papers Registration System (JPRS)** is a purpose-built, web-based platform — a sibling system to the Conference Registration System (CRS) — that will digitise, automate, and intelligently manage this end-to-end workflow: from initial faculty submission of an accepted journal paper, through the same multi-tier approval chain used across UD's research systems, automated PRF generation for the APC payment, and **dedicated, real-time tracking of each Dean's budget** consumption.

> **Strategic Objective:** Reduce APC request processing time from an average of 10–15 working days to under 3 working days, eliminate manual data re-entry, give each Dean (and their approval chain) live visibility into their own budget's committed and remaining balance, and provide leadership real-time insight into publication output, Scopus/ranking quality, and associated APC expenditure across all three colleges.

---

## 2. Problem Statement & Current-State Analysis

### 2.1 Current Workflow Pain Points

- Faculty must hand-fill and route an APC request/PRF through multiple departments via email and printed forms.
- There is no automated notification system; approvers are unaware of pending requests without manual follow-up.
- No central visibility: Deans cannot see, in real time, how much of their own budget has already been committed to APC payments this academic year — overspend is often discovered only at year-end reconciliation.
- No shared system of record between the Journal APC process and the university's other research systems (e.g. CRS), leading to inconsistent reporting and duplicated administrative effort.
- PRF documents must be separately prepared and manually routed through a second approval chain, duplicating effort already captured in the paper/journal submission.
- Historic data is locked in disconnected Excel files, making trend analysis (publication output, Scopus compliance, spend per college) manual and inconsistent.
- No systematic tracking of whether an approved, funded paper is later used for university visibility/promotion (e.g. no equivalent of a "compliance" step once the paper is published).

---

## 3. Goals & Success Metrics

### 3.1 Primary Goals

1. Eliminate all paper-based and email-based journal APC approval workflows.
2. Automate the complete approval chain with in-system notifications and email alerts for both the journal paper application and PRF/APC payment processing.
3. Auto-populate the PRF from the approved journal paper application, eliminating duplicate entry.
4. Provide **dedicated, separate tracking of each College Dean's budget** — allocated, committed, and spent — distinct from any centralised research budget, with real-time balance visibility at every approval stage.
5. Provide a real-time executive dashboard accessible to Dean, Director of Research, VP Academic Affairs, and UD President.
6. Maintain a searchable, auditable historical record of all journal paper applications, their APC payments, and their outcomes.
7. Support post-publication compliance tracking (LinkedIn/university visibility announcement) once the paper is published, mirroring the CRS post-conference compliance model.

### 3.2 Success Metrics (KPIs)

| KPI | Baseline | Target (12 months post-launch) |
|---|---|---|
| Average approval cycle time | 10–15 working days | ≤ 3 working days |
| Manual data entry hours per application | ~40 minutes | 0 minutes |
| Application submission errors | ~30% (missing docs/invoice) | < 5% |
| PRF generation time | 30 minutes | < 5 minutes (auto-fill) |
| Dean's budget balance visibility | Not tracked (year-end only) | Real-time, always current |
| Management report generation | 4–8 hours manual | Real-time, self-service |
| Faculty satisfaction score | N/A | ≥ 4.2 / 5.0 |
| On-time publication announcement compliance | ~0% (not tracked) | ≥ 85% |
| Budget overrun incidents (Dean's budget exceeded without prior escalation) | Undetermined | 0 |

---

## 4. Stakeholders & User Roles

### 4.1 Stakeholder Map

> Roles mirror the Conference Registration System (CRS) exactly, so faculty and approvers experience one consistent model across both systems. Responsibilities below are adapted to the journal/APC context.

| Role | Access Level | Primary Responsibilities in JPRS |
|---|---|---|
| **Faculty Member** | Applicant | Submit journal paper (APC) application, upload documents, track own requests, view PRF, complete post-publication compliance task. |
| **College Dean** (Engineering & IT / Business / Law) | Approver — Level 1 | Review applications from own college, approve/reject/comment, **check and commit against own College's Dean's Budget**, view college-level budget dashboard. |
| **Director of Research** | Approver — Level 2 | Review all applications post-Dean, manage research committee stage, flag Scopus/ranking compliance. |
| **VP of Academic Affairs** | Approver — Level 3 | Final academic sign-off before President, view cross-college analytics and budget summaries. |
| **UD President** | Approver — Level 4 (Application) / Level 5 (PRF) | Final approval, dashboard overview, digital signature, executive summary reports. |
| **Finance Department** | PRF Approver | Review and approve PRF budget lines, **confirm the request is within the relevant College Dean's remaining budget balance**, release funds/settle APC payment to publisher. |
| **Procurement Department** | PRF Final Stage | Receive approved PRF, process publisher/vendor payment for the APC invoice, update payment status. |
| **Research Committee** | Advisory | Add comments/pending issues before Dean stage (mirrors the CRS advisory stage). |
| **System Administrator** | Admin | Manage users, roles, academic year configuration, **Dean's Budget allocations**, notification templates, audit logs. |
| **HR Department** | Observer (limited) | Receive automated notifications of faculty publication records for use in promotion, tenure, and annual review documentation. |

---

## 5. System Architecture Overview

### 5.1 Technology Stack Recommendations

| Layer | Technology / Approach |
|---|---|
| **Frontend** | React.js (TypeScript) with Tailwind CSS. Responsive design supporting desktop and tablet. Role-based UI rendering. Shared component library with CRS for visual and behavioural consistency. |
| **Backend** | Node.js / Express.js REST API, or Django (Python) — to be confirmed with IT team, ideally the same stack as CRS to allow shared services (auth, notifications, audit). |
| **Database** | PostgreSQL — relational model for structured approval chains, audit logs, form data, and **dedicated Dean's Budget ledger tables**. |
| **Authentication** | OAuth 2.0 / SAML 2.0 integration with existing UD Active Directory / Microsoft 365 SSO. MFA enforced for all approver roles. Shared identity/session model with CRS where feasible. |
| **File Storage** | Supabase (or Azure Blob Storage) for uploaded documents (acceptance letters, manuscripts, invoices). Version-controlled with access logs. |
| **Email Service** | Microsoft Exchange integration or SendGrid for automated notification emails with deep-link tokens. |
| **Digital Signature** | DocuSign API integration (or Adobe Sign) for binding electronic signatures on approval records. |
| **Hosting** | Azure Government / on-premise UD data centre per institutional policy. TLS 1.3 in transit, AES-256 at rest. |
| **Version Control** | GitHub (private repository under UD organisation). GitFlow branching strategy. |
| **CI/CD** | GitHub Actions for automated testing, linting, and deployment pipelines. |

### 5.2 Architecture Note

> JPRS follows the same **three-tier architecture** as CRS: (1) a React SPA served via CDN / Azure Static Web Apps, (2) a stateless REST API layer with JWT token validation, and (3) a PostgreSQL database with read replicas for dashboard queries. All tiers are deployed within UD's private VNET with WAF protection. Where practical, JPRS and CRS should share authentication, notification, audit, and reporting services to reduce duplication and give leadership a **unified research-systems view**, while keeping each system's domain data (conference vs. journal/APC) and **budget ledgers fully separate**.

---

## 6. Functional Requirements

### 6.1 Module 1: User Authentication & Profile Management

#### FR-AUTH-001 — Single Sign-On
Faculty and staff must authenticate via UD's existing **Microsoft 365 SSO**. No separate password registration. All roles are provisioned by the System Administrator.

#### FR-AUTH-002 — Role-Based Access Control (RBAC)
- Each user is assigned exactly one primary role (see Section 4). Roles determine visible menu items, accessible records, and available actions.
- Approvers can only see applications assigned to their approval stage.
- Faculty can only view and edit their own applications.
- Deans can only view and commit against **their own college's** Dean's Budget.
- Admins have read access to all records and write access to configuration tables, including budget allocation.

#### FR-AUTH-003 — Faculty Profile Auto-Population
On first login, the system auto-populates the faculty profile from Active Directory:
- Full Name, Employee ID, College affiliation, Academic rank, Email address.
- Faculty confirm.
- This profile data becomes the auto-filled **"Author"** field on every journal paper application (see 6.2).

---

### 6.2 Module 2: Journal Paper (APC) Application Form

#### FR-APP-001 — Form Sections

The digital application form captures all fields structured into logical sections:

| # | Section | Fields |
|---|---|---|
| **A** | Applicant Information | Full name (auto), Employee ID (auto), College (auto), Academic rank (auto), Contact email (auto), Submission date (auto). |
| **B** | Paper Details | **Paper Title**, **Author** (auto pre-filled — the submitting faculty member's name), **Co-authors' names and affiliations** (repeatable list — each entry: name, affiliation/institution, is UD-affiliated Yes/No). |
| **C** | Journal Details | **Journal Title**, **Is it Scopus indexed?** (Yes / No / Pending Verification), **Journal Ranking** (e.g. Scimago Quartile Q1–Q4, Impact Factor / SJR score, or ranking tier as configured by Admin). |
| **D** | Eligibility Checklist | Probationary period completed (Yes/No, if applicable), Paper formally accepted for publication (Yes/No), "University of Dubai" appears as an author affiliation in the paper (Yes/No), Journal is peer-reviewed & Scopus-indexed (Yes/No). **All applicable items must be Yes to proceed**; a "No" on Scopus indexing routes to a Dean waiver/justification step instead of a hard block. |
| **E** | Document Uploads | Acceptance letter/email from the journal (PDF, required), Manuscript / accepted paper draft (PDF, required), Proof of Scopus indexing and/or journal ranking (PDF/screenshot, required), Official APC invoice from the publisher (PDF, required), Co-author affiliation confirmation (optional). |
| **F** | Fees & Financial Estimate | **Article Processing Charge — APC (AED)**, Additional publication charges if any (e.g. colour figures, open-access surcharge, page charges) (AED), **Total (auto-calculated)**, Funding source (auto-populated: *"Dean's Budget — [College Name]"*). |

#### FR-APP-002 — Smart Validation
- Section D eligibility: if any required answer is **"No"** (other than Scopus indexing, which routes to waiver), the form displays an inline warning and **prevents submission**, showing which requirement is unmet and the relevant policy reference.
- All required document uploads must be present before the Submit button is enabled, including the APC invoice.
- Financial totals auto-calculate in real time as fields are filled.
- **Live Dean's Budget check**: as soon as the total fee is entered, the form displays the current available balance of the relevant College's Dean's Budget (read-only indicator) so faculty and the Dean have visibility before submission — see Module 5.

#### FR-APP-003 — Save as Draft
Faculty can save the form at any point and return to complete it. Drafts are retained for **90 days**. The system sends a reminder email at 7 days and 3 days before expiry.

#### FR-APP-004 — Application Reference Number
Upon submission, the system auto-generates a unique reference number in the format:

```
JPRS-[YEAR]-[COLLEGE CODE]-[SEQUENTIAL NUMBER]
Example: JPRS-2026-CEIT-0007
```

This reference is displayed prominently and included in all notification emails.

---

### 6.3 Module 3: Application Approval Workflow

#### FR-WF-001 — Approval Chain Sequence

The approval workflow follows the same strict **sequential chain** used in CRS. Each stage must be completed before the next is triggered:

| Stage | Approver | SLA Target | Actions Available |
|---|---|---|---|
| **1** | Dean of College (CEIT / Business / Law) | 2 working days | Approve, Reject, Return to faculty with comments, Request additional information, Delegate to College Research Committee for advisory review. **Approval provisionally commits the fee amount against the Dean's Budget** (see Module 5). |
| **1A (Optional Advisory Stage)** | Research Committee (College-level Advisory Review) | 2 working days | Provide advisory feedback, Add recommendations, Highlight pending issues (e.g. journal quality/predatory concerns), Request clarifications through Dean. No direct approval/rejection authority. Request returns to Dean after review. |
| **1B (Post-Advisory Review)** | Dean of College (CEIT / Business / Law) | 2 working days | Review Research Committee feedback and proceed with: Approve, Reject, Return to faculty with comments, Escalate to Director of Research. |
| **2** | Director of Research | 2 working days | Approve, Reject, Return with comments, Request additional documents, verify Scopus/ranking claim. |
| **3** | VP of Academic Affairs | 1 working day | Approve, Reject, Return with comments. |
| **4** | UD President | 1 working day | **Final Approve, Final Reject.** Digital signature captured. |

#### FR-WF-002 — Approver Actions

| Action | Description |
|---|---|
| **Approve** | Moves application to next stage. Captures approver name, digital signature, timestamp, and optional comments. If the Dean approves, the fee amount is provisionally committed against that Dean's Budget. |
| **Reject** | Terminates workflow. Faculty receives notification with rejection reason. Application is archived. **Any provisional Dean's Budget commitment is released.** |
| **Return for Revision** | Application sent back to faculty with specific comments. Faculty may update and resubmit. Revision history preserved. |
| **Request Information** | Approver posts a question to the faculty member without formally returning the form. Thread attached to application record. |
| **Delegate** | Approver may temporarily delegate authority to a named deputy. System logs the delegation with timestamps. |

#### FR-WF-003 — SLA Monitoring & Escalation
- At **50% of SLA elapsed**: reminder email sent to approver.
- At **100% of SLA elapsed**: second reminder email sent to approver, dashboard flags application as **"Urgent"** in red.

#### FR-WF-004 — Comments & Audit Trail
Every action is recorded with: actor identity, timestamp, IP address, action type, and full comment text. This log is **immutable** and available to System Administrators and UD President.

#### FR-WF-005 — Notification Emails
All notification emails include: application reference number, applicant name, paper title, journal title, current stage, **direct deep-link URL** to the application in JPRS, deadline reminder, and the university logo and footer.

---

### 6.4 Module 4: Purchase Requisition Form (PRF) Auto-Generation — Article Processing Charges

#### FR-PRF-001 — PRF Category Selection

The PRF module supports request categories consistent with CRS, with the journal-specific category as the Phase 1 focus:

| Category | Status | Notes |
|---|---|---|
| **Article Processing Charge (APC)** | ✅ Phase 1 focus | Auto-fill from approved journal paper application. Funded from the relevant College Dean's Budget. |
| **Equipment** | 🔜 Available option | Manual entry of items, quantities, supplier recommendations. |
| **Visiting Faculty** | 🔜 Available option | Fields for visiting scholar details, accommodation, and honorarium. |
| **Other** | 🔜 Available option | Free-form description with standard approval chain. |

#### FR-PRF-002 — Auto-Population from Journal Paper Application

Upon application approval (President's signature), the system immediately creates a **draft PRF pre-filled** with:

| PRF Field | Source in Journal Paper Application |
|---|---|
| Date | Auto: date of PRF creation |
| College / Support Department | Faculty profile — College affiliation |
| Requester Name | Faculty profile — Full name |
| Organisation Code | Mapped: **"Dean's Budget — [College]"** (always for APC PRFs, distinct from central research budget codes) |
| Purpose | Auto-text: `"Article Processing Charge — [Paper Title] — [Journal Title]"` |
| Item 1: APC Fee | Section F — Article Processing Charge |
| Item 2: Additional Publication Charges | Section F — Additional charges (if any) |
| Total Cost | Auto-calculated sum of all items |
| Payee | Journal / Publisher name, extracted from the uploaded APC invoice |

#### FR-PRF-003 — Faculty Review of PRF
The faculty member receives a notification and is directed to **review the pre-filled PRF**. They may edit financial estimates if actual invoice amounts differ (with a mandatory explanation note). Once confirmed, the faculty member submits the PRF to begin the PRF approval chain.

#### FR-PRF-004 — PRF Approval Chain

| Stage | Approver | SLA Target | Notes |
|---|---|---|---|
| **1** | Dean of College | 1 working day | **Confirms available balance in own Dean's Budget** and formally commits the amount. |
| **2** | Director of Research | 1 working day | Research/publication quality confirmation. |
| **3** | VP of Academic Affairs | 1 working day | Academic alignment sign-off. |
| **4** | Finance Department | 2 working days | **Budget availability check against the specific College's Dean's Budget ledger** (not a central pool); may partially approve or adjust amounts. |
| **5** | UD President | 1 working day | Final binding approval with digital signature. |
| **6** | Procurement Department | N/A — notified | Receive approved PRF. Process payment/wire transfer to the publisher for the APC invoice. Update payment status in JPRS. |
| **7** | Faculty Member Review & Confirmation | 1 working day | Faculty member receives automated notification with payment confirmation details. Faculty member may: Accept, Request modifications, or Add comments/clarifications before final closure. |

#### FR-PRF-005 — Invoice Attachment
The official publisher APC invoice is mandatory and must already be attached from the original application (Section E). Faculty or Procurement may attach additional supporting documents (e.g. payment confirmation, receipt) directly to the PRF record.

---

### 6.5 Module 5: Dean's Budget Management & Tracking

> This module exists specifically because APC funding is drawn from each College Dean's own budget, not a shared central research fund. It must give Deans, Finance, and leadership a clear, always-current, **college-by-college** view of budget health.

#### FR-BUD-001 — Budget Allocation
At the start of each academic year, the System Administrator (in coordination with Finance and each Dean) sets the **Dean's Budget allocation** for each college in JPRS. Allocations can be adjusted mid-year (e.g. top-ups) with a logged reason and approver.

#### FR-BUD-002 — Budget Ledger (Allocated / Committed / Spent)
Each College's Dean's Budget is tracked as a running ledger with three figures, always visible together:
- **Allocated** — the total budget approved for the academic year.
- **Committed** — sum of amounts provisionally reserved by applications currently in the approval pipeline (from Dean approval at Stage 1 onward).
- **Spent** — sum of amounts for PRFs that have completed Procurement payment.
- **Available Balance** = Allocated − Committed − Spent, shown in real time.

#### FR-BUD-003 — Automatic Commit / Release / Spend Transitions
- **Commit**: triggered automatically when the Dean approves a journal paper application at Stage 1 (or 1B).
- **Release**: triggered automatically if the application is rejected, withdrawn, or the PRF amount is later reduced.
- **Spend (finalise)**: triggered automatically when Procurement confirms payment to the publisher, converting the committed amount into spent.
- Every transition is written to an immutable **budget transaction log** (entity, amount, type, actor, timestamp) for audit purposes, fully separate from any centralised research budget ledger used by CRS.

#### FR-BUD-004 — Threshold Alerts
- Automated alert to the Dean, Director of Research, and Finance at **75%** and **95%** of a college's Dean's Budget committed.
- At **100%**, new applications from that college are flagged at submission with a warning banner; the Dean may still approve with a mandatory justification note, or request a budget top-up through the Admin/Finance workflow.

#### FR-BUD-005 — Budget Dashboard & Reporting
- Dean's own dashboard: live ledger (Allocated / Committed / Spent / Available) for their college only, plus a list of applications contributing to each figure.
- Director of Research / VP / President dashboard: side-by-side comparison of all three colleges' Dean's Budgets.
- Exportable budget report (Excel/PDF) by academic year, by college, with drill-down to individual applications and PRFs.
- Year-end **budget carry-forward rule** configurable by Admin (e.g. unspent balance lapses, or a defined percentage carries forward).

---

### 6.6 Module 6: Dashboard & Analytics

#### FR-DASH-001 — Faculty Dashboard
- **My Applications**: list of all submitted applications with status badge.
  - Statuses: `Draft` · `Pending RC` · `Pending Dean` · `Pending Director` · `Pending VP` · `Pending President` · `Approved` · `Rejected` · `Returned`
- **Timeline view**: visual horizontal progress bar showing current stage and completed stages.
- **Notification centre**: in-app alerts for stage changes, approver comments, and PRF/payment status.
- **Quick-action buttons**: Continue Draft, View Status, Download Approval Letter, View PRF.
- **Post-publication checklist**: reminder banner appears once the paper's publication is confirmed.

#### FR-DASH-002 — Dean / Director / VP Dashboard
- Pending Approvals queue: sorted by submission date, flagged by SLA colour:
  - 🟢 Green = within SLA
  - 🟡 Amber = 50–100% of SLA elapsed
  - 🔴 Red = overdue
- College-level statistics: applications by status, by journal ranking/Scopus status, by faculty member, year-to-date.
- **Dean's Budget summary widget**: Allocated / Committed / Spent / Available for the relevant college(s), current academic year.
- Export to Excel / PDF at any time.

#### FR-DASH-003 — Executive Dashboard (VP + President)
- University-wide real-time counters: Total Applications YTD, Approved, Pending, Rejected, PRFs in process.
- **Interactive charts**:
  - Applications by college (pie chart)
  - Applications by month (bar chart)
  - Approval cycle time trend (line chart)
  - Journals by Scopus status / ranking distribution (Q1–Q4)
  - **Dean's Budget committed vs. spent, per college (gauge/bar comparison)**
- College comparison table: side-by-side view of all three colleges, including budget health.
- Research output tracker: papers published, by faculty, by journal, by Scopus/ranking status.
- Configurable date range filter (academic year or calendar year options).
- **One-click export**: formatted PDF executive summary report.

#### FR-DASH-004 — Finance Dashboard
- PRFs pending Finance approval with financial summaries.
- **Dean's Budget consumption by college and by academic year** — Finance's primary reconciliation view, kept fully separate from any central research budget reporting.
- Committed vs. actual expenditure comparison (once Procurement confirms payment).

#### FR-DASH-005 — System Administrator Dashboard
- User management: add/edit/deactivate users, assign roles, manage delegation records.
- Workflow configuration: edit SLA thresholds, approval chain structure, notification templates.
- **Dean's Budget configuration**: set/adjust annual allocations per college, configure carry-forward rules and alert thresholds.
- Audit log viewer: searchable, exportable log of all system events, including budget transactions.
- Academic year management: open/close academic year cycle, archive old applications, roll over budgets per configured rule.

---

## 7. Post-Publication Compliance Module

### 7.1 Publication Visibility Task

Once a journal paper's publication is confirmed (Director of Research or faculty marks the paper as **"Published"** with a link/DOI), the system automatically activates a **single post-publication compliance task** for the faculty member: publishing a LinkedIn post about their published paper, mentioning and tagging the University of Dubai's official LinkedIn account with the required hashtag.

#### Task Requirements

| Field | Requirement |
|---|---|
| **Task** | Publish a LinkedIn post about your published journal paper |
| **Deadline** | Within 7 days of the publication confirmation date |
| **Required mention** | Tag `@University of Dubai` (official LinkedIn page) |
| **Required hashtag** | `#UDResearch` |
| **Evidence** | Paste the public URL of the LinkedIn post into the system |
| **Minimum content** | Post must reference the paper title and journal name, and note that the research was conducted at/affiliated with UD |

#### Suggested Post Template (shown to faculty in the system)
> *"Excited to share that our paper '[Paper Title]' has been published in [Journal Name]! Proud to contribute to @University of Dubai's growing research output. #UDResearch #UniversityOfDubai #Research"*

#### Incentive & Engagement Features
- **Publication Post Leaderboard** — a light gamification element visible on the faculty dashboard showing the top posts by engagement (likes + comments + shares) among UD faculty for the current academic year.
- **Dean's Pick Badge** — Dean can mark one post per semester as "Dean's Pick", highlighted on the leaderboard and shared on official UD social media channels.
- **Engagement Score** — the system records likes, comments, and shares on each submitted post URL (via LinkedIn public data or manual entry), feeding the Research Impact dashboard.
- **Automatic Reminder Emails** — sent at D+3 and D+5 if the task is not yet completed, with the suggested template pre-filled in the email body.
- **Completion Acknowledgement** — upon submitting the LinkedIn post URL, the faculty member receives an in-system congratulations message and a digital "UD Research Ambassador" badge displayed on their profile within JPRS.

### 7.2 Compliance Tracking & Reporting

- **Status tracking:** Each application record shows the publication task as `Pending` / `Submitted — Under Review` / `Verified` / `Overdue`.
- **Verification:** The system stores the submitted LinkedIn post URL. Admins or the Director of Research can click to view the live post and manually mark it as `Verified`.
- **Overdue escalation:** If the task is not completed within **7 days** of the publication confirmation date, an automated alert is sent to the faculty member's Dean.
- **Non-compliance flag:** A non-compliance flag is recorded on the faculty member's JPRS profile. Visible to the Director of Research and may be considered during future application reviews (configurable by Admin).
- **Dashboard visibility:** The Executive Dashboard and Director of Research dashboard display:
  - Total publication posts submitted this academic year
  - Compliance rate (% of approved/published papers resulting in a verified post)
  - Total estimated reach (sum of engagement scores across all posts)
  - Leaderboard of top posts by engagement

---

## 8. Non-Functional Requirements

### 8.1 Performance
- Page load time ≤ **2 seconds** for all primary views on a standard university network (100 Mbps).
- Dashboard data refresh ≤ **5 seconds**, including Dean's Budget ledger figures.
- Form auto-save completes within **1 second** of field blur.
- System supports minimum **200 concurrent users** without degradation.

### 8.2 Security & Compliance
- All data encrypted in transit (**TLS 1.3**) and at rest (**AES-256**).
- Role-based data isolation: faculty cannot access other faculty records; Deans cannot access another college's budget ledger.
- All file uploads (including APC invoices) scanned for malware before storage.
- Session timeout: **30 minutes** for approver roles, **60 minutes** for faculty.
- Complete audit log retained for minimum **7 years**, including all budget transactions.
- Compliant with UAE data protection regulations and UD's Information Security Policy.
- OWASP Top 10 vulnerabilities addressed and verified by penetration testing prior to launch.

### 8.3 Availability & Reliability
- Target uptime: **99.5%** (excluding scheduled maintenance windows).
- Scheduled maintenance: Fridays 02:00–04:00 GST with at least 48 hours advance notice.
- Automated daily database backups with 30-day retention and tested restore procedure.
- Disaster recovery: **RTO ≤ 4 hours**, **RPO ≤ 1 hour**.

### 8.4 Usability & Accessibility
- Responsive design: fully functional on desktop (≥1024px) and tablet (768–1023px). Mobile read-only for status checking.
- **Arabic language support**: all UI text and email templates available in Arabic. RTL layout supported.
- **WCAG 2.1 Level AA** accessibility compliance.
- Inline contextual help text for every form field, including a plain-language explanation of the Dean's Budget balance indicator.
- Progress indicator on multi-section form showing completion percentage.

### 8.5 Integrations

| Integration | Purpose |
|---|---|
| **Microsoft 365 / Active Directory** | SSO authentication and automatic user profile population. |
| **Email (Exchange / SMTP)** | Transactional notification emails with deep-link tokens. |
| **DocuSign or Adobe Sign** | Binding e-signatures for approval records. |
| **Scopus API** *(future)* | Auto-verify journal Scopus indexing status and ranking/quartile. |
| **UD ERP / Finance System** *(future)* | Dean's Budget allocation sync, payment issuance integration, reconciliation with central Finance ledgers. |
| **CRS (Conference Registration System)** *(future)* | Shared auth/notification/audit services and a unified "Research Systems" reporting layer, while keeping budget ledgers separate. |

---

## 9. GitHub Repository Structure

### 9.1 Repository

```
github.com/university-of-dubai/journal-papers-registration-system
```

### 9.2 Directory Layout

```
journal-papers-registration-system/
│
├── README.md                        ← This file (PRD)
├── .gitignore
├── docker-compose.yml
├── .env.example
│
├── docs/
│   ├── PRD.md                       ← Full PRD (this document)
│   ├── architecture/
│   │   ├── system-diagram.png
│   │   └── database-erd.png
│   ├── api/
│   │   └── openapi.yaml             ← OpenAPI 3.0 specification
│   └── wireframes/
│       └── ...
│
├── frontend/                        ← React (TypeScript) application
│   ├── public/
│   ├── src/
│   │   ├── components/              ← Reusable UI components (shared with CRS where possible)
│   │   ├── pages/
│   │   │   ├── ApplicationForm/     ← 6-section wizard (Applicant, Paper, Journal, Eligibility, Documents, Fees)
│   │   │   ├── Dashboard/           ← Faculty dashboard
│   │   │   ├── ApprovalQueue/       ← Approver queue view
│   │   │   ├── PRFModule/           ← PRF review and tracking
│   │   │   ├── BudgetModule/        ← Dean's Budget ledger, alerts, reporting
│   │   │   ├── PostPublication/     ← Post-publication compliance checklist
│   │   │   └── Admin/               ← System admin panel
│   │   ├── hooks/
│   │   ├── store/                   ← State management (Redux / Zustand)
│   │   ├── services/                ← API call functions
│   │   ├── types/                   ← TypeScript interfaces
│   │   └── utils/
│   ├── tailwind.config.js
│   └── package.json
│
├── backend/                         ← Node.js / Express API
│   ├── src/
│   │   ├── routes/
│   │   ├── controllers/
│   │   ├── models/
│   │   ├── middleware/
│   │   │   ├── auth.middleware.ts
│   │   │   ├── rbac.middleware.ts
│   │   │   └── audit.middleware.ts
│   │   ├── services/
│   │   │   ├── approvalWorkflow.service.ts
│   │   │   ├── prf.service.ts
│   │   │   ├── deanBudget.service.ts      ← Dedicated Dean's Budget ledger logic
│   │   │   ├── notification.service.ts
│   │   │   ├── signature.service.ts
│   │   │   └── audit.service.ts
│   │   └── utils/
│   └── package.json
│
├── database/
│   ├── migrations/                  ← Numbered SQL migration files
│   ├── seeds/                       ← Dev/test seed scripts
│   └── erd.png
│
├── infrastructure/
│   ├── terraform/                   ← Azure IaC scripts
│   ├── k8s/                         ← Kubernetes manifests
│   └── nginx/
│
├── .github/
│   ├── ISSUE_TEMPLATE/
│   │   ├── bug_report.md
│   │   ├── feature_request.md
│   │   └── security_vulnerability.md
│   └── workflows/
│       ├── lint.yml
│       ├── test.yml
│       ├── deploy-staging.yml
│       └── deploy-production.yml
│
├── tests/
│   ├── unit/
│   ├── integration/
│   └── e2e/                         ← Playwright end-to-end tests
│
└── scripts/
    ├── migrate-from-excel.js        ← Historical data import utility
    ├── seed-roles.js
    └── generate-test-data.js
```

### 9.3 Branching Strategy (GitFlow)

| Branch | Purpose |
|---|---|
| `main` | Production-ready code only. Protected — requires 2 approvals + passing CI before merge. |
| `develop` | Integration branch. All feature branches merge here first. |
| `feature/[ticket-id]-[description]` | Individual features. e.g. `feature/JPRS-17-budget-ledger` |
| `hotfix/[description]` | Critical production bug fixes. Branch from `main`, merge back to both `main` and `develop`. |
| `release/[version]` | Release preparation. Version bumps, changelogs, final QA. |

### 9.4 GitHub Issues & Project Board

- **Labels**: `bug` · `feature` · `enhancement` · `documentation` · `security` · `ux` · `budget`
- **GitHub Projects (Kanban)**: `Backlog → To Do → In Progress → In Review → Done`
- **Milestones**: map to 2-week sprint cycles and project phases
- **Issue templates**: Bug Report · Feature Request · Security Vulnerability (private)

---

## 10. Implementation Roadmap

| Phase | Scope | Duration | Key Deliverables |
|---|---|---|---|
| **Phase 0** — Discovery | Requirements validation, stakeholder interviews (incl. Deans on budget rules), data model design, UX wireframes, tech stack finalisation. | 4 weeks | Approved wireframes, ERD, finalised tech stack, signed-off PRD. |
| **Phase 1** — Foundation | SSO integration, user management, database setup, application form (Sections A–D), file upload, draft save, reference number generation. | 6 weeks | Working authentication, form submission to database, file storage. |
| **Phase 2** — Workflow Engine | Application approval chain (all stages), notification system, SLA monitoring, escalation logic, approver dashboard, faculty status view. | 6 weeks | End-to-end application approval flow in staging environment. |
| **Phase 3** — PRF & Dean's Budget Module | PRF auto-population, PRF approval chain (7 stages), **Dean's Budget ledger (allocation, commit/release/spend, thresholds)**, Finance dashboard, Procurement notification. | 6 weeks | Working PRF workflow with live, per-college budget tracking. |
| **Phase 4** — Dashboards & Analytics | Executive dashboard, college dashboards, budget comparison views, charts, export (PDF/Excel), post-publication compliance module, leaderboard, engagement tracking. | 4 weeks | Full dashboards. Publication compliance task, leaderboard, and Dean's Pick feature live. |
| **Phase 5** — UAT & Launch | User Acceptance Testing, bug fixes, performance tuning, penetration test, Arabic localisation, go-live. | 4 weeks | Production-ready system. User training completed. |
| **Phase 6** — Post-Launch | Monitoring, feedback, Scopus API integration, ERP integration planning, CRS/JPRS shared-services alignment. | Ongoing | v1.1 enhancement releases. Integration roadmap. |

> **Total estimated timeline (Phases 0–5):** approximately **7–8 months** from project kick-off.
> **Assumed team:** 1 Project Manager · 2 Frontend Developers · 2 Backend Developers · 1 DevOps Engineer · 1 QA Engineer.

---

## 11. Core Data Model (Entity Overview)

### 11.1 Key Entities

| Entity | Key Attributes |
|---|---|
| `users` | id, employee_id, full_name, email, role, college_id, is_active, created_at, last_login |
| `colleges` | id, name, code (CEIT/CB/CL), dean_user_id |
| `journal_applications` | id, reference_number, faculty_user_id, college_id, paper_title, author_name (auto), co_authors (JSONB — name, affiliation, is_ud_affiliated), journal_title, is_scopus_indexed, journal_ranking, eligibility_flags (JSONB), financial_estimate (JSONB — apc_fee, additional_charges, total), status (ENUM), current_stage, academic_year |
| `application_documents` | id, application_id, document_type (ENUM: acceptance_letter, manuscript, scopus_proof, apc_invoice, coauthor_consent), file_name, storage_path, uploaded_by, uploaded_at, is_current_version |
| `approval_records` | id, application_id, stage (ENUM), approver_user_id, action (ENUM: APPROVED/REJECTED/RETURNED/INFO_REQUEST), comment, signature_reference, timestamp, delegate_user_id |
| `prf_requests` | id, reference_number, application_id, category (ENUM — includes 'APC'), requester_user_id, purpose, items (JSONB array), total_amount, payee_name, status (ENUM), current_stage |
| `prf_approval_records` | id, prf_id, stage (ENUM), approver_user_id, action (ENUM), comment, adjusted_amount, signature_reference, timestamp |
| `dean_budgets` | id, college_id, academic_year, allocated_amount, committed_amount, spent_amount, carry_forward_rule, updated_at |
| `budget_transactions` | id, dean_budget_id, application_id (nullable), prf_id (nullable), type (ENUM: COMMIT/RELEASE/SPEND/ADJUSTMENT), amount, actor_user_id, timestamp |
| `post_publication_tasks` | id, application_id, task_type (ENUM), due_date, completed_at, evidence_path, is_compliant |
| `notifications` | id, user_id, type, reference_id, message, is_read, sent_at, email_sent_at |
| `audit_logs` | id, actor_user_id, action_type, entity_type, entity_id, old_value (JSONB), new_value (JSONB), ip_address, timestamp |

---

## 12. UI/UX Design Guidelines

### 12.1 Design Principles

| Principle | Description |
|---|---|
| **Clarity first** | Every screen must have one primary action. No hidden or ambiguous buttons. Status must always be visible. |
| **Trust through transparency** | Show the complete approval journey at all times, including the **live Dean's Budget balance** relevant to the application. Faculty should never wonder "where is my application?" and Deans should never wonder "how much budget do I have left?" |
| **Reduce cognitive load** | Multi-section form with progress indicator. Auto-fill wherever possible (Author, College, Funding Source). Inline validation — not end-of-form error dumps. |
| **Mobile-conscious** | Approvers often need to review on mobile. Approval actions must be accessible on a 375px-wide screen. |
| **Institutional identity** | Primary: UD Navy Blue `#1B3A6B`. Accent: UD Gold `#C8972A`. Professional aesthetic aligned with UD branding, consistent with CRS for visual continuity across UD research systems. |

### 12.2 Key Screens

1. Login page (SSO redirect, no password field)
2. Faculty home / My Applications dashboard
3. New Application Form (multi-step wizard: Applicant, Paper, Journal, Eligibility, Documents, Fees — with live budget indicator)
4. Application status detail view (timeline, comments thread, documents)
5. Approver queue view (filterable, sortable, SLA-highlighted list)
6. Single application review (read-only form + approve/reject/return actions in sticky footer, with Dean's Budget balance shown at the Dean stage)
7. PRF review and confirm (pre-filled editable form with change log)
8. PRF status tracker
9. Dean's Budget dashboard (Allocated / Committed / Spent / Available, drill-down list)
10. Executive dashboard (charts, counters, college comparison, budget comparison)
11. Post-publication LinkedIn compliance task & leaderboard
12. System Admin panel (users, budget configuration, audit log)

---

## 13. Creative & AI Enhancement Suggestions

> These features go beyond replicating the current manual process and are recommended to make JPRS a strategic asset for research management at UD.

### 13.1 🤖 Intelligent Application Assistant
An AI-powered assistant that guides faculty during form completion:
- Suggests likely APC fee ranges based on the journal name and historical UD data.
- **Flags predatory or low-quality journals** — integrates with a curated warning list (e.g. Beall's-style list) before submission.
- Offers a "Policy Check" button that summarises the relevant UD publication funding policy in plain language.

### 13.2 ✅ Smart Scopus & Ranking Verification
Integration with the Scopus API (or Scimago) allows **real-time journal indexing and quartile verification**. The application form displays a live badge:
- `✅ Scopus Verified — Q[n]` — green
- `❌ Not Found in Scopus` — red
- `⏳ Verification Pending` — amber

This prevents a common rejection reason before the form is submitted.

### 13.3 📊 Research Impact Tracker
A separate view (accessible to Director of Research and VP) that aggregates journal output into a **research impact profile**: papers per faculty, journal quartile distribution (Q1–Q4), citations (future Scopus API link), and year-on-year growth in publication activity. This data feeds directly into UD's QS and KHDA accreditation reporting.

### 13.4 📄 Automated Annual Research Report
At end of each academic year, the system **auto-generates a formatted PDF report**: "University of Dubai Annual Journal Publication & APC Report" containing all approved papers, total APC expenditure per college, faculty participation, and Scopus/ranking breakdown. This currently takes the research office several days to compile manually.

### 13.5 💰 Dean's Budget Forecast Widget
Each Dean's dashboard includes a forward-looking widget: based on pending applications and historical seasonal publication patterns, the system **projects end-of-year APC expenditure** against the allocated budget. Automated alerts at 75% and 95% commitment (see FR-BUD-004).

### 13.6 🔗 QR Code on Approval Letter
The digitally signed approval letter (PDF) includes a **QR code** that links directly to the application record in JPRS, letting the publisher-facing finance paperwork be verified in real time.

### 13.7 🔄 Smart Delegation & Out-of-Office Management
Approvers can configure automatic delegation rules:
> *"If I do not act within 48 hours, automatically delegate to [named deputy]."*

This prevents workflow stalls during annual leave or travel — a significant current pain point.

### 13.8 🔀 Unified Research Systems View
A lightweight, read-only combined view (for VP/President) that pulls key figures from both CRS and JPRS side by side — total research-related expenditure, output counts, and Scopus compliance — while keeping each system's underlying budget ledgers fully separate and independently auditable.

---

## 14. Risks & Mitigations

| Risk | Likelihood / Impact | Mitigation |
|---|---|---|
| Low user adoption among senior faculty unfamiliar with digital forms | Medium / High | Mandatory training workshop, video tutorials, faculty champions programme. Paper fallback for first 3 months with parallel running. |
| Active Directory / SSO integration delays | Medium / Medium | Begin SSO integration in Phase 0. Maintain email/password fallback for Phase 1 UAT. |
| **A Dean's Budget is exceeded without prior visibility, causing a funding dispute** | Medium / High | Real-time commit/release ledger with mandatory balance display at submission and at Dean approval; hard alert at 100% committed requiring explicit justification before further approval. |
| Scope creep from stakeholders requesting new features mid-build | High / Medium | Strict change control process. New features logged in GitHub Issues and deferred to Phase 6 unless critical. |
| Data migration from Excel: inconsistent historical data | Medium / Low | Historical data imported as read-only archive. New system starts fresh from go-live date, with opening budget balances entered manually and verified by Finance. |
| Approval chain bottlenecks persist (human behaviour, not system) | High / High | SLA monitoring with escalation. Management KPI dashboard makes bottlenecks visible to leadership. |
| DocuSign / Adobe Sign licensing cost exceeds budget | Low / Medium | Evaluate open-source e-signature alternatives (e.g., Documenso) as contingency. |
| Security breach or data leak | Low / High | Penetration testing pre-launch, MFA enforcement, role-based data isolation, WAF, monthly security reviews. |

---

## 15. Acceptance Criteria for Go-Live

The following criteria must all be met before production deployment:

- [ ] Faculty can submit a complete journal paper (APC) application with all required documents through the web portal.
- [ ] The application automatically triggers Stage RC notification to the Research Committee.
- [ ] Each approval stage correctly routes to the next approver upon approval, and notifies the faculty member.
- [ ] Rejection at any stage sends an email to the faculty with the reason, stops the chain, and **releases any provisional Dean's Budget commitment**.
- [ ] An approved journal paper application (President-signed) automatically creates a pre-filled PRF draft.
- [ ] The PRF approval chain routes through all 7 stages correctly.
- [ ] **Dean's Budget ledger (Allocated / Committed / Spent / Available) updates in real time at every commit, release, and spend event, and is tracked separately per college with no cross-contamination between colleges or with any central research budget.**
- [ ] Executive dashboard displays real-time application counts, status breakdowns, and per-college budget summaries.
- [ ] All notification emails contain correct content and direct deep-links.
- [ ] System supports Arabic language toggle across all major views.
- [ ] Load test confirms system performance with 200 concurrent users.
- [ ] Penetration test report issued with **no Critical or High severity findings**.
- [ ] User Acceptance Testing sign-off obtained from: Faculty representative, Dean, Director of Research, VP Academic Affairs, Finance, and IT.

---

## 16. Glossary

| Term | Definition |
|---|---|
| **APC** | Article Processing Charge — the fee a publisher charges to make an accepted paper openly available; the primary funding item processed by JPRS. |
| **CAO / Provost** | Chief Academic Officer / Provost — equivalent to VP of Academic Affairs in this document. |
| **CEIT** | College of Engineering & IT. |
| **CRS** | Conference Registration System — UD's sibling platform for conference attendance requests. |
| **Dean's Budget** | The dedicated funding pool allocated to and managed by each College Dean, from which APC payments in this system are drawn; tracked entirely separately from any centralised research budget. |
| **GitFlow** | A branching model for Git that defines a strict branching structure for project releases. |
| **JPRS** | Journal Papers Registration System — the platform described in this PRD. |
| **KHDA** | Knowledge and Human Development Authority — Dubai's regulatory authority for higher education. |
| **MFA** | Multi-Factor Authentication. |
| **PRD** | Product Requirements Document. |
| **PRF** | Purchase Requisition Form — UD's standard form for initiating procurement/payment. |
| **Quartile (Q1–Q4)** | Scimago/journal ranking tier used to assess journal quality, Q1 being the highest. |
| **RBAC** | Role-Based Access Control. |
| **RPO** | Recovery Point Objective — maximum acceptable data loss in a disaster. |
| **RTO** | Recovery Time Objective — maximum acceptable system downtime in a disaster. |
| **Scopus** | Elsevier's abstract and citation database; used as a journal quality benchmark at UD. |
| **SLA** | Service Level Agreement — the maximum time an approver should take to act. |
| **SSO** | Single Sign-On — one login credential (UD Microsoft 365) used across all systems. |
| **UAT** | User Acceptance Testing. |
| **VNET** | Virtual Network — an isolated private network in Azure. |
| **WAF** | Web Application Firewall. |
| **YTD** | Year-to-Date. |

---

## 17. Document Sign-Off

This document requires review and formal approval from the following stakeholders before development commences:

| Name & Title | Role in JPRS | Signature | Date |
|---|---|---|---|
| Director of Research | Document Owner / System Sponsor | | |
| VP of Academic Affairs | Executive Sponsor | | |
| UD President | Final Approver | | |
| IT Director / CIO | Technical Authority | | |
| Dean, Engineering & IT | College Stakeholder / Budget Owner | | |
| Dean, Business | College Stakeholder / Budget Owner | | |
| Dean, Law | College Stakeholder / Budget Owner | | |
| Finance Director | PRF & Budget Workflow Approver | | |

---

<div align="center">

**University of Dubai · Journal Papers Registration System · PRD v1.0**

*Confidential — Internal Use Only*

</div>
