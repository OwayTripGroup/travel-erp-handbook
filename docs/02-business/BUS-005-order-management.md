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

This document defines Order Management in Travel MidOffice.

An Order is the operational representation of a Commercial Transaction. It coordinates product lines, customers, vendors, validation, confirmation, financial document generation, amendment, reporting, and audit.

---

## 2. Business Context

Orders are received from online and offline source systems.

Online Orders may originate from the Website or Mobile App after payment.

Offline or corporate Orders may originate from Sales Operation or Amadeus and enter Travel MidOffice as Draft Orders.

---

## 3. Order Lifecycle

Current implementation:

```text
Draft -> Validate -> Confirm -> Invoice
```

Architecture recommendation:

```text
Draft -> Validated -> Confirmed -> Completed
```

Financial state should be tracked separately from operational Order state.

---

## 4. Validation

Validation confirms that the Order is commercially and operationally ready.

Validation may include:

- Customer mapping
- Product completeness
- Vendor mapping
- Cost validation
- Selling price validation
- Currency validation
- Exchange rate validation
- Tax availability
- Required travel information

Operations validates the whole Order as one atomic business unit.

---

## 5. Financial Document Generation

Current design:

- One Order generates one Customer Invoice.
- One Order may generate multiple Vendor Bills.
- Vendor Bills are generated based on cost and grouped by Vendor where applicable.

---

## 6. Amendment

After invoicing or Odoo synchronization, commercial changes should not directly edit the original Order.

The approved correction pattern is:

```text
Original Order
  -> Full Credit Note
  -> Re-Invoice Order
```

Original Orders remain viewable, searchable, and read-only.

---

## 7. Business Rules

| Rule ID | Rule |
|---|---|
| BR-ORD-001 | Every Order must belong to exactly one Customer. |
| BR-ORD-002 | An Order may contain multiple product lines. |
| BR-ORD-003 | An Order is validated and confirmed as one atomic operational unit. |
| BR-ORD-004 | Operations validates the whole Order before confirmation. |
| BR-ORD-008 | After invoice generation and Odoo synchronization, commercial correction shall use amendment workflows rather than direct editing. |
| BR-INV-001 | One Order shall generate one Customer Invoice. |
| BR-VB-001 | One Order may generate multiple Vendor Bills. |

---

## 8. Open Questions

- Final permission model for validation, confirmation, cancellation, amendment, and Odoo sync
- Final approval policy after beta feedback
- Final naming for terminal Order status
- Whether partial credit will be supported in the future
