# Product Requirements Document (PRD)

## Product Name

**BarberHub (Working Title)**

Version: 1.0 (MVP)

---

# 1. Overview

## Background

Barbershop owners masih banyak yang mengelola booking secara manual melalui WhatsApp, telepon, atau walk-in. Hal ini menyebabkan jadwal yang tidak teratur, risiko double booking, dan pengalaman pelanggan yang kurang optimal.

Produk ini bertujuan membangun platform SaaS yang memungkinkan banyak barbershop menggunakan sistem yang sama untuk mengelola bisnis mereka secara online.

MVP difokuskan pada validasi pasar dengan menyediakan fitur inti tanpa kompleksitas yang tidak diperlukan.

---

# 2. Product Goal

Menyediakan platform online yang memungkinkan:

* Customer menemukan barbershop
* Customer melakukan booking secara online
* Owner mengelola barber dan jadwal
* Setiap barbershop memiliki dashboard sendiri (Multi Tenant)

---

# 3. Target Users

## Customer

Orang yang ingin:

* mencari barbershop
* melihat barber
* melakukan booking
* menyimpan barber favorit

---

## Barber

Staff yang menerima booking dari customer.

---

## Barbershop Owner

Pemilik usaha yang ingin:

* mengelola barber
* mengatur jadwal
* menerima booking
* melihat data pelanggan

---

## Super Admin

Pengelola platform SaaS.

---

# 4. Scope MVP

## Included

* Authentication
* Multi Tenant
* Barbershop Profile
* Barber Management
* Online Booking
* Schedule Management
* Customer Management
* Favorite Barber
* Favorite Barbershop
* Location View

---

## Not Included

* Membership
* Loyalty Points
* Review System
* Chat
* Push Notification
* Payroll
* Inventory
* POS
* Analytics Advanced
* Coupon
* Subscription Billing
* Mobile Application

---

# 5. User Flow

## Customer

Register/Login

↓

Browse Barbershop

↓

View Barbers

↓

Choose Barber

↓

Choose Date

↓

Choose Time

↓

Confirm Booking

↓

Booking Success

---

## Owner

Login

↓

Dashboard

↓

Manage Barber

↓

Manage Schedule

↓

View Booking

↓

Accept / Complete Booking

---

# 6. Functional Requirements

## Authentication

Customer

* Register
* Login
* Forgot Password

Owner

* Login
* Logout
* Reset Password

---

## Multi Tenant

Each tenant has:

* Own dashboard
* Own customers
* Own bookings
* Own barbers
* Own services

Tenant cannot access another tenant's data.

---

## Barbershop Module

Owner can:

* Create profile
* Upload logo
* Upload cover image
* Edit address
* Add contact number
* Set opening hours

Customer can:

* View profile
* View operating hours
* View location

---

## Barber Module

Owner can:

* Add barber
* Edit barber
* Delete barber
* Upload photo
* Set specialization
* Set working schedule

Customer can:

* Browse barber
* View profile
* View availability

---

## Booking Module

Customer can:

* Select barber
* Select date
* Select available time
* Confirm booking
* View booking history
* Cancel booking (before scheduled time)

Owner can:

* View bookings
* Accept booking
* Reject booking
* Complete booking

Booking Status:

* Pending
* Confirmed
* Completed
* Cancelled

---

## Schedule Module

Owner can:

* Set working hours
* Set unavailable dates
* Block schedule

System should prevent double booking.

---

## Favorite Module

Customer can:

* Favorite barber
* Favorite barbershop
* Remove favorite
* View favorite list

---

## Location Module

Customer can:

* View address
* Open map
* Get directions

---

# 7. Non Functional Requirements

## Performance

* Page load < 3 seconds
* API response < 500ms (average)

---

## Security

* JWT / Laravel Sanctum Authentication
* Password Hashing
* HTTPS
* Role-based Access Control

---

## Scalability

Architecture should support:

* Hundreds of tenants
* Thousands of bookings
* Mobile App integration

---

## Availability

Target uptime:

99%

---

# 8. User Roles

## Super Admin

* Manage tenants
* Manage subscriptions (future)
* Manage platform

---

## Owner

* Manage barbershop
* Manage barber
* Manage booking

---

## Barber

(Optional in MVP)

View assigned bookings.

---

## Customer

Book services.

---

# 9. Database (High-Level)

Users

* id
* tenant_id
* role
* name
* email
* password

Tenants

* id
* name
* slug
* address
* phone
* logo

Barbers

* id
* tenant_id
* name
* specialization
* photo

Services

* id
* tenant_id
* name
* duration
* price

Schedules

* id
* barber_id
* date
* start_time
* end_time

Bookings

* id
* tenant_id
* customer_id
* barber_id
* service_id
* booking_date
* booking_time
* status

Favorites

* id
* customer_id
* barber_id
* tenant_id

Payments (Future)

* id
* booking_id
* amount
* payment_status

---

# 10. API (High-Level)

Authentication

POST /register

POST /login

POST /logout

---

Barbershop

GET /barbershops

GET /barbershops/{id}

PUT /barbershops

---

Barbers

GET /barbers

POST /barbers

PUT /barbers/{id}

DELETE /barbers/{id}

---

Booking

GET /bookings

POST /bookings

PUT /bookings/{id}

DELETE /bookings/{id}

---

Favorites

GET /favorites

POST /favorites

DELETE /favorites/{id}

---

# 11. Suggested Tech Stack

## Frontend

* React.js atau Vue.js
* Tailwind CSS
* Axios
* React Query / Vue Query

---

## Backend

* Laravel 12 (Recommended)
* Laravel Sanctum
* MySQL/PostgreSQL
* Redis (Future)
* REST API

Alternative:

* Go (Gin/Fiber)

---

# 12. MVP Success Metrics

Business Metrics

* 10+ onboarded barbershops
* 100+ registered customers
* 300+ successful bookings
* 30% repeat bookings

Technical Metrics

* No critical bugs
* No double bookings
* API uptime >99%
* Response time <500ms

---

# 13. Future Roadmap

Phase 2

* Online Payment
* Ratings & Reviews
* Promotions
* Membership
* Notifications
* Loyalty Program

Phase 3

* Native Mobile App (iOS & Android)
* Multi-location support
* POS Integration
* Inventory Management
* Employee Attendance
* Revenue Analytics
* Subscription & Billing
* AI-powered booking recommendations
