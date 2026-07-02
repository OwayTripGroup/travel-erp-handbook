# GOV-002 - Domain Dictionary

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** GOV-002  
**Document Type:** Governance  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

The Domain Dictionary defines the official vocabulary used throughout the Travel MidOffice knowledge base.

It exists to establish one shared language across Product, Engineering, Operations, Sales, Finance, Management, QA, and integration partners.

All architecture documents, workflow documents, API specifications, database designs, implementation plans, and test cases should use the terms defined here.

---

## 2. Terminology Principles

- Business terminology takes precedence over technical terminology.
- One business concept should have one official definition.
- Database table names do not define business language.
- Implementation names may differ from business concepts where necessary.
- Deprecated or legacy terms should remain documented when they help explain historical context.

---

## 3. Core Domain Terms

### Commercial Transaction

The commercial agreement between Oway Travel and a customer to purchase one or more travel products or services.

A Commercial Transaction begins when the customer commits to purchase or when the business commits to fulfill the purchase.

It is the highest-level business concept in the Travel MidOffice domain.

### Order

The operational representation of a Commercial Transaction inside Travel MidOffice.

An Order is used to validate travel data, coordinate suppliers, generate customer invoices, generate vendor bills, perform amendments, and support reporting.

### Customer

The purchasing party of a Commercial Transaction.

Every Order must belong to exactly one Customer. Anonymous Orders are not supported.

### Vendor

An external supplier that provides one or more travel products or services.

Examples include airlines, hotels, insurance providers, bus operators, visa agencies, ticketing agents, consolidators, and tour operators.

### Product

A sellable travel service offered by the business.

Examples include Flight, Hotel, Insurance, Visa, Bus, Car Rental, Tour, and future travel services.

### Product Line

A specific travel product or service within an Order.

A Product Line may have its own vendor, selling price, cost, currency, exchange rate, tax, and operational data.

---

## 4. Sales and Commercial Terms

### Selling Price

The amount charged to the Customer for a product line or Order.

### Cost

The amount payable to a Vendor for a product line or service.

### Margin

The difference between Selling Price and Cost.

Margin may be analyzed as an amount or as a percentage.

### Discount

A reduction of Selling Price.

Discounts may come from online promotions, campaigns, corporate pricing, manual adjustments, or order-level discount policies.

### Sales Channel

The source through which a Commercial Transaction originates.

Examples include Oway Travel Website, Oway Travel Mobile App, Sales Operation, Amadeus, and future partner systems.

---

## 5. Operational Terms

### Draft

The entry state of an Order in Travel MidOffice.

### Validation

The operational process that verifies whether an Order is ready for confirmation.

Validation may include customer mapping, product completeness, vendor mapping, cost validation, selling amount validation, currency validation, exchange rate validation, tax availability, and required travel information.

### Confirmation

The operational decision that an Order is valid and ready for financial document generation.

### Cancellation

The process of stopping an Order before financial documents are generated, subject to permission and workflow rules.

### Amendment

The process of correcting or replacing a Commercial Transaction after confirmation or invoicing.

Travel MidOffice uses document-based amendment rather than direct editing or order versioning.

### Amendment Chain

The full relationship between the original Order, Full Credit Note, Re-Invoice Order, Customer Invoice, Vendor Bill, and any later amendments.

---

## 6. Financial Terms

### Customer Invoice

The billing document generated from an Order and issued to the Customer.

Current design: one Order generates one Customer Invoice.

### Vendor Bill

The payable document generated for a Vendor based on product-line cost.

One Order may generate multiple Vendor Bills.

### Full Credit Note

A full reversal document created by copying the original Order and related financial documents with negative values.

### Re-Invoice

A replacement workflow that begins with a Full Credit Note and creates a new Draft Order copied from the original Order with revised values.

### Base Currency

The reporting and base calculation currency used by Travel MidOffice.

Current design: USD.

### Transaction Currency

The currency used for the customer transaction or financial document.

Current design: USD or MMK.

### Exchange Rate

The conversion rate between Base Currency and Transaction Currency.

Exchange rate governance belongs to Finance.

### Tax

Accounting tax information configured by Finance in Odoo and synchronized into Travel MidOffice where required.

---

## 7. Integration Terms

### Source System

A system that creates or sends a Commercial Transaction into Travel MidOffice.

Examples include Website, Mobile App, Amadeus, and future partner systems.

### Operational System of Record

The authoritative system for operational business data.

Travel MidOffice is the Operational System of Record.

### Accounting System of Record

The authoritative system for accounting data.

Odoo is the Accounting System of Record.

### Synchronization

The controlled transfer of business documents or status information between systems.

### Sync Job

A background process responsible for synchronizing data with an external system.

### Callback

A response from an external system indicating processing outcome or status change.

---

## 8. Reporting and Audit Terms

### Business Event

A meaningful business occurrence that changes system state or must be recorded for traceability.

Examples include Order Created, Order Validated, Order Confirmed, Customer Invoice Generated, Vendor Bill Generated, Full Credit Note Created, and Re-Invoice Created.

### Audit Trail

The chronological record of actions, changes, and business events related to a business object.

### Timeline

The ordered business history of a Commercial Transaction or Order.

### Profitability

The financial outcome of a Commercial Transaction, considering selling price, discount, cost, credit notes, re-invoices, and amendment chain effects.

---

## 9. Ownership

This dictionary is owned by the Enterprise Architecture Team.

Any change to canonical terminology should be reviewed because terminology changes affect the full knowledge base, implementation, API naming, reporting, and user understanding.

---

## 10. Related Documents

- GOV-001 Documentation Standard
- GOV-003 Business Capability Map
- GOV-004 Business Event Catalog
- GOV-005 Business Rules Catalog
- BUS-000 Travel ERP Business Overview
- ARC-000 Design Principles
- ADR-001 Travel MidOffice as Operational System of Record
- ADR-002 Odoo as Accounting System of Record
- ADR-003 Document-Based Amendment Strategy
