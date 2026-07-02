# ADR-003 - Document-Based Amendment Strategy

**Project:** Travel ERP Enterprise Architecture Handbook  
**ADR ID:** ADR-003  
**Status:** Accepted  
**Version:** 1.0.0  
**Date:** 2026-07-02  
**Decision Owner:** ERP Architecture Team

---

## Revision History

| Version | Date | Author | Description |
|---|---|---|---|
| 1.0.0 | 2026-07-02 | ERP Architecture Team | Initial ADR for document-based amendment strategy. |

---

## 1. Summary

The Travel ERP shall use a document-based amendment strategy instead of direct editing or order-version-based amendment.

When a confirmed or invoiced transaction requires correction, the original Order is preserved as read-only. Corrections are performed through explicit business documents such as Full Credit Note and Re-Invoice.

This strategy prioritizes auditability, accounting integrity, Odoo reconciliation, and operational traceability.

---

## 2. Context

The Travel ERP manages travel transactions that may originate from online channels, offline sales operations, Amadeus, and other future systems.

An Order may contain multiple product lines such as flight, hotel, insurance, visa, bus, or tour package components. Each Order may generate one Customer Invoice and multiple Vendor Bills.

After financial documents are generated and synchronized with Odoo, direct modification becomes risky because changes may affect:

- Customer billing
- Vendor payable amounts
- Revenue
- Cost
- Margin
- Tax
- Accounting balances
- Reporting
- Audit history
- Odoo reconciliation

The project previously considered order versioning, but current business design uses Full Credit Note and Re-Invoice workflows instead.

---

## 3. Decision

The Travel ERP will not use order versioning as the primary amendment mechanism.

Instead, the system will use document-based amendment.

The approved amendment pattern is:

1. Preserve the original Order as read-only.
2. Create a Full Credit Note by copying the original Order, Customer Invoice, and Vendor Bills with negative values.
3. For Re-Invoice, create a new draft Order copied from the original Order.
4. Allow authorized users to manually update the copied draft Order.
5. Re-run the normal workflow: Draft, Validate, Confirm, Invoice, and Odoo synchronization.
6. Preserve all original and amendment relationships for audit and reporting.

---

## 4. Business Rationale

The decision is based on the following business objectives:

- Keep the original business transaction visible and unchanged.
- Maintain clean accounting correction history.
- Avoid hidden edits after financial documents exist.
- Support simple and auditable amendment operations.
- Make Odoo reversal and re-invoicing behavior easier to reconcile.
- Allow full amendment chain reporting in Power BI and operational reports.

---

## 5. Approved Amendment Workflows

### 5.1 Full Credit Note

A Full Credit Note copies the original Order and related financial documents using negative values.

Copied objects include:

- Order header
- Order product lines
- Customer reference
- Passenger or travel details where applicable
- Selling amounts
- Cost amounts
- Taxes
- Customer Invoice
- Vendor Bills
- Operational notes where applicable

All financial values are multiplied by negative one.

### 5.2 Re-Invoice

A Re-Invoice always begins with a Full Credit Note.

The process is:

```text
Original Order
  -> Full Credit Note
  -> New Draft Order copied from original
  -> Manual revision
  -> Validate
  -> Confirm
  -> Generate Customer Invoice and Vendor Bills
  -> Sync to Odoo
```

A Re-Invoice may itself be amended again, producing an amendment chain.

---

## 6. Status Model Implication

The system stores separate Order Status and Invoice Status.

For a credited Order:

- Order Status may remain Invoiced.
- Invoice Status becomes Credited.

This separation should be retained because Order state and financial document state are different concepts.

Architecture recommendation: future refinement should consider replacing the current terminal Order status named Invoice with a more operational term such as Completed, while preserving invoice status separately.

---

## 7. Relationship Requirements

The system must preserve relationships across amendment chains.

Recommended relationship fields include:

- Original Order reference
- Original Customer Invoice reference
- Original Vendor Bill reference
- Credit Note reference
- Re-Invoice Order reference
- Amendment type
- Amendment reason
- Amendment chain or group reference
- Created by
- Approved by where applicable
- Created timestamp

These relationships are required for audit, reporting, operational support, and Odoo reconciliation.

---

## 8. Consequences

### Positive Consequences

- Strong auditability.
- Clear financial correction trail.
- Original Orders remain unchanged.
- Easier Odoo reversal and re-invoice mapping.
- Easier profitability reconstruction across amendment chains.
- Reduced risk of hidden financial changes.

### Trade-offs

- More records are created during amendments.
- Users must understand amendment chains.
- Reporting must aggregate original, credit, and re-invoice records correctly.
- UI must clearly show original and replacement relationships.
- Data model must support relationship chains well.

---

## 9. Alternatives Considered

### Alternative 1 - Direct Editing

Direct editing of confirmed or invoiced Orders was rejected.

Reason:

- Weak auditability.
- Risk of changing historical financial data.
- Difficult reconciliation with Odoo.
- Harder to explain changes to Finance and auditors.

### Alternative 2 - Order Versioning

Order versioning was considered but not selected as the primary amendment mechanism.

Reason:

- The current business correction model is tied to financial documents.
- Full Credit Note and Re-Invoice better match accounting correction behavior.
- Document-based amendment is simpler for Odoo synchronization and accounting reversal.

### Alternative 3 - Partial Product-Level Amendment

Partial amendment of individual product lines was not selected for the current implementation.

Reason:

- Current business preference is simplicity and clean auditability.
- If part of the Order changes, the system performs Full Credit Note and Re-Invoice.
- Partial credit can be considered as a future enhancement after beta feedback.

---

## 10. Business Rules Introduced

| Rule ID | Rule |
|---|---|
| BR-AMD-001 | Confirmed or invoiced Orders shall not be directly edited for commercial changes. |
| BR-AMD-002 | Full Credit Note shall copy the full original Order and related financial documents with negative values. |
| BR-AMD-003 | Re-Invoice shall always begin with Full Credit Note. |
| BR-AMD-004 | Original Orders shall remain viewable, searchable, and read-only after amendment. |
| BR-AMD-005 | Amendment chains shall be preserved for audit and reporting. |
| BR-AMD-006 | Profitability reporting shall consider the full amendment chain. |

These rules should be added to the Business Rules Catalog when GOV-005 is completed.

---

## 11. Implementation Implications

The implementation should support:

- Immutable original Order after amendment.
- Full copy of original business and financial data.
- Negative-value reversal documents.
- New draft Order creation for Re-Invoice.
- Relationship tracking between original, credit, and replacement documents.
- Clear UI timeline of amendment chain.
- Reporting logic that calculates net effect across the chain.
- Odoo synchronization for credit and re-invoice documents.

---

## 12. Open Items

The following topics remain open or policy-dependent:

- Final amendment approval rules after beta feedback.
- Paid or reconciled document amendment controls.
- Partial credit support as future enhancement.
- Attachment copy policy.
- Customer-facing document numbering for amendment chains.
- UI design for amendment timeline.

---

## 13. Related Documents

- ARC-000 Design Principles
- BUS-000 Travel ERP Business Overview
- REF-001 Order Domain Discovery Record
- BUS-001 Order Management
- BUS-004 Credit Note Workflow
- BUS-005 Re-Invoice Workflow
- ACC-001 Accounting Lifecycle
- INT-001 Odoo Integration
