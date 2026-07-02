# ACC-003 - Currency and Exchange Rate Strategy

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** ACC-003  
**Document Type:** Accounting Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the currency and exchange-rate strategy for Travel MidOffice.

Currency handling affects Orders, Customer Invoices, Vendor Bills, Full Credit Notes, Re-Invoices, Odoo synchronization, and reporting.

---

## 2. Currency Model

Travel MidOffice uses two currency concepts:

| Currency | Meaning |
|---|---|
| Base Currency | Internal reporting and calculation currency. Current design: USD. |
| Transaction Currency | Currency used for the customer transaction or financial document. Current design: USD or MMK. |

---

## 3. Online Orders

Online Orders may provide exchange rates per product line through API.

This reflects the commercial rate used by the online platform at the time of sale.

Product-line exchange rates should be preserved for audit and reporting.

---

## 4. Manual and Offline Orders

Manual or offline Orders may use order-level currency and a finance-approved exchange rate maintained in Travel MidOffice.

Finance owns exchange rate governance.

---

## 5. Credit Note and Re-Invoice

Full Credit Notes should use the original transaction values and exchange-rate context to preserve financial traceability.

Re-Invoice Orders should use the appropriate rate according to the new transaction context and business policy.

---

## 6. Business Rules

| Rule ID | Rule |
|---|---|
| BR-CUR-001 | Travel MidOffice shall support Base Currency and Transaction Currency. |
| BR-CUR-002 | Current Base Currency is USD. |
| BR-CUR-003 | Transaction Currency may be USD or MMK depending on source and business context. |
| BR-CUR-004 | Online Orders may provide product-line exchange rates through API. |
| BR-CUR-005 | Manual Orders may use order-level currency and finance-approved exchange rate from MidOffice. |
| BR-CUR-006 | Exchange rate governance belongs to Finance. |
| BR-CUR-007 | Exchange rates used in business transactions must be preserved for audit. |

---

## 7. Odoo Considerations

Odoo company currency and accounting currency behavior must be respected during synchronization.

Travel MidOffice should send financial document currency, exchange-rate context where required, and references needed for reconciliation.

---

## 8. Reporting Requirements

Reporting should support:

- Base currency amount
- Transaction currency amount
- Exchange rate used
- Source of exchange rate
- Original vs credit vs re-invoice exchange-rate context

---

## 9. Open Questions

- Final exchange-rate freezing point by workflow
- Whether rate override approval is required
- Whether source-system rates should be validated against finance rates
- Whether re-invoice always uses new active rate or original rate depending on reason

---

## 10. Related Documents

- GOV-005 Business Rules Catalog
- BUS-005 Order Management
- BUS-006 Customer Invoice
- BUS-007 Vendor Bill
- BUS-008 Full Credit Note
- BUS-009 Re-Invoice
- ADR-002 Odoo Accounting System of Record
