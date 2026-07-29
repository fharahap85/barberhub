# TASK-403: Booking API (4d) — Critical
`POST /bookings` — validasi: tenant active, barber available, dalam jam kerja, no double booking.
`GET /bookings/my` — history customer. `PATCH /bookings/{id}/status` — cancel (sebelum waktu).

Referensi: API Spec.md → Booking API (baris 577-680); SCHEMA.md → bookings + booking_items; RULES.md → BR-012 s.d BR-017
Hitung total_price dari booking_items. Test semua aturan double booking.