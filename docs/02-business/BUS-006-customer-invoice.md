# BUS-006 - Customer Invoice

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-006  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines Customer Invoice behavior in Travel MidOffice.

A Customer Invoice is the billing document generated from an Order and synchronized to Odoo for accounting.

---

## 2. Business Rule

Current design: one Order generates one Customer Invoice.

The Customer Invoice consolidates customer-facing charges from all Product Lines in the Order.

---

## 3. Lifecycle

```text
Order Confirmed
  -> Customer Invoice Generated
  -> Odoo Sync Requested
  -> Odoo Sync Completed
  -> Payment / Reconciliation in Odoo
```

---

## 4. Ownership

Travel MidOffice owns invoice preparation and operational linkage.

Odoo owns accounting receivables, payment, reconciliation, and journal impact.

---

## 5. Amendment

A posted or synchronized Customer Invoice should not be edited directly for commercial changes.

Corrections should use Full Credit Note and Re-Invoice.
