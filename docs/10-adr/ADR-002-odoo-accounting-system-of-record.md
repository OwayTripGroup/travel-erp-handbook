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

## 4. Responsibility Boundary

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
