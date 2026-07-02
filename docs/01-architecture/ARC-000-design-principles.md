# ARC-000 - Design Principles

**Project:** Travel ERP Enterprise Architecture Handbook  
**Document ID:** ARC-000  
**Document Type:** Architecture Principle  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** ERP Architecture Team  
**Last Updated:** 2026-07-02

---

## Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0.0 | 2026-07-02 | ERP Architecture Team | Initial design principles captured from architecture discovery workshops. |

---

## 1. Purpose

This document defines the foundational design principles for the Travel ERP System.

These principles are derived from architecture discovery discussions about order management, online and offline sales channels, Odoo accounting integration, amendments, credit notes, re-invoices, currency handling, vendor billing, and reporting.

The purpose of this document is to prevent architectural drift during implementation and beta rollout.

---

## 2. Scope

These principles apply to all Travel ERP modules, including:

- Order Management
- Customer Invoice
- Vendor Bill
- Full Credit Note
- Re-Invoice
- Payment
- Reporting
- Odoo Integration
- Currency and Exchange Rate
- Settings and Business Policies

---

## 3. Principle Classification

Because the product is still in implementation and has not yet reached beta, the handbook uses four levels of confidence.

| Level | Meaning |
|---|---|
| Confirmed | Stable architecture that should not change without an ADR |
| Current Design | Current implementation target; may evolve after beta feedback |
| Policy Candidate | Business policy expected to be refined after user feedback |
| Future Consideration | Not current scope, but intentionally anticipated |

This distinction is important because some workflow policies, especially approvals, may change after feedback from Finance, Operations, and Sales.

---

## 4. Core Design Principles

### Principle 1 - Travel ERP is the Operational System of Record

**Level:** Confirmed

The Travel ERP is the authoritative system for operational business data, including customers, vendors, products, orders, invoices, vendor bills, amendments, operational reporting, and integration tracking.

Odoo is not the operational source of truth. Odoo is used for accounting.

---

### Principle 2 - Odoo is the Accounting System

**Level:** Confirmed

Odoo owns accounting records such as journal entries, ledgers, accounts receivable, accounts payable, taxes, payments, and reconciliation.

The Travel ERP sends accounting documents to Odoo but does not allow Odoo to become the owner of operational workflows.

---

### Principle 3 - Business Events Drive Workflow

**Level:** Confirmed

The Travel ERP is event-driven rather than CRUD-driven.

Important business events include:

- Order received
- Order validated
- Order confirmed
- Invoice generated
- Vendor bill generated
- Accounting document synchronized
- Credit note created
- Re-invoice created
- Payment recorded

Users should not arbitrarily modify business records after key lifecycle events.

---

### Principle 4 - Order is an Atomic Operational Unit

**Level:** Confirmed

An Order is validated and confirmed as a whole business unit.

Even when an Order contains multiple products such as flight, hotel, insurance, visa, bus, or tour package components, Operations validates the whole Order rather than independently confirming individual product lines.

---

### Principle 5 - One Order Belongs to One Customer

**Level:** Confirmed

Every Order must be mapped to a Customer.

The system does not support anonymous Orders. Customer mapping is mandatory for both online and offline Orders.

---

### Principle 6 - One Order Generates One Customer Invoice

**Level:** Current Design

Each Order generates one Customer Invoice.

An Order may contain multiple product lines, but customer billing is consolidated into a single Customer Invoice for that Order.

---

### Principle 7 - One Order May Generate Multiple Vendor Bills

**Level:** Current Design

An Order may generate multiple Vendor Bills depending on supplier cost and vendor grouping.

Vendor Bill generation is cost-driven. If an Order has no supplier cost, no Vendor Bill is created.

When multiple product lines share the same vendor, their costs may be combined into one Vendor Bill for that vendor.

---

### Principle 8 - Commercial Changes Use Document-Based Amendment

**Level:** Confirmed

The Travel ERP does not use Order versioning as the primary amendment mechanism.

Instead, amendments are handled through document-based correction:

1. Original Order remains read-only.
2. Full Credit Note copies the original Order, Customer Invoice, and Vendor Bills with negative values.
3. Re-Invoice copies the original Order into a new draft flow with revised values.
4. Original and amendment relationships are stored for traceability.

---

### Principle 9 - Original Orders Are Locked After Amendment

**Level:** Confirmed

When an amendment is performed, the original Order must remain available for view and search, but it must be locked from further direct changes.

Travel-related data is stored at Order level, so maintaining the original Order as immutable is essential for audit and operational traceability.

---

### Principle 10 - Re-Invoice Always Starts With Full Credit

**Level:** Confirmed

A Re-Invoice workflow always begins by creating a Full Credit Note.

The revised Order then starts again from Draft and proceeds through validation, confirmation, invoice generation, and synchronization.

---

### Principle 11 - Discounts Reduce Selling Price

**Level:** Confirmed

Discounts are treated as reductions of selling price.

This applies to online discounts, order-level discounts, and manual discounts unless a future accounting policy requires a separate discount line treatment.

---

### Principle 12 - Currency Uses Base and Transaction Currency

**Level:** Confirmed

The Travel ERP maintains both Base Currency and Transaction Currency for financial documents.

The current base currency is USD. Transaction currency may be USD or MMK depending on source and business context.

---

### Principle 13 - Exchange Rate Ownership Belongs to Finance

**Level:** Confirmed

Exchange rate governance is owned by Finance in the MidOffice.

For online Orders, the Online Platform may send product-line exchange rates through API. For manual Orders, MidOffice applies an order-level currency and the relevant finance-approved exchange rate.

Exchange rates used for business transactions must be preserved for audit.

---

### Principle 14 - Tax Configuration is Owned by Finance and Odoo

**Level:** Confirmed

Tax configuration is maintained by Finance in Odoo and synchronized into the MidOffice where needed.

The Travel ERP consumes tax configuration but should not become the source of truth for accounting tax policy.

---

### Principle 15 - Approval Rules Are Configurable Policy Candidates

**Level:** Policy Candidate

Approval workflow rules are expected to evolve after beta feedback from Finance, Operations, Sales, and other departments.

The architecture should support configurable approval policies instead of hardcoding all approval conditions.

Examples of configurable policies may include:

- Approval required after payment
- Approval required after Odoo posting
- Approval required above amount threshold
- Approval required when margin falls below target
- Auto-approval for authorized roles

---

### Principle 16 - Reporting Must Consider Amendment Chains

**Level:** Confirmed

Profitability and operational reporting must consider the full amendment chain, not only the latest document.

Original Orders, Full Credit Notes, Re-Invoices, Customer Invoices, and Vendor Bills must remain traceable together.

---

### Principle 17 - Policy Must Be Separated From Core Rules

**Level:** Confirmed

The handbook distinguishes between core business rules and configurable company policy.

Core business rules include structural rules such as one Order requiring one Customer.

Policy rules include approval thresholds, margin goals, department-based permissions, and workflow exceptions that may change after beta feedback.

---

## 5. Related Documents

- GOV-001 Documentation Standard
- GOV-005 Business Rules Catalog
- ADR-001 MidOffice Data Ownership
- ADR-002 Odoo Accounting Responsibility
- ADR-003 Document-Based Amendment Strategy
- BUS-001 Order Management
- BUS-004 Credit Note Workflow
- BUS-005 Re-Invoice Workflow
- ACC-003 Exchange Rate Strategy
- INT-001 Odoo Integration

---

## 6. Open Items

The following topics require further workshop confirmation before being finalized:

- Final approval policy after beta feedback
- Margin threshold policy
- Department role matrix
- Order completion status naming
- Paid and reconciled amendment controls
- Partial credit support as future enhancement
