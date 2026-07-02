# GOV-005 - Business Rules Catalog

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** GOV-005  
**Document Type:** Governance Catalog  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document is the central catalog of business rules for Travel MidOffice.

Workflow documents, API specifications, database designs, QA test cases, and implementation tasks should reference these rule IDs instead of redefining the same rules repeatedly.

---

## 2. Rule Categories

| Prefix | Domain |
|---|---|
| BR-ORD | Order Management |
| BR-CUS | Customer |
| BR-PRD | Product and Product Line |
| BR-INV | Customer Invoice |
| BR-VB | Vendor Bill |
| BR-AMD | Amendment |
| BR-CRN | Credit Note |
| BR-RIN | Re-Invoice |
| BR-CUR | Currency and Exchange Rate |
| BR-TAX | Tax |
| BR-INT | Integration |
| BR-RPT | Reporting |
| BR-SEC | Security and Permission |
| BR-AUD | Audit |
| BR-POL | Configurable Business Policy |

---

## 3. Order Management Rules

| Rule ID | Rule | Level |
|---|---|---|
| BR-ORD-001 | Every Order must belong to exactly one Customer. | Confirmed |
| BR-ORD-002 | An Order may contain multiple product lines. | Confirmed |
| BR-ORD-003 | An Order is validated and confirmed as one atomic operational unit. | Confirmed |
| BR-ORD-004 | Operations validates the whole Order before confirmation. | Confirmed |
| BR-ORD-005 | Draft is the entry status for Orders received into MidOffice. | Current Design |
| BR-ORD-006 | Orders shall not be physically deleted; cancellation status shall be used where applicable. | Confirmed |
| BR-ORD-007 | Before invoice generation, an Order may be cancelled according to permission rules. | Current Design |
| BR-ORD-008 | After invoice generation and Odoo synchronization, commercial correction shall use amendment workflows rather than direct editing. | Confirmed |

---

## 4. Customer Rules

| Rule ID | Rule | Level |
|---|---|---|
| BR-CUS-001 | Anonymous Orders are not supported. | Confirmed |
| BR-CUS-002 | Customer mapping is mandatory before an Order can be processed in MidOffice. | Confirmed |

---

## 5. Product and Vendor Rules

| Rule ID | Rule | Level |
|---|---|---|
| BR-PRD-001 | A single Order may include different product types such as Flight, Hotel, Insurance, Visa, Bus, or Tour Package components. | Confirmed |
| BR-PRD-002 | Product lines may have their own vendor, cost, currency, exchange rate, and operational details. | Confirmed |
| BR-VB-001 | One Order may generate multiple Vendor Bills. | Confirmed |
| BR-VB-002 | Vendor Bill generation is cost-driven. | Confirmed |
| BR-VB-003 | If no supplier cost exists, no Vendor Bill shall be generated for that cost. | Confirmed |
| BR-VB-004 | Product lines with the same vendor may be grouped into one Vendor Bill. | Confirmed |

---

## 6. Financial and Amendment Rules

| Rule ID | Rule | Level |
|---|---|---|
| BR-INV-001 | One Order shall generate one Customer Invoice. | Current Design |
| BR-AMD-001 | Commercial changes after confirmation or invoicing shall use document-based amendment rather than direct editing. | Confirmed |
| BR-AMD-002 | Original Orders shall remain viewable, searchable, and read-only after amendment. | Confirmed |
| BR-CRN-001 | Full Credit Note shall copy the original Order and related financial documents. | Confirmed |
| BR-CRN-002 | Full Credit Note shall multiply financial values by negative one. | Confirmed |
| BR-RIN-001 | Re-Invoice shall always begin with Full Credit Note. | Confirmed |
| BR-RIN-002 | Re-Invoice shall create a new Draft Order copied from the original Order. | Confirmed |

---

## 7. Currency, Tax, Integration, Reporting

| Rule ID | Rule | Level |
|---|---|---|
| BR-CUR-001 | Travel MidOffice shall support Base Currency and Transaction Currency. | Confirmed |
| BR-CUR-002 | Current Base Currency is USD. | Confirmed |
| BR-CUR-003 | Transaction Currency may be USD or MMK depending on source and business context. | Confirmed |
| BR-CUR-006 | Exchange rate governance belongs to Finance. | Confirmed |
| BR-TAX-001 | Tax configuration is owned by Finance and Odoo. | Confirmed |
| BR-INT-001 | Travel MidOffice is the operational system of record. | Confirmed |
| BR-INT-002 | Odoo is the accounting system. | Confirmed |
| BR-RPT-001 | Profitability reporting shall consider the full amendment chain. | Confirmed |
