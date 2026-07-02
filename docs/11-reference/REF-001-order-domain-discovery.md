# REF-001 - Order Domain Discovery Record

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** REF-001  
**Document Type:** Architecture Discovery Record  
**Version:** 1.0.0  
**Status:** Temporary  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document preserves important discovery findings from the Order, amendment, pricing, currency, and integration workshops.

It is temporary and should eventually be merged into official Business, ADR, Governance, Accounting, and Integration documents.

---

## 2. Confirmed Findings

- Order is the central operational point from online and offline systems.
- A Commercial Transaction is the top-level business concept.
- An Order is the operational representation of a Commercial Transaction.
- Every Order must map to a Customer.
- An Order may contain multiple Product Lines.
- Operations validates the whole Order.
- One Order generates one Customer Invoice.
- One Order may generate multiple Vendor Bills.
- Vendor Bills are generated only when supplier cost exists.
- Vendor Bills may be grouped by Vendor.
- Discounts reduce selling price.
- Original Orders are not modified during amendment.
- Full Credit Note copies everything with negative values.
- Re-Invoice always starts with Full Credit Note.
- Amendment can happen multiple times.
- Profitability reporting must consider the full amendment chain.
- Travel MidOffice owns operational truth.
- Odoo owns accounting truth.

---

## 3. Open Questions

- Organization and security model
- Final approval rules after beta feedback
- Margin threshold policy
- Payment and reconciliation design
- Partial credit support as future enhancement
