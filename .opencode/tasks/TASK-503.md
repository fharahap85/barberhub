# TASK-503: Favorite API (2d)
`POST /favorites` (barber_id atau tenant_id), `DELETE /favorites/{id}`, `GET /favorites`.

Referensi: API Spec.md → Favorite API (baris 683-722); SCHEMA.md → favorites table; RULES.md → BR-018, BR-019
Customer only. No duplicate (unique constraint customer_id + target).