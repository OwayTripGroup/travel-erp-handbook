# BUS-006 - Customer Invoice

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-006  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines Customer Invoice behavior in Travel MidOffice.

A Customer Invoice is the customer billing document generated from an Order and synchronized to Odoo for accounting.

---

## 2. Business Rules

| Rule ID | Rule |
|---|---|
| BR-INV-001 | One Order shall generate one Customer Invoice. |
| BR-INV-002 | Customer billing is consolidated at Order level even when the Order has multiple product lines. |
| BR-INV-003 | Posted or synchronized Customer Invoices shall not be edited directly for commercial changes. |

---

## 3. Lifecycle

```text
Order Confirmed
  -> Customer Invoice Generated
  -> Odoo Sync Requested
  -> Odoo Sync Completed
  -> Payment / Accounting Handling in Odoo
```

---

## 4. Odoo Responsibility

Travel MidOffice prepares and sends the Customer Invoice.

Odoo owns accounting treatment, receivables, journal entries, tax posting, payment, and reconciliation.

---

## 5. Amendment

If a Customer Invoice must be corrected after invoicing or Odoo synchronization, the correction should use Full Credit Note and Re-Invoice.

---

## 6. Related Documents

- BUS-005 Order Management
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- ADR-002 Odoo Accounting System of Record
- ADR-003 Document-Based Amendment Strategy
