# DATA-002 - Audit Data Model

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** DATA-002  
**Document Type:** Data Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the audit data model principles for Travel MidOffice.

Audit data supports traceability, compliance, support, finance review, operational review, and amendment history.

---

## 2. Audit Principles

- Audit data should be append-only where possible.
- Audit data should preserve who, what, when, and why.
- Financially relevant changes should always be traceable.
- Amendment chains must preserve full historical relationships.
- Audit data should not be editable by normal users.

---

## 3. Recommended Audit Record Fields

| Field | Purpose |
|---|---|
| id | Technical identifier |
| event_id | Business event or audit event reference |
| auditable_type | Business object type |
| auditable_id | Business object identifier |
| action | Action performed |
| old_values | Previous values where applicable |
| new_values | New values where applicable |
| reason | Business reason where applicable |
| user_id | User who performed the action |
| source_system | Source of the event |
| request_id | Request or trace reference |
| created_at | Event timestamp |

---

## 4. Timeline Relationship

Audit data is system-facing.

Timeline data is user-facing.

The timeline may be derived from audit events or business events, but it should be readable by operations, finance, and support users.

---

## 5. High-Value Audit Events

Audit should capture:

- Order creation
- Customer mapping
- Order validation
- Order confirmation
- Financial document generation
- Odoo sync request
- Odoo sync failure
- Odoo sync success
- Full Credit Note creation
- Re-Invoice creation
- Report generation
- User permission-sensitive actions

---

## 6. Amendment Audit

Amendment audit must preserve:

- Original Order reference
- Full Credit Note reference
- Re-Invoice Order reference
- Original and replacement invoice references
- Original and replacement vendor bill references
- Odoo reversal references where available

---

## 7. Related Documents

- OPS-002 Audit Trail and Activity Timeline
- GOV-004 Business Event Catalog
- ADR-003 Document-Based Amendment Strategy
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
