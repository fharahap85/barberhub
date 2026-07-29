# Business Rules Specification

## BarberHub SaaS MVP

Version: 1.0

---

# 1. General Rules

## BR-001 Multi Tenant Isolation

Setiap data bisnis harus terhubung dengan satu tenant.

Rules:

* Setiap barbershop memiliki `tenant_id`.
* User hanya dapat mengakses data tenant yang dimilikinya.
* Tenant tidak dapat melihat data tenant lain.
* Semua query bisnis wajib menggunakan filter `tenant_id`.

Example:

Owner Barbershop A tidak dapat melihat:

* Booking Barbershop B
* Barber Barbershop B
* Customer Barbershop B

---

# 2. User Rules

## BR-002 User Registration

Customer dapat melakukan registrasi sendiri.

Owner hanya dapat dibuat melalui:

* Admin invitation
* Owner onboarding

Barber dapat dibuat oleh:

* Owner

---

## BR-003 User Role Access

System roles:

| Role        | Access                    |
| ----------- | ------------------------- |
| Super Admin | Semua tenant              |
| Owner       | Tenant sendiri            |
| Barber      | Jadwal & booking miliknya |
| Customer    | Booking & profile sendiri |

---

## BR-004 Email Uniqueness

Email harus unik dalam sistem.

Tidak boleh:

* Dua user dengan email sama
* Login menggunakan email yang tidak terdaftar

---

# 3. Tenant Rules

## BR-005 Tenant Creation

Ketika tenant dibuat:

System harus membuat:

* Tenant profile
* Owner account
* Default settings

---

## BR-006 Tenant Status

Tenant memiliki status:

* Active
* Suspended
* Deleted

Rules:

Jika tenant suspended:

* Customer tidak dapat melakukan booking baru.
* Owner tidak dapat mengubah data.
* Data tetap tersimpan.

---

# 4. Barber Rules

## BR-007 Barber Ownership

Setiap barber hanya dapat dimiliki oleh satu tenant.

Example:

Barber John:

Allowed:

```
Barbershop A
```

Not allowed:

```
Barbershop A
+
Barbershop B
```

---

## BR-008 Barber Availability

Barber hanya dapat menerima booking ketika:

* Status aktif
* Memiliki jadwal kerja
* Tidak sedang unavailable

---

## BR-009 Barber Schedule

Owner dapat mengatur:

* Hari kerja
* Jam kerja
* Hari libur

Example:

```
Monday

09:00 - 17:00
```

---

# 5. Service Rules

## BR-010 Service Ownership

Service hanya berlaku pada tenant sendiri.

Example:

Haircut Barbershop A:

Tidak dapat digunakan oleh:

Barbershop B

---

## BR-011 Service Duration

Setiap service wajib memiliki:

* Nama
* Durasi
* Harga

Duration digunakan untuk menghitung slot booking.

---

# 6. Booking Rules

## BR-012 Booking Availability

Customer hanya dapat booking jika:

* Tenant aktif
* Barber aktif
* Service aktif
* Slot tersedia

---

## BR-013 Booking Time Validation

System harus mengecek:

1. Barber bekerja pada tanggal tersebut.
2. Jam booking berada dalam jam kerja.
3. Tidak ada booking aktif pada waktu tersebut.

---

## BR-014 Prevent Double Booking

Satu barber tidak boleh memiliki dua booking aktif pada waktu yang sama.

Invalid:

```
Barber A

10:00 Customer 1

10:00 Customer 2
```

Valid:

```
Barber A

10:00 Customer 1

11:00 Customer 2
```

---

## BR-015 Booking Status Flow

Status booking:

```
Pending
   |
   ▼
Confirmed
   |
   ▼
Completed
```

Alternative:

```
Pending
   |
   ▼
Cancelled
```

---

## BR-016 Booking Cancellation

Customer dapat cancel booking jika:

* Status masih Pending/Confirmed
* Belum melewati waktu booking

Example:

Booking:

15 August
10:00

Cannot cancel:

15 August
11:00

---

## BR-017 Booking Modification

MVP:

Customer tidak dapat mengubah booking.

Flow:

Cancel existing booking

*

Create new booking

---

# 7. Favorite Rules

## BR-018 Favorite Barber

Customer dapat:

* Add favorite barber
* Remove favorite barber

Constraint:

Tidak boleh duplicate.

Example:

Invalid:

```
Customer A

Favorite Barber X

Favorite Barber X
```

---

## BR-019 Favorite Tenant

Customer dapat menyimpan barbershop favorit.

---

# 8. Payment Rules (Future)

## BR-020 Payment Requirement

Payment tidak wajib untuk MVP.

Booking tetap valid tanpa pembayaran.

---

## BR-021 Payment Status

Payment:

```
Pending
 |
 ▼
Paid
 |
 ▼
Completed
```

Failed:

```
Pending
 |
 ▼
Failed
```

---

# 9. Security Rules

## BR-022 Authentication Required

Endpoint tertentu wajib login:

Required:

* Create booking
* Manage barber
* Manage schedule
* View private data

---

## BR-023 Authorization Check

Setiap request harus mengecek:

1. User login
2. User role
3. Tenant ownership

---

## BR-024 Password Rules

Password:

Minimum:

* 8 characters

Recommended:

* Uppercase
* Lowercase
* Number

---

# 10. Data Rules

## BR-025 Soft Delete

Data penting tidak langsung dihapus.

Menggunakan:

```
deleted_at
```

Untuk:

* Users
* Barbers
* Services
* Bookings

---

## BR-026 Audit Tracking

System mencatat:

* Created by
* Updated by
* Created date
* Updated date

---

# 11. Notification Rules (Future)

## BR-027 Booking Notification

Trigger:

Booking created

Send:

* Customer notification
* Owner notification

---

## BR-028 Reminder Notification

Future:

Reminder dikirim:

24 jam sebelum booking.

---

# 12. API Rules

## BR-029 API Response Standard

Success:

```json
{
 "success": true,
 "data": {}
}
```

Error:

```json
{
 "success": false,
 "message": "Error message"
}
```

---

## BR-030 API Tenant Validation

Setiap API bisnis wajib melakukan:

```
Authenticate User

↓

Identify Tenant

↓

Validate Ownership

↓

Execute Action
```

---

# 13. Booking Conflict Rules

Conflict Priority:

1. Existing Completed booking
2. Existing Confirmed booking
3. Existing Pending booking

System tidak boleh membuat booking baru jika conflict ditemukan.

---

# 14. MVP Simplification Rules

Untuk menjaga scope MVP:

Included:

* Basic booking
* Basic schedule
* Tenant management
* Barber management

Excluded:

* Dynamic pricing
* Multiple branches
* Subscription billing
* Advanced analytics
* AI recommendation
* Loyalty program

---

# 15. Core Business Principle

The system must ensure:

1. Customer dapat menemukan barber dengan mudah.
2. Customer tidak mengalami double booking.
3. Owner dapat mengelola bisnisnya secara mandiri.
4. Data antar tenant selalu terisolasi.
5. Arsitektur siap dikembangkan menjadi mobile application.
