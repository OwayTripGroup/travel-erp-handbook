# INT-001 - Odoo Integration

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** INT-001  
**Document Type:** Integration Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the integration boundary between Travel MidOffice and Odoo.

Travel MidOffice owns operational workflows. Odoo owns accounting records.

---

## 2. Integration Scope

The Odoo integration includes:

- Customer partner synchronization where required
- Vendor partner synchronization where required
- Customer Invoice synchronization
- Vendor Bill synchronization
- Full Credit Note synchronization
- Re-Invoice synchronization
- Tax reference consumption
- Odoo callback handling
- Sync job tracking and retry

---

## 3. Ownership Boundary

| Area | Owner |
|---|---|
| Operational Order workflow | Travel MidOffice |
| Customer Invoice preparation | Travel MidOffice |
| Vendor Bill preparation | Travel MidOffice |
| Credit Note workflow | Travel MidOffice |
| Re-Invoice workflow | Travel MidOffice |
| Accounting posting | Odoo |
| Journal entries | Odoo |
| Tax accounting | Odoo / Finance |
| Payment and reconciliation | Odoo / Finance |

---

## 4. Document Synchronization Lifecycle

```text
Document Generated in Travel MidOffice
  -> Sync Job Created
  -> Payload Sent to Odoo
  -> Odoo Document Created or Updated
  -> Odoo Callback or Response Received
  -> Sync Status Updated
  -> Audit Trail Recorded
```

---

## 5. Required Traceability

Travel MidOffice should preserve:

- MidOffice document identifier
- Odoo document identifier
- Odoo document number
- Sync status
- Sync attempt count
- Last sync date
- Error message where applicable
- Original document reference for credit or reversal

---

## 6. Error Handling Principles

- Sync failures should not silently disappear.
- Failed sync jobs should be visible to operations or administration.
- Retry should be controlled and auditable.
- Business documents should not be duplicated in Odoo without clear idempotency control.

---

## 7. Business Rules

| Rule ID | Rule |
|---|---|
| BR-INT-002 | Odoo is the accounting system. |
| BR-INT-003 | Customer Invoices and Vendor Bills shall be synchronized to Odoo for accounting. |
| BR-INT-004 | Odoo shall not become the owner of operational workflow state. |
| BR-INT-005 | Integration operations should preserve traceability between MidOffice and Odoo documents. |

---

## 8. Related Documents

- ADR-001 Travel MidOffice Operational System of Record
- ADR-002 Odoo Accounting System of Record
- ACC-001 Accounting Lifecycle
- ACC-002 Odoo Invoice and Vendor Bill Lifecycle
- BUS-006 Customer Invoice
- BUS-007 Vendor Bill
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
