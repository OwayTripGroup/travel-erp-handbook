# SEC-001 - Organization Structure

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** SEC-001  
**Document Type:** Security and Organization Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the organization structure assumptions used for Travel MidOffice security, ownership, approval, and visibility design.

The final organization structure should be validated with business stakeholders before production.

---

## 2. Core Departments

Travel MidOffice should support at least the following business functions:

- Sales
- Operations
- Finance
- Product
- Customer Service
- IT / Engineering
- Management
- System Administration

---

## 3. Ownership by Department

| Department | Primary Responsibility |
|---|---|
| Sales | Customer relationship, selling price, offline sales ownership, corporate customer handling |
| Operations | Order validation, supplier coordination, product-line operational completeness |
| Finance | Accounting policy, exchange rate governance, tax governance, Odoo accounting review |
| Product | Product configuration, product categories, product analytics mapping |
| Customer Service | Customer communication and operational follow-up where applicable |
| IT / Engineering | System configuration, integration, platform reliability, technical operations |
| Management | Approval policy, visibility policy, strategic reporting |
| System Administration | User, role, permission, and system setting administration |

---

## 4. Team and Channel Ownership

Orders may belong to different teams based on source and sales ownership.

Examples:

- Online System for Oway Travel Website and Mobile App orders
- Respective Sales Team for offline orders
- Operations Team responsible for validation
- Finance Team responsible for accounting-sensitive review

---

## 5. Future Structure Considerations

The security model should be flexible enough to support:

- Department
- Team
- Position
- Branch
- Company
- Future multi-company structure

Multi-company is not required immediately, but the architecture should not block it.

---

## 6. Related Documents

- SEC-002 Role-Based Access Control
- SEC-003 Permission Matrix
- SEC-004 Approval Framework
- DATA-001 Data Ownership Matrix
