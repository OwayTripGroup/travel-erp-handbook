# BUS-004 - Commercial Transaction

**Project:** Travel MidOffice Enterprise Architecture Handbook  
**Document ID:** BUS-004  
**Document Type:** Business Architecture  
**Version:** 1.0.0  
**Status:** Draft  
**Owner:** Enterprise Architecture Team  
**Last Updated:** 2026-07-02

---

## 1. Purpose

This document defines the Commercial Transaction concept.

A Commercial Transaction is the top-level business concept that represents the commercial agreement between Oway Travel and a Customer.

---

## 2. Business Definition

A Commercial Transaction begins when the Customer commits to purchase or when the business commits to fulfill the purchase.

Travel MidOffice receives the Commercial Transaction and creates an operational Order to process it.

---

## 3. Relationship to Order

The Order is the operational representation of the Commercial Transaction.

```text
Commercial Transaction
  -> Order
  -> Customer Invoice
  -> Vendor Bill
  -> Full Credit Note
  -> Re-Invoice
```

---

## 4. Ownership

Travel MidOffice owns the Commercial Transaction once it is received from a source system.

Source systems are producers, not operational owners.

---

## 5. Source Systems

Commercial Transactions may originate from:

- Oway Travel Website
- Oway Travel Mobile App
- Sales Operation
- Amadeus
- Future partner systems

---

## 6. Architecture Notes

Commercial Transaction is a business architecture concept. It does not require a new database table immediately.

It provides a stable parent concept for Order, Invoice, Vendor Bill, Credit Note, Re-Invoice, reporting, and audit.
