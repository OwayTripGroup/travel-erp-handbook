# GOV-003 - Business Capability Map

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** GOV-003  
**Document Type:** Governance  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the business capabilities of Travel MidOffice.

A business capability describes what the business must be able to do, independent of screens, database tables, source code, teams, or implementation details.

This map is used to organize the knowledge base, identify ownership, define roadmap priorities, and prevent the system from being documented only as isolated modules.

---

## 2. Capability Principles

- Capabilities describe business ability, not software screens.
- Capabilities are more stable than modules.
- One module may support multiple capabilities.
- One capability may require multiple systems.
- Capability ownership belongs to business functions, not software code.

---

## 3. Capability Landscape

```text
Travel MidOffice
  Commercial Management
  Operations Management
  Financial Document Management
  Customer Management
  Vendor Management
  Product Management
  Integration Management
  Reporting and Analytics
  Platform Services
  Administration and Governance
```

---

## 4. Commercial Management

**Purpose:** Manage the commercial agreement between Oway Travel and the Customer.

Capabilities:

- Commercial Transaction Management
- Sales Channel Intake
- Order Management
- Pricing
- Discount Management
- Amendment Management
- Customer Commercial History

Primary owner: Sales

Supporting teams: Operations, Finance, Product, Engineering

---

## 5. Operations Management

**Purpose:** Ensure that travel transactions can be fulfilled correctly and consistently.

Capabilities:

- Order Validation
- Order Confirmation
- Supplier Coordination
- Product-Line Operational Review
- Booking Reference Management
- Operational Exception Handling
- Cancellation Before Invoicing

Primary owner: Operations

---

## 6. Financial Document Management

**Purpose:** Generate operational financial documents and prepare them for accounting synchronization.

Capabilities:

- Customer Invoice Generation
- Vendor Bill Generation
- Full Credit Note
- Re-Invoice
- Currency Handling
- Exchange Rate Usage
- Tax Reference Usage
- Odoo Synchronization Preparation

Primary owner: Finance and Operations

Accounting system: Odoo

---

## 7. Supporting Capabilities

| Capability | Purpose | Primary Owner |
|---|---|---|
| Customer Management | Maintain customer data for commercial transactions | Sales |
| Vendor Management | Maintain supplier data for cost and fulfillment | Operations |
| Product Management | Maintain travel products and product categories | Product Team |
| Integration Management | Manage communication with external systems | Engineering |
| Reporting and Analytics | Provide operational, financial, and management visibility | Management |
| Platform Services | Provide notification, audit, files, settings, background jobs and search | Engineering |
| Administration and Governance | Manage users, roles, permissions, approvals and policy configuration | System Administration |

---

## 8. Capability Ownership Matrix

| Capability | Primary Owner | Primary System |
|---|---|---|
| Commercial Management | Sales | Travel MidOffice |
| Operations Management | Operations | Travel MidOffice |
| Financial Document Management | Finance / Operations | Travel MidOffice + Odoo |
| Customer Management | Sales | Travel MidOffice |
| Vendor Management | Operations | Travel MidOffice |
| Product Management | Product Team | Travel MidOffice |
| Integration Management | Engineering | Travel MidOffice |
| Reporting and Analytics | Management | Travel MidOffice + Power BI |
| Platform Services | Engineering | Travel MidOffice |
| Administration and Governance | System Administration | Travel MidOffice |

---

## 9. Capability Dependency

```text
Commercial Management
  -> Operations Management
  -> Financial Document Management
  -> Integration Management
  -> Reporting and Analytics
```

Customer Management, Vendor Management, Product Management, Platform Services, and Administration support the full capability chain.

---

## 10. Architecture Note

Commercial Transaction Management should be treated as the parent capability for Orders, Customer Invoices, Vendor Bills, Full Credit Notes, and Re-Invoices.

This does not require a new database table immediately. It is a business architecture concept that helps organize the domain and future evolution.

---

## 11. Related Documents

- GOV-002 Domain Dictionary
- GOV-004 Business Event Catalog
- GOV-005 Business Rules Catalog
- BUS-000 Travel ERP Business Overview
- ARC-000 Design Principles
- ADR-001 Travel MidOffice as Operational System of Record
- ADR-002 Odoo as Accounting System of Record
- ADR-003 Document-Based Amendment Strategy
