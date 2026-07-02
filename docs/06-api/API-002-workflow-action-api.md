# API-002 - Workflow Action API

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** API-002  
**Document Type:** API Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the API approach for workflow actions in Travel MidOffice.

Workflow actions represent business decisions and state transitions. They should not be treated as simple field updates.

---

## 2. Core Order Actions

Recommended endpoints:

```text
POST /api/orders/{id}/validate
POST /api/orders/{id}/confirm
POST /api/orders/{id}/cancel
POST /api/orders/{id}/generate-financial-documents
```

Each action should enforce permission, validate business rules, record audit data, and emit business events.

---

## 3. Amendment Actions

Recommended endpoints:

```text
POST /api/orders/{id}/full-credit-note
POST /api/orders/{id}/re-invoice
```

The Re-Invoice action should begin from the approved Full Credit Note flow.

---

## 4. Action Response

Recommended response:

```json
{
  "success": true,
  "data": {
    "id": 123,
    "status": "confirmed"
  },
  "message": "Order confirmed successfully."
}
```

---

## 5. Business Rules

| Rule ID | Rule |
|---|---|
| BR-ORD-003 | An Order is validated and confirmed as one atomic operational unit. |
| BR-ORD-004 | Operations validates the whole Order before confirmation. |
| BR-AMD-001 | Commercial changes after confirmation or invoicing use document-based amendment. |

---

## 6. Related Documents

- BUS-005 Order Management
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- STD-003 API Standard
- STD-004 Error Handling Standard
