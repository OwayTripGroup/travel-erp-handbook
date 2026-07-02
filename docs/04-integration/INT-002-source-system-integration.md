# INT-002 - Source System Integration

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** INT-002  
**Document Type:** Integration Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines how external source systems send Commercial Transactions into Travel MidOffice.

Source systems initiate or send transaction data. Travel MidOffice becomes the operational system of record after receipt.

---

## 2. Source Systems

Current and expected source systems include:

- Oway Travel Website
- Oway Travel Mobile App
- Amadeus
- Sales Operation systems
- Manual MidOffice entry
- Future partner systems

---

## 3. Integration Principle

Source systems are transaction producers. They are not the downstream operational owner.

After a transaction is received, Travel MidOffice owns operational validation, confirmation, financial document generation, amendment, and reporting.

---

## 4. Intake Lifecycle

```text
Source System Creates Transaction
  -> Transaction Sent to Travel MidOffice
  -> Commercial Transaction Received
  -> Customer Mapped
  -> Draft Order Created
  -> Validation Begins
```

---

## 5. Required Mapping

Incoming transactions should be mapped to:

- Source system
- Source reference number
- Customer
- Product lines
- Selling price
- Cost where available
- Vendor where available
- Currency
- Exchange rate where available
- Payment status where available

---

## 6. Online Order Notes

For online transactions from Website or Mobile App:

- Order may be created after payment is received online.
- Online platform may own promotion and discount decisions.
- Online platform may send product-line exchange rates.
- Travel MidOffice performs operational validation after receipt.

---

## 7. Offline Order Notes

For offline or sales operation transactions:

- Order may start as Draft in Travel MidOffice.
- Sales team owns selling price.
- Operations validates cost and supplier information.
- Finance-approved exchange rate may be used for manual orders.

---

## 8. Traceability Requirements

Travel MidOffice should preserve:

- Source system name
- Source transaction ID
- Source booking reference
- Received timestamp
- Mapping status
- Processing status
- Error message where applicable

---

## 9. Related Documents

- ADR-001 Travel MidOffice Operational System of Record
- BUS-004 Commercial Transaction
- BUS-005 Order Management
- ACC-003 Currency and Exchange Rate Strategy
- GOV-004 Business Event Catalog
