# SEC-002 - Role-Based Access Control

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** SEC-002  
**Document Type:** Security Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the role-based access control model for Travel MidOffice.

RBAC ensures that users can only access actions and data appropriate to their business responsibility.

---

## 2. RBAC Principles

- Permissions should follow business responsibility.
- Sensitive actions should require explicit permission.
- Finance-sensitive actions should be separated from operational actions.
- Users may have multiple roles where business requires it.
- Permission checks should be enforced by backend APIs, not only frontend UI.
- UI should hide or disable actions the user cannot perform.

---

## 3. Recommended Role Groups

| Role Group | Example Roles |
|---|---|
| Sales | Sales Executive, Sales Manager |
| Operations | Operations Executive, Operations Manager |
| Finance | Finance Executive, Finance Manager |
| Product | Product Executive, Product Manager |
| Customer Service | Customer Service Executive, Customer Service Manager |
| IT / Engineering | Developer, Support Engineer, Integration Admin |
| Management | Department Head, General Manager |
| System Administration | System Admin, Super Admin |

---

## 4. Permission Structure

Permissions should be action-based.

Examples:

```text
orders.create
orders.view
orders.validate
orders.confirm
orders.cancel
orders.full_credit_note
orders.re_invoice
customer_invoices.view
customer_invoices.sync_odoo
vendor_bills.view
vendor_bills.sync_odoo
settings.manage
reports.generate
reports.download
```

---

## 5. Backend Enforcement

Every workflow action API should verify:

- User identity
- Role
- Permission
- Data visibility
- Object status
- Business rule eligibility

---

## 6. Related Documents

- SEC-003 Permission Matrix
- SEC-004 Approval Framework
- API-002 Workflow Action API
- STD-003 API Standard
