# API Specification

## BarberHub SaaS MVP

Version: 1.0

---

# 1. API Overview

## Base URL

Development:

```
https://api-dev.barberhub.com/api
```

Production:

```
https://api.barberhub.com/api
```

---

# 2. API Architecture

Style:

* REST API
* JSON Response
* Stateless Authentication
* Mobile Ready

HTTP Methods:

| Method | Purpose       |
| ------ | ------------- |
| GET    | Retrieve data |
| POST   | Create data   |
| PUT    | Update data   |
| DELETE | Delete data   |

---

# 3. Authentication

Authentication:

Laravel Sanctum Token

Header:

```
Authorization: Bearer {access_token}
```

Example:

```http
GET /api/profile

Authorization: Bearer eyJ0eXAiOiJKV1Qi...
```

---

# 4. Standard Response Format

## Success Response

HTTP 200

```json
{
    "success": true,
    "message": "Request successful",
    "data": {}
}
```

---

## Created Response

HTTP 201

```json
{
    "success": true,
    "message": "Created successfully",
    "data": {}
}
```

---

## Validation Error

HTTP 422

```json
{
    "success": false,
    "message": "Validation error",
    "errors": {
        "email": [
            "Email is required"
        ]
    }
}
```

---

## Unauthorized

HTTP 401

```json
{
    "success": false,
    "message": "Unauthenticated"
}
```

---

## Forbidden

HTTP 403

```json
{
    "success": false,
    "message": "Access denied"
}
```

---

## Not Found

HTTP 404

```json
{
    "success": false,
    "message": "Data not found"
}
```

---

# 5. Authentication API

---

# Register Customer

## POST

```
/auth/register
```

Permission:

Public

Request:

```json
{
    "name": "John Doe",
    "email": "john@email.com",
    "phone": "08123456789",
    "password": "password123"
}
```

Response:

```json
{
    "success": true,
    "data": {
        "user": {
            "id": 1,
            "name": "John Doe",
            "role": "customer"
        },
        "token": "xxxxx"
    }
}
```

---

# Login

## POST

```
/auth/login
```

Request:

```json
{
    "email": "john@email.com",
    "password": "password123"
}
```

Response:

```json
{
    "success": true,
    "data": {
        "token": "xxxxx",
        "user": {
            "id":1,
            "role":"customer"
        }
    }
}
```

---

# Logout

## POST

```
/auth/logout
```

Auth:

Required

Response:

```json
{
    "success": true,
    "message": "Logged out"
}
```

---

# Get Current User

## GET

```
/auth/me
```

Response:

```json
{
    "success":true,
    "data":{
        "id":1,
        "name":"John",
        "role":"customer"
    }
}
```

---

# 6. Tenant API

Owner only.

---

# Get Tenant Profile

## GET

```
/tenant
```

Response:

```json
{
    "id":1,
    "name":"Fresh Cut Barbershop",
    "address":"Jakarta",
    "phone":"081234567"
}
```

---

# Update Tenant Profile

## PUT

```
/tenant
```

Request:

```json
{
    "name":"Fresh Cut",
    "address":"Jakarta Selatan",
    "phone":"081234567"
}
```

---

# 7. Barbershop Discovery API

Public.

---

# List Barbershops

## GET

```
/barbershops
```

Query:

```
?page=1
&search=fresh
&location=jakarta
```

Response:

```json
{
    "data":[
        {
            "id":1,
            "name":"Fresh Cut",
            "address":"Jakarta"
        }
    ]
}
```

---

# Detail Barbershop

## GET

```
/barbershops/{id}
```

Response:

```json
{
    "id":1,
    "name":"Fresh Cut",
    "address":"Jakarta",
    "barbers":[]
}
```

---

# 8. Barber API

---

## Customer View Barber List

GET

```
/barbershops/{tenant_id}/barbers
```

Response:

```json
[
 {
    "id":1,
    "name":"Alex",
    "specialization":"Hair Style"
 }
]
```

---

## Owner Create Barber

POST

```
/barbers
```

Request:

```json
{
    "name":"Alex",
    "specialization":"Hair Style",
    "experience":3
}
```

---

## Update Barber

PUT

```
/barbers/{id}
```

---

## Delete Barber

DELETE

```
/barbers/{id}
```

---

# 9. Service API

---

## List Services

GET

```
/services
```

Response:

```json
[
 {
    "id":1,
    "name":"Haircut",
    "duration":30,
    "price":150000
 }
]
```

---

## Create Service

POST

```
/services
```

Request:

```json
{
"name":"Haircut",
"duration":30,
"price":150000
}
```

---

## Update Service

PUT

```
/services/{id}
```

---

## Delete Service

DELETE

```
/services/{id}
```

---

# 10. Schedule API

---

# Get Available Schedule

GET

```
/availability
```

Query:

```
barber_id=1
date=2026-08-01
```

Response:

```json
{
"available_slots":[
"09:00",
"10:00",
"11:00"
]
}
```

---

# Manage Schedule

Owner:

POST

```
/schedules
```

Request:

```json
{
"barber_id":1,
"date":"2026-08-01",
"start_time":"09:00",
"end_time":"17:00"
}
```

---

# 11. Booking API

---

# Create Booking

Customer

POST

```
/bookings
```

Request:

```json
{
"tenant_id":1,
"barber_id":2,
"service_id":3,
"booking_date":"2026-08-01",
"booking_time":"10:00"
}
```

Validation:

* Barber available
* Schedule available
* No conflict

Response:

```json
{
"id":100,
"status":"pending"
}
```

---

# Customer Booking History

GET

```
/bookings/my
```

---

# Owner Booking List

GET

```
/bookings
```

Filter:

```
?status=pending
&date=2026-08-01
```

---

# Update Booking Status

PUT

```
/bookings/{id}/status
```

Request:

```json
{
"status":"confirmed"
}
```

Allowed:

```
pending
confirmed
completed
cancelled
```

---

# Cancel Booking

DELETE

```
/bookings/{id}
```

---

# 12. Favorite API

---

# Add Favorite Barber

POST

```
/favorites/barbers/{id}
```

---

# Remove Favorite Barber

DELETE

```
/favorites/barbers/{id}
```

---

# Favorite List

GET

```
/favorites
```

Response:

```json
{
"barbers":[],
"shops":[]
}
```

---

# 13. Dashboard API

Owner

---

# Dashboard Summary

GET

```
/dashboard
```

Response:

```json
{
"today_booking":10,
"completed":5,
"revenue":750000
}
```

---

# 14. File Upload API

---

# Upload Image

POST

```
/uploads
```

Content-Type:

multipart/form-data

Request:

```
file=image.jpg
type=barber_photo
```

Response:

```json
{
"url":"storage/barbers/image.jpg"
}
```

---

# 15. API Permission Matrix

| Endpoint          | Customer | Barber | Owner | Admin |
| ----------------- | -------- | ------ | ----- | ----- |
| Login             | ✓        | ✓      | ✓     | ✓     |
| View Shop         | ✓        | ✓      | ✓     | ✓     |
| Booking           | ✓        | -      | ✓     | ✓     |
| Manage Barber     | -        | -      | ✓     | ✓     |
| Manage Service    | -        | -      | ✓     | ✓     |
| Dashboard         | -        | -      | ✓     | ✓     |
| Tenant Management | -        | -      | -     | ✓     |

---

# 16. API Development Rules

1. Semua response harus JSON.
2. Semua endpoint private wajib menggunakan authentication.
3. Semua data bisnis wajib menggunakan tenant validation.
4. Semua input wajib memiliki validation.
5. Tidak boleh expose database ID sensitif tanpa kebutuhan.
6. Gunakan pagination untuk list data.
7. Gunakan API versioning jika ada perubahan besar.

---

# 17. Future API Expansion

Akan ditambahkan:

```
/payments
/notifications
/reviews
/subscriptions
/mobile
/reports
```

---

# 18. Definition of API Complete

API dianggap selesai jika:

* Semua endpoint tersedia.
* Authentication berjalan.
* Authorization berjalan.
* Tenant isolation aktif.
* Validation lengkap.
* Error response konsisten.
* Dokumentasi Swagger tersedia.
* Automated test tersedia.
