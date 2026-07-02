# FE-002 - Workflow UI Patterns

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** FE-002  
**Document Type:** Frontend Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines recommended UI patterns for workflow-heavy screens in Travel MidOffice.

The goal is to make operational workflows clear, controlled, and auditable.

---

## 2. Workflow Screen Layout

Recommended order detail layout:

```text
Header Summary
  -> Status Bar
  -> Action Panel
  -> Validation Issues
  -> Product Lines
  -> Customer and Vendor Data
  -> Financial Documents
  -> Timeline and Audit
```

---

## 3. Status Display

Each major object should clearly display:

- Order Status
- Invoice Status
- Odoo Sync Status
- Payment Status where applicable
- Amendment Status where applicable

Status should not be hidden inside tabs.

---

## 4. Action Panel

Actions should be grouped by business intent.

Examples:

- Validate Order
- Confirm Order
- Generate Financial Documents
- Sync to Odoo
- Create Full Credit Note
- Create Re-Invoice
- Retry Sync

Dangerous actions should require confirmation and permission.

---

## 5. Validation UX

Validation failures should show:

- What is missing
- Which section is affected
- How to fix it
- Whether the issue blocks confirmation

---

## 6. Amendment UX

Amendment screens should clearly show:

- Original Order link
- Full Credit Note link
- Re-Invoice Order link
- Read-only original data
- Reason for amendment
- Current amendment chain status

---

## 7. Related Documents

- BUS-005 Order Management
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- OPS-002 Audit Trail and Activity Timeline
