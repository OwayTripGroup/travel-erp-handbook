# BUS-007 - Vendor Bill

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-007  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines Vendor Bill behavior in Travel MidOffice.

A Vendor Bill is a supplier payable document generated from product-line cost and synchronized to Odoo for accounting.

---

## 2. Business Rules

| Rule ID | Rule |
|---|---|
| BR-VB-001 | One Order may generate multiple Vendor Bills. |
| BR-VB-002 | Vendor Bill generation is cost-driven. |
| BR-VB-003 | If no supplier cost exists, no Vendor Bill shall be generated for that cost. |
| BR-VB-004 | Product lines with the same vendor may be grouped into one Vendor Bill. |
| BR-VB-005 | Product lines with different vendors shall generate separate Vendor Bills. |

---

## 3. Vendor Grouping

Vendor Bills are grouped by Vendor.

Example:

```text
Order
  Flight -> Vendor A
  Insurance -> Vendor A
  Hotel -> Vendor B

Generated Vendor Bills
  Vendor Bill A: Flight + Insurance
  Vendor Bill B: Hotel
```

---

## 4. Odoo Responsibility

Travel MidOffice prepares Vendor Bills.

Odoo owns accounts payable, vendor accounting, journal entries, payment, and reconciliation.

---

## 5. Amendment

If Vendor Bills require correction after invoicing or Odoo synchronization, the correction should follow Full Credit Note and Re-Invoice workflows.

---

## 6. Related Documents

- BUS-002 Vendor Management
- BUS-003 Product Management
- BUS-005 Order Management
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- ADR-002 Odoo Accounting System of Record
