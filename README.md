# Travel ERP Enterprise Architecture Handbook

This repository contains the official architecture handbook for the Travel ERP System.

The handbook is designed to serve as the single source of truth for business architecture, accounting architecture, integration architecture, data architecture, API design, frontend guidance, operations, standards, and architecture decision records.

## Purpose

The handbook supports:

- Onboarding new developers, business analysts, QA engineers, and implementation partners
- Preserving architecture decisions and design rationale
- Standardizing ERP workflows and integration patterns
- Maintaining traceability between requirements, business rules, architecture, and implementation
- Supporting long-term maintainability of the Travel ERP platform

## Recommended Local Setup

This repository is structured for MkDocs Material.

```bash
pip install mkdocs-material
mkdocs serve
```

Then open the local MkDocs URL shown in the terminal.

## Repository Structure

```text
docs/
  00-governance/
  01-architecture/
  02-business/
  03-accounting/
  04-integration/
  05-data/
  06-api/
  07-frontend/
  08-operations/
  09-standards/
  10-adr/
  11-reference/
  12-requirements/
  assets/
  templates/
```

## Architecture Principle

The Travel ERP is the operational system of record. Odoo is used as the accounting system. Business workflows, master data, orders, customer invoices, vendor bills, credit notes, re-invoices, and operational reporting are owned by the Travel ERP. Accounting entries, ledgers, AR/AP, tax accounting, payments, and reconciliation are owned by Odoo.

## Status

Initial handbook scaffold created.
