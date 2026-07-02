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

A Vendor Bill is the payable document generated for a Vendor based on Product Line cost.

---

## 2. Business Rules

- One Order may generate multiple Vendor Bills.
- Vendor Bill generation is cost-driven.
- If no supplier cost exists, no Vendor Bill is generated.
- Product Lines with the same Vendor may be grouped into one Vendor Bill.
- Product Lines with different Vendors generate separate Vendor Bills.

---

## 3. Lifecycle

```text
Order Confirmed
  -> Vendor Bill Generated
  -> Odoo Sync Requested
  -> Odoo Sync Completed
  -> Payment / Reconciliation in Odoo
```

---

## 4. Ownership

Travel MidOffice owns vendor bill preparation and operational linkage.

Odoo owns accounting payables, payment, reconciliation, and journal impact.
