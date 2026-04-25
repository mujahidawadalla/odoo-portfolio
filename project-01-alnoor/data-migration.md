# 📦 Data Migration — Al-Noor Trading Co.

---

## Migration Overview

| Data | Records | Method | Status |
|------|---------|--------|--------|
| Customers | 15 | CSV Import | ✅ Done |
| Vendors | 8 | CSV Import | ✅ Done |
| Products | 15 | CSV Import | ✅ Done |
| Opening Stock | 15 lines | Physical Inventory | ✅ Done |
| Opening Balances | — | Journal Entry | ⬜ Pending |

---

## Migration Order & Why

Customers & Vendors first
← Products reference nothing
← But Invoices reference Customers
Products second
← Opening Stock references Products
Opening Stock third
← Needs Products + Locations to exist
Opening Balances last
← Needs all accounts configured first


---

## Pre-Migration Checklist
✅ Payment Terms created (Cash, 30 Days, 60 Days)
✅ Product Categories created (سيراميك, رخام, دهانات)
✅ Units of Measure enabled (m², Units)
✅ Taxes renamed (VAT 14% Sales, VAT 14% Purchases)
✅ Warehouses created (GIZ, HLW, TEN)
✅ Locations verified (GIZ/Stock, HLW/Stock, TEN/Stock)

---

## Issues Encountered & Resolved

| # | Issue | Root Cause | Solution |
|---|-------|-----------|---------|
| 1 | Payment Terms not matching | Terms created after CSV prepared | Created Cash/30 Days/60 Days to match CSV |
| 2 | Product Type 'product' not found | Odoo 18 renamed to 'Goods' | Updated CSV value to 'Goods' |
| 3 | Tax '14%' had 2 matches | Egypt localization creates Sales + Purchase tax with same name | Renamed to 'VAT 14% Sales' and 'VAT 14% Purchases' |
| 4 | Arabic UOM 'م²' not recognized | Odoo stores UOM in English | Changed to 'm²' in CSV |
| 5 | Location 'GIZ/المخزون' not found | Location name changed to English after warehouse edit | Used 'GIZ/Stock' format |
| 6 | Product Categories not found | Categories need full path | Used 'All / سيراميك' format |

---

## Key Lesson Learned
Always Export a sample record from Odoo first
then build your CSV to match the exact format.
This avoids 90% of import errors.

---

## Opening Stock — Distribution

| Warehouse | Products | Total Quantity |
|-----------|---------|----------------|
| GIZ/Stock (الجيزة) | Ceramics + Tiles (7 products) | 2,150 m² |
| HLW/Stock (حلوان) | Marble (4 products) | 660 m² |
| TEN/Stock (العاشر) | Paint (3 products) | 950 Units |

---

## Pending — Opening Balances
To be completed after:
✅ Chart of Accounts finalized
✅ Trial balance received from client accountant
✅ Go-Live date confirmed
Method: Manual Journal Entry
Date:   01/01/2024 (Go-Live date)

