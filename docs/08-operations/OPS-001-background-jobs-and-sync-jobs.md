# OPS-001 - Background Jobs and Sync Jobs

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** OPS-001  
**Document Type:** Operations Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the background job and sync job architecture for Travel MidOffice.

Background jobs are used for work that should not block the user interface or API request lifecycle.

Sync jobs are a specialized type of background job used to synchronize Travel MidOffice data with external systems such as Odoo, Power BI, reporting exports, and future integrations.

---

## 2. Use Cases

Background jobs should be used for:

- Odoo synchronization
- Report generation
- Scheduled report delivery
- Large file generation
- Retry processing
- Notification delivery
- External API callbacks
- Long-running exports

---

## 3. Job Lifecycle

```text
Job Created
  -> Queued
  -> Processing
  -> Completed
```

Failure lifecycle:

```text
Job Created
  -> Queued
  -> Processing
  -> Failed
  -> Retried
  -> Completed or Permanently Failed
```

---

## 4. Required Job Metadata

A job should track:

- Job number
- Job type
- Source module
- Related business object
- Status
- Attempt count
- Created by
- Started time
- Completed time
- Duration
- Error message where applicable

---

## 5. Sync Job Requirements

Sync jobs should additionally track:

- External system name
- Payload reference
- External document ID
- External document number
- Sync status
- Last sync date
- Retry count
- Idempotency key where applicable

---

## 6. Operational Principles

- Failed jobs must be visible to administrators.
- Retried jobs must preserve history.
- Sync jobs must avoid duplicate external documents.
- Large report jobs should notify users when complete.
- Job duration should be tracked for performance monitoring.

---

## 7. Related Documents

- INT-001 Odoo Integration
- INT-003 Power BI and Reporting Integration
- GOV-004 Business Event Catalog
- BUS-006 Customer Invoice
- BUS-007 Vendor Bill
