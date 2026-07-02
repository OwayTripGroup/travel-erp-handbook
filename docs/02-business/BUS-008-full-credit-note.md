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

A Full Credit Note is the approved mechanism for fully reversing an original Order and related financial documents.

---

## 2. Business Definition

A Full Credit Note copies the original Order, Customer Invoice, and Vendor Bill structure using negative values.

It is used when the original transaction must be reversed for correction, cancellation, or re-invoicing.

---

## 3. Business Rules

| Rule ID | Rule |
|---|---|
| BR-CRN-001 | Full Credit Note shall copy the original Order and related financial documents. |
| BR-CRN-002 | Full Credit Note shall multiply financial values by negative one. |
| BR-CRN-003 | Full Credit Note shall behave as a reversal-style document for Odoo accounting synchronization. |
| BR-AMD-002 | Original Orders shall remain viewable, searchable, and read-only after amendment. |

---

## 4. Copied Data

The Full Credit Note should copy:

- Order header
- Product Lines
- Customer
- Vendor references
- Passenger or travel details where applicable
- Selling amounts
- Cost amounts
- Taxes
- Customer Invoice
- Vendor Bills
- Operational notes where applicable

---

## 5. Odoo Synchronization

The Full Credit Note is synchronized to Odoo as a reversal-style accounting document.

The relationship between original Odoo documents and reversal documents must be traceable.

---

## 6. Related Documents

- BUS-005 Order Management
- BUS-006 Customer Invoice
- BUS-007 Vendor Bill
- BUS-009 Re-Invoice
- ADR-003 Document-Based Amendment Strategy
