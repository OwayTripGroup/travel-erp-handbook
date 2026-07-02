# BUS-001 - Customer Management

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-001  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Customer Management domain for Travel MidOffice.

Customer Management ensures that every Commercial Transaction and Order is linked to a valid Customer before operational processing, financial document generation, Odoo synchronization, reporting, and audit.

---

## 2. Business Context

A Customer is the purchasing party of a Commercial Transaction.

Travel MidOffice does not support anonymous Orders. Customer mapping is mandatory because customer identity is required for operational ownership, customer invoice generation, Odoo partner synchronization, reporting, and audit.

---

## 3. Scope

Customer Management includes:

- Customer profile
- Customer classification
- Corporate customer support
- Customer contact details
- Customer search
- Customer transaction history
- Customer mapping from source systems
- Odoo partner synchronization where required

Customer Management does not own accounting receivable balances. Accounting receivables are owned by Odoo.

---

## 4. Ownership

| Area | Owner |
|---|---|
| Customer commercial relationship | Sales |
| Customer operational usage | Travel MidOffice |
| Customer accounting partner | Odoo / Finance |
| Customer reporting | Travel MidOffice and Power BI |

---

## 5. Business Rules

| Rule ID | Rule |
|---|---|
| BR-CUS-001 | Anonymous Orders are not supported. |
| BR-CUS-002 | Customer mapping is mandatory before an Order can be processed in MidOffice. |
| BR-ORD-001 | Every Order must belong to exactly one Customer. |

---

## 6. Customer Lifecycle

```text
Customer Created
  -> Customer Validated
  -> Customer Used in Order
  -> Customer Synced to Odoo if required
  -> Customer History Updated
```

Customer records should remain available for historical transactions even if later made inactive.

---

## 7. Customer Types

Travel MidOffice should support customer classification.

Typical classifications include:

- Individual Customer
- Corporate Customer
- Internal Customer where applicable
- Future customer categories

Corporate customer support is important for offline and business travel workflows.

---

## 8. Source System Mapping

Customers may originate from online or offline channels.

For online transactions, customer information may come from the Website or Mobile App.

For offline transactions, customer information may be created or selected by Sales or Operations.

Travel MidOffice must map source customer data into one valid Customer record before Order processing.

---

## 9. Odoo Considerations

When accounting documents are synchronized to Odoo, the Customer must be mapped to an Odoo partner where required.

Travel MidOffice owns operational customer data. Odoo owns accounting partner usage for receivables, payments, and reconciliation.

Customer synchronization should preserve:

- Travel MidOffice customer identifier
- Odoo partner identifier
- Sync status
- Last sync date
- Error status where applicable

---

## 10. Audit and Reporting

Customer changes that affect financial or operational documents should be auditable.

Reporting should support visibility into:

- Orders by customer
- Customer transaction history
- Corporate customer volume
- Customer invoice history
- Amendment history by customer

---

## 11. Architecture Notes

Customer Management is a foundational domain because every Order requires a Customer.

The Customer domain should avoid becoming overloaded with accounting responsibilities. Accounting balances, payments, and reconciliation remain Odoo responsibilities.

---

## 12. Open Questions

The following items require future organization and security discovery:

- Which roles can create Customers?
- Which roles can edit Customers?
- Whether Finance approval is required for accounting-sensitive customer changes
- Whether duplicate customer detection is required before beta
- Whether corporate customer credit limits are required in the future

---

## 13. Related Documents

- GOV-002 Domain Dictionary
- GOV-005 Business Rules Catalog
- BUS-000 Travel ERP Business Overview
- ADR-001 Travel MidOffice as Operational System of Record
- ADR-002 Odoo as Accounting System of Record
