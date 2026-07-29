# UI/UX Design Specification

## BarberHub SaaS MVP

Version: 1.0

---

# 1. Design Philosophy

## Goals

* Simple
* Clean
* Fast
* Mobile First
* Easy to Use

Design Style

* Modern
* Minimalist
* Spacious
* Rounded Corners
* Soft Shadow

Target users should be able to book an appointment in under **2 minutes**.

---

# 2. Design System

## Color Palette

### Primary

```
#111827
```

Dark Gray

---

### Secondary

```
#2563EB
```

Blue

---

### Success

```
#22C55E
```

Green

---

### Warning

```
#F59E0B
```

Amber

---

### Danger

```
#EF4444
```

Red

---

### Background

```
#F8FAFC
```

Light Gray

---

### Card

```
#FFFFFF
```

White

---

# Typography

Font

* Inter

Heading

* 32px
* Bold

Sub Heading

* 24px

Body

* 16px

Caption

* 14px

Button

* 15px SemiBold

---

# Border Radius

Small

8px

Medium

12px

Large

16px

---

# Shadow

Card

```
0 4px 12px rgba(0,0,0,.08)
```

---

# Button

Primary

Blue Background

White Text

Secondary

White Background

Gray Border

Danger

Red Background

---

# 3. Responsive Breakpoints

Mobile

375px

Tablet

768px

Desktop

1280px

---

# 4. Navigation

## Customer

```
Home

Search

Bookings

Favorites

Profile
```

Bottom Navigation (Mobile)

Top Navigation (Desktop)

---

## Owner Dashboard

Sidebar

```
Dashboard

Bookings

Barbers

Services

Schedule

Customers

Settings
```

---

# 5. Customer Screens

---

## Splash Screen

Logo

Tagline

Loading

↓

Home

---

## Home

```
--------------------------------

Logo

Search Bar

Current Location

Featured Shops

Nearby Shops

Popular Barbers

--------------------------------

Bottom Navigation

```

---

## Search

```
Search Bar

Filters

Shop List

Map Button

```

Filter

* Distance
* Rating (Future)
* Open Now

---

## Shop Detail

```
Cover Image

Logo

Shop Name

Address

Open Hours

Book Now Button

Barbers

Services

Location Map

```

---

## Barber Detail

```
Photo

Name

Experience

Specialization

Working Hours

Available Slots

Book Button

```

---

## Booking

Step 1

Choose Service

↓

Step 2

Choose Barber

↓

Step 3

Choose Date

↓

Step 4

Choose Time

↓

Step 5

Confirmation

---

## Booking Success

Large Check Icon

Booking Number

Date

Time

Barber

Button

View Booking

---

## Booking History

Upcoming

Completed

Cancelled

Card Layout

---

## Favorites

Tabs

Barbers

Shops

---

## Profile

Avatar

Name

Email

Phone

Logout

---

# 6. Owner Dashboard

---

## Login

```
Logo

Email

Password

Login Button

```

---

## Dashboard

Cards

Today's Bookings

Today's Revenue

Future

Monthly Revenue

Recent Bookings

Upcoming Schedule

---

## Barber Management

Table

Photo

Name

Specialization

Status

Edit

Delete

Add Barber

---

## Booking Management

Status Colors

Pending

Yellow

Confirmed

Blue

Completed

Green

Cancelled

Red

---

## Schedule

Calendar View

Working Hours

Unavailable Days

Block Time

---

## Customer List

Name

Phone

Total Booking

Last Visit

---

## Settings

Shop Information

Business Hours

Address

Logo Upload

Password

---

# 7. Components

Primary Button

Secondary Button

Icon Button

Text Field

Password Field

Search Field

Dropdown

Checkbox

Radio

Date Picker

Time Picker

Modal

Drawer

Toast

Alert

Badge

Card

Avatar

Chip

Pagination

Table

Calendar

---

# 8. Empty States

No Booking

Illustration

"Belum ada booking"

Button

Book Now

---

No Favorites

Illustration

Cari barber favorit Anda

---

No Search Result

Illustration

Tidak ditemukan

---

# 9. Loading States

Skeleton Loading

Cards

Tables

Avatar

Buttons

---

# 10. Error States

Network Error

Retry Button

Server Error

Contact Support

404

Go Home

---

# 11. Notifications

Booking Success

Green Toast

Booking Failed

Red Toast

Favorite Saved

Blue Toast

---

# 12. Icons

Lucide Icons

Examples

Calendar

Clock

Location

Heart

Search

User

Scissors

Shop

Settings

---

# 13. Accessibility

Minimum Contrast

WCAG AA

Clickable Area

44px

Keyboard Navigation

Supported

Focus Indicator

Visible

Alt Text

Required

---

# 14. UI Flow

Customer

```
Home

↓

Search Shop

↓

Shop Detail

↓

Choose Barber

↓

Booking

↓

Confirmation

↓

Booking Success
```

Owner

```
Login

↓

Dashboard

↓

Manage Barber

↓

Manage Schedule

↓

Receive Booking

↓

Complete Booking
```

---

# 15. Design Tools

Wireframe

Figma

UI Design

Figma

Prototype

Figma

Design System

Figma Variables

Icons

Lucide

Illustrations

unDraw / Storyset

---

# 16. MVP Design Checklist

Customer

* Login
* Register
* Home
* Search
* Shop Detail
* Barber Detail
* Booking
* Booking History
* Favorites
* Profile

Owner

* Login
* Dashboard
* Manage Barbers
* Manage Bookings
* Schedule
* Customers
* Settings

Admin

* Login
* Tenant List
* Tenant Detail
* User Management

---

# 17. Design Principles

* Gunakan maksimal 3 warna utama agar antarmuka tetap konsisten.
* Setiap aksi penting (Booking, Simpan, Hapus) memiliki konfirmasi atau umpan balik yang jelas.
* Proses booking dirancang tidak lebih dari 5 langkah.
* Prioritaskan tampilan mobile terlebih dahulu, kemudian desktop (mobile-first).
* Komponen UI menggunakan desain yang konsisten dan dapat digunakan kembali (reusable).
* Optimalkan pengalaman pengguna dengan status loading, empty state, dan error state yang informatif.
