# BUS-003 - Product Management

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-003  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Product Management domain for Travel MidOffice.

Product Management ensures that travel products can be represented consistently inside Orders, financial documents, reporting, and integrations.

---

## 2. Product Types

Travel MidOffice supports multiple travel product types, including:

- Flight
- Hotel
- Bus
- Insurance
- Visa
- Car Rental
- Tour
- Future product types

A single Order may contain multiple product types.

Tour packages may include multiple Product Lines.

---

## 3. Product Line

A Product Line is a specific travel service within an Order.

Each Product Line may have:

- Product type
- Vendor
- Cost
- Selling price
- Currency
- Exchange rate
- Tax
- Operational details
- Booking reference
- Travel-specific attributes

---

## 4. Business Rules

| Rule ID | Rule |
|---|---|
| BR-PRD-001 | A single Order may include different product types. |
| BR-PRD-002 | Product lines may have their own vendor, cost, currency, exchange rate, and operational details. |
| BR-PRD-003 | A single product type may involve more than one vendor where business scenarios require it. |
| BR-PRD-004 | If one product line changes after invoicing, the preferred correction pattern is Full Credit Note and Re-Invoice. |

---

## 5. Architecture Notes

Products should be modeled flexibly enough to support future travel products without redesigning the Order domain.

Product-specific details should be separated from shared Order and Product Line concepts.
