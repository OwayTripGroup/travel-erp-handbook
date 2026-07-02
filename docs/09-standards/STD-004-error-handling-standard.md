# STD-004 - Error Handling Standard

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** STD-004  
**Document Type:** Standard  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines standard error handling principles for Travel MidOffice.

Error handling should make failures understandable, traceable, and recoverable.

---

## 2. Error Principles

- Errors should be structured.
- Errors should be actionable.
- Business validation errors should be separated from system errors.
- Integration errors should preserve external system context.
- Sensitive internal details should not be exposed to end users.
- Errors should be logged with enough context for support and debugging.

---

## 3. Error Response Shape

Recommended error response:

```json
{
  "success": false,
  "error": {
    "code": "ORDER_VALIDATION_FAILED",
    "message": "Order validation failed.",
    "details": [],
    "trace_id": "optional-trace-id"
  }
}
```

---

## 4. Error Categories

| Category | Example |
|---|---|
| Validation Error | Missing customer, invalid currency, missing vendor |
| Permission Error | User cannot confirm Order |
| Business Rule Error | Cannot edit invoiced Order directly |
| Integration Error | Odoo sync failed |
| System Error | Unexpected exception |
| Not Found Error | Order not found |

---

## 5. Integration Errors

Integration errors should capture:

- External system name
- Request reference
- Payload reference where safe
- Error message
- Error code where available
- Retry eligibility
- Related sync job

---

## 6. Business Rule Errors

Business rule errors should reference the violated rule where possible.

Example:

```text
BR-ORD-001: Every Order must belong to exactly one Customer.
```

---

## 7. Related Documents

- GOV-005 Business Rules Catalog
- STD-003 API Standard
- OPS-001 Background Jobs and Sync Jobs
- INT-001 Odoo Integration
