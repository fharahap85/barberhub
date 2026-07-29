KERJAKAN: 
# TASK-101: Customer Registration API (1d)
`POST /auth/register` — validasi, hash password, simpan user role=customer.

Referensi: RULES.md → BR-002, BR-004, BR-024; API Spec.md → baris 158-198; SCHEMA.md → users table
Harus: response format `{success, data: {user, token}}`; test happy path + duplicate email.