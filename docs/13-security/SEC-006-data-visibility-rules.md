# SEC-006 - Data Visibility Rules

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** SEC-006  
**Document Type:** Security Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines data visibility rules for Travel MidOffice.

Visibility rules control which users can see which business records and sensitive fields.

---

## 2. Visibility Principles

- Visibility should follow business responsibility.
- Permissions and visibility are related but not identical.
- Some users may view a record but not see sensitive financial fields.
- Finance, Operations, Sales, and Management may require different views of the same Order.
- Backend APIs must enforce visibility rules.

---

## 3. Visibility Dimensions

Recommended dimensions:

- Own records
- Own team records
- Department records
- Branch records
- Company-wide records
- Management-wide records
- Admin-wide records

---

## 4. Sensitive Fields

Sensitive fields may include:

- Cost
- Margin
- Vendor cost details
- Exchange rate override
- Finance approval information
- Odoo accounting references
- Internal notes
- Report export data

---

## 5. Draft Visibility Rules

| Area | Sales | Operations | Finance | Product | Management | Admin |
|---|---:|---:|---:|---:|---:|---:|
| Own Orders | Yes | Yes | Yes | Limited | Yes | Yes |
| Other Team Orders | Limited | Limited | Yes | Limited | Yes | Yes |
| Cost | Limited | Yes | Yes | Limited | Yes | Yes |
| Margin | Limited | Limited | Yes | Limited | Yes | Yes |
| Odoo Sync Status | Limited | Yes | Yes | No | Yes | Yes |
| Reports | Permission-based | Permission-based | Permission-based | Permission-based | Yes | Yes |

---

## 6. Open Questions

The final visibility model requires confirmation from department stakeholders.

Open questions:

- Can Sales view margin?
- Can Operations view margin?
- Can Product view selling price and profitability?
- Should Finance see all Orders?
- Should team managers see all team records?
- Is branch-level visibility required?

---

## 7. Related Documents

- SEC-002 Role-Based Access Control
- SEC-003 Permission Matrix
- DATA-001 Data Ownership Matrix
- BUS-005 Order Management
