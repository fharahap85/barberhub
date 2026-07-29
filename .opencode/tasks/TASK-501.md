KERJAKAN: 
# TASK-501: Owner Booking Dashboard API (2d)
`GET /bookings?status=&date=` — list booking milik tenant.
`PATCH /bookings/{id}/status` — confirm, complete, cancel.
`GET /dashboard` — summary: today_booking, pending, completed, revenue.

Referensi: API Spec.md → baris 629-679, Dashboard API (baris 727-748); RULES.md → BR-015, BR-016
Owner only. Validasi status flow (pending→confirmed→completed).