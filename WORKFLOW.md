# Workflow — Pola Kerja Tim

## Aturan Utama

1. **Setiap perubahan = 1 Issue** — jangan gabung banyak hal dalam 1 commit/PR, sekecil apapun perubahannya (termasuk typo, 1 file, non-fungsional)
2. **Test dulu sebelum push** — jalankan lint, typecheck, test backend
3. **Commit kecil & fokus** — satu fitur/fix per commit, judul jelas
4. **PR wajib untuk semua perubahan** — tidak ada perubahan yang langsung ke `master`

---

## 0. Sebelum Mulai: Buat Issue

Setiap pekerjaan WAJIB dibuatkan Issue GitHub terlebih dahulu. **Tidak ada pengecualian — termasuk typo, perubahan 1 file, atau perubahan non-fungsional.**

```bash
# Buat issue via gh CLI
gh issue create \
  --title "feat: tambah halaman galeri website" \
  --body "**Deskripsi:** Halaman publik untuk lihat semua website user\n**Langkah:**\n1. API endpoint baru\n2. Halaman frontend /explore\n3. Filter industri\n**Acceptance Criteria:**\n- [ ] GET /api/public/websites\n- [ ] Grid responsif\n- [ ] Filter berfungsi"
```

Atau buat via Web GitHub → Issues → New Issue.

### Format Judul Issue
```
feat: <fitur baru>
fix: <perbaikan bug>
chore: <tugas maintenance>
refactor: <refaktor kode>
docs: <dokumentasi>
```

### Format Body Issue
- Deskripsi singkat
- Checklist acceptance criteria
- Link ke referensi (file, gambar, dll)

---

## 0b. Task Sizing (AI Session)

Agar work selesai dalam 1 sesi AI tanpa overflow context window:

### Batas 1 Issue
- **1 issue = 1 task dari TASK_BREAKDOWN.md** (misal: `TASK-101 Register API`)
- Jika task masih terlalu besar, **pecah jadi subtask** dengan checklist di body issue
- Jangan gabung backend + frontend dalam 1 issue — buat issue terpisah

### Estimasi
- Setiap issue harus bisa dikerjakan dalam **1–3 jam** dengan AI
- Jika estimasi > 3 jam → pecah lagi

### Patokan Aman
```
1 task kecil  (1 API + 1 halaman)   → 1 issue
1 task sedang (CRUD + daftar)        → maksimal 2 issue (BE + FE)
1 task besar  (booking engine)        → pecah per endpoint
```

### Checklist Issue yang Siap AI
- [ ] Body issue berisi acceptance criteria konkret
- [ ] Referensi file/link tersedia
- [ ] Dapat dikerjakan < 3 jam AI

---

## 0c. Cara Kerja dengan AI

### Mulai Sesi
Kirim file task langsung — AI akan baca dan kerjakan:
```
@.opencode/tasks/TASK-xxx.md
```
Atau dengan perintah eksplisit:
```
@opencode baca AGENTS.md + .opencode/tasks/TASK-xxx.md lalu kerjakan. WAJIB baca CODING_CONVENTION.md
```

### Aturan 1 Sesi
- **1 sesi AI = 1 task** dari `.opencode/tasks/TASK-xxx.md` — jangan gabung
- Baca `CODING_CONVENTION.md` di awal sesi
- Baca file referensi yang relevan saja (lihat File Index di AGENTS.md)
- `DEFINITION_OF_DONE.md` wajib dicek sebelum bilang selesai

### Session Save Protocol
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

---

## 1. Git Branching & Merge

1. **Ambil issue → buat branch** dari `master`
   ```bash
   git checkout master && git pull --ff-only
   git checkout -b feat/nama-fitur-#<issue-number>
   ```
2. **Kerjakan perubahan** di branch tsb
3. **Test & lint** (lihat bagian Testing)
4. **Push branch**
   ```bash
   git add . && git commit -m "feat: deskripsi singkat (closes #<issue-number>)"
   git push origin feat/nama-fitur-#<issue-number>
   ```
5. **Buat PR** via GitHub (`gh pr create`) atau Web
   ```bash
   gh pr create \
     --title "feat: deskripsi" \
     --body "Closes #<issue-number>" \
     --base master
   ```
6. **Review** — cek diff, pastikan hanya file relevan
7. **Merge PR** ke `master`
   ```bash
   gh pr merge --squash
   ```
8. **Tarik `master`** setelah merge
   ```bash
   git checkout master && git pull --ff-only
   ```
9. **Hapus branch** remote & lokal
   ```bash
   git branch -D feat/nama-fitur-#<issue-number>
   git push origin --delete feat/nama-fitur-#<issue-number>
   ```

> ⚠️ Pakai `-D` (force delete) karena squash merge bikin commit baru — branch lokal tidak terdeteksi sebagai merged.

## 2. Deploy & Restart System

### Frontend (styling/UI)
```bash
docker compose up -d --build frontend
```
- Container `frontend` otomatis recreates + start
- Nginx di dalam container serve file baru

### Backend (API/logic)
```bash
docker compose up -d --build backend
```
- Container `backend` otomatis recreates + start
- PM2 di dalam container handle Node.js process

### Full stack
```bash
docker compose up -d --build
```

### Cek status
```bash
docker compose ps
docker compose logs <service> --tail=50
```

## 3. Testing & Lint (Sebelum Commit)

Sebelum commit/PR, WAJIB menjalankan:

### Backend
```bash
# Unit & integration test
cd backend && npm test

# Lint (jika tersedia)
# cd backend && npx eslint src/
```

### Frontend
```bash
# Build test (vite compile)
cd frontend && npm run build

# E2E test (jika ada)
# cd frontend && npm run test:e2e

# Lint (jika tersedia)
# cd frontend && npx eslint src/
```

### Docker build test
```bash
docker compose up -d --build frontend  # pastikan build lolos
docker compose up -d --build backend   # pastikan backend nyala
```

> **Jika test ada yang merah, FIX DAHULU sebelum commit/PR.**
> Jika tidak ada test untuk kode baru, tambahkan test minimal.

---

## 4. Edit → Build → Deploy Cycle

1. Edit file
2. **Test & lint** lokal
3. **Build & deploy**:
   ```bash
   docker compose up -d --build frontend
   # atau
   docker compose up -d --build backend
   # atau full stack
   docker compose up -d --build
   ```
4. Pastikan build sukses & container sehat (`docker compose ps`)
5. **Commit & push** ke branch
6. **Buat PR** atau merge langsung

> Setiap edit styling harus diikuti rebuild container — Vite build dari dalam Docker, bukan dev server.
