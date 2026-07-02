# BUS-009 - Re-Invoice

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-009  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Re-Invoice workflow.

Re-Invoice is the approved mechanism for replacing an original Order after a Full Credit Note.

---

## 2. Business Definition

A Re-Invoice always starts with a Full Credit Note.

After the Full Credit Note, Travel MidOffice creates a new Draft Order copied from the original Order. Authorized users then make the required business changes and process the new Order through the normal lifecycle.

---

## 3. Business Rules

| Rule ID | Rule |
|---|---|
| BR-RIN-001 | Re-Invoice shall always begin with Full Credit Note. |
| BR-RIN-002 | Re-Invoice shall create a new Draft Order copied from the original Order. |
| BR-RIN-003 | Authorized users shall manually update the copied Draft Order according to the amendment scenario. |
| BR-RIN-004 | The Re-Invoice Order shall proceed through the normal Order lifecycle after manual changes. |
| BR-RIN-005 | Re-Invoice Orders may themselves be amended again. |

---

## 4. Workflow

```text
Original Order
  -> Full Credit Note
  -> New Draft Order
  -> Manual Revision
  -> Validate
  -> Confirm
  -> Generate Customer Invoice and Vendor Bills
  -> Sync to Odoo
```

---

## 5. Amendment Chain

Re-Invoice must preserve relationship to:

- Original Order
- Original Customer Invoice
- Original Vendor Bills
- Full Credit Note
- New replacement Order
- New Customer Invoice
- New Vendor Bills

---

## 6. Reporting

Reporting must consider the full amendment chain.

Reports should show original value, credit value, re-invoice value, and final net outcome.

---

## 7. Related Documents

- BUS-004 Commercial Transaction
- BUS-005 Order Management
- BUS-008 Full Credit Note
- ADR-003 Document-Based Amendment Strategy
