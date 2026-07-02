# DATA-001 - Data Ownership Matrix

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** DATA-001  
**Document Type:** Data Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the ownership of major data domains in Travel MidOffice.

Data ownership clarifies who is accountable for correctness, governance, and business meaning of each major object.

---

## 2. Ownership Principles

- A system may store data without owning the business meaning.
- Operational ownership and accounting ownership may differ.
- Reporting may consume data from multiple systems but should not redefine ownership.
- Every major business object should have a clear accountable owner.

---

## 3. Data Ownership Matrix

| Data Object | Business Owner | Operational System of Record | Accounting System | Reporting Source |
|---|---|---|---|---|
| Customer | Sales | Travel MidOffice | Odoo partner where required | Travel MidOffice / Power BI |
| Vendor | Operations | Travel MidOffice | Odoo partner where required | Travel MidOffice / Power BI |
| Product | Product Team | Travel MidOffice | Odoo reference where required | Travel MidOffice / Power BI |
| Commercial Transaction | Sales / Operations | Travel MidOffice | Not applicable | Travel MidOffice / Power BI |
| Order | Operations | Travel MidOffice | Not applicable | Travel MidOffice / Power BI |
| Customer Invoice | Finance / Operations | Travel MidOffice | Odoo | Travel MidOffice / Odoo / Power BI |
| Vendor Bill | Finance / Operations | Travel MidOffice | Odoo | Travel MidOffice / Odoo / Power BI |
| Full Credit Note | Finance / Operations | Travel MidOffice | Odoo | Travel MidOffice / Odoo / Power BI |
| Re-Invoice | Finance / Operations | Travel MidOffice | Odoo | Travel MidOffice / Odoo / Power BI |
| Exchange Rate | Finance | Travel MidOffice | Referenced by Odoo where applicable | Travel MidOffice / Power BI |
| Tax | Finance | Odoo | Odoo | Odoo / Travel MidOffice reference |
| Payment | Finance | Odoo | Odoo | Odoo / Power BI |
| Sync Job | Engineering / Operations | Travel MidOffice | Not applicable | Travel MidOffice |
| Report Job | Engineering / Business Owner | Travel MidOffice | Not applicable | Travel MidOffice |

---

## 4. Key Architecture Decisions

Travel MidOffice is the operational system of record.

Odoo is the accounting system of record.

Power BI is a reporting and analytics consumer, not a source of truth.

---

## 5. Open Questions

- Final business owner per department after Organization and Security Discovery
- Whether branch-level data ownership is required
- Whether multi-company ownership will be required in the future

---

## 6. Related Documents

- ADR-001 Travel MidOffice Operational System of Record
- ADR-002 Odoo Accounting System of Record
- GOV-002 Domain Dictionary
- BUS-005 Order Management
- INT-001 Odoo Integration
