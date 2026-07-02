# API-001 - API Architecture Overview

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** API-001  
**Document Type:** API Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the API architecture overview for Travel MidOffice.

The API layer exposes business capabilities to the frontend, integrations, reporting workflows, and future systems while enforcing validation, authorization, audit, and business rules.

---

## 2. API Principles

- APIs should use canonical domain language.
- Business actions should be explicit.
- APIs should enforce business rules, not only database validation.
- API responses should be consistent.
- API errors should be structured.
- APIs should preserve audit and traceability for financial and integration actions.

---

## 3. API Categories

| Category | Purpose |
|---|---|
| Master Data API | Customers, Vendors, Products, Settings |
| Transaction API | Commercial Transactions and Orders |
| Financial Document API | Customer Invoices, Vendor Bills, Credit Notes, Re-Invoices |
| Integration API | Odoo sync, source-system intake, callbacks |
| Reporting API | Report requests, report downloads, dashboard data |
| Admin API | Users, roles, permissions, configuration |

---

## 4. Action-Based API Design

Business state transitions should use action endpoints.

Examples:

```text
POST /api/orders/{id}/validate
POST /api/orders/{id}/confirm
POST /api/orders/{id}/generate-financial-documents
POST /api/orders/{id}/full-credit-note
POST /api/orders/{id}/re-invoice
```

These actions should create audit records and business events.

---

## 5. Related Documents

- STD-003 API Standard
- STD-004 Error Handling Standard
- BUS-005 Order Management
- INT-001 Odoo Integration
- OPS-002 Audit Trail and Activity Timeline
