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
| `WORKFLOW.md` | Git branching, deploy, testing, task sizing, cara kerja AI |
| `CODING_CONVENTION.md` | Naming, structure, API response format, testing style |
| `DEFINITION_OF_DONE.md` | 9 kriteria selesai — **wajib dicek sebelum PR** |
| `.opencode/tasks/TASK-xxx.md` | Prompt per task — kirim file ini langsung ke AI untuk dikerjakan |

## Tech Stack
- Backend: Laravel 12, PHP 8.4, Sanctum, MySQL 8
- Frontend: React + Vite + TypeScript, Tailwind, shadcn/ui, TanStack Query, Zustand
- Infra: Docker, Nginx, GitHub Actions

## Flow Otomatis (setiap kali `@AGENTS.md`)

1. **Baca konteks** — file ini (AGENTS.md)
2. **Cek status** — list `.opencode/plans/*.md` untuk lihat task terakhir & statusnya
3. **Tanya user**:
   - Jika ada task `partial`/`blocked` → "Ada task yang belum selesai: [TASK-xxx]. Lanjutkan? (y/n)"
   - Jika semua `done` atau tidak ada plans → "Task mana yang mau dikerjakan?"
4. **Tunggu jawaban** — user jawab (y / nomor task / n)
5. **Baca task file** — `.opencode/tasks/TASK-xxx.md`
6. **Baca CODING_CONVENTION.md**
7. **Baca file referensi** yang disebut di task file
8. **Kerjakan** sesuai isi task
9. **Jika task terlalu besar** (melebihi konteks / > 30 menit):
   - Tanya user: "Task ini cukup besar. Lanjutkan atau simpan dulu? (lanjut/simpan)"
   - Jika simpan → tulis status `partial`, catat progress, selesai
   - User juga bisa bilang "stop" kapan saja → langsung simpan status partial
10. **Simpan status** — ke `.opencode/plans/<task-id>.md` setelah selesai
11. **Tanya** — "Lanjut task lain? (y/n)"
    - y → ulangi dari langkah 3
    - n → "Jangan lupa commit & push ya." (selesai)

## Aturan Kerja
1. 1 sesi AI = 1 task dari `TASK_BREAKDOWN.md` (jangan gabung)
2. Baca `CODING_CONVENTION.md` di awal sesi
3. Baca file referensi yang relevan saja (lihat File Index)
4. Ikuti workflow lengkap di `WORKFLOW.md` → **0c. Cara Kerja dengan AI**
