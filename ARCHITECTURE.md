# System Architecture

## BarberHub SaaS MVP

Version 1.0

---

# 1. Architecture Overview

```text
                    Internet
                        │
                ┌─────────────────┐
                │     Browser      │
                │ React / Vue SPA  │
                └────────┬─────────┘
                         │ HTTPS
                         ▼
                ┌─────────────────┐
                │ Laravel API     │
                │ Authentication  │
                │ Business Logic  │
                └────────┬─────────┘
                         │
          ┌──────────────┼──────────────┐
          │              │              │
          ▼              ▼              ▼
    MySQL Database     Storage       Cache
     Multi-Tenant      Images        Redis*
                                     (Future)

```

*Redis tidak wajib pada MVP.

---

# 2. High-Level Components

## Frontend

Framework

* React atau Vue

Responsibilities

* Login
* Dashboard
* Booking
* Barber Catalogue
* Schedule
* Customer Profile
* Favorites

Communicates with

REST API

---

## Backend

Laravel 12

Responsibilities

* Authentication
* Authorization
* Multi Tenant
* Booking Engine
* Schedule Validation
* CRUD
* API

---

## Database

MySQL

Stores

* Tenants
* Users
* Barbers
* Services
* Bookings
* Favorites
* Schedule

---

## Storage

Local Storage (MVP)

Later

* Amazon S3
* Cloudflare R2

Stores

* Barber Photos
* Shop Logo
* Cover Images

---

# 3. Multi-Tenant Architecture

Recommended Model

Shared Database

Shared Schema

Tenant Isolation using tenant_id

```text
Database

Users
--------------------------
id
tenant_id
name

Barbers
--------------------------
id
tenant_id
name

Bookings
--------------------------
id
tenant_id
customer_id

Services
--------------------------
id
tenant_id
```

Advantages

* Cheap
* Easy deployment
* Suitable for MVP
* Easy maintenance

Future Upgrade

Dedicated Database per Tenant

---

# 4. Backend Layer

```text
Controller
      │
      ▼
Service Layer
      │
      ▼
Repository
      │
      ▼
Database
```

Responsibilities

Controller

* Request Validation
* API Response

Service

* Business Logic
* Booking Validation
* Schedule Validation

Repository

* Database Query

Model

* Eloquent ORM

---

# 5. Authentication Flow

```text
User

 │

 ▼

Login

 │

 ▼

Laravel Sanctum

 │

 ▼

Access Token

 │

 ▼

Protected API
```

Roles

* Super Admin
* Owner
* Customer

Future

* Barber

---

# 6. Authorization

Role Based Access Control

```text
Super Admin

├── Manage Tenants
├── Manage Platform
└── Manage Users

Owner

├── Manage Shop
├── Manage Barber
├── Manage Booking
└── Manage Schedule

Customer

├── Booking
├── Favorites
└── Profile
```

---

# 7. Booking Architecture

```text
Customer

     │

     ▼

Choose Shop

     │

     ▼

Choose Barber

     │

     ▼

Select Date

     │

     ▼

Available Time

     │

     ▼

Booking Request

     │

     ▼

Booking Validation

     │

     ▼

Save Booking

     │

     ▼

Confirmation
```

Validation

* Barber Available
* Working Hours
* No Double Booking
* Booking Date Valid

---

# 8. Folder Structure (Laravel)

```text
app/

├── Http/
│   ├── Controllers/
│   ├── Middleware/
│   └── Requests/
│
├── Models/
│
├── Services/
│
├── Repositories/
│
├── Policies/
│
├── Events/
│
├── Listeners/
│
└── Helpers/

routes/

database/

storage/

config/

```

---

# 9. Frontend Structure

```text
src/

components/

pages/

layouts/

services/

hooks/

stores/

router/

assets/

utils/

```

---

# 10. API Communication

```text
Frontend

     │

 REST API

     │

Laravel

     │

Business Logic

     │

Database
```

Response Format

```json
{
  "success": true,
  "message": "Booking created successfully",
  "data": {}
}
```

Error Format

```json
{
  "success": false,
  "message": "Time slot unavailable"
}
```

---

# 11. Database Architecture

```text
Tenant

│

├── Users

├── Barbers

├── Services

├── Bookings

├── Schedules

├── Favorites

└── Settings
```

Relationships

Tenant

↓

Many Users

↓

Many Barbers

↓

Many Services

↓

Many Bookings

---

# 12. Deployment Architecture

```text
             Cloud Server

          Ubuntu 24.04

                 │

      ┌──────────┴──────────┐

      │                     │

 Nginx Reverse Proxy     SSL

      │

Laravel API

      │

PHP-FPM

      │

MySQL

      │

Storage

```

Recommended Server

* 2 vCPU
* 4 GB RAM
* 80 GB SSD

Suitable for approximately 50–100 tenants in the MVP stage.

---

# 13. Future Architecture

```text
                    Load Balancer

                          │

         ┌────────────────┴───────────────┐

         ▼                                ▼

    Laravel API 1                   Laravel API 2

         │                                │

         └───────────────┬────────────────┘

                         ▼

                       Redis

                         ▼

                      MySQL Cluster

                         ▼

                    Object Storage

                         ▼

                 Mobile App + Web App
```

Future Enhancements

* Queue Worker
* Redis Cache
* WebSocket Notifications
* Payment Gateway
* Search Engine (Meilisearch/Elasticsearch)
* CDN
* Monitoring (Prometheus & Grafana)
* Logging (ELK Stack)
* Auto Scaling

---

# 14. Recommended Technology Stack

| Layer            | Technology                |
| ---------------- | ------------------------- |
| Frontend         | React + Vite + TypeScript |
| UI               | Tailwind CSS + shadcn/ui  |
| State Management | TanStack Query + Zustand  |
| Backend          | Laravel 12                |
| Authentication   | Laravel Sanctum           |
| Database         | MySQL 8                   |
| ORM              | Eloquent                  |
| File Storage     | Local Storage (MVP)       |
| API              | REST                      |
| Web Server       | Nginx                     |
| Runtime          | PHP 8.4                   |
| Deployment       | Docker + Docker Compose   |
| CI/CD            | GitHub Actions            |
| Version Control  | GitHub                    |

---

# 15. Architecture Principles

* API-first design agar mudah digunakan kembali oleh aplikasi mobile.
* Tenant isolation menggunakan `tenant_id` pada seluruh data bisnis.
* Layered architecture (Controller → Service → Repository → Database) untuk menjaga kode tetap terstruktur.
* Stateless REST API agar mudah diskalakan.
* Modular sehingga fitur seperti pembayaran, notifikasi, atau loyalty dapat ditambahkan tanpa perubahan besar pada arsitektur inti.
