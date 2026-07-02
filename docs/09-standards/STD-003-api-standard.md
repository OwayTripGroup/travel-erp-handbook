# STD-003 - API Standard

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** STD-003  
**Document Type:** Standard  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines API design principles for Travel MidOffice.

The API standard exists to make backend services predictable, consistent, secure, and maintainable across frontend, mobile, integrations, reporting, and future systems.

---

## 2. API Principles

- APIs should use business language from the Domain Dictionary.
- API behavior should respect business rules.
- API responses should be consistent across modules.
- Errors should be structured and actionable.
- APIs should not expose internal implementation details unnecessarily.
- Integration APIs should preserve traceability and idempotency where needed.

---

## 3. Resource Naming

Use plural nouns for resource collections.

Examples:

```text
/api/customers
/api/vendors
/api/products
/api/orders
/api/customer-invoices
/api/vendor-bills
```

---

## 4. Action Endpoints

Use explicit action endpoints when the operation represents a business action rather than simple CRUD.

Examples:

```text
POST /api/orders/{id}/validate
POST /api/orders/{id}/confirm
POST /api/orders/{id}/generate-financial-documents
POST /api/orders/{id}/full-credit-note
POST /api/orders/{id}/re-invoice
POST /api/odoo-sync-jobs/{id}/retry
```

---

## 5. Response Shape

Recommended response envelope:

```json
{
  "success": true,
  "data": {},
  "message": "Completed successfully"
}
```

For errors, use the error standard defined in `STD-004`.

---

## 6. Pagination

List endpoints should support pagination.

Recommended parameters:

```text
page
per_page
sort
filter
search
```

---

## 7. Related Documents

- GOV-002 Domain Dictionary
- GOV-005 Business Rules Catalog
- STD-004 Error Handling Standard
- BUS-005 Order Management
- INT-001 Odoo Integration
