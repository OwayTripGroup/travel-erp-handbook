# REF-001 - Order Domain Discovery Record

**Project:** Travel ERP Enterprise Architecture Handbook  
**Document ID:** REF-001  
**Document Type:** Architecture Discovery Record  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** ERP Architecture Team  
**Last Updated:** 2026-07-02

---

## Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0.0 | 2026-07-02 | ERP Architecture Team | Initial Order domain discovery based on architecture workshop. |

---

## 1. Purpose

This document records confirmed discovery findings for the Travel ERP Order domain.

It is intentionally written as a discovery record, not the final Order Management specification. The purpose is to preserve domain knowledge, decisions, policy candidates, and open questions before they are converted into formal business, architecture, accounting, and integration documents.

---

## 2. Product Stage

The Travel ERP is currently in implementation and has not yet been released as beta.

Some workflow policies, especially approval rules, are expected to change after feedback from departments such as:

- Finance
- Operations
- Sales
- Management

For that reason, this document separates confirmed architecture from current design and policy candidates.

---

## 3. Order Definition

An Order is the central operational business entity in the Travel ERP.

It represents a customer travel transaction that may originate from multiple source systems, is validated and confirmed in MidOffice, and then generates downstream financial documents such as Customer Invoice and Vendor Bill.

A professional business definition is:

> An Order is the primary operational business entity within the Travel ERP. It represents a customer's confirmed or pending travel purchase, consolidates one or more travel products into a single commercial transaction, coordinates operational validation, and serves as the source for downstream customer invoicing, vendor billing, amendment, reporting, and Odoo accounting synchronization.

---

## 4. Source Systems

Orders may originate from different source systems.

| Source | Description |
|---|---|
| Oway Travel Mobile App | Online customer booking channel |
| Oway Travel Website | Online customer booking channel |
| Amadeus / Sales Operation | Offline booking channel created by sales agents and sent to MidOffice via API |
| Manual MidOffice Entry | Offline or internal manual order creation where applicable |

Each source system may have its own workflow status, but the MidOffice maintains its own operational Order lifecycle.

---

## 5. Customer Requirement

An Order cannot exist without a Customer.

Customer data must be available and mapped before the Order can be processed in MidOffice.

This applies to both online and offline Orders.

---

## 6. Order Creation Rules

Order creation differs by source.

### Online Orders

For online bookings from the Oway Travel App or Website, the Order is created after payment is received by the online system.

### Corporate or Offline Orders

For corporate or offline bookings, a Draft Order may be created in MidOffice after booking confirmation, even before final accounting documents are generated.

---

## 7. Order Lifecycle

The current operational lifecycle is:

```text
Draft -> Validate -> Confirm -> Invoice
```

However, architecturally, Invoice is better treated as a financial milestone or document relationship rather than a pure operational status.

Recommended future model:

```text
Draft -> Validated -> Confirmed -> Completed
```

With a separate invoice status lifecycle:

```text
Not Generated -> Generated -> Synced -> Credited -> Paid
```

This recommendation should be reviewed during implementation because the system already stores both Order Status and Invoice Status.

---

## 8. Lifecycle Definitions

| Status | Meaning |
|---|---|
| Draft | Entry point of the Order in MidOffice |
| Validate | Stage where cost, selling amount, product data, customer mapping, vendor data, currency, and operational completeness are checked |
| Confirm | Stage indicating all required data is valid and ready for invoice and vendor bill generation |
| Invoice | Current implementation status indicating Customer Invoice and Vendor Bill have been generated and synchronized or prepared for synchronization |

---

## 9. Validation Stage

Validation is a core business control point.

The purpose is to confirm that the Order is commercially and operationally ready.

Validation may include:

- Customer mapping exists
- Product lines are complete
- Vendor mapping exists
- Selling amount is valid
- Cost amount is valid
- Currency is valid
- Exchange rate is available
- Taxes are available where applicable
- Travel product details are complete
- Operations has reviewed the whole Order

Operations validates the whole Order as one atomic business unit, not each product line independently.

---

## 10. Product Model

An Order may contain multiple product lines.

Examples:

- Flight
- Hotel
- Insurance
- Visa
- Bus
- Tour package components

A tour package may contain multiple product lines in one Order.

The Order is treated as one commercial transaction even when it contains multiple products.

---

## 11. Product-Level Financial Attributes

Each product line may have its own:

- Vendor
- Cost
- Currency
- Exchange rate
- Status or product-level operational detail

A single product type may have multiple vendors in some scenarios. For example, a flight may involve an airline, consolidator, or ticketing agent.

---

## 12. Vendor Bill Generation

One Order may generate multiple Vendor Bills.

Vendor Bill generation is based on supplier cost and vendor grouping.

Rules discovered:

- If there is no cost for an Order or product line, no Vendor Bill is generated for that cost.
- If multiple product lines use the same vendor, they may be combined into the same Vendor Bill.
- If product lines use different vendors, separate Vendor Bills are generated.

Example:

```text
Order
  Flight -> Vendor A
  Hotel -> Vendor B
  Insurance -> Vendor A

Vendor Bill A
  Flight
  Insurance

Vendor Bill B
  Hotel
```

---

## 13. Customer Invoice Generation

Each Order generates one Customer Invoice.

Even when the Order contains multiple product lines, customer billing is consolidated into one Customer Invoice.

---

## 14. Discount Treatment

Discounts reduce the selling price.

Discounts may come from:

- Online promotions
- Online discounts
- Manual order-level discounts
- Manual discounts applied by authorized users

The current business interpretation is that discount is not a separate financial line; it reduces the net selling value used for profitability and invoicing.

---

## 15. Currency and Exchange Rate

The Travel ERP uses Base Currency and Transaction Currency.

Confirmed design:

- Base Currency: USD
- Transaction Currency: USD or MMK

Online Orders may provide exchange rates per product line through API.

Manual Orders may use order-level currency and finance-approved exchange rate from MidOffice.

Exchange rate governance belongs to Finance.

---

## 16. Tax Ownership

Tax configuration is owned by Finance and Odoo.

Taxes are configured in Odoo and synchronized into MidOffice where needed.

MidOffice consumes tax data but should not become the source of truth for accounting tax policy.

---

## 17. Amendment Strategy

The Travel ERP does not currently use Order versioning.

Instead, it uses document-based amendment.

There are two major amendment workflows:

1. Full Credit Note
2. Re-Invoice

---

## 18. Full Credit Note

A Full Credit Note copies the whole original Order, Customer Invoice, and Vendor Bill structure using negative values.

It is treated as a reversal-style document for Odoo accounting purposes.

Copied items include:

- Order header
- Order items
- Customer
- Passenger and travel data where applicable
- Selling amounts
- Cost amounts
- Taxes
- Customer Invoice
- Vendor Bills
- Notes and related operational data where applicable

All financial values are multiplied by negative one.

---

## 19. Re-Invoice

A Re-Invoice always starts with Full Credit Note.

The process is:

```text
Original Order
  -> Full Credit Note
  -> Copy Original Order
  -> New Draft Order
  -> Manual Changes
  -> Validate
  -> Confirm
  -> Generate Invoice and Vendor Bill
  -> Sync to Odoo
```

The new draft Order contains copied data from the original Order. Authorized users then make the necessary manual changes based on the business scenario.

---

## 20. Amendment Chain

An Order may be amended multiple times.

Example:

```text
Original Order
  -> Full Credit Note
  -> Re-Invoice Order 1
  -> Full Credit Note
  -> Re-Invoice Order 2
```

There is currently no maximum amendment depth.

The system must store relationship values for original and amendment records.

Important relationship fields may include:

- Original Order reference
- Original Customer Invoice reference
- Original Vendor Bill reference
- Credit Note reference
- Re-Invoice Order reference
- Amendment reason
- Amendment type
- Amendment chain or group reference

---

## 21. Order and Invoice Status

The system stores two statuses at Order level:

1. Order Status
2. Invoice Status

For Full Credit Note:

- Order Status remains Invoiced
- Invoice Status becomes Credited

This separation is important and should be retained.

---

## 22. Cancellation Rule

Before invoice generation, an Order may be cancelled.

After invoice generation and Odoo synchronization, correction should be handled through Full Credit Note or Re-Invoice.

Orders are not physically deleted. Cancelled status is used instead.

---

## 23. Reporting Requirement

Profitability and reporting must consider the entire amendment chain.

Reports should be able to show:

- Original Order
- Credit Note
- Re-Invoice Order
- Final net outcome
- Full amendment chain profitability

Power BI receives daily transaction data and should reflect the complete transaction history.

---

## 24. Ownership

Order-level responsibility belongs to the Sales and Operations teams that created and processed the Order.

General ownership patterns discovered:

| Area | Owner |
|---|---|
| Online selling price | Online Platform |
| Offline selling price | Respective Sales team |
| Cost validation | Operations |
| Vendor mapping | MidOffice / Operations |
| Exchange rate governance | Finance |
| Tax configuration | Finance / Odoo |
| Accounting posting | Odoo |
| Amendment action | Permission-based authorized users |

---

## 25. Approval Policy

Approval workflow is a policy candidate because the product is not yet in beta.

Current direction:

- Authorized users can perform amendment workflows based on permissions.
- Approval rules may change after department feedback.
- Finance, Operations, and Sales feedback should influence final approval configuration.

Architecture recommendation:

Approval rules should be configurable through business policies rather than hardcoded.

---

## 26. Confirmed Facts

The following facts are confirmed from workshop discussion:

- Order is the central operational point from online and offline systems.
- An Order must always map to a Customer.
- An Order may contain multiple product lines.
- One Order generates one Customer Invoice.
- One Order may generate multiple Vendor Bills.
- Vendor Bills are generated only when supplier cost exists.
- Vendor Bills may be grouped by vendor.
- Discount reduces selling price.
- Operations validates the whole Order.
- Original Order is locked/read-only after amendment.
- Full Credit Note copies everything with negative values.
- Re-Invoice always starts with Full Credit Note.
- Amendment can happen multiple times.
- Reporting must consider the full amendment chain.

---

## 27. Open Questions

The following topics require further discovery:

- Final approval workflow after beta feedback
- Department and permission matrix
- Final Order terminal status naming
- Paid and reconciled document amendment controls
- Margin threshold goals and policy
- Partial credit support as future enhancement
- Attachment copy rules during amendment
- Customer-facing document numbering rules for amendment chains

---

## 28. Related Documents

- ARC-000 Design Principles
- GOV-001 Documentation Standard
- GOV-005 Business Rules Catalog
- BUS-001 Order Management
- BUS-004 Credit Note Workflow
- BUS-005 Re-Invoice Workflow
- ACC-003 Exchange Rate Strategy
- INT-001 Odoo Integration
