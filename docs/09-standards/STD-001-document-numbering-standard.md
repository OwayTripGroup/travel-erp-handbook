# STD-001 - Document Numbering Standard

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** STD-001  
**Document Type:** Standard  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the numbering standard for handbook documents.

The goal is to keep the repository predictable, searchable, and easy to maintain as the knowledge base grows.

---

## 2. Document Prefixes

| Prefix | Meaning |
|---|---|
| GOV | Governance document |
| ARC | Architecture principle or architecture overview |
| ADR | Architecture Decision Record |
| BUS | Business domain document |
| ACC | Accounting architecture document |
| INT | Integration architecture document |
| DATA | Data architecture document |
| API | API architecture document |
| FE | Frontend architecture document |
| OPS | Operations architecture document |
| STD | Standard |
| REF | Reference or temporary discovery document |
| REQ | Requirement document |

---

## 3. File Naming Format

```text
<PREFIX>-<NUMBER>-<kebab-case-title>.md
```

Examples:

```text
BUS-005-order-management.md
ACC-003-currency-and-exchange-rate-strategy.md
ADR-003-document-based-amendment-strategy.md
```

---

## 4. Numbering Rules

- Numbers should be three digits.
- Existing document numbers should not be reused after deletion.
- Temporary reference documents may be deleted after incorporation into permanent documents.
- ADR numbers must remain stable after publication.
- Document titles may be refined, but document IDs should remain stable where possible.

---

## 5. Related Documents

- GOV-001 Documentation Standard
- GOV-002 Domain Dictionary
