# Enterprise Risk Assessment — Waffarah E-Commerce Platform

<p align="left">
  <img src="https://img.shields.io/badge/Status-Complete-brightgreen"/>
  <img src="https://img.shields.io/badge/Type-Risk%20Assessment-informational"/>
  <img src="https://img.shields.io/badge/Pillar-Governance%20%7C%20Risk-blueviolet"/>
</p>

| | |
|---|---|
| **Author** | Joud Alhussain |
| **Date** | August 2026 |
| **Methodology** | ISO/IEC 27005 Information Security Risk Management |
| **Report** | [PDF Report](#) |
| **Presentation** | [Business Presentation (PPTX)](#) |

---

## 📋 Project Overview

This project conducts an enterprise risk assessment of Waffarah, a fictional mid-size e-commerce company, following the ISO/IEC 27005 information security risk management process. Unlike the technical penetration test in the Enterprise Security Assessment project, this assessment takes a broader governance and risk management view — covering people, process, technology, and third-party risk, not just the web application.

## 🏢 Business Scenario

Waffarah is a mid-size e-commerce company (~150 employees) handling customer orders and payment data. As part of maturing its security posture ahead of a compliance audit, Waffarah's leadership commissioned a formal information security risk assessment to identify, evaluate, and prioritize risks across the business — informing budget and resourcing decisions for the year ahead.

## 🎯 Objectives

- Identify Waffarah's key information assets and their business value
- Identify relevant threats and vulnerabilities for each asset
- Score and prioritize risks using a likelihood/impact risk matrix
- Produce a risk treatment plan with clear ownership and next steps
- Present findings in a business-readable format for leadership

## 🔍 Scope

**In scope:** Information assets, systems, and processes core to Waffarah's e-commerce operations — customer data, payment processing, employee access, key third-party vendors, and physical premises security.

**Out of scope:** Full technical penetration testing (covered separately in the [Enterprise Security Assessment](https://github.com/JoudAlhussain/enterprise-security-assessment) project), financial/market risk, and legal/contractual risk not related to information security.

## 🧭 Methodology

This assessment follows the ISO/IEC 27005 information security risk management process: context establishment, risk identification (asset-based), risk analysis, risk evaluation, and risk treatment.

Assets were rated for **Confidentiality, Integrity, and Availability (CIA)** impact. Risks were scored using the same **Likelihood × Impact** severity matrix used in the Enterprise Security Assessment project, ensuring consistency across the portfolio:

| Likelihood → / Impact ↓ | Low | Medium | High |
|---|---|---|---|
| **High** | Medium | High | **Critical** |
| **Medium** | Low | Medium | High |
| **Low** | Low | Low | Medium |

---

## 📦 Asset Inventory

### Data Assets

| Data Asset | Description | Confidentiality | Integrity | Availability |
|---|---|---|---|---|
| Customer PII | Names, addresses, contact details | High | High | Medium |
| Payment card data | Stored/processed card details | Critical | High | High |
| Order & transaction history | Purchase records, order status | Medium | High | Medium |
| Employee HR data | Staff records, payroll info | High | Medium | Low |
| Authentication credentials | Passwords, session tokens, security questions | Critical | High | High |
| Product & pricing data | Catalog, pricing, inventory levels | Low | Medium | High |
| Customer support records | Complaint logs, communication history | Medium | Low | Low |
| Business/financial records | Revenue data, vendor contracts | High | High | Medium |

### Systems & Technology Assets

| System/Technology Asset | Description | Confidentiality | Integrity | Availability |
|---|---|---|---|---|
| E-commerce web application | Customer-facing storefront (login, checkout, search) | Medium | High | Critical |
| Payment processing system | Handles transaction processing | Critical | Critical | Critical |
| Customer database | Stores customer accounts, PII, order history | High | High | High |
| Admin panel / back-office system | Internal management of orders, users, inventory | High | High | Medium |
| Web/application servers | Infrastructure hosting the storefront and APIs | Medium | High | Critical |
| Employee endpoints | Staff devices with access to internal systems | Medium | Medium | Medium |
| Identity & Access Management (IAM) system | Manages employee/customer authentication and permissions | Critical | High | High |
| Backup systems | Backups of databases and critical files | High | High | High |
| Network infrastructure | Firewalls, routers, internal network | Medium | High | Critical |

### People & Process Assets

| People/Process Asset | Description | Confidentiality | Integrity | Availability |
|---|---|---|---|---|
| Employee access credentials | Staff logins to admin panel, IAM, internal tools | High | High | Medium |
| Privileged/admin accounts | IT admin, database admin, and similar high-privilege roles | Critical | Critical | High |
| Onboarding/offboarding process | Granting and revoking employee system access | Medium | High | Medium |
| Incident response process | Detection, response, and recovery from security incidents | Medium | High | Critical |
| Vendor/third-party access | External parties with system access | High | High | Medium |
| Physical access control | Badge access, visitor management | Medium | Medium | Medium |
| Security awareness & training program | Employee understanding of phishing, social engineering | Low | Medium | Low |

---

## 🔎 Risk Register

Risks were identified across all three asset categories and scored using the Likelihood × Impact matrix above. Where possible, ratings were directly informed by confirmed findings from the Enterprise Security Assessment project (noted below), rather than assumed.

| ID | Asset | Threat | Likelihood | Impact | Risk Rating |
|---|---|---|---|---|---|
| R1 | Payment card data | Interception/compromise at rest or in transit | Medium | Critical | **Critical** |
| R2 | Authentication credentials | Exposed via misconfiguration *(confirmed — exposed `.kdbx` file)* | High | Critical | **Critical** |
| R3 | Admin panel / back-office | Broken access control / privilege escalation *(confirmed — SQL injection)* | High | Critical | **Critical** |
| R4 | E-commerce web application | Injection attacks (SQLi/XSS) *(confirmed)* | High | Critical | **Critical** |
| R5 | Customer PII | Technical vulnerability exploitation | Medium | High | **High** |
| R6 | Backup systems | Exposure via misconfiguration *(confirmed — exposed `/ftp` directory)* | High | High | **High** |
| R7 | Payment processing system | PCI DSS non-compliance | Medium | High | **High** |
| R8 | Product & pricing data | Price manipulation *(confirmed — wallet balance manipulation)* | Medium | Medium | **Medium** |
| R9 | Onboarding/offboarding process | Delayed access revocation | Medium | Medium | **Medium** |
| R10 | Customer PII | Data resale on black market | Medium | High | **High** |
| R11 | Vendor/third-party access | Vendor account compromise | Low | High | **Medium** |
| R12 | Employee HR data | Insider misuse of access | Low | Medium | **Low-Medium** |
| R13 | Incident response process | Inadequate/untested response plan | Medium | High | **High** |
| R14 | Security awareness & training | Employee susceptibility to phishing | Medium | High | **High** |
| R15 | Customer support records | Exposure of complaint details | Low | Low | **Low** |

**Severity breakdown:** 4 Critical · 6 High · 3 Medium · 2 Low-Medium/Low

---

## ✅ Risk Treatment Plan

| ID | Risk | Rating | Treatment | Key Actions |
|---|---|---|---|---|
| R1 | Payment card interception (rest/transit) | Critical | Mitigate | Enforce TLS/HTTPS on payment pages; tokenize card data instead of storing raw numbers; adopt formal PCI DSS compliance program; mask displayed card numbers |
| R2 | Authentication credentials exposed via misconfiguration | Critical | Mitigate | Disable directory listing at server level; remove credential/backup files from any web-accessible path; add automated scanning for sensitive files in public directories |
| R3 | Admin panel broken access control | Critical | Mitigate | Use parameterized queries for all database interactions; add input validation as defense in depth; enforce server-side role checks on every admin route |
| R4 | Web app injection (SQLi/XSS) | Critical | Mitigate | Treat all user input as data, not code (parameterized queries + output encoding); apply Content-Security-Policy header; conduct regular security testing |
| R5 | Customer PII technical exploitation | High | Mitigate | Apply secure coding practices app-wide; minimize PII collection/retention; purge data on account deletion; mask PII in admin interfaces |
| R6 | Backup systems exposed | High | Mitigate | Remove backups from web-accessible paths; disable directory listing (shared fix with R2); encrypt backup files as a second layer |
| R7 | PCI DSS non-compliance | High | Mitigate | Conduct formal PCI DSS gap assessment; assign clear compliance ownership; schedule regular compliance audits |
| R8 | Price manipulation (business logic) | Medium | Mitigate | Server-side validation of all transaction amounts; integrate a real validated payment processor; add anomaly detection/logging for unusual transactions |
| R9 | Delayed access revocation | Medium | Mitigate | Automate access revocation tied to HR termination process; apply least privilege from onboarding; conduct periodic access reviews |
| R10 | PII resale on black market | High | Mitigate | Dark web monitoring for leaked data; pre-prepared breach notification plan; offer credit monitoring to affected customers |
| R11 | Vendor/third-party compromise | Medium | Mitigate / Transfer | Enforce least-privilege vendor access; require security standards contractually; conduct regular vendor access reviews |
| R12 | Employee HR data insider misuse | Low-Medium | Mitigate | Role-based access restricting HR data to HR/payroll staff; audit logging of HR record access |
| R13 | Inadequate incident response plan | High | Mitigate | Formalize a documented IR plan; conduct regular tabletop exercises; establish post-incident review process |
| R14 | Security awareness / phishing susceptibility | High | Mitigate | Mandatory recurring security awareness training; simulated phishing campaigns; targeted follow-up training for repeat failures |
| R15 | Customer support record exposure | Low | Accept | Restrict full complaint text visibility to staff who need it; otherwise accept given low severity |

**Treatment summary:** 13 Mitigate · 1 Mitigate/Transfer · 1 Accept

### Remediation Roadmap

| Phase | Timeline | Key Actions |
|---|---|---|
| **Immediate** | 0–30 days | Fix SQL injection (parameterized queries); disable directory listing; remove exposed backups/credentials; enforce server-side admin role checks |
| **Short-term** | 30–90 days | PCI DSS gap assessment; formalize & test incident response plan; launch recurring security awareness training |
| **Ongoing** | Continuous | Quarterly access reviews; regular penetration testing; vendor security audits |

---

## 💼 Business Impact

Four Critical risks — SQL injection, credential exposure, admin panel access control, and payment card data protection — share overlapping root causes in input validation and access control, all independently confirmed during the Enterprise Security Assessment. Addressing these root causes resolves the majority of Waffarah's critical exposure in a single coordinated effort. The remaining High-severity risks span compliance (PCI DSS), organizational readiness (incident response, security awareness), and secondary harm (data resale, backup exposure) — areas requiring process and governance investment alongside technical fixes.

## 📚 Lessons Learned

- **Risk assessment and penetration testing reinforce each other.** Several risk ratings in this project were directly validated by confirmed findings from the Enterprise Security Assessment, turning what could have been guesswork into evidence-based scoring.
- **First-instinct ratings often need revision.** Multiple risks (price manipulation, PII resale, security awareness) were initially underrated until tracing through the full consequence chain — a useful discipline to build deliberately rather than trust gut feeling alone.
- **Not every "asset" is a physical thing.** People and processes (onboarding, incident response, training) are legitimate ISO/IEC 27005 asset categories, and often the weakest link — a lesson that reframed how I think about risk beyond just technical systems.
- **Not every risk needs active mitigation.** Consciously choosing to Accept a low-severity risk (R15) rather than over-investing in it is itself a valid, professional risk management decision.
- **Root-cause thinking multiplies efficiency.** Several Critical risks share the same underlying fix (input validation, access control) — recognizing that early avoids duplicated remediation effort.

## 📎 Repository Resources

- 📄 [Full PDF Report](https://github.com/JoudAlhussain/enterprise-risk-assessment/blob/main/Waffarah_Enterprise_Risk_Assessment_Report.pdf)
- 📊 [Business Presentation (PPTX)](#)
- 💼 [LinkedIn Post](#)

---
<p align="center"><i>Part of the <a href="https://github.com/JoudAlhussain/JoudAlhussain">Cybersecurity Professional Portfolio</a></i></p>
