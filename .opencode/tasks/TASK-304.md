KERJAKAN: 
# TASK-304: Schedule API (3d)
`POST /schedules` (set jadwal), block date, `GET /availability?barber_id=&date=`.

Referensi: API Spec.md → Schedule API (baris 521-573); RULES.md → BR-013, BR-014
Availability: generate 30/60 menit slot dari start_time-end_time, exclude booking existing.