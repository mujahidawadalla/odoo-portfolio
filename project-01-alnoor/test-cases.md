# 🧪 Test Cases — Al-Noor Trading Co.

---

## Test Environment
| Field | Details |
|-------|---------|
| Odoo Version | 18 Community |
| Database | al-noor-trading |
| Test Date | 04/28/2026 |
| Tested By | Mujahid Awadalla |

---

## TC-001 — Full Sales Cycle (Cash Customer)

**Scenario:** Standard sale to local customer — full delivery — early payment

| Field | Value |
|-------|-------|
| Customer | شركة النيل للمقاولات |
| Product | سيراميك أبيض 60×60 |
| Quantity | 100 m² |
| Unit Price | 85 EGP |
| Tax | VAT 14% Sales |
| Payment Terms | 30 Days |
| Expected Total | 9,690 EGP |

### Steps & Results

| # | Step | Expected | Actual | Status |
|---|------|----------|--------|--------|
| 1 | Create Quotation | SO created with VAT | ✅ S00001 — 9,690 EGP | ✅ Pass |
| 2 | Confirm Sales Order | Delivery auto-created | ✅ GIZ/OUT/00001 | ✅ Pass |
| 3 | Validate Delivery | Stock deducted 100 m² | ✅ Delivered = 100 | ✅ Pass |
| 4 | Create Invoice | Invoice from SO | ✅ الفات/2026/00001 | ✅ Pass |
| 5 | Confirm Invoice | Journal Entry posted | ✅ Dr. AR 9,690 | ✅ Pass |
| 6 | Register Payment | Invoice IN PAYMENT | ✅ 9,690 via بنك CIB | ✅ Pass |
| 7 | Bank Reconciliation | Invoice PAID | ⏸️ Community limitation | ⏸️ Deferred |

### Journal Entry Generated
| Account | Debit | Credit |
|---------|-------|--------|
| 102011 Accounts Receivable | 9,690 | — |
| 500015 إيرادات سيراميك | — | 8,500 |
| 201017 VAT Output | — | 1,190 |

### Issues Found
| # | Issue | Impact | Solution |
|---|-------|--------|---------|
| 1 | Product income account defaulted to 500001 | Wrong revenue account | Set income account on each product |
| 2 | Customer AR defaulted to 102011 | Not using specific AR accounts | Set AR account on each Contact → Accounting tab |
| 3 | Bank Reconciliation UI changed in Odoo 18 | Cannot complete reconciliation | Deferred to Phase 2 investigation |

---

## TC-002 — Full Sales Cycle (Credit Customer)
**Status: ⬜ Pending**

---

## TC-003 — Customer Return + Credit Note
**Status: ⬜ Pending**

---

## TC-004 — Full Purchase Cycle
**Status: ⬜ Pending**

---

## TC-005 — Bank Reconciliation
**Status: ⏸️ Deferred**
**Reason:** Odoo 18 Community Bank Reconciliation workflow 
differs from previous versions. To be investigated and 
completed in next session.
**Priority:** High — required for monthly close process
---
## TC-006 — Aged Receivables Report
**Status: ⬜ Pending**

---

## TC-007 — AR Follow-up Automation
**Status: ⬜ Pending**

---

## Summary

| Total Tests | Passed | Failed | Pending | Deferred |
|-------------|--------|--------|---------|---------|
| 7 | 1 | 0 | 5 | 1 |