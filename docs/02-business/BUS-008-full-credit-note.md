# BUS-008 - Full Credit Note

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-008  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Full Credit Note workflow.

A Full Credit Note reverses the financial effect of the original Order and related financial documents by copying them with negative values.

---

## 2. Business Behavior

A Full Credit Note copies:

- Original Order
- Product Lines
- Customer Invoice
- Vendor Bills
- Selling amounts
- Cost amounts
- Taxes
- Operational relationships

All financial values are multiplied by negative one.

---

## 3. Relationship to Re-Invoice

Re-Invoice always starts with Full Credit Note.

```text
Original Order
  -> Full Credit Note
  -> New Draft Order
```

---

## 4. Business Rules

| Rule ID | Rule |
|---|---|
| BR-CRN-001 | Full Credit Note shall copy the original Order and related financial documents. |
| BR-CRN-002 | Full Credit Note shall multiply financial values by negative one. |
| BR-RIN-001 | Re-Invoice shall always begin with Full Credit Note. |
