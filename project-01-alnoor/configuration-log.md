# ⚙️ Configuration Log — Al-Noor Trading Co.

> Every setting documented with the reason why.
> This is the single source of truth for this implementation.

---

## Company Setup

| Setting | Value | Reason |
|---------|-------|--------|
| Company Name | Al-Noor Trading Co. | — |
| Country | Egypt | — |
| Currency | EGP | Primary trading currency |
| Fiscal Year | January → December | Standard Egyptian fiscal year |

---

## Accounting Settings

| Setting | Value | Reason |
|---------|-------|--------|
| Fiscal Localization | Egypt | Loads Egyptian CoA + VAT structure |
| Sales Tax | VAT 14% Sales | Egyptian VAT law |
| Purchase Tax | VAT 14% Purchases | Egyptian VAT law |
| Tax Display | Tax Excluded | B2B — prices shown without tax |
| Rounding Method | Round per Line | Standard for Egypt |
| Analytic Accounting | ✅ Enabled | Future profitability analysis |
| Lock Date | Set monthly after close | Prevent backdated edits |

---

## Chart of Accounts — Additions

| Code | Account Name | Type | Reason |
|------|-------------|------|--------|
| 500015 | إيرادات سيراميك | Income | Revenue tracking per product line |
| 500016 | إيرادات رخام | Income | Revenue tracking per product line |
| 500017 | إيرادات دهانات | Income | Revenue tracking per product line |
| 106012 | مخزون سيراميك | Current Assets | Inventory per category |
| 106013 | مخزون رخام | Current Assets | Inventory per category |
| 106014 | مخزون دهانات | Current Assets | Inventory per category |
| 101030 | بنك QNB (USD) | Bank and Cash | USD import payments |

### Accounts Modified
| Account | Change | Reason |
|---------|--------|--------|
| Bank (default) | Renamed → بنك CIB | Company uses CIB and QNB only |
| Tax 14% (Sales) | Renamed → VAT 14% Sales | Avoid ambiguity with purchase tax |
| Tax 14% (Purchase) | Renamed → VAT 14% Purchases | Avoid ambiguity with sales tax |

---

## Payment Terms Created

| Name | Terms | Used For |
|------|-------|---------|
| Cash | Due immediately | Walk-in customers |
| 30 Days | Net 30 | Regular customers |
| 60 Days | Net 60 | Large contractors |

---

## Inventory Settings

| Setting | Value | Reason |
|---------|-------|--------|
| Costing Method | AVCO | Building materials mixed in storage |
| Storage Locations | ✅ Enabled | 3 warehouses need location tracking |
| Units of Measure | ✅ Enabled | m² for tiles/marble, Units for paint |

## Warehouses Created

| Name | Short Code | Location | Products |
|------|-----------|----------|---------|
| مستودع الجيزة | GIZ | Giza | Ceramics + Tiles |
| مستودع حلوان | HLW | Helwan | Marble |
| مستودع العاشر | TEN | 10th of Ramadan | Paint |

---

## Sales Settings

| Setting | Value | Reason |
|---------|-------|--------|
| Invoicing Policy | Delivered Quantities | Pay for what was received |
| Margins | ✅ Enabled | Management profitability view |
| Sale Warnings | ✅ Enabled | Alert for late-paying customers |
| Lock Confirmed Sales | ✅ Enabled | No edits after confirmation |
| Delivery Methods | ✅ Enabled | Company handles delivery |
| Default Quotation Validity | 30 days | Market standard |
| Variants | ❌ Disabled | Independent products not variants |
| Pricelists | ❌ Disabled | Unified pricing |
| Discounts | ❌ Disabled | Fixed prices |

---

## Key Decisions Log

| Decision | Alternatives Considered | Chosen Because |
|----------|------------------------|----------------|
| AVCO costing | FIFO | Materials mixed in storage — AVCO more practical |
| 3 separate Warehouses | 1 warehouse + locations | Geographic separation + per-branch reporting |
| Delivered invoicing | Ordered invoicing | Customer pays for received goods only |
| No Pricelists | Pricelists per customer | All customers have same fixed price |