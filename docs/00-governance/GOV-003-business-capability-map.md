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

## 7. Related Documents

- GOV-002 Domain Dictionary
- GOV-004 Business Event Catalog
- GOV-005 Business Rules Catalog
- BUS-000 Travel ERP Business Overview
- ARC-000 Design Principles
