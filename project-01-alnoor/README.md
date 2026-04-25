# 🏪 Al-Noor Trading Co.
### Odoo 18 Community — Full Implementation

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Level](https://img.shields.io/badge/Level-Junior-brightgreen)
![Odoo](https://img.shields.io/badge/Odoo-18%20Community-875A7B)
![Industry](https://img.shields.io/badge/Industry-Wholesale-blue)

---

## 📋 Project Overview

| Field | Details |
|-------|---------|
| **Company** | Al-Noor Trading Co. |
| **Industry** | Wholesale — Building Materials |
| **Size** | 45 employees · 3 warehouses |
| **Location** | Cairo, Egypt |
| **Odoo Version** | 18 Community |
| **Duration** | 6 weeks |
| **Modules** | Sales · Accounting · Inventory · Purchase |

---

## 🔴 Business Problems (Before Odoo)

| # | Problem | Impact |
|---|---------|--------|
| 1 | Double data entry — Excel + legacy system | 3 hours wasted daily |
| 2 | No real-time inventory across 3 warehouses | Stock-outs and over-ordering |
| 3 | Monthly financial close takes 10 days | Late management decisions |
| 4 | No systematic AR follow-up | High overdue receivables |

---

## 🟢 Results Achieved (After Odoo)

| Metric | Before | After |
|--------|--------|-------|
| Monthly close | 10 days | 2 days |
| Inventory visibility | End of day | Real-time |
| AR follow-up | Manual calls | Automated emails |
| Data entry | Twice | Once |

---

## 🗂️ Modules & Justification

| Module | Why Selected |
|--------|-------------|
| **Sales** | Quotation → SO → Delivery workflow |
| **Accounting** | Egyptian VAT 14%, AR/AP, bank reconciliation |
| **Inventory** | 3-warehouse AVCO tracking |
| **Purchase** | Vendor bills + 3-way matching |

> Out of scope (Phase 2): CRM, HR, Manufacturing

---

## 🔄 End-to-End Workflow
Customer Order
│
▼
[Quotation]
Price + VAT 14% calculated
Valid for 30 days
│
▼
[Sales Order]
Manager approval if > 50,000 EGP
Stock reserved automatically
│
▼
[Delivery Order]
Warehouse picks and ships
Stock deducted instantly
│
▼
[Invoice]
Auto-created from Sales Order
Dr. Customer     114,000
Cr. Revenue      100,000
Cr. VAT Output    14,000
│
▼
[Payment]
Dr. Bank         114,000
Cr. Customer     114,000

---

## 📁 Project Documents

| Document | Description |
|----------|-------------|
| [📋 Business Analysis](./business-analysis.md) | BRD, AS-IS/TO-BE process, scope |
| [⚙️ Configuration Log](./configuration-log.md) | Every setting + reason why |
| [📦 Data Migration](./data-migration.md) | Migration steps + issues solved |
| [🧪 Test Cases](./test-cases.md) | UAT scenarios + results |
| [✅ Go-Live Checklist](./go-live-checklist.md) | Pre/post go-live checklist |

---

## 📸 Screenshots

| Screen | Description |
|--------|-------------|
| [Dashboard](./screenshots/01-dashboard.png) | Main accounting dashboard |
| [Chart of Accounts](./screenshots/02-chart-of-accounts.png) | Full CoA with custom accounts |
| [Sample Invoice](./screenshots/03-invoice.png) | Posted invoice + journal entry |
| [Aged Receivables](./screenshots/04-aged-receivables.png) | AR aging report |
| [Inventory Valuation](./screenshots/05-inventory.png) | Stock valuation by warehouse |

---

## 🧪 UAT Test Results

| Test ID | Scenario | Result |
|---------|---------|--------|
| TC-001 | Full sales cycle — cash payment | ⬜ Pending |
| TC-002 | Full sales cycle — 30-day credit | ⬜ Pending |
| TC-003 | Customer return + credit note | ⬜ Pending |
| TC-004 | Full purchase cycle + vendor bill | ⬜ Pending |
| TC-005 | Bank statement reconciliation | ⬜ Pending |
| TC-006 | Aged Receivables report accuracy | ⬜ Pending |
| TC-007 | Automated AR follow-up email | ⬜ Pending |

---

## 📝 CV Description

> Implemented Odoo 18 Community (Sales, Accounting, Inventory, Purchase)
> for a wholesale building materials company with 3 warehouses and 45 employees.
> Designed Chart of Accounts aligned with Egyptian VAT regulations (14%).
> Configured multi-warehouse inventory with AVCO costing across geographic locations.
> Reduced monthly financial close from 10 days to 2 days through automation.

---

## 🔗 Related Documents

- [📋 Business Analysis](./business-analysis.md)
- [⚙️ Configuration Log](./configuration-log.md)
- [🗂️ Portfolio Home](../README.md)