# GOV-004 - Business Event Catalog

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** GOV-004  
**Document Type:** Governance Catalog  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the official business events used by Travel MidOffice.

A business event is a meaningful business occurrence that changes state, creates audit history, triggers integration, produces notification, or supports reporting.

---

## 2. Event Principles

- Events should use business language.
- Events should describe meaningful milestones, not low-level technical updates.
- Events should be recorded when they support audit, reporting, integration, or operational visibility.
- Events should be named in past tense.

---

## 3. Commercial Events

| Event ID | Event | Description |
|---|---|---|
| EVT-COM-001 | Commercial Transaction Received | A transaction is received from a source system into Travel MidOffice. |
| EVT-COM-002 | Customer Mapped | The transaction is linked to a valid Customer. |
| EVT-COM-003 | Sales Channel Identified | The transaction source channel is identified. |

---

## 4. Order Events

| Event ID | Event | Description |
|---|---|---|
| EVT-ORD-001 | Order Created | A Draft Order is created in Travel MidOffice. |
| EVT-ORD-002 | Order Validated | Operations completes validation. |
| EVT-ORD-003 | Order Confirmed | The Order is confirmed and ready for financial document generation. |
| EVT-ORD-004 | Order Cancelled | An Order is cancelled before financial document generation. |
| EVT-ORD-005 | Order Locked | An Order becomes read-only after amendment or financial correction. |

---

## 5. Financial Document Events

| Event ID | Event | Description |
|---|---|---|
| EVT-FIN-001 | Customer Invoice Generated | A Customer Invoice is generated from an Order. |
| EVT-FIN-002 | Vendor Bill Generated | One or more Vendor Bills are generated from Order cost. |
| EVT-FIN-003 | Full Credit Note Created | A full reversal document is created. |
| EVT-FIN-004 | Re-Invoice Created | A replacement Draft Order is created after Full Credit Note. |

---

## 6. Integration Events

| Event ID | Event | Description |
|---|---|---|
| EVT-INT-001 | Odoo Sync Requested | A document is queued for Odoo synchronization. |
| EVT-INT-002 | Odoo Sync Completed | Odoo synchronization completes successfully. |
| EVT-INT-003 | Odoo Sync Failed | Odoo synchronization fails. |
| EVT-INT-004 | Odoo Callback Received | Travel MidOffice receives a callback from Odoo. |

---

## 7. Reporting Events

| Event ID | Event | Description |
|---|---|---|
| EVT-RPT-001 | Transaction Exported | Transaction data is exported for reporting or analytics. |
| EVT-RPT-002 | Report Generated | A report is generated. |
| EVT-RPT-003 | Report Downloaded | A user downloads a generated report. |
