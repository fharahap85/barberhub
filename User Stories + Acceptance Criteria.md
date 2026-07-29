# User Stories & Acceptance Criteria

## BarberHub SaaS MVP

Version: 1.0

---

# Epic 1 — Authentication & User Management

## US-001 Customer Registration

### User Story

**As a customer,**
I want to create an account,
so that I can book a barber online.

### Acceptance Criteria

### Scenario 1: Successful Registration

Given:

* User is on registration page

When:

* User enters valid name, email, phone, and password
* User submits registration form

Then:

* Account is created
* User role is set as customer
* User can login

---

### Scenario 2: Duplicate Email

Given:

* Email already exists

When:

* User registers using the same email

Then:

* System rejects registration
* Error message is displayed

---

## US-002 User Login

### User Story

**As a user,**
I want to login,
so that I can access my account.

### Acceptance Criteria

Given:

* User has registered account

When:

* User enters valid credentials

Then:

* System authenticates user
* Access token is generated
* User is redirected according to role

---

## US-003 Role-Based Access

### User Story

**As an owner,**
I want access control,
so that only authorized users can manage my business.

### Acceptance Criteria

Given:

* User has customer role

When:

* User accesses owner dashboard URL

Then:

* System denies access

---

# Epic 2 — Multi Tenant Management

## US-004 Tenant Isolation

### User Story

**As a barbershop owner,**
I want my data isolated,
so that other shops cannot access my information.

### Acceptance Criteria

Given:

* Tenant A and Tenant B exist

When:

* Owner from Tenant A requests booking data

Then:

* Only Tenant A bookings are returned

---

## US-005 Owner Shop Profile Management

### User Story

**As a barbershop owner,**
I want to manage my shop profile,
so that customers can find my business information.

### Acceptance Criteria

Owner can:

* Update shop name
* Update address
* Update phone
* Upload logo
* Update operating hours

Changes are visible on customer pages.

---

# Epic 3 — Barber Management

## US-006 Add Barber

### User Story

**As a barbershop owner,**
I want to add barbers,
so that customers can choose available staff.

### Acceptance Criteria

Given:

* Owner is logged in

When:

* Owner submits barber information

Then:

* Barber is created
* Barber belongs to owner's tenant

---

## US-007 Edit Barber Profile

### User Story

**As an owner,**
I want to update barber information,
so that customer sees accurate data.

### Acceptance Criteria

Owner can update:

* Name
* Photo
* Bio
* Experience
* Specialization
* Status

---

## US-008 Customer View Barber Catalogue

### User Story

**As a customer,**
I want to browse barbers,
so that I can select my preferred barber.

### Acceptance Criteria

Customer can see:

* Barber photo
* Name
* Specialization
* Experience
* Availability

---

# Epic 4 — Service Management

## US-009 Create Service

### User Story

**As an owner,**
I want to create services,
so that customers know available treatments.

### Acceptance Criteria

Owner can create service with:

* Name
* Duration
* Price
* Status

---

## US-010 Customer View Services

### User Story

**As a customer,**
I want to see services and prices,
so that I can decide before booking.

### Acceptance Criteria

Customer can view:

* Service name
* Duration
* Price

---

# Epic 5 — Schedule Management

## US-011 Manage Barber Schedule

### User Story

**As an owner,**
I want to set barber schedules,
so that customers can only book available times.

### Acceptance Criteria

Owner can:

* Add working hours
* Edit schedule
* Block unavailable dates

---

## US-012 View Available Slots

### User Story

**As a customer,**
I want to see available booking times,
so that I can select a suitable schedule.

### Acceptance Criteria

Given:

* Barber works from 09:00-17:00

When:

* Customer checks availability

Then:

* Available slots are displayed
* Existing bookings are excluded

---

# Epic 6 — Booking System

## US-013 Create Booking

### User Story

**As a customer,**
I want to book a barber online,
so that I can reserve my appointment.

### Acceptance Criteria

Given:

* Barber has available schedule

When:

* Customer selects barber, service, date, and time

Then:

* Booking is created
* Status is pending
* Customer receives confirmation

---

## US-014 Prevent Double Booking

### User Story

**As a system,**
I want to prevent schedule conflicts,
so that one barber cannot have two customers at the same time.

### Acceptance Criteria

Given:

* Barber already has booking at 10:00

When:

* Another customer books 10:00

Then:

* Booking is rejected
* Error message displayed

---

## US-015 Owner View Booking

### User Story

**As an owner,**
I want to view incoming bookings,
so that I can manage appointments.

### Acceptance Criteria

Owner can see:

* Customer name
* Barber
* Service
* Date
* Time
* Status

---

## US-016 Update Booking Status

### User Story

**As an owner,**
I want to update booking status,
so that appointment progress is tracked.

### Acceptance Criteria

Allowed status:

Pending → Confirmed

Confirmed → Completed

Pending/Confirmed → Cancelled

---

## US-017 Customer Booking History

### User Story

**As a customer,**
I want to view my bookings,
so that I can track appointments.

### Acceptance Criteria

Customer can view:

* Upcoming bookings
* Completed bookings
* Cancelled bookings

---

# Epic 7 — Favorites

## US-018 Favorite Barber

### User Story

**As a customer,**
I want to save favorite barbers,
so that I can book them faster next time.

### Acceptance Criteria

Customer can:

* Add favorite barber
* Remove favorite barber
* View favorite list

---

## US-019 Favorite Barbershop

### User Story

**As a customer,**
I want to save favorite shops,
so that I can quickly access them.

### Acceptance Criteria

Customer can:

* Add shop favorite
* Remove shop favorite
* View favorite shops

---

# Epic 8 — Location

## US-020 View Shop Location

### User Story

**As a customer,**
I want to see barbershop location,
so that I can visit the shop easily.

### Acceptance Criteria

Customer can view:

* Address
* Map location
* Navigation link

---

# Epic 9 — Dashboard

## US-021 Owner Dashboard

### User Story

**As a barbershop owner,**
I want to see business summary,
so that I understand daily activity.

### Acceptance Criteria

Dashboard displays:

* Today's bookings
* Pending bookings
* Completed bookings
* Revenue summary (future/payment enabled)

---

# Epic 10 — Payment (Future)

## US-022 Online Payment

### User Story

**As a customer,**
I want to pay online,
so that booking confirmation is easier.

### Acceptance Criteria

Future feature:

* Payment gateway integration
* Payment status tracking
* Transaction history

---

# MVP Release Criteria

The MVP is ready when:

## Customer

✓ Can register/login
✓ Can browse shops
✓ Can view barbers
✓ Can view services
✓ Can create booking
✓ Can view booking history
✓ Can save favorites

---

## Owner

✓ Can login
✓ Can manage shop profile
✓ Can manage barber
✓ Can manage services
✓ Can manage schedules
✓ Can manage bookings

---

## System

✓ Multi tenant isolation works
✓ No double booking
✓ API authentication works
✓ Role authorization works
✓ Responsive web application works

---

# QA Priority

High Priority:

1. Authentication
2. Tenant isolation
3. Booking creation
4. Double booking prevention
5. Role permission

Medium Priority:

6. Favorites
7. Profile management
8. Dashboard

Low Priority:

9. Payment
10. Advanced analytics
