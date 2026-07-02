# BUS-002 - Vendor Management

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-002  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Vendor Management domain for Travel MidOffice.

Vendor Management ensures that product-line costs are linked to the correct supplier so Vendor Bills can be generated, grouped, synchronized to Odoo, and reported accurately.

---

## 2. Business Context

A Vendor is an external supplier that provides travel products or services.

Examples include:

- Airlines
- Hotels
- Insurance providers
- Bus operators
- Visa agencies
- Ticketing agents
- Consolidators
- Tour operators

---

## 3. Scope

Vendor Management includes:

- Vendor profile
- Vendor classification
- Vendor product mapping
- Vendor contact information
- Supplier cost reference
- Vendor bill grouping
- Odoo partner mapping where required
- Vendor transaction history

Vendor Management does not own accounts payable balances. Accounting payables are owned by Odoo.

---

## 4. Vendor and Product Relationship

Each Product Line may have its own Vendor.

A single Order may contain multiple Product Lines with different Vendors.

If multiple Product Lines use the same Vendor, their costs may be grouped into one Vendor Bill.

---

## 5. Business Rules

| Rule ID | Rule |
|---|---|
| BR-VB-001 | One Order may generate multiple Vendor Bills. |
| BR-VB-002 | Vendor Bill generation is cost-driven. |
| BR-VB-003 | If no supplier cost exists, no Vendor Bill shall be generated for that cost. |
| BR-VB-004 | Product lines with the same vendor may be grouped into one Vendor Bill. |
| BR-VB-005 | Product lines with different vendors shall generate separate Vendor Bills. |

---

## 6. Odoo Considerations

Vendors may need to be mapped to Odoo partners when Vendor Bills are synchronized.

Travel MidOffice owns operational supplier usage. Odoo owns accounting payable treatment.

---

## 7. Open Questions

- Which roles can create or edit Vendors?
- Is vendor duplicate detection required before beta?
- Should vendor approval be required before use in financial documents?
- Should vendor contract terms be captured in the first release?
