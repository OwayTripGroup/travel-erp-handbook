# API-003 - Odoo Sync API

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** API-003  
**Document Type:** API Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines API behavior for Odoo synchronization from Travel MidOffice.

Odoo sync APIs should support controlled document synchronization, retry, error visibility, traceability, and audit.

---

## 2. Syncable Documents

Supported document types include:

- Customer Invoice
- Vendor Bill
- Full Credit Note
- Re-Invoice related documents
- Customer partner where required
- Vendor partner where required

---

## 3. Recommended Endpoints

```text
POST /api/odoo-sync-jobs
GET /api/odoo-sync-jobs
GET /api/odoo-sync-jobs/{id}
POST /api/odoo-sync-jobs/{id}/retry
POST /api/odoo/callbacks
```

---

## 4. Sync Job Payload Principles

Payloads should preserve:

- MidOffice document ID
- Document type
- Odoo model target
- Odoo document ID if already synchronized
- Idempotency key where applicable
- Source object references
- Retry eligibility

---

## 5. Error Handling

Odoo sync errors should be stored and visible.

Failures should include:

- Odoo error name
- Odoo error message
- Related MidOffice document
- Sync attempt count
- Last attempted time
- Retry status

---

## 6. Related Documents

- INT-001 Odoo Integration
- ACC-002 Odoo Invoice and Vendor Bill Lifecycle
- OPS-001 Background Jobs and Sync Jobs
- STD-004 Error Handling Standard
