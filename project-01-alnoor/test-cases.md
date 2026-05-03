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

## TC-002 — Sales Cycle Without Payment (Credit Customer)

**Scenario:** Standard sale to Outside of Cairo customers without payment

| Field | Value |
|-------|-------|
| Customer |     شركة اﻹسكندرية للتطوير     |
| Product |       بلاط أرضي بيج 40×40     |
| Quantity |     100 m²       |
| Unit Price |     70 EGP       |
| Tax |     VAT 14%      |
| Payment Terms |      60 Days      |
| Expected Total |      7980 EGP (incl. VAT 14%)      |

### Steps & Results

| # | Step | Expected | Actual | Status |
|---|------|----------|--------|--------|
| 1 | Create Quotation | SO created with VAT | ✅ S00002 - 7980 EGP  | ✅ Pass   |
| 2 | Confirm Sales Order | Delivery auto-created | ✅ GIZ/OUT/00002  | ✅ Pass   |
| 3 | Validate Delivery | Stock deducted 100 m² | ✅ Delivered = 100  | ✅ Pass   |
| 4 | Create Invoice | Invoice from SO | ✅ 2026/00002/الفات | ✅ Pass   |
| 5 | Confirm Invoice | Journal Entry posted | ✅ Dr. AR 7980  | ✅ Pass   |
| 6 | Verify Aged Receivables | Invoice appears unpaid | ✅ شركة الإسكندرية —EGP 7,980 في عمود 0-30  | ✅ Pass   |

### Journal Entry Generated
| Account | Debit | Credit |
|---------|-------|--------|
|   	102021 عملاء خارج القاهرة      |  7980.00 LE   | — |
|   	201017 VAT Output    | — |  980.00 LE   |
|   	500015 ايرادات سيراميك    | — |  7000.00 LE   |

### Issues Found
| # | Issue | Impact | Solution |
|---|-------|--------|---------|
| 1 |     Income Account defaulted to 500001    |    Wrong revenue account on invoice    |    Set income account on product to 500015    |
| 2 |     AR Account defaulted to 102011      |    Cannot differentiate between local and outside Cairo customers in AR reports   |   Set AR account on contact to 102021    |

---

## TC-003 — Customer Return + Credit Note

**Scenario:** Partial return of 20 m² damaged goods from invoice الفات/2026/00001

| Field | Value |
|-------|-------|
| Customer |        شركة النيل للمقاولات     |
| Original Invoice |        الفات/2026/00001    |
| Product |  سيراميك أبيض 60×60 |
| Return Quantity | 20 m²  |
| Unit Price | 85 EGP |
| Expected Credit | 1,938 EGP |

### Steps & Results

| # | Step | Expected | Actual | Status |
|---|------|----------|--------|--------|
| 1 | Return Delivery | Return transfer created (GIZ/IN/00001)  | ✅ GIZ/IN/00001 — 20 m² returned to stock  | ✅ Pass |
| 2 | Validate Return | Return transfer validated (GIZ/IN/00001) | ✅ GIZ/IN/00001 — 20 m² returned to stock | ✅ Pass |
| 3 | Create Credit Note | Credit Note created (Rالفات/2026/00001) | ✅ Rالفات/2026/00001 Credit Note created | ✅ Pass |
| 4 | Adjust Quantity to 20 m² | Modify quantity to 20 m² | ✅ 20 m² Credit Note value | ✅ Pass |
| 5 | Confirm Credit Note | Confirm the Credit Note | ✅ Rالفات/2026/00001 Credit note confirmed | ✅ Pass |

### Journal Entry Generated
| Account | Debit | Credit |
|---------|-------|--------|
| 500015 ايرادات سيراميك | 1,700.00 LE | — |
| 201017 VAT Output | 238.00 LE | — |
| 102011 Accounts Receivable | — | 1,938.00 LE |

### Issues Found
| # | Issue | Impact | Solution |
|---|-------|--------|---------|
| 1 | Credit Note Quantity | opened with (100 m²) | Modify manually to 20 m² |
| 2 | AR Account defaulted to 102011 | Cannot differentiate local vs outside Cairo customers | Set AR account on Contact to 102020 |
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