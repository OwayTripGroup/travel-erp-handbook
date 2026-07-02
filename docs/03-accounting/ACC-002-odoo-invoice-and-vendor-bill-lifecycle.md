# ACC-002 - Odoo Invoice and Vendor Bill Lifecycle

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** ACC-002  
**Document Type:** Accounting Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document explains how Customer Invoices and Vendor Bills prepared by Travel MidOffice relate to Odoo accounting documents.

---

## 2. Customer Invoice Lifecycle

```text
Travel MidOffice Customer Invoice
  -> Sync to Odoo
  -> Odoo Customer Invoice Created
  -> Odoo Posted State
  -> Payment / Reconciliation in Odoo
```

Travel MidOffice should track sync status and Odoo document identifiers.

---

## 3. Vendor Bill Lifecycle

```text
Travel MidOffice Vendor Bill
  -> Sync to Odoo
  -> Odoo Vendor Bill Created
  -> Odoo Posted State
  -> Vendor Payment / Reconciliation in Odoo
```

Travel MidOffice prepares supplier payable documents. Odoo owns accounting payables.

---

## 4. Draft, Posted, Paid, Reversed

| Odoo State | Meaning |
|---|---|
| Draft | Accounting document exists but is not final. |
| Posted | Accounting document is official in Odoo. |
| Paid | Payment and reconciliation are completed in Odoo. |
| Reversed | Original accounting impact is reversed through credit or reversal document. |

---

## 5. Reversal and Re-Invoice

Travel MidOffice uses Full Credit Note and Re-Invoice to correct financial documents.

The Odoo side should reflect reversal and replacement accounting documents, while Travel MidOffice preserves the operational amendment chain.

---

## 6. Integration Requirements

Travel MidOffice should store:

- Odoo document ID
- Odoo document name or number
- Sync status
- Sync date
- Error message where applicable
- Original document reference for reversals

---

## 7. Related Documents

- ACC-001 Accounting Lifecycle
- ADR-002 Odoo Accounting System of Record
- BUS-006 Customer Invoice
- BUS-007 Vendor Bill
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- INT-001 Odoo Integration
