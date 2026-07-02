# DATA-003 - Settings and Configuration Model

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** DATA-003  
**Document Type:** Data Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the settings and configuration model for Travel MidOffice.

Settings support business flexibility without requiring code changes for every operational configuration.

---

## 2. Configuration Principles

- Settings should be auditable.
- Settings should have ownership.
- Settings should be validated before use.
- Settings should not become an uncontrolled dumping ground.
- Settings should be grouped by module and business purpose.
- Configuration changes that affect finance or accounting should require appropriate ownership and audit.

---

## 3. Recommended Settings Structure

A flexible settings table may include:

| Field | Purpose |
|---|---|
| id | Technical identifier |
| module | Module or domain owner |
| key | Unique setting key within module |
| value | JSON value |
| description | Human-readable explanation |
| status | Active or inactive |
| created_by | Creator |
| updated_by | Last updater |
| created_at | Created timestamp |
| updated_at | Updated timestamp |

---

## 4. Example Settings

Examples:

```json
{
  "module": "product",
  "key": "product_type.analytics_mapping",
  "value": {
    "flight": "analytics-flight",
    "hotel": "analytics-hotel"
  }
}
```

```json
{
  "module": "finance",
  "key": "exchange_rate.policy",
  "value": {
    "source": "mid_office_finance",
    "allow_manual_override": false
  }
}
```

---

## 5. Governance

Settings should have clear business ownership.

Examples:

| Setting Area | Owner |
|---|---|
| Product configuration | Product Team |
| Analytics mapping | Product / Finance / Reporting |
| Exchange rate policy | Finance |
| Tax references | Finance / Odoo |
| Approval policy | Management / Department Owner |
| Integration retry policy | Engineering |

---

## 6. Audit Requirements

Settings changes should record:

- Old value
- New value
- User
- Timestamp
- Reason where required

Finance-sensitive settings should be especially traceable.

---

## 7. Related Documents

- GOV-005 Business Rules Catalog
- ACC-003 Currency and Exchange Rate Strategy
- INT-001 Odoo Integration
- OPS-002 Audit Trail and Activity Timeline
