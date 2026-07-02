# INT-003 - Power BI and Reporting Integration

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** INT-003  
**Document Type:** Integration Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines how Travel MidOffice provides transaction data to Power BI and reporting systems.

Power BI is used for management analytics. Travel MidOffice remains the operational source for transaction data.

---

## 2. Reporting Scope

Reporting integration should support:

- Sales reporting
- Operations reporting
- Financial document reporting
- Profitability reporting
- Product reporting
- Vendor reporting
- Amendment chain reporting
- Sync job and integration monitoring

---

## 3. Data Principles

- Reporting must include original transactions and amendments.
- Reporting must not rely only on the latest Order when an amendment chain exists.
- Credit and Re-Invoice records must be traceable to the original transaction.
- Exchange rate and currency context must be preserved.
- Source system and team classification should be available for reporting.

---

## 4. Amendment Chain Reporting

Reporting must support this pattern:

```text
Original Order
  -> Full Credit Note
  -> Re-Invoice Order
  -> Final Net Outcome
```

Reports should show gross value, reversal value, replacement value, and final profitability.

---

## 5. Data Export Lifecycle

```text
Business Event Occurs
  -> Transaction Data Prepared
  -> Reporting Dataset Updated
  -> Power BI Consumes Data
  -> Management Dashboard Updated
```

---

## 6. Required Reporting Dimensions

Recommended dimensions include:

- Source system
- Sales channel
- Sales team
- Operations team
- Customer
- Vendor
- Product type
- Currency
- Exchange rate
- Order status
- Invoice status
- Sync status
- Amendment type

---

## 7. Related Documents

- BUS-004 Commercial Transaction
- BUS-005 Order Management
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- ACC-003 Currency and Exchange Rate Strategy
- GOV-004 Business Event Catalog
- GOV-005 Business Rules Catalog
