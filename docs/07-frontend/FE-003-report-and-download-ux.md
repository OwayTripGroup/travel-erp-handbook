# FE-003 - Report and Download UX

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** FE-003  
**Document Type:** Frontend Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the frontend user experience for report generation, report downloads, and scheduled reports.

The goal is to make reporting operationally useful while keeping long-running report generation clear to the user.

---

## 2. Report Generation UX

For small reports, the system may return a downloadable file immediately.

For larger reports, the system should create a background job and notify the user when the report is ready.

---

## 3. Download Center

The Download Center should show:

- Report name
- Report type
- Requested by
- Requested date
- Status
- Format
- File size where available
- Expiration date
- Download action

---

## 4. Report Job Statuses

Recommended statuses:

```text
Queued
Processing
Completed
Failed
Expired
```

---

## 5. Scheduled Report UX

Users should be able to configure scheduled reports based on permission.

Scheduled report configuration may include:

- Report type
- Frequency
- Delivery time
- Format
- Recipients where allowed
- Active or inactive status

---

## 6. Access Control UX

Users should only see or download reports they are authorized to access.

Shared or common reports should be clearly marked.

---

## 7. Related Documents

- API-004 Report and Download API
- OPS-001 Background Jobs and Sync Jobs
- OPS-003 Notification and Alerting
- INT-003 Power BI and Reporting Integration
