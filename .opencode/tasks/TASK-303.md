KERJAKAN: 
# TASK-303: Schedule DB & Logic (1d)
`Schedules` table migration. Logic availability: generate slot berdasarkan work_date, start_time, end_time, is_available.

Referensi: SCHEMA.md → schedules table (baris 209-218); RULES.md → BR-009, BR-012, BR-013
Availability = jadwal aktif - existing booking overlap.