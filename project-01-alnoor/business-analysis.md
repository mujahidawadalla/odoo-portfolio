# 📋 Business Analysis — Al-Noor Trading Co.

---

## Company Profile

| Field | Details |
|-------|---------|
| **Company** | Al-Noor Trading Co. |
| **Industry** | Wholesale — Building Materials |
| **Size** | 45 employees |
| **Locations** | 3 warehouses — Cairo (Giza, Helwan, 10th of Ramadan) |
| **Revenue** | ~12M EGP/month |
| **Previous System** | Excel + disconnected legacy accounting software |

---

## AS-IS Process (Before Odoo)

### Sales Cycle
Customer calls → Excel order recorded → Manual invoice in legacy system
→ Paper delivery note to warehouse → Manual stock deduction
→ Manual collection follow-up → Manual journal entry

### Problems Identified

| # | Problem | Business Impact | Priority |
|---|---------|----------------|---------|
| 1 | Double data entry (Excel + accounting system) | 3 hours wasted daily | High |
| 2 | No real-time inventory visibility | Stock-outs, over-ordering | High |
| 3 | Monthly close takes 10 days | Late management decisions | High |
| 4 | No systematic AR follow-up | High overdue receivables | Medium |
| 5 | No per-warehouse reporting | Cannot measure branch performance | Medium |

---

## TO-BE Process (After Odoo)

### Sales Cycle
Quotation in Odoo → Sales Order (approval if >50K EGP)
→ Delivery Order (warehouse notified instantly)
→ Invoice auto-created → Payment registered
→ Automated AR follow-up if overdue

### Expected Results

| Metric | Before | After | Improvement |
|--------|--------|-------|-------------|
| Monthly close | 10 days | 2 days | 80% faster |
| AR follow-up | Manual | Automated | 100% systematic |
| Stock visibility | End of day | Real-time | Instant |
| Data entry | Twice | Once | 50% less effort |

---

## Scope

### In Scope — Phase 1
- Sales Management
- Accounting & Finance
- Inventory Management (3 warehouses)
- Purchase Management

### Out of Scope — Phase 2
- CRM
- HR & Payroll
- Manufacturing
- eCommerce

---

## Kickoff Meeting — Key Decisions

| Question | Answer | Odoo Setting |
|----------|--------|-------------|
| Who approves quotations? | Manager if > 50,000 EGP | Purchase Approval |
| Invoice timing? | After delivery | Invoicing Policy: Delivered |
| Foreign currency? | No | Single currency EGP |
| Fixed prices? | Yes — all customers same price | No Pricelists |
| Discounts policy? | Fixed prices, no discounts | Discounts: Disabled |
| Inventory costing? | Average cost | AVCO |
| Warehouse structure? | 3 geographic locations | 3 separate Warehouses |

---

## Data Migration Summary

| Data | Source | Records | Method |
|------|--------|---------|--------|
| Customers | Excel | 15 | CSV Import |
| Vendors | Excel | 8 | CSV Import |
| Products | Manual | 15 | CSV Import |
| Opening Stock | Physical count | 15 lines | Physical Inventory |
| Opening Balances | Trial balance 31/12 | Pending | Journal Entry |