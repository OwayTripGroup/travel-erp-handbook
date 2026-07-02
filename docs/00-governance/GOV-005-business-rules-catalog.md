# GOV-005 - Business Rules Catalog

**Project:** Travel ERP Enterprise Architecture Handbook  
**Document ID:** GOV-005  
**Document Type:** Governance Catalog  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** ERP Architecture Team  
**Last Updated:** 2026-07-02

---

## Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0.0 | 2026-07-02 | ERP Architecture Team | Initial catalog seeded with confirmed rules from architecture discovery. |

---

## 1. Purpose

This document is the central catalog of business rules for the Travel ERP System.

Business rules define what the system must enforce or preserve from a business perspective. Workflow documents, API specifications, database designs, QA test cases, and implementation tasks should reference these rule IDs instead of redefining the same rules repeatedly.

This catalog is especially important because the Travel ERP is still in implementation and some policies will evolve after beta feedback from Finance, Operations, Sales, and Management.

---

## 2. Rule Confidence Levels

| Level | Meaning |
|---|---|
| Confirmed | Stable rule based on confirmed architecture or business decision |
| Current Design | Current implementation target, but may evolve |
| Policy Candidate | Business policy expected to change after beta feedback |
| Future Consideration | Not current scope, but intentionally anticipated |

---

## 3. Rule Categories

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

Rule IDs must not be reused, even when a rule is deprecated.

---

## 4. Order Management Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-ORD-001 | Every Order must belong to exactly one Customer. | Confirmed | BUS-000, REF-001 |
| BR-ORD-002 | An Order may contain multiple product lines. | Confirmed | BUS-000, REF-001 |
| BR-ORD-003 | An Order is validated and confirmed as one atomic operational unit. | Confirmed | ARC-000, REF-001 |
| BR-ORD-004 | Operations validates the whole Order before confirmation. | Confirmed | REF-001 |
| BR-ORD-005 | Draft is the entry status for Orders received into MidOffice. | Current Design | REF-001 |
| BR-ORD-006 | Orders shall not be physically deleted; cancellation status shall be used where applicable. | Confirmed | REF-001 |
| BR-ORD-007 | Before invoice generation, an Order may be cancelled according to permission rules. | Current Design | REF-001 |
| BR-ORD-008 | After invoice generation and Odoo synchronization, commercial correction shall use amendment workflows rather than direct editing. | Confirmed | ADR-003 |

---

## 5. Customer Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-CUS-001 | Anonymous Orders are not supported. | Confirmed | BUS-000, REF-001 |
| BR-CUS-002 | Customer mapping is mandatory before an Order can be processed in MidOffice. | Confirmed | REF-001 |

---

## 6. Product and Product Line Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-PRD-001 | A single Order may include different product types such as Flight, Hotel, Insurance, Visa, Bus, or Tour Package components. | Confirmed | BUS-000, REF-001 |
| BR-PRD-002 | Product lines may have their own vendor, cost, currency, exchange rate, and operational details. | Confirmed | REF-001 |
| BR-PRD-003 | A single product type may involve more than one vendor where business scenarios require it. | Confirmed | REF-001 |
| BR-PRD-004 | If one product line changes after invoicing, the preferred correction pattern is Full Credit Note and Re-Invoice rather than partial line editing. | Current Design | ADR-003, REF-001 |

---

## 7. Customer Invoice Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-INV-001 | One Order shall generate one Customer Invoice. | Current Design | BUS-000, REF-001 |
| BR-INV-002 | Customer billing is consolidated at Order level even when the Order has multiple product lines. | Current Design | REF-001 |
| BR-INV-003 | Posted or synchronized Customer Invoices shall not be edited directly for commercial changes. | Confirmed | ADR-003 |

---

## 8. Vendor Bill Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-VB-001 | One Order may generate multiple Vendor Bills. | Confirmed | BUS-000, REF-001 |
| BR-VB-002 | Vendor Bill generation is cost-driven. | Confirmed | BUS-000, REF-001 |
| BR-VB-003 | If no supplier cost exists, no Vendor Bill shall be generated for that cost. | Confirmed | REF-001 |
| BR-VB-004 | Product lines with the same vendor may be grouped into one Vendor Bill. | Confirmed | REF-001 |
| BR-VB-005 | Product lines with different vendors shall generate separate Vendor Bills. | Confirmed | REF-001 |

---

## 9. Amendment Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-AMD-001 | Commercial changes after confirmation or invoicing shall use document-based amendment rather than direct editing. | Confirmed | ADR-003 |
| BR-AMD-002 | Original Orders shall remain viewable, searchable, and read-only after amendment. | Confirmed | ADR-003, REF-001 |
| BR-AMD-003 | Amendment chains shall preserve relationships between original Order, Credit Note, Re-Invoice, Customer Invoice, and Vendor Bills. | Confirmed | ADR-003 |
| BR-AMD-004 | Amendment can happen multiple times; there is currently no maximum amendment depth. | Current Design | REF-001 |
| BR-AMD-005 | Approval rules for amendment are configurable policy candidates until beta feedback is collected. | Policy Candidate | ARC-000, REF-001 |

---

## 10. Credit Note Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-CRN-001 | Full Credit Note shall copy the original Order and related financial documents. | Confirmed | ADR-003, REF-001 |
| BR-CRN-002 | Full Credit Note shall multiply financial values by negative one. | Confirmed | ADR-003, REF-001 |
| BR-CRN-003 | Full Credit Note shall behave as a reversal-style document for Odoo accounting synchronization. | Confirmed | ADR-003 |
| BR-CRN-004 | Partial credit support is a future consideration unless later approved for implementation. | Future Consideration | ADR-003 |

---

## 11. Re-Invoice Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-RIN-001 | Re-Invoice shall always begin with Full Credit Note. | Confirmed | ADR-003, REF-001 |
| BR-RIN-002 | Re-Invoice shall create a new Draft Order copied from the original Order. | Confirmed | ADR-003, REF-001 |
| BR-RIN-003 | Authorized users shall manually update the copied Draft Order according to the amendment scenario. | Confirmed | REF-001 |
| BR-RIN-004 | The Re-Invoice Order shall proceed through the normal Order lifecycle after manual changes. | Confirmed | ADR-003 |
| BR-RIN-005 | Re-Invoice Orders may themselves be amended again. | Current Design | REF-001 |

---

## 12. Currency and Exchange Rate Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-CUR-001 | The Travel ERP shall support Base Currency and Transaction Currency. | Confirmed | ARC-000, BUS-000 |
| BR-CUR-002 | Current Base Currency is USD. | Confirmed | BUS-000 |
| BR-CUR-003 | Transaction Currency may be USD or MMK depending on source and business context. | Confirmed | BUS-000 |
| BR-CUR-004 | Online Orders may provide product-line exchange rates through API. | Confirmed | REF-001 |
| BR-CUR-005 | Manual Orders may use order-level currency and finance-approved exchange rate from MidOffice. | Confirmed | REF-001 |
| BR-CUR-006 | Exchange rate governance belongs to Finance. | Confirmed | ARC-000, REF-001 |
| BR-CUR-007 | Exchange rates used in business transactions must be preserved for audit. | Confirmed | ARC-000 |

---

## 13. Tax Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-TAX-001 | Tax configuration is owned by Finance and Odoo. | Confirmed | ARC-000, BUS-000 |
| BR-TAX-002 | MidOffice consumes synchronized tax configuration where required. | Confirmed | ARC-000 |
| BR-TAX-003 | MidOffice shall not become the accounting tax source of truth. | Confirmed | ARC-000 |

---

## 14. Integration Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-INT-001 | Travel ERP is the operational system of record. | Confirmed | ARC-000, BUS-000 |
| BR-INT-002 | Odoo is the accounting system. | Confirmed | ARC-000, BUS-000 |
| BR-INT-003 | Customer Invoices and Vendor Bills shall be synchronized to Odoo for accounting. | Current Design | BUS-000 |
| BR-INT-004 | Odoo shall not become the owner of operational workflow state. | Confirmed | ARC-000 |
| BR-INT-005 | Integration operations should preserve traceability between MidOffice documents and Odoo documents. | Confirmed | ADR-003 |

---

## 15. Reporting Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-RPT-001 | Profitability reporting shall consider the full amendment chain. | Confirmed | ARC-000, ADR-003, REF-001 |
| BR-RPT-002 | Power BI reporting shall receive transaction data required to reconstruct original, credit, and re-invoice outcomes. | Current Design | BUS-000, REF-001 |
| BR-RPT-003 | Reports shall not rely only on the latest Order when amendment chains exist. | Confirmed | REF-001 |

---

## 16. Security and Permission Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-SEC-001 | Amendment actions shall be permission-controlled. | Confirmed | REF-001 |
| BR-SEC-002 | Approval rules may vary by department, role, amount, margin, payment state, or accounting state. | Policy Candidate | ARC-000 |
| BR-SEC-003 | Policy-based approval configuration is preferred over hardcoded approval behavior. | Policy Candidate | ARC-000 |

---

## 17. Audit Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-AUD-001 | Original Orders must remain available for view and search after amendment. | Confirmed | ADR-003 |
| BR-AUD-002 | Financial correction must be traceable through explicit documents. | Confirmed | ADR-003 |
| BR-AUD-003 | Amendment reason and amendment type should be stored for audit. | Confirmed | ADR-003 |
| BR-AUD-004 | User and timestamp information should be preserved for amendment actions. | Confirmed | ADR-003 |

---

## 18. Business Policy Rules

| Rule ID | Rule | Level | Related Documents |
|---|---|---|---|
| BR-POL-001 | Approval workflow is not final until beta feedback is collected. | Policy Candidate | ARC-000, REF-001 |
| BR-POL-002 | Margin threshold policy is not currently enforced by the system, but margin goals exist as a business target. | Policy Candidate | REF-001 |
| BR-POL-003 | Configurable business policy is preferred for approval rules, thresholds, and department-specific controls. | Policy Candidate | ARC-000 |

---

## 19. Governance Rules

- Every new business rule must have a unique Rule ID.
- A rule must belong to one primary category.
- Deprecated rule IDs must not be reused.
- Workflow documents should reference Rule IDs instead of redefining the same rule.
- Rules should be reviewed when beta feedback changes policy.
- Implementation behavior should not contradict Confirmed rules without a new ADR or approved rule update.

---

## 20. Related Documents

- GOV-001 Documentation Standard
- ARC-000 Design Principles
- BUS-000 Travel ERP Business Overview
- REF-001 Order Domain Discovery Record
- ADR-003 Document-Based Amendment Strategy
