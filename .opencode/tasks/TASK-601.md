# TASK-601: API Testing (3d)
Feature tests untuk: auth (register, login, logout, forgot), permission (role access), booking (create, double booking, cancel, status flow), tenant isolation (tenant A tidak bisa lihat data B).

Referensi: RULES.md → BR-001 s.d BR-030; API Spec → semua endpoint; DEFINITION_OF_DONE.md
Harus: `php artisan test` hijau. Validasi edge cases.