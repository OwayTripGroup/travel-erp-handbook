# BUS-005 - Order Management

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-005  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Order Management domain for Travel MidOffice.

Order Management is the operational heart of the platform. It converts a Commercial Transaction into a controlled operational workflow that supports validation, confirmation, financial document generation, Odoo synchronization, amendment, reporting, and audit.

---

## 2. Business Definition

An Order is the operational representation of a Commercial Transaction inside Travel MidOffice.

It is the central operational object used to coordinate:

- Customer
- Product Lines
- Vendors
- Selling price
- Cost
- Currency
- Exchange rate
- Customer Invoice
- Vendor Bills
- Full Credit Note
- Re-Invoice
- Reporting

---

## 3. Source Channels

Orders may originate from:

- Oway Travel Website
- Oway Travel Mobile App
- Amadeus
- Sales Operation
- Manual MidOffice entry
- Future partner systems

Each source system may have its own status, but Travel MidOffice maintains its own operational lifecycle.

---

## 4. Core Business Rules

| Rule ID | Rule |
|---|---|
| BR-ORD-001 | Every Order must belong to exactly one Customer. |
| BR-ORD-002 | An Order may contain multiple product lines. |
| BR-ORD-003 | An Order is validated and confirmed as one atomic operational unit. |
| BR-ORD-004 | Operations validates the whole Order before confirmation. |
| BR-ORD-006 | Orders shall not be physically deleted; cancellation status shall be used. |
| BR-INV-001 | One Order shall generate one Customer Invoice. |
| BR-VB-001 | One Order may generate multiple Vendor Bills. |
| BR-AMD-001 | Commercial changes after confirmation or invoicing use document-based amendment. |

---

## 5. Order Lifecycle

Current implementation lifecycle:

```text
Draft
  -> Validate
  -> Confirm
  -> Invoice
```

Recommended target model:

```text
Draft
  -> Validated
  -> Confirmed
  -> Completed
  -> Cancelled
```

Invoice generation should be treated as a financial milestone rather than a pure Order status.

---

## 6. Lifecycle Definitions

| Stage | Meaning |
|---|---|
| Draft | Entry point for Orders received into Travel MidOffice. |
| Validate | Operational review of customer, product, vendor, price, cost, currency, exchange rate, tax, and required travel data. |
| Confirm | Business decision that the Order is valid and ready for financial document generation. |
| Invoice | Current implementation state indicating financial documents have been generated. |
| Completed | Recommended future operational terminal state. |
| Cancelled | Order stopped before financial document generation. |

---

## 7. Validation

Validation is a core business control point.

Validation should confirm:

- Customer is mapped
- Product Lines are complete
- Vendors are mapped
- Selling amount is valid
- Cost amount is valid
- Currency is valid
- Exchange rate is available
- Required travel data exists
- Tax references are available where required

Operations validates the whole Order as one atomic business unit.

---

## 8. Financial Document Generation

After confirmation, the Order can generate:

- One Customer Invoice
- One or more Vendor Bills

Vendor Bills are generated based on supplier cost and vendor grouping.

If there is no cost for a product line, no Vendor Bill is generated for that cost.

---

## 9. Amendment

After confirmation or invoicing, direct commercial editing is not allowed.

Correction must use:

- Full Credit Note
- Re-Invoice

The original Order remains viewable, searchable, and read-only.

---

## 10. Status Separation

Travel MidOffice should maintain separation between:

- Order Status
- Invoice Status
- Odoo Sync Status
- Payment Status

This avoids mixing operational workflow with financial or integration milestones.

---

## 11. Reporting

Order reporting must support:

- Orders by source channel
- Orders by customer
- Orders by product type
- Orders by team
- Orders by status
- Profitability by amendment chain
- Original vs final transaction outcome

---

## 12. Open Questions

- Final target status naming before production
- Role-based permission matrix
- Approval policy after beta feedback
- Whether partial credit will be supported later
- Final UI timeline design for amendment chains

---

## 13. Related Documents

- BUS-004 Commercial Transaction
- BUS-001 Customer Management
- BUS-002 Vendor Management
- BUS-003 Product Management
- BUS-006 Customer Invoice
- BUS-007 Vendor Bill
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- ADR-003 Document-Based Amendment Strategy
