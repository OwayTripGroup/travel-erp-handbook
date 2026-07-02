# BUS-004 - Commercial Transaction

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-004  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines Commercial Transaction as the highest-level business concept in the Travel MidOffice domain.

A Commercial Transaction represents the commercial agreement between Oway Travel and a Customer to purchase one or more travel products or services.

---

## 2. Business Definition

A Commercial Transaction begins when the Customer commits to purchase, or when Oway Travel commits to fulfill the purchase.

The Order is the operational representation of the Commercial Transaction inside Travel MidOffice.

```text
Commercial Transaction
  -> Order
  -> Customer Invoice
  -> Vendor Bill
  -> Amendment if required
```

---

## 3. Source Systems

Commercial Transactions may originate from:

- Oway Travel Website
- Oway Travel Mobile App
- Sales Operation
- Amadeus
- Manual MidOffice entry
- Future partner systems

Source systems create or send Commercial Transactions, but Travel MidOffice becomes the operational owner once the transaction is received.

---

## 4. Ownership

| Area | Owner |
|---|---|
| Commercial agreement | Sales / Online Platform |
| Operational ownership after receipt | Travel MidOffice |
| Accounting records | Odoo |
| Reporting | Travel MidOffice / Power BI |

---

## 5. Lifecycle

```text
Customer Commits
  -> Commercial Transaction Created
  -> Travel MidOffice Receives Transaction
  -> Draft Order Created
  -> Order Validated
  -> Order Confirmed
  -> Financial Documents Generated
  -> Odoo Synchronization
  -> Reporting and Audit
```

---

## 6. Relationship to Order

The Order is not the same as the Commercial Transaction.

The Commercial Transaction is the business concept.

The Order is the operational object used by Travel MidOffice to validate, confirm, invoice, bill vendors, amend, and report the transaction.

This distinction allows the handbook to remain stable even if implementation evolves.

---

## 7. Amendment Relationship

Commercial changes after confirmation or invoicing are handled through document-based amendment.

```text
Original Commercial Transaction
  -> Original Order
  -> Full Credit Note
  -> Re-Invoice Order
```

The amendment chain preserves the history of the original transaction and its corrections.

---

## 8. Business Rules

| Rule ID | Rule |
|---|---|
| BR-INT-001 | Travel MidOffice is the operational system of record after transaction receipt. |
| BR-ORD-001 | Every Order must belong to exactly one Customer. |
| BR-AMD-003 | Amendment chains must preserve relationships between original and replacement documents. |

---

## 9. Reporting Requirements

Reporting must support:

- Original commercial value
- Credit impact
- Re-invoice value
- Final net outcome
- Full amendment chain profitability

---

## 10. Related Documents

- GOV-002 Domain Dictionary
- GOV-003 Business Capability Map
- GOV-004 Business Event Catalog
- GOV-005 Business Rules Catalog
- BUS-005 Order Management
- ADR-001 Travel MidOffice Operational System of Record
- ADR-003 Document-Based Amendment Strategy
