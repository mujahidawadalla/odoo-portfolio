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
| 5 | Confirm Invoice | Journal Entry posted | ✅ Dr. AR 7980  | ✅ Pass	   |
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

**Scenario:** Standard Purchase from local Vendor 

| Field | Value |
|-------|-------|
| Vendor | شركة ألوان مصر للدهانات |
| Product | دهان أبيض 10 لتر |
| Quantity | 100 Units |
| Unit Price | 68 EGP |
| Tax | VAT 14% |
| Payment Terms | Cash |
| Expected Total | 	7,752.00 LE |

### Steps & Results

| # | Step | Expected | Actual | Status |
|---|------|----------|--------|--------|
| 1 | Create RFQ | PO created | ✅ P00001 - 7,752.00 EGP | ✅ Pass |
| 2 | Confirm PO | Receipt Auto created | ✅ GIZ/IN/00002 | ✅ Pass |
| 3 | Receive Products | Stock increased | ✅ Received = 100 | ✅ Pass |
| 4 | Create Bill | Bill from PO | ✅ فاتور/2026/05/0001| ✅ Pass |
| 5 | Confirm Bill | Journal entry created | ✅	Cr. AP 7,752 | ✅ Pass |
| 6 | Register Payment | Bill paid | ✅ 7,752.00 via Cash | ✅ Pass |

### Journal Entry Generated
| Account | Debit | Credit |
|---------|-------|--------|
| 	106013 مخزون دهانات | 6,800.00 LE | — |
| 	104041 VAT Input | 952.00 LE | — |
| 	201002 Payables | — | 7,752.00 LE |

### Issues Found
| # | Issue | Impact | Solution |
|---|-------|--------|---------|
| 1 | Product expense account defaulted to 400028 Others | Wrong expense account | Set at 106013 مخزون دهانات |
| 2 | Vendor AP account defaulted to 201002 Payables | Cannot differentiate local vs foreign vendors | Set AP account on Contact to 201031 موردو الداخل |

---

## TC-005 — Bank Reconciliation
**Status: ⏸️ Deferred**
**Reason:** Odoo 18 Community Bank Reconciliation workflow 
differs from previous versions. To be investigated and 
completed in next session.
**Priority:** High — required for monthly close process
---
## TC-006 — Aged Receivables Report

**Scenario:** Verify outstanding customer balances appear correctly in Aged Receivables

| Field | Value |
|-------|-------|
| Report | Aged Receivables |
| Start Date | 05/03/2026 |
| Period Length | 30 days |
| Target Moves | All Posted Entries |

### Steps & Results

| # | Step | Expected | Actual | Status |
|---|------|----------|--------|--------|
| 1 | Open Aged Receivables | Report loads | ✅ Report loaded successfully | ✅ Pass |
| 2 | Verify شركة الإسكندرية | 7,980 EGP in Not Due (60 days payment terms) | ✅ Verified successfully | ✅ Pass |
| 3 | Verify شركة النيل | 7,752 EGP in Not Due  | ✅ Verified successfully | ✅ Pass |
| 4 | Verify Credit Note impact |  النيل balance = 9,690 - 1,938 = 7,752 EGP | ✅ Verified successfully | ✅ Pass |

### Report Results
| Partner | Not Due | 0-30 | Total |
|---------|---------|------|-------|
| شركة اﻹسكندرية للتطوير | 7,980.00 LE | 0.00 LE | 7,980.00 LE |
| شركة النيل للمقاولات | 7,752.00 LE | 0.00 LE | 7,752.00 LE |

### Issues Found
None — report verified successfully

---

## TC-007 — AR Follow-up Automation

**Scenario:** Verify follow-up levels trigger correctly 
for overdue invoices in Odoo 18 Community

| Field | Value |
|-------|-------|
| Customer | شركة سيناء للإنشاءات |
| Invoice | الفات/2026/00003 |
| Due Date | 04/26/2026 |
| Days Overdue | 7 days |
| Expected Level | Level 1 — Email |

### Issues Found
| # | Issue | Impact | Solution |
|---|-------|--------|---------|
| 1 | No automated Follow-up Scheduled Action in Odoo 18 Community | Follow-up levels not assigned automatically | Run Follow-up manually via Follow-Ups → Send Letters and Emails |
| 2 | Send Overdue Email returns Invalid Operation error |  Cannot send follow-up emails directly from Contact | Configure email template in Accounting → Configuration → Follow-up Levels |

---

## Summary

| Total Tests | Passed | Failed | Pending | Deferred |
|-------------|--------|--------|---------|---------|
| 7 | 6 | 0 | 0 | 1 |