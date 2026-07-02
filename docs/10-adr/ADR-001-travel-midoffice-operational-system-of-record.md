# ADR-001 - Travel MidOffice as Operational System of Record

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**ADR ID:** ADR-001  
**Status:** Accepted  
**Version:** 1.0.0  
**Date:** 2026-07-02  
**Decision Owner:** Enterprise Architecture Team

---

## 1. Decision

Travel MidOffice is the operational system of record for Commercial Transactions once they are received from source systems.

Source systems such as the Oway Travel Website, Oway Travel Mobile App, Amadeus, and future partner systems create or send Commercial Transactions, but Travel MidOffice owns operational processing after receipt.

---

## 2. Context

Commercial Transactions may originate from multiple channels.

Each source system may have its own workflow and status. However, Travel MidOffice requires one unified operational workflow for validation, confirmation, invoice generation, vendor bill generation, amendment, reporting, and audit.

---

## 3. Rationale

This decision supports:

- Unified operational workflow
- Clear ownership after transaction intake
- Consistent Order validation
- Centralized audit trail
- Reliable reporting
- Consistent Odoo synchronization
- Future scalability across more source systems

---

## 4. Consequences

Positive consequences:

- Travel MidOffice becomes the authoritative operational platform.
- Source systems do not need to own downstream finance or amendment workflows.
- Operational reporting can be centralized.
- Odoo integration becomes more predictable.

Trade-offs:

- Source system statuses must be mapped carefully into Travel MidOffice.
- Integration boundaries must be clearly documented.
- Duplicate ownership between source systems and Travel MidOffice must be avoided.
