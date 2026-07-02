# SEC-005 - Audit and Compliance

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** SEC-005  
**Document Type:** Security Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines audit and compliance expectations for Travel MidOffice.

Audit and compliance controls are required because the system handles customer data, supplier data, operational Orders, financial documents, Odoo synchronization, amendments, and reporting.

---

## 2. Audit Principles

- Sensitive business actions must be auditable.
- Financial history should not be overwritten.
- Original documents should remain searchable and viewable after amendment.
- Approval actions must preserve approver, timestamp, decision, and reason.
- Integration failures and retries must be traceable.
- Settings changes should preserve old and new values.

---

## 3. Compliance-Sensitive Areas

Compliance-sensitive areas include:

- Customer data
- Vendor data
- Order commercial values
- Cost and margin information
- Customer Invoice generation
- Vendor Bill generation
- Full Credit Note
- Re-Invoice
- Odoo synchronization
- Exchange rate changes
- Tax references
- Report downloads
- Permission changes

---

## 4. Required Audit Controls

| Control | Description |
|---|---|
| User traceability | Every sensitive action should record the user. |
| Timestamp traceability | Every sensitive action should record date and time. |
| Value traceability | Important changes should preserve old and new values. |
| Reason capture | Amendments and approvals should capture reason where required. |
| Integration traceability | Odoo sync attempts and failures should be traceable. |
| Report access traceability | Report generation and downloads should be auditable. |

---

## 5. Related Documents

- OPS-002 Audit Trail and Activity Timeline
- DATA-002 Audit Data Model
- SEC-004 Approval Framework
- ADR-003 Document-Based Amendment Strategy
