# BUS-000 - Travel ERP Business Overview

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-000  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Executive Summary

Travel MidOffice is the central operational platform for Oway Travel.

It manages the operational lifecycle of commercial transactions from order intake through validation, confirmation, accounting document generation, Odoo synchronization, amendment, reporting, and audit.

Travel MidOffice is not the accounting system. Odoo is used as the accounting system of record.

---

## 2. Business Mission

To provide a single operational platform that enables Oway Travel to manage every commercial transaction consistently, accurately, and auditably across sales channels while integrating with accounting, reporting, and external systems.

---

## 3. Business Scope

Travel MidOffice supports operational processing for travel products including:

- Flight
- Hotel
- Bus
- Insurance
- Visa
- Tour Packages
- Future travel products

A single customer purchase may include multiple travel product lines.

---

## 4. Sales Channels

Online sales originate from the Oway Travel Website or Mobile App.

Offline sales are created by Sales Operation, often through external systems such as Amadeus, and sent to Travel MidOffice through API or manual creation.

---

## 5. Core Business Flow

```text
Commercial Transaction Received
  -> Draft Order Created
  -> Operational Validation
  -> Order Confirmed
  -> Customer Invoice Generated
  -> Vendor Bill Generated
  -> Sync to Odoo
  -> Reporting and Audit
  -> Amendment if Required
```

---

## 6. Financial Document Strategy

- One Order generates one Customer Invoice.
- One Order may generate multiple Vendor Bills.
- Vendor Bills are cost-driven.
- Vendor Bills may be grouped by vendor.
- Full Credit Note reverses the original Order and related financial documents using negative values.
- Re-Invoice creates a replacement Draft Order after Full Credit Note.

---

## 7. Amendment Philosophy

Travel MidOffice uses document-based amendment rather than order-version-based amendment.

The original Order remains unchanged and read-only.

Financial correction is explicit and reporting can reconstruct the full amendment chain.
