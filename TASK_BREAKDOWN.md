# Technical Task Breakdown — BarberHub MVP

Diselaraskan dengan **Sprint Backlog** (2-week sprints, 1 BE + 1 FE + part-time UI/QA).

---

## Sprint 0 — Project Foundation (1 week)

### TASK-001 Backend Project Setup (1d)
- Init Laravel 12, configure MySQL, env, CORS
- API structure, git repo

### TASK-002 Frontend Project Setup (1d)
- Init React + Vite + TypeScript
- Tailwind, shadcn/ui, TanStack Query, Zustand
- Router, Axios instance, layouts

### TASK-003 Development Environment (1d)
- Docker Compose (nginx, php-fpm, mysql)
- CI (GitHub Actions)

---

## Sprint 1 — Authentication & Multi Tenant (2 weeks)

### TASK-101 Customer Registration API (1d)
- `POST /auth/register` — validation, hashing, customer role

### TASK-102 Login System (2d)
- `POST /auth/login`, `POST /auth/logout`, `GET /auth/me`
- Sanctum token, role-based redirect

### TASK-103 Frontend Auth (3d)
- Login, register, forgot password pages
- Auth guard, token persistence

### TASK-104 Tenant Migration (1d)
- `tenants` table, relationships, seeder

### TASK-105 Tenant Middleware (2d)
- `TenantScope` global scope, `SetTenant` middleware
- Tenant isolation on all queries

### TASK-106 Role Permission System (2d)
- Middleware `role:super_admin,owner,customer`
- CRUD permission checks

### TASK-107 Owner Onboarding (2d)
- Create tenant + owner account in one flow
- Seed default settings

**Deliverable:** Login, register, role system, tenant isolation.

---

## Sprint 2 — Shop & Barber Management (2 weeks)

### TASK-201 Shop Profile API (2d)
- `GET /tenant`, `PUT /tenant`
- Logo upload, business hours (JSON)

### TASK-202 Owner Dashboard Layout (3d)
- Sidebar, header, dashboard layout
- Navigation: Dashboard, Bookings, Barbers, Services, Schedule, Customers, Settings

### TASK-203 Shop Profile UI (2d)
- Shop info, edit form, image upload

### TASK-204 Barber CRUD API (3d)
- `GET /barbers`, `POST /barbers`, `PUT /barbers/{id}`, `DELETE /barbers/{id}`
- Photo upload

### TASK-205 Barber Management UI (3d)
- Table list, add/edit modal, delete confirmation

**Deliverable:** Owner dashboard, shop profile, barber CRUD.

---

## Sprint 3 — Service & Schedule (2 weeks)

### TASK-301 Service CRUD API (2d)
- `GET /services`, `POST /services`, `PUT /services/{id}`, `DELETE /services/{id}`

### TASK-302 Service Management UI (2d)
- Service list, add/edit form

### TASK-303 Schedule DB & Logic (1d)
- `schedules` table, availability calculation

### TASK-304 Schedule API (3d)
- `POST /schedules`, block dates
- `GET /availability?barber_id=&date=` — time slot generation

### TASK-305 Schedule UI (3d)
- Calendar view, working hours, block date

**Deliverable:** Services ready, schedule ready, availability engine.

---

## Sprint 4 — Customer Booking Flow (2 weeks)

### TASK-401 Shop Discovery API (2d)
- `GET /barbershops` — list, search, location filter
- `GET /barbershops/{id}` — detail with barbers & services

### TASK-402 Customer Shop UI (3d)
- Home, search, shop detail, barber detail
- Location/map view

### TASK-403 Booking API (4d) — **Critical**
- `POST /bookings` — validate: tenant active, barber available, working hours, no double booking
- `GET /bookings/my` — customer history
- `PATCH /bookings/{id}/status` — cancel (before time)

### TASK-404 Booking UI (4d) — **Critical**
- Multi-step wizard: service → barber → date → time → confirm
- Booking success page, history page, cancel action

**Deliverable:** Customer completes booking, availability validated, double booking prevented.

---

## Sprint 5 — Booking Management & Favorites (2 weeks)

### TASK-501 Owner Booking Dashboard API (2d)
- `GET /bookings?status=&date=` — filtered list
- `PATCH /bookings/{id}/status` — confirm/complete/cancel
- `GET /dashboard` — summary (today's bookings, pending, completed)

### TASK-502 Owner Booking UI (3d)
- Booking table with status colors, filter, status actions

### TASK-503 Favorite API (2d)
- `POST /favorites`, `DELETE /favorites/{id}`, `GET /favorites`
- Barber & shop favorites

### TASK-504 Favorite UI (2d)
- Favorite tabs (barbers / shops), toggle on detail pages

### TASK-505 Customer Profile (1d)
- `GET /profile`, `PUT /profile`
- Edit name, phone, avatar

**Deliverable:** Owner manages bookings, customer favorites & profile.

---

## Sprint 6 — Polish, Testing & Deploy (2 weeks)

### TASK-601 API Testing (3d)
- Feature tests: auth, permission, booking, tenant isolation
- Validation edge cases

### TASK-602 Frontend Testing (2d)
- Vitest for critical components, user flow

### TASK-603 Bug Fixing (3d)
- Error boundaries, rate limiting, sanitization, responsive QA

### TASK-604 Production Setup (2d)
- Production Dockerfiles, SSL, env config
- Deploy script

### TASK-605 Documentation (2d)
- Deployment guide, API doc, user guide

**Deliverable:** Tested MVP, production deployment, docs complete.

---

## Dependency Map

```
Sprint 0
   │
   ▼
Sprint 1 ──► Sprint 2 ──► Sprint 3 ──► Sprint 4 ──► Sprint 5
                                                         │
                                                         ▼
                                                    Sprint 6
```
