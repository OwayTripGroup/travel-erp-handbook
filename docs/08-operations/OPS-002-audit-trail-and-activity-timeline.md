# OPS-002 - Audit Trail and Activity Timeline

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** OPS-002  
**Document Type:** Operations Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines audit trail and activity timeline principles for Travel MidOffice.

Auditability is a core architecture principle because Travel MidOffice manages operational and financial business documents that must remain traceable over time.

---

## 2. Audit Trail Definition

An audit trail is the chronological record of meaningful business actions, state changes, and user activity related to a business object.

Audit trails should answer:

- Who performed the action?
- When was the action performed?
- What changed?
- Why did it change where a reason is required?
- Which business object was affected?

---

## 3. Activity Timeline Definition

An activity timeline is the user-facing business history of a Commercial Transaction, Order, Invoice, Vendor Bill, Credit Note, or Re-Invoice.

The timeline should show major business milestones in a readable way.

---

## 4. Events to Capture

Important events include:

- Commercial Transaction Received
- Order Created
- Order Validated
- Order Confirmed
- Customer Invoice Generated
- Vendor Bill Generated
- Odoo Sync Requested
- Odoo Sync Completed
- Odoo Sync Failed
- Full Credit Note Created
- Re-Invoice Created
- Report Generated

---

## 5. Required Audit Metadata

Audit records should preserve:

- Business object type
- Business object ID
- Event name
- User ID
- Timestamp
- Old value where applicable
- New value where applicable
- Reason where applicable
- Source system where applicable
- IP or request reference where applicable

---

## 6. Amendment Audit

Amendment workflows must preserve the full chain between:

- Original Order
- Full Credit Note
- Re-Invoice Order
- Related Customer Invoices
- Related Vendor Bills
- Odoo documents

This is required for operational support, finance review, and reporting.

---

## 7. Governance Principles

- Financial history should not be overwritten.
- Original Orders should remain viewable and searchable.
- Important business actions should be event-based.
- Audit data should be protected from normal user editing.

---

## 8. Related Documents

- GOV-004 Business Event Catalog
- GOV-005 Business Rules Catalog
- ADR-003 Document-Based Amendment Strategy
- BUS-005 Order Management
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
