# BUS-001 - Customer Management

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-001  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Customer Management domain for Travel MidOffice.

Customer Management ensures that every Commercial Transaction and Order is linked to a valid Customer before operational processing, financial document generation, Odoo synchronization, reporting, and audit.

---

## 2. Business Context

A Customer is the purchasing party of a Commercial Transaction.

Travel MidOffice does not support anonymous Orders. Customer mapping is mandatory.

---

## 3. Scope

Customer Management includes:

- Customer profile
- Customer classification
- Corporate customer support
- Customer contact details
- Customer search
- Customer transaction history
- Customer mapping from source systems
- Odoo partner synchronization where required

Customer Management does not own accounting receivable balances. Accounting receivables are owned by Odoo.

---

## 4. Business Rules

| Rule ID | Rule |
|---|---|
| BR-CUS-001 | Anonymous Orders are not supported. |
| BR-CUS-002 | Customer mapping is mandatory before an Order can be processed in MidOffice. |
| BR-ORD-001 | Every Order must belong to exactly one Customer. |
