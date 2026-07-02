# BUS-003 - Product Management

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-003  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Product Management domain for Travel MidOffice.

Product Management ensures that travel products and product lines are consistently classified, configured, mapped to vendors, used in Orders, and reported across operational, financial, and integration workflows.

---

## 2. Business Context

A Product is a sellable travel service offered by Oway Travel.

Supported product types include:

- Flight
- Hotel
- Bus
- Insurance
- Visa
- Car Rental
- Tour
- Future travel products

A single Order may contain multiple Product Lines. This is especially important for tour packages and bundled travel transactions.

---

## 3. Product vs Product Line

A Product is the reusable business category or service type.

A Product Line is the actual instance of that product within an Order.

Example:

```text
Product Type: Flight

Order Product Line:
  Flight from Yangon to Bangkok
  Vendor: Airline or consolidator
  Selling Price: 500
  Cost: 430
```

---

## 4. Ownership

| Area | Owner |
|---|---|
| Product category | Product Team |
| Product operational usage | Operations |
| Product selling policy | Sales / Online Platform |
| Product vendor mapping | Operations |
| Product analytics mapping | Product / Finance / Reporting |
| Accounting mapping | Finance / Odoo |

---

## 5. Business Rules

| Rule ID | Rule |
|---|---|
| BR-PRD-001 | A single Order may include different product types. |
| BR-PRD-002 | Product lines may have their own vendor, cost, currency, exchange rate, and operational details. |
| BR-PRD-003 | A single product type may involve more than one vendor where business scenarios require it. |
| BR-PRD-004 | If one product line changes after invoicing, correction should use Full Credit Note and Re-Invoice rather than partial line editing in the current design. |

---

## 6. Product-Line Financial Attributes

Each Product Line may carry:

- Selling amount
- Cost amount
- Vendor
- Currency
- Exchange rate
- Tax reference
- Discount effect
- Product analytics mapping

This allows profitability and reporting to be calculated accurately even when one Order contains multiple products.

---

## 7. Vendor Relationship

A Product Line may be linked to one or more vendors depending on the business scenario.

Examples:

- Flight sold through airline directly
- Flight sold through consolidator
- Hotel booked through hotel vendor
- Insurance sold through insurance provider
- Visa processed through visa agency

Vendor Bill generation should use product-line cost and vendor grouping rules.

---

## 8. Reporting Requirements

Product reporting should support:

- Sales by product type
- Profitability by product type
- Vendor cost by product type
- Product mix by source system
- Product performance by team
- Amendment impact by product type

---

## 9. Odoo Considerations

Product information may be used for Odoo invoice lines, analytics, account mapping, or reporting references.

Travel MidOffice owns operational product usage. Odoo owns accounting treatment.

---

## 10. Open Questions

- Final product master data fields
- Product analytics mapping rules
- Whether product configuration should be fully dynamic
- Whether product-level approval rules are required
- Future supplier contract management

---

## 11. Related Documents

- GOV-002 Domain Dictionary
- GOV-005 Business Rules Catalog
- BUS-004 Commercial Transaction
- BUS-005 Order Management
- BUS-007 Vendor Bill
- ADR-002 Odoo Accounting System of Record
