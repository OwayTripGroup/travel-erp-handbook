# ADR-003 - Document-Based Amendment Strategy

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**ADR ID:** ADR-003  
**Status:** Accepted  
**Version:** 1.0.0  
**Date:** 2026-07-02  
**Decision Owner:** Enterprise Architecture Team

---

## 1. Decision

Travel MidOffice shall use a document-based amendment strategy instead of direct editing or order-version-based amendment.

When a confirmed or invoiced transaction requires correction, the original Order is preserved as read-only. Corrections are performed through Full Credit Note and Re-Invoice.

---

## 2. Approved Pattern

1. Preserve the original Order as read-only.
2. Create a Full Credit Note by copying the original Order, Customer Invoice, and Vendor Bills with negative values.
3. For Re-Invoice, create a new Draft Order copied from the original Order.
4. Allow authorized users to manually update the copied Draft Order.
5. Re-run the normal workflow: Draft, Validate, Confirm, Invoice, and Odoo synchronization.
6. Preserve all relationships for audit and reporting.

---

## 3. Rationale

This decision supports:

- Auditability
- Accounting integrity
- Odoo reconciliation
- Operational traceability
- Clean reporting across amendment chains

---

## 4. Consequences

Positive consequences:

- Original Orders remain unchanged.
- Financial correction trail is explicit.
- Odoo reversal and re-invoice mapping becomes clearer.
- Profitability can be reconstructed across amendment chains.

Trade-offs:

- More records are created during amendments.
- Users must understand amendment chains.
- Reporting must aggregate original, credit, and re-invoice records correctly.
