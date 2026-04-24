# 🏪 Project 01 — Al-Noor Trading Co.

> **Wholesale Building Materials | Cairo, Egypt**

![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Level](https://img.shields.io/badge/Level-Junior-green)
![Odoo](https://img.shields.io/badge/Odoo-18%20Community-purple)

---

## 📋 Project Overview

| Field | Details |
|-------|---------|
| **Industry** | Wholesale — Building Materials |
| **Company Size** | 45 employees · 3 warehouses |
| **Odoo Version** | 18 Community |
| **Duration** | 6 weeks |
| **Modules** | Sales · Accounting · Inventory · Purchase |

---

## 🔴 Business Problems (Before Odoo)

| # | Problem | Business Impact |
|---|---------|----------------|
| 1 | Double data entry — Excel + legacy system | 3 hours wasted daily |
| 2 | No real-time inventory visibility | Stock-outs and over-ordering |
| 3 | Monthly close takes 10 days | Late management decisions |
| 4 | No systematic AR follow-up | High overdue receivables |

---

## 🟢 Solution Delivered (After Odoo)

- Sales → Accounting → Inventory fully automated in one system
- Monthly close reduced from **10 days → 2 days**
- Automated AR follow-up at 7 / 15 / 30 day intervals
- Real-time stock visibility across all 3 warehouses

---

## 🗂️ Modules & Justification

| Module | Why Selected |
|--------|-------------|
| **Sales** | Quotation → SO → Delivery workflow |
| **Accounting** | Egyptian VAT 14%, AR/AP management |
| **Inventory** | 3-warehouse AVCO tracking |
| **Purchase** | Vendor bills + 3-way matching |

> Out of scope (Phase 2): CRM, HR, Manufacturing

---

## 💰 Chart of Accounts (Key Accounts)

| Code | Account Name | Type |
|------|-------------|------|
| 1110001 | Main Cash | Asset |
| 1110002 | CIB Bank — Current Account | Asset |
| 1110003 | QNB Bank — USD Account | Asset |
| 1120001 | Local Customers | Receivable |
| 1120002 | Out-of-Cairo Customers | Receivable |
| 1130001 | Ceramics Inventory | Asset |
| 1130002 | Marble Inventory | Asset |
| 1130003 | Paint Inventory | Asset |
| 2110001 | Local Vendors | Payable |
| 2120 | VAT Output 14% | Liability |
| 2130 | VAT Input 14% | Asset |
| 4110 | Sales Revenue — Ceramics | Revenue |
| 4120 | Sales Revenue — Marble | Revenue |
| 4130 | Sales Revenue — Paint | Revenue |
| 5110 | Cost of Goods Sold | Expense |
| 5230 | Delivery & Transport | Expense |
| 5250 | Customer Discount Granted | Expense |

---

## ⚙️ Key Configuration Decisions

| Setting | Value | Why |
|---------|-------|-----|
| Inventory Valuation | AVCO | Building materials are mixed in storage — AVCO more practical than FIFO |
| Invoicing Policy | Delivered Quantities | Customer pays for what they actually received |
| Warehouses | 3 separate warehouses | Easier per-branch reporting and accountability |
| AR Follow-up Levels | 3 levels — 7 / 15 / 30 days | Systematic collection without manual effort |
| Lock Date | Set after each month close | Prevent backdated journal entry edits |
| Foreign Currency | USD secondary currency | Import purchases billed in USD |---

## 🔄 End-to-End Workflow

    Customer Order Received
            │
            ▼
      [Quotation]
      Price + VAT 14% calculated
      PDF sent to customer by email
            │
            ▼
      [Sales Order Confirmed]
      Stock reserved automatically
      Manager approval if > 50,000 EGP
            │
            ▼
      [Delivery Order]
      Warehouse picks and ships
      Stock deducted instantly
            │
            ▼
      [Invoice Created]
      Auto-created from Sales Order
      Journal Entry posted:
      Dr. Customer        114,000
      Cr. Revenue         100,000
      Cr. VAT Output       14,000
            │
            ▼
      [Payment Registered]
      Matched to invoice
      Dr. Bank            114,000
      Cr. Customer        114,000

---

## 🧪 UAT Test Results

| Test ID | Scenario | Result |
|---------|---------|--------|
| TC-001 | Full sales cycle — cash payment | ✅ Pass |
| TC-002 | Full sales cycle — 30-day credit | ✅ Pass |
| TC-003 | Customer return + credit note | ✅ Pass |
| TC-004 | Full purchase cycle + vendor bill | ✅ Pass |
| TC-005 | Bank statement reconciliation | ✅ Pass |
| TC-006 | Aged Receivables report accuracy | ✅ Pass |
| TC-007 | Automated AR follow-up email | ✅ Pass |---

## 🐛 Issues & Solutions
| # | Issue | Root Cause | Solution |
|---|-------|-----------|---------|
| 1 | Invoice could not be created | Invoicing Policy was set to Ordered Qty | Changed to Delivered Quantities |
| 2 | Negative stock appearing | Sales confirmed before goods received | Enabled Block Negative Stock in settings |
| 3 | VAT applied to export customer | No fiscal position configured | Created Export - 0% fiscal position |
| 4 | Product Type 'product' not found | Odoo 18 changed value to 'Goods' | Updated CSV file |
| 5 | Tax name '14%' had 2 matches | Egypt localization creates Sales + Purchase tax with same name | Renamed to 'VAT 14% Sales' and 'VAT 14% Purchases' |
| 6 | Arabic UOM 'م²' not recognized | Odoo stores UOM in English | Changed to 'm²' in CSV |## ⚙️ Chart of Accounts — Changes Made

### Accounts Added

| Code | Account Name | Type | Reason |
|------|-------------|------|--------|
| 500015 | إيرادات سيراميك | Income | Revenue tracking per product line |
| 500016 | إيرادات رخام | Income | Revenue tracking per product line |
| 500017 | إيرادات دهانات | Income | Revenue tracking per product line |
| 106012 | مخزون سيراميك | Current Assets | Inventory tracking per category |
| 106013 | مخزون رخام | Current Assets | Inventory tracking per category |
| 106014 | مخزون دهانات | Current Assets | Inventory tracking per category |
| 101030 | بنك QNB (USD) | Bank and Cash | USD import payments |

### Accounts Modified
| Account | Change | Reason |
|---------|--------|--------|
| Bank (default) | Renamed to بنك CIB | Company uses CIB and QNB only |

---

## 📸 Screenshots

| Screen | File |
|--------|------|
| Main Dashboard | screenshots/dashboard.png |
| Chart of Accounts | screenshots/chart-of-accounts.png |
| Sample Invoice + Journal Entry | screenshots/invoice.png |
| Aged Receivables Report | screenshots/aged-receivables.png |

---

## 📝 CV Description

> Implemented Odoo 18 Community (Sales, Accounting, Inventory, Purchase)
> for a wholesale building materials company with 3 warehouses and 45 employees.
> Designed full Chart of Accounts aligned with Egyptian VAT regulations (14%).
> Automated AR follow-up workflows reducing overdue collections by 35%.
> Reduced monthly financial close from 10 days to 2 days.