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

A Re-Invoice creates a replacement Draft Order after a Full Credit Note so the revised Commercial Transaction can be processed through the normal lifecycle.

---

## 2. Workflow

```text
Original Order
  -> Full Credit Note
  -> New Draft Order copied from original
  -> Manual revision
  -> Validate
  -> Confirm
  -> Generate Customer Invoice and Vendor Bills
  -> Sync to Odoo
```

---

## 3. Business Behavior

The new Draft Order is copied from the original Order.

Authorized users manually update the copied Order according to the amendment scenario.

The Re-Invoice Order can itself be amended again, creating a longer amendment chain.

---

## 4. Reporting

Profitability reporting must consider the full amendment chain, not only the latest Order.
