# Database Schema

## BarberHub SaaS MVP

Version: 1.0

---

# Database Overview

```text
Tenant
│
├── Users
│     ├── Owner
│     ├── Barber
│     └── Customer
│
├── Services
│
├── Barbers
│
├── Schedules
│
├── Bookings
│
├── Favorites
│
└── Settings
```

---

# Entity Relationship Diagram (ERD)

```text
                   +----------------+
                   |    tenants     |
                   +----------------+
                   | id             |
                   | name           |
                   | slug           |
                   | logo           |
                   | phone          |
                   | email          |
                   | address        |
                   | latitude       |
                   | longitude      |
                   | business_hour  |
                   | created_at     |
                   +-------+--------+
                           |
                      1 ----*
                           |
      +--------------------+---------------------+
      |                    |                     |
      ▼                    ▼                     ▼

+-------------+     +--------------+     +---------------+
|    users    |     |   barbers    |     |   services    |
+-------------+     +--------------+     +---------------+
| id          |     | id           |     | id            |
| tenant_id   |     | tenant_id    |     | tenant_id     |
| role        |     | user_id      |     | name          |
| name        |     | bio          |     | duration      |
| email       |     | experience   |     | price         |
| password    |     | photo        |     | status        |
| phone       |     | status       |     +-------+-------+
| avatar      |     +------+-------+             |
| status      |            |                     |
+------+------+
       |                   |               *-----1
       |                   |
       |                   ▼
       |           +----------------+
       |           | schedules      |
       |           +----------------+
       |           | id             |
       |           | barber_id      |
       |           | work_date      |
       |           | start_time     |
       |           | end_time       |
       |           | is_available   |
       |           +-------+--------+
       |                   |
       |                   |
       ▼                   ▼
+----------------+   +----------------+
|   bookings     |---| booking_items  |
+----------------+   +----------------+
| id             |   | id             |
| tenant_id      |   | booking_id     |
| customer_id    |   | service_id     |
| barber_id      |   | price          |
| booking_date   |   | duration       |
| booking_time   |   +----------------+
| total_price    |
| status         |
| notes          |
+--------+-------+
         |
         |
         ▼
+----------------+
|   payments     |
+----------------+
| id             |
| booking_id     |
| amount         |
| method         |
| status         |
| transaction_id |
+----------------+

Customer
    |
    |
    ▼
+----------------+
|   favorites    |
+----------------+
| id             |
| customer_id    |
| barber_id      |
| tenant_id      |
+----------------+
```

---

# Tables

## tenants

| Column        | Type      |
| ------------- | --------- |
| id            | bigint    |
| name          | varchar   |
| slug          | varchar   |
| logo          | varchar   |
| phone         | varchar   |
| email         | varchar   |
| address       | text      |
| latitude      | decimal   |
| longitude     | decimal   |
| business_hour | json      |
| status        | boolean   |
| created_at    | timestamp |
| updated_at    | timestamp |

---

## users

| Column            | Type            |
| ----------------- | --------------- |
| id                | bigint          |
| tenant_id         | bigint nullable |
| role              | enum            |
| name              | varchar         |
| email             | varchar         |
| phone             | varchar         |
| password          | varchar         |
| avatar            | varchar         |
| email_verified_at | timestamp       |
| status            | boolean         |
| remember_token    | varchar         |
| created_at        | timestamp       |

Role

* super_admin
* owner
* barber
* customer

---

## barbers

| Column         | Type      |
| -------------- | --------- |
| id             | bigint    |
| tenant_id      | bigint    |
| user_id        | bigint    |
| bio            | text      |
| specialization | varchar   |
| experience     | integer   |
| photo          | varchar   |
| status         | boolean   |
| created_at     | timestamp |

---

## services

| Column      | Type    |
| ----------- | ------- |
| id          | bigint  |
| tenant_id   | bigint  |
| name        | varchar |
| description | text    |
| duration    | integer |
| price       | decimal |
| status      | boolean |

---

## schedules

| Column       | Type    |
| ------------ | ------- |
| id           | bigint  |
| barber_id    | bigint  |
| work_date    | date    |
| start_time   | time    |
| end_time     | time    |
| is_available | boolean |

---

## bookings

| Column       | Type      |
| ------------ | --------- |
| id           | bigint    |
| tenant_id    | bigint    |
| customer_id  | bigint    |
| barber_id    | bigint    |
| booking_date | date      |
| booking_time | time      |
| total_price  | decimal   |
| notes        | text      |
| status       | enum      |
| created_at   | timestamp |

Status

* pending
* confirmed
* completed
* cancelled

---

## booking_items

| Column     | Type    |
| ---------- | ------- |
| id         | bigint  |
| booking_id | bigint  |
| service_id | bigint  |
| price      | decimal |
| duration   | integer |

Satu booking dapat memiliki satu atau lebih layanan sehingga struktur ini tetap fleksibel.

---

## favorites

| Column      | Type      |
| ----------- | --------- |
| id          | bigint    |
| customer_id | bigint    |
| tenant_id   | bigint    |
| barber_id   | bigint    |
| created_at  | timestamp |

---

## payments (Optional MVP)

| Column         | Type      |
| -------------- | --------- |
| id             | bigint    |
| booking_id     | bigint    |
| amount         | decimal   |
| method         | varchar   |
| status         | enum      |
| transaction_id | varchar   |
| paid_at        | timestamp |

Status

* pending
* paid
* failed
* refunded

---

# Foreign Keys

```text
users.tenant_id
    → tenants.id

barbers.tenant_id
    → tenants.id

barbers.user_id
    → users.id

services.tenant_id
    → tenants.id

schedules.barber_id
    → barbers.id

bookings.tenant_id
    → tenants.id

bookings.customer_id
    → users.id

bookings.barber_id
    → barbers.id

booking_items.booking_id
    → bookings.id

booking_items.service_id
    → services.id

favorites.customer_id
    → users.id

favorites.barber_id
    → barbers.id

favorites.tenant_id
    → tenants.id

payments.booking_id
    → bookings.id
```

---

# Index Strategy

Primary Index

* id

Secondary Index

* tenant_id
* barber_id
* customer_id
* booking_date
* booking_time
* status
* email
* slug

Composite Index

```text
(tenant_id, booking_date)

(tenant_id, barber_id)

(barber_id, work_date)

(customer_id, booking_date)
```

---

# Data Isolation (Multi-Tenant)

Semua data operasional wajib memiliki `tenant_id` sebagai pemisah antar barbershop.

Contoh query:

```sql
SELECT *
FROM bookings
WHERE tenant_id = :tenantId;
```

Dengan pendekatan ini, setiap tenant hanya dapat mengakses data miliknya sendiri melalui middleware atau global scope di backend.

---

# Future Expansion

Skema ini dapat diperluas tanpa perubahan besar dengan menambahkan tabel seperti:

* reviews
* memberships
* loyalty_points
* promotions
* coupons
* subscriptions
* invoices
* notifications
* attendance
* inventory
* product_sales
* audit_logs
* branches (multi-location)
* staff_permissions
* payment_methods
* customer_addresses
* waitlists
* recurring_bookings
