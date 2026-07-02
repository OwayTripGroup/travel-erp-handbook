# ACC-001 - Accounting Lifecycle

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** ACC-001  
**Document Type:** Accounting Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the accounting lifecycle boundary between Travel MidOffice and Odoo.

Travel MidOffice owns operational financial document preparation. Odoo owns accounting records, journal entries, receivables, payables, payments, and reconciliation.

---

## 2. System Boundary

| Area | Owner |
|---|---|
| Order validation | Travel MidOffice |
| Customer invoice preparation | Travel MidOffice |
| Vendor bill preparation | Travel MidOffice |
| Credit note workflow | Travel MidOffice |
| Re-invoice workflow | Travel MidOffice |
| Journal entries | Odoo |
| Tax posting | Odoo |
| Accounts receivable | Odoo |
| Accounts payable | Odoo |
| Payment and reconciliation | Odoo |

---

## 3. High-Level Lifecycle

```text
Order Confirmed
  -> Customer Invoice Generated
  -> Vendor Bill Generated
  -> Odoo Sync Requested
  -> Odoo Documents Created / Posted
  -> Payment and Reconciliation in Odoo
  -> Reporting and Audit
```

---

## 4. Correction Lifecycle

Corrections after invoicing should not directly edit historical operational or accounting documents.

Approved correction lifecycle:

```text
Original Order
  -> Full Credit Note
  -> Re-Invoice if required
  -> New Customer Invoice and Vendor Bills
  -> Odoo Synchronization
```

---

## 5. Accounting Governance

Finance owns accounting policy.

Odoo owns accounting treatment.

Travel MidOffice must preserve enough reference data to trace each accounting document back to its operational source.

---

## 6. Related Documents

- ADR-002 Odoo Accounting System of Record
- ADR-003 Document-Based Amendment Strategy
- BUS-005 Order Management
- BUS-006 Customer Invoice
- BUS-007 Vendor Bill
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
