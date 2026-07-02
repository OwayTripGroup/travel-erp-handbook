# SEC-003 - Permission Matrix

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** SEC-003  
**Document Type:** Security Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the initial permission matrix for Travel MidOffice.

The matrix is a foundation and should be validated with Sales, Operations, Finance, Management, and Administration before production.

---

## 2. Permission Categories

| Category | Example Actions |
|---|---|
| View | View list, view detail, view timeline |
| Create | Create master data or transaction |
| Edit | Modify editable records |
| Workflow | Validate, confirm, cancel, approve, reject |
| Finance | Generate invoice, generate vendor bill, sync Odoo, credit, re-invoice |
| Reporting | Generate, download, schedule reports |
| Administration | Manage users, roles, settings, mappings |

---

## 3. Draft Permission Matrix

| Object / Action | Sales | Operations | Finance | Product | Admin | Management |
|---|---:|---:|---:|---:|---:|---:|
| Customer view | Yes | Yes | Yes | Limited | Yes | Yes |
| Customer create | Yes | Yes | Limited | No | Yes | No |
| Customer edit | Yes | Yes | Limited | No | Yes | No |
| Vendor view | Limited | Yes | Yes | Yes | Yes | Yes |
| Vendor create | No | Yes | Limited | Limited | Yes | No |
| Product view | Yes | Yes | Yes | Yes | Yes | Yes |
| Product manage | No | Limited | Limited | Yes | Yes | No |
| Order create | Yes | Yes | No | No | Yes | No |
| Order validate | No | Yes | Limited | No | Yes | No |
| Order confirm | Limited | Yes | Limited | No | Yes | No |
| Order cancel before invoice | Limited | Yes | Limited | No | Yes | No |
| Generate customer invoice | No | Yes | Yes | No | Yes | No |
| Generate vendor bill | No | Yes | Yes | No | Yes | No |
| Sync to Odoo | No | Limited | Yes | No | Yes | No |
| Full Credit Note | Limited | Yes | Yes | No | Yes | Approval View |
| Re-Invoice | Limited | Yes | Yes | No | Yes | Approval View |
| Reports generate | Yes | Yes | Yes | Limited | Yes | Yes |
| Settings manage | No | No | Limited | Limited | Yes | No |

---

## 4. Notes

This is not yet the final production permission matrix.

The final matrix should be refined after department feedback and beta usage.

---

## 5. Related Documents

- SEC-001 Organization Structure
- SEC-002 Role-Based Access Control
- SEC-004 Approval Framework
- DATA-001 Data Ownership Matrix
