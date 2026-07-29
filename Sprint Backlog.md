# Sprint Backlog

## BarberHub SaaS MVP

Version: 1.0

---

# Development Strategy

## Sprint Duration

2 weeks / sprint

## Team Assumption

* 1 Backend Developer
* 1 Frontend Developer
* 1 UI/UX Designer (part-time)
* 1 QA (part-time)

---

# Sprint 0 — Project Foundation

Duration:
1 week

Goal:
Prepare development environment and project foundation.

---

## Epic: Project Setup

### TASK-001 Backend Project Setup

Priority:
High

Estimate:
1 day

Description:

Setup Laravel backend project.

Tasks:

* Create Laravel project
* Configure environment
* Configure MySQL
* Setup API structure
* Configure CORS
* Setup Git repository

Acceptance Criteria:

* Laravel runs successfully
* Database connected
* API endpoint accessible

---

### TASK-002 Frontend Project Setup

Priority:
High

Estimate:
1 day

Tasks:

* Setup React/Vue project
* Configure TypeScript
* Install Tailwind CSS
* Setup routing
* Setup API client

Acceptance Criteria:

* Frontend runs successfully
* Basic layout available

---

### TASK-003 Development Environment

Priority:
Medium

Estimate:
1 day

Tasks:

* Docker configuration
* Local database
* Environment documentation

---

# Sprint 1 — Authentication & Multi Tenant Foundation

Duration:
2 weeks

Goal:
User authentication and tenant architecture ready.

---

# Epic: Authentication

## TASK-101 Customer Registration API

Priority:
High

Estimate:
1 day

Backend:

Create:

POST /api/auth/register

Implement:

* Validation
* Password hashing
* Customer role assignment

---

## TASK-102 Login System

Priority:
High

Estimate:
2 days

Implement:

POST /api/auth/login

Features:

* Email login
* Password verification
* Token generation

---

## TASK-103 Frontend Authentication

Priority:
High

Estimate:
3 days

Pages:

* Login
* Register
* Logout

---

# Epic: Multi Tenant

## TASK-104 Tenant Migration

Priority:
High

Estimate:
1 day

Create:

* tenants table
* tenant relationship

---

## TASK-105 Tenant Middleware

Priority:
High

Estimate:
2 days

Implement:

* Tenant identification
* Tenant access validation
* Data isolation

---

## TASK-106 Role Permission System

Priority:
High

Estimate:
2 days

Roles:

* Admin
* Owner
* Barber
* Customer

---

Sprint 1 Deliverable:

✓ User login
✓ User registration
✓ Role system
✓ Tenant isolation foundation

---

# Sprint 2 — Shop Management

Duration:
2 weeks

Goal:
Owner can manage barbershop information.

---

# Epic: Barbershop Profile

## TASK-201 Shop Profile API

Priority:
High

Estimate:
2 days

Features:

* View profile
* Update profile
* Upload logo

---

## TASK-202 Owner Dashboard Layout

Priority:
Medium

Estimate:
3 days

Create:

* Sidebar
* Header
* Dashboard layout

---

## TASK-203 Shop Profile UI

Priority:
High

Estimate:
2 days

Pages:

* Shop information
* Edit profile
* Upload image

---

# Epic: Barber Management

## TASK-204 Barber CRUD API

Priority:
High

Estimate:
3 days

Endpoints:

GET /barbers

POST /barbers

PUT /barbers/{id}

DELETE /barbers/{id}

---

## TASK-205 Barber Management UI

Priority:
High

Estimate:
3 days

Features:

* Barber list
* Add barber
* Edit barber
* Delete barber

---

Sprint 2 Deliverable:

✓ Owner dashboard
✓ Shop profile management
✓ Barber CRUD

---

# Sprint 3 — Service & Schedule Management

Duration:
2 weeks

Goal:
Prepare booking availability system.

---

# Epic: Service Management

## TASK-301 Service CRUD API

Priority:
High

Estimate:
2 days

Features:

* Create service
* Update service
* Delete service
* List service

---

## TASK-302 Service Management UI

Priority:
High

Estimate:
2 days

---

# Epic: Schedule Management

## TASK-303 Schedule Database Implementation

Priority:
High

Estimate:
1 day

Create:

* schedules table
* availability logic

---

## TASK-304 Schedule API

Priority:
High

Estimate:
3 days

Features:

* Add schedule
* Update schedule
* Block schedule
* Check availability

---

## TASK-305 Schedule UI

Priority:
High

Estimate:
3 days

Features:

* Calendar view
* Working hours
* Block date

---

Sprint 3 Deliverable:

✓ Services ready
✓ Barber schedule ready
✓ Availability engine ready

---

# Sprint 4 — Customer Booking Flow

Duration:
2 weeks

Goal:
Customer can complete booking.

---

# Epic: Customer Experience

## TASK-401 Shop Discovery API

Priority:
High

Estimate:
2 days

Features:

* List shops
* Search shops
* Shop detail

---

## TASK-402 Customer Shop UI

Priority:
High

Estimate:
3 days

Pages:

* Home
* Search
* Shop detail

---

# Epic: Booking System

## TASK-403 Booking API

Priority:
Critical

Estimate:
4 days

Features:

* Create booking
* Validate availability
* Prevent double booking
* Booking status

---

## TASK-404 Booking UI

Priority:
Critical

Estimate:
4 days

Pages:

* Choose barber
* Choose service
* Choose time
* Confirmation

---

Sprint 4 Deliverable:

✓ Customer booking complete
✓ Availability validation
✓ Double booking prevention

---

# Sprint 5 — Booking Management & Favorites

Duration:
2 weeks

Goal:
Complete MVP business flow.

---

# Epic: Owner Booking Management

## TASK-501 Booking Dashboard API

Priority:
High

Estimate:
2 days

Features:

* List bookings
* Filter status
* Update status

---

## TASK-502 Booking Management UI

Priority:
High

Estimate:
3 days

Features:

* Booking table
* Status update
* Detail view

---

# Epic: Favorite System

## TASK-503 Favorite API

Priority:
Medium

Estimate:
2 days

Features:

* Add favorite
* Remove favorite
* List favorite

---

## TASK-504 Favorite UI

Priority:
Medium

Estimate:
2 days

Pages:

* Favorite barber
* Favorite shop

---

Sprint 5 Deliverable:

✓ Owner manages bookings
✓ Customer favorites available

---

# Sprint 6 — Polish, Testing & Deployment

Duration:
2 weeks

Goal:
Prepare MVP release.

---

# Epic: Quality Assurance

## TASK-601 API Testing

Priority:
High

Estimate:
3 days

Test:

* Authentication
* Permission
* Booking
* Tenant isolation

---

## TASK-602 Frontend Testing

Priority:
Medium

Estimate:
2 days

Test:

* User flow
* Responsive layout
* Error handling

---

## TASK-603 Bug Fixing

Priority:
High

Estimate:
3 days

---

# Epic: Deployment

## TASK-604 Production Setup

Priority:
High

Estimate:
2 days

Setup:

* Server
* Database
* SSL
* Environment

---

## TASK-605 Documentation

Priority:
Medium

Estimate:
2 days

Create:

* Deployment guide
* API documentation
* User guide

---

Sprint 6 Deliverable:

✓ Tested MVP
✓ Production deployment
✓ Documentation complete

---

# MVP Release Checklist

## Backend

✓ Laravel API
✓ Authentication
✓ Multi tenant
✓ RBAC
✓ Booking engine
✓ Validation

---

## Frontend

✓ Customer website
✓ Owner dashboard
✓ Responsive design

---

## Business Flow

✓ Customer finds shop
✓ Customer chooses barber
✓ Customer books schedule
✓ Owner manages booking

---

# Future Backlog (Post MVP)

Priority: Later

## Payment

* Midtrans/Stripe integration

## Notification

* Email notification
* WhatsApp notification
* Push notification

## Review

* Rating barber
* Customer feedback

## Mobile App

* React Native / Flutter

## Subscription SaaS

* Monthly billing
* Plan management
* Feature limits
