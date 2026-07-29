# BarberHub — AI Project Context

## Project
BarberHub: SaaS multi-tenant booking barbershop. Laravel 12 + React + TypeScript.

## File Index (baca sesuai task, jangan semua)

| File | Isi |
|------|-----|
| `PRD.md` | Kebutuhan produk, user roles, fitur MVP vs future |
| `RULES.md` | Business rules BR-001 s.d BR-030 — **wajib dipatuhi** |
| `SCHEMA.md` | DB schema, tables, foreign keys, indexes |
| `ARCHITECTURE.md` | System design, backend layer (Controller→Service→Repository), deployment |
| `DESIGN.md` | UI/UX: warna, typografi, screens, components |
| `API Specification.md` | Semua endpoint: path, method, request/response, permission matrix |
| `USER STORIES + ACCEPTANCE CRITERIA.md` | User stories dengan acceptance criteria per fitur |
| `TASK_BREAKDOWN.md` | Sprint plan, task ID, estimates, dependencies |
| `WORKFLOW.md` | Git branching, deploy, testing, task sizing |
| `CODING_CONVENTION.md` | Naming, structure, API response format, testing style |
| `DEFINITION_OF_DONE.md` | 9 kriteria selesai — **wajib dicek sebelum PR** |

## Tech Stack
- Backend: Laravel 12, PHP 8.4, Sanctum, MySQL 8
- Frontend: React + Vite + TypeScript, Tailwind, shadcn/ui, TanStack Query, Zustand
- Infra: Docker, Nginx, GitHub Actions

## Aturan Kerja
1. 1 sesi AI = 1 task dari `TASK_BREAKDOWN.md` (jangan gabung)
2. Baca `CODING_CONVENTION.md` di awal sesi
3. Baca file referensi yang relevan saja (lihat File Index)
4. Setelah selesai, simpan status ke `.opencode/plans/<task-id>.md`
5. `Definition of Done` wajib dicek sebelum bilang selesai

## Template Perintah
```
@opencode baca AGENTS.md + .opencode/tasks/TASK-xxx.md lalu kerjakan. WAJIB baca CODING_CONVENTION.md
```

## Session Save Protocol
Setiap selesai task, tulis file `.opencode/plans/<task-id>.md`:

```md
# TASK-xxx — [nama task]
STATUS: done | partial | blocked
DURASI: [jam]
YANG DIBUAT:
- [file1] → [apa yg dibuat]
- [file2] → [apa yg dibuat]
CATATAN: [issue/blocker untuk sesi berikutnya]
```

### Cross-Device
- `.opencode/plans/` di-track git — commit & push setelah sesi selesai
- Di device lain: `git pull` — file plans terbawa semua
- Mulai sesi baru: lihat file `.opencode/plans/*.md` untuk status terakhir
- **Jangan commit ulang file plans yang tidak berubah**
