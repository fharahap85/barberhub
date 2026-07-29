KERJAKAN: 
# TASK-105: Tenant Middleware (2d)
`TenantScope` global scope untuk model bisnis. `SetTenant` middleware dari authed user.

Referensi: RULES.md → BR-001 tenant isolation; SCHEMA.md → Data Isolation (baris 372-384); ARCHITECTURE.md → Multi-Tenant
Setiap query bisnis Wajib filter tenant_id.