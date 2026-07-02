# API-004 - Report and Download API

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** API-004  
**Document Type:** API Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines API behavior for report generation, downloads, and scheduled reports.

Reports may be generated immediately for small data sets or processed as background jobs for larger outputs.

---

## 2. Report Generation Modes

| Mode | Behavior |
|---|---|
| Immediate | Small reports may return directly to the user. |
| Background Job | Larger reports should be queued and notify the user when completed. |
| Scheduled | Scheduled reports may be generated and delivered through email. |

---

## 3. Recommended Endpoints

```text
POST /api/reports/generate
GET /api/report-jobs
GET /api/report-jobs/{id}
GET /api/report-jobs/{id}/download
POST /api/report-schedules
GET /api/report-schedules
PUT /api/report-schedules/{id}
DELETE /api/report-schedules/{id}
```

---

## 4. Access Control

Users should only download reports they are authorized to access.

Generated report files should preserve:

- Requesting user
- Report type
- Generated date
- Expiration date
- Download permission
- Job duration
- Status

---

## 5. Audit and Performance

Report generation should track:

- Who generated the report
- When it was requested
- When it completed
- Duration
- Filters used
- Export format
- Download activity

---

## 6. Related Documents

- OPS-001 Background Jobs and Sync Jobs
- OPS-003 Notification and Alerting
- INT-003 Power BI and Reporting Integration
- STD-003 API Standard
