# ADR-002 - Odoo as Accounting System of Record

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**ADR ID:** ADR-002  
**Status:** Accepted  
**Version:** 1.0.0  
**Date:** 2026-07-02  
**Decision Owner:** Enterprise Architecture Team

---

## 1. Decision

Odoo is the accounting system of record.

Travel MidOffice owns operational workflows and prepares financial business documents. Odoo owns accounting records such as ledgers, journals, receivables, payables, taxes, payments, and reconciliation.

---

## 2. Context

Travel MidOffice generates operational financial documents such as Customer Invoices, Vendor Bills, Full Credit Notes, and Re-Invoices.

These documents are synchronized to Odoo for accounting treatment.

The system boundary must be clear because Travel MidOffice and Odoo serve different purposes.

Travel MidOffice is optimized for travel operations. Odoo is optimized for accounting.

---

## 3. Rationale

This decision supports:

- Clear separation of operational and accounting responsibilities
- Better auditability
- Cleaner Odoo integration
- Reduced duplication of accounting logic in Travel MidOffice
- Easier tax and journal governance through Odoo
- Better alignment with Finance ownership

---

## 4. Responsibilities

| Area | Owner |
|---|---|
| Order workflow | Travel MidOffice |
| Operational validation | Travel MidOffice |
| Customer Invoice preparation | Travel MidOffice |
| Vendor Bill preparation | Travel MidOffice |
| Full Credit Note workflow | Travel MidOffice |
| Re-Invoice workflow | Travel MidOffice |
| Journal entries | Odoo |
| Accounts receivable | Odoo |
| Accounts payable | Odoo |
| Tax configuration | Odoo / Finance |
| Payment and reconciliation | Odoo / Finance |

---

## 5. Consequences

### Positive Consequences

- Finance can govern accounting in Odoo.
- Travel MidOffice avoids becoming a duplicate accounting engine.
- Operational teams can focus on travel workflows.
- Integration contracts become explicit.

### Trade-offs

- Synchronization reliability becomes critical.
- Odoo identifiers must be tracked in Travel MidOffice.
- Tax and accounting master data must be synchronized or referenced correctly.
- Error recovery and retry workflows are required.

---

## 6. Business Rules Introduced

| Rule ID | Rule |
|---|---|
| BR-INT-002 | Odoo is the accounting system. |
| BR-TAX-001 | Tax configuration is owned by Finance and Odoo. |
| BR-TAX-003 | MidOffice shall not become the accounting tax source of truth. |

---

## 7. Related Documents

- GOV-002 Domain Dictionary
- GOV-005 Business Rules Catalog
- BUS-000 Travel ERP Business Overview
- ARC-000 Design Principles
- ADR-001 Travel MidOffice as Operational System of Record
- ADR-003 Document-Based Amendment Strategy
- INT-001 Odoo Integration
