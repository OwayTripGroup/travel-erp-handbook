# ARC-000 - Design Principles

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** ARC-000  
**Document Type:** Architecture Principle  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the foundational design principles for Travel MidOffice.

These principles should guide business design, implementation, integration, reporting, and future enhancements.

---

## 2. Core Principles

### Principle 1 - Travel MidOffice is the Operational System of Record

Travel MidOffice is authoritative for operational business data, including Commercial Transactions, Orders, Customer Invoices, Vendor Bills, amendments, operational reporting, and integration tracking.

### Principle 2 - Odoo is the Accounting System of Record

Odoo owns accounting records such as journals, ledgers, receivables, payables, taxes, payments, and reconciliation.

### Principle 3 - Business Events Drive Workflow

Important milestones such as Order Created, Order Validated, Order Confirmed, Invoice Generated, Odoo Sync Completed, Credit Note Created, and Re-Invoice Created should be treated as business events.

### Principle 4 - Orders Are Atomic Operational Units

An Order is validated and confirmed as a whole business unit, even when it contains multiple product lines.

### Principle 5 - One Order Requires One Customer

Every Order must belong to exactly one Customer.

### Principle 6 - Financial Corrections Are Document-Based

Confirmed or invoiced commercial changes use Full Credit Note and Re-Invoice instead of direct editing.

### Principle 7 - Original Orders Remain Auditable

Original Orders remain searchable and read-only after amendment.

### Principle 8 - Policy Must Be Configurable Where Practical

Approval thresholds, margin policies, and department-level controls should be configurable where practical.

### Principle 9 - Reporting Must Consider Amendment Chains

Profitability and operational reports must include original orders, credit notes, re-invoices, customer invoices, and vendor bills.
