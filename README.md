# ðŸ™ FlacTopus AI

> **Sistem Pendidikan Adaptif Berbasis Skill Tree dengan AI Socratic Tutor**
>
> Platform manajemen kelas & kurikulum interaktif yang memetakan pemahaman murid layaknya *Skill Tree* dalam game RPG. Guru membangun rute belajar secara visual, murid menjelajahi materi seperti quest, dan AI Gemini membimbing lewat dialog sokratik â€” bukan sekadar memberi jawaban.

![License](https://img.shields.io/badge/license-GPLv3-green)
![React](https://img.shields.io/badge/React-19-61DAFB?logo=react)
![Vite](https://img.shields.io/badge/Vite-8-646CFF?logo=vite)
![PHP](https://img.shields.io/badge/PHP-8-777BB4?logo=php)
![MySQL](https://img.shields.io/badge/MySQL-MariaDB-4479A1?logo=mysql)

---

## ðŸ“Œ Daftar Isi

- [Tentang Project](#-tentang-project)
- [Masalah yang Dijawab](#-masalah-yang-dijawab)
- [Fitur Utama](#-fitur-utama)
- [Teknologi yang Digunakan](#-teknologi-yang-digunakan)
- [Arsitektur Sistem](#-arsitektur-sistem)
- [Struktur Project](#-struktur-project)
- [Prasyarat](#-prasyarat)
- [Cara Instalasi](#-cara-instalasi)
- [Cara Penggunaan](#-cara-penggunaan)
- [Sistem Keamanan](#-sistem-keamanan)
- [RBAC (Role-Based Access Control)](#-rbac-role-based-access-control)
- [Database Schema](#-database-schema)
- [API Endpoints](#-api-endpoints)
- [Kontribusi](#-kontribusi)

---

## ðŸŒ¿ Tentang Project

FlacTopus AI adalah **sistem pendidikan adaptif bertenaga AI** yang dikembangkan untuk kompetisi **OSCAR 3.0 x GDGOC STT NF â€” Web Development Competition**.

Project ini menjawab tantangan dalam pendidikan konvensional di mana:
- Guru kesulitan memetakan pemahaman **individual** setiap murid
- Materi belajar bersifat **statis** dan tidak adaptif
- Tidak ada mekanisme evaluasi **berkelanjutan** yang interaktif
- Proses ujian terasa **membosankan** dan tidak memotivasi

FlacTopus mengubah paradigma tersebut dengan menghadirkan **Skill Tree visual** (seperti game RPG), **AI Socratic Tutor** yang membimbing lewat dialog, dan **sistem gamifikasi** yang membuat proses belajar jadi menyenangkan.

---

## ðŸŽ¯ Masalah yang Dijawab

| Masalah | Solusi FlacTopus |
| --- | --- |
| Guru sulit memetakan pemahaman individual murid | **Skill Tree visual** â€” guru melihat progress tiap node materi |
| Belajar tidak adaptif (satu materi untuk semua) | **AI Tutor Gemini** mendeteksi kesalahan & menjelaskan dengan pendekatan berbeda per murid |
| Materi statis, tidak interaktif | **Visual Builder** drag-and-drop untuk membangun skill tree sendiri |
| Tidak ada mekanisme evaluasi berkelanjutan | **Kuis interaktif** (pilihan ganda + isi rumpang) terintegrasi di setiap node |
| Ujian terasa membosankan | **Boss Fight Mode** bergaya RPG dengan HP, efek visual, dan transisi sinematik |

---

## âœ¨ Fitur Utama

### ðŸŒ³ Skill Tree Visual (ReactFlow)
Guru membangun kurikulum sebagai graf nodes & edges dengan **drag-and-drop**. Murid melihat rute belajar sebagai peta interaktif â€” node terkunci â†’ in-progress â†’ completed. Progress disimpan sebagai file JSON per ruangan.

### ðŸ¤– Socratic AI Tutor (Google Gemini)
Saat murid salah menjawab, AI **tidak langsung memberi jawaban**. Sebaliknya, AI bertanya balik secara dialogis: *"Mengapa kamu memilih X? Apa yang kamu pahami dari konsep ini?"* â€” menuntun murid menemukan jawaban sendiri melalui pendekatan Socrates.

### ðŸŽ® Gamifikasi & Boss Fight Mode
Kuis memiliki mode **Boss Fight** bergaya RPG lengkap dengan:
- Health Point (HP) Boss dan Murid
- Efek visual saat jawaban benar/salah
- Transisi sinematik dan musik latar Ã©pik
- Suara retro 8-bit (Web Audio API) untuk respons real-time

### ðŸ« Sistem Ruangan Kelas
- Guru buat ruangan â†’ dapat **kode unik 6 karakter**
- Murid gabung pakai kode â†’ otomatis masuk ke skill tree guru
- **Soft Delete** â€” guru hapus ruangan â†’ data tersimpan 30 hari, admin bisa pulihkan
- **Heartbeat system** â€” browser mengirim sinyal tiap 3 menit
- **Ketua Kelas** â€” guru bisa mengangkat murid sebagai sub-admin

### ðŸ›¡ï¸ Panel Admin (3 Tab)
- **ðŸ‘¥ Kelola User** â€” filter/search, approve/reject registrasi, ubah role, reset password
- **ðŸ—‘ï¸ Ruangan Terhapus** â€” lihat ruangan soft-deleted, **pulihkan** atau **hapus permanen** (retensi 30 hari)
- **ðŸ“Š Activity Log** â€” audit trail semua aksi + auto-refresh 15 detik

### ðŸ“Š Class Analytics & Anti-Cheat
- Dashboard analitik: rata-rata nilai, partisipasi, materi tersulit
- **Deteksi Nyontek** â€” otomatis merekam jika murid berpindah tab saat kuis
- Data non-akademik (Ice Breaking) dikecualikan dari grafik

---

## ðŸ› ï¸ Teknologi yang Digunakan

| Layer | Teknologi | Keterangan |
| --- | --- | --- |
| **Frontend** | React 19 + Vite 8 | SPA dengan React Router v7 |
| **Visualisasi Skill Tree** | ReactFlow (@xyflow/react) | Drag-and-drop nodes & edges |
| **Animasi** | Framer Motion + Canvas Confetti | Transisi UI & efek selebrasi |
| **AI Tutor** | Google Gemini API | Socratic questioning approach |
| **Backend** | PHP 8 Murni (tanpa framework) | API JSON, session-based auth |
| **Database** | MySQL (MariaDB via XAMPP) | 8 tabel + file JSON silabus |
| **Keamanan** | CSRF, Session Hijack Detection, Dual Rate Limiter, Activity Log, Soft Delete | Berdasarkan referensi MEeL |
| **Build** | Vite build â†’ bash build.sh â†’ XAMPP | Production-ready |
| **Linting** | OxLint | Cepat, ringan |
| **CI/CD** | GitHub Actions | Secret scanning |
| **Migrasi** | db/migration.php (CLI-only) | Version-based, idempotent (v1-v6) |

---

## ðŸ—ï¸ Arsitektur Sistem

```
â”Œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”
â”‚                    FRONTEND (React SPA)                   â”‚
â”‚  React + Vite + React Router + ReactFlow                 â”‚
â”‚  Pages: Landing, Login, Register, ClassDashboard,        â”‚
â”‚         TeacherDashboard, StudentDashboard, Quiz,         â”‚
â”‚         RoomDetail, AdminPanel (3 tabs), ErrorPage        â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚                   BACKEND (PHP Murni)                     â”‚
â”‚  API JSON: auth/*.php, ruangan.php, admin.php, quiz.php  â”‚
â”‚  Logic: LoginRegisterLogic, RuanganLogic,                 â”‚
â”‚         RateLimiter, ActivityLogger, GarbageCollector     â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚                     DATABASE (MySQL)                      â”‚
â”‚  Tables: users, ruangan, class_members, syllabus,         â”‚
â”‚          quiz_attempts, login_attempts, activity_log,     â”‚
â”‚          schema_version                                   â”‚
â”‚  + File JSON per ruangan di storage/ruangan/<id>.json     â”‚
â”œâ”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”¤
â”‚                    AI (Google Gemini)                      â”‚
â”‚  Socratic AI Tutor â€” menuntun murid lewat dialog         â”‚
â”‚  via backend proxy (gemini.php) â€” API key server-side     â”‚
â””â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”€â”˜
```

**Alur Aplikasi:**
1. **React (JSX)** menggambar semua halaman UI
2. **PHP** berperan sebagai backend murni â€” mengembalikan JSON
3. **MySQL** menyimpan data user, ruangan, & keanggotaan
4. **File JSON** menyimpan struktur skill tree per ruangan (DB hanya pointer)
5. **Google Gemini** menyediakan AI Socratic Tutor (diproxy lewat backend)

---

## ðŸ“ Struktur Project

```
FlacTopus/
â”œâ”€â”€ frontend/                      # React App (Vite)
â”‚   â”œâ”€â”€ src/
â”‚   â”‚   â”œâ”€â”€ pages/                 # Landing, Login, Register, ClassDashboard,
â”‚   â”‚   â”‚                          # TeacherDashboard, StudentDashboard, Quiz,
â”‚   â”‚   â”‚                          # RoomDetail, AdminPanel, ErrorPage
â”‚   â”‚   â”œâ”€â”€ components/            # ProtectedRoute, quiz/*, analytics/*
â”‚   â”‚   â”œâ”€â”€ hooks/                 # useAuth (session PHP), useRoomHeartbeat
â”‚   â”‚   â”œâ”€â”€ utils/                 # api.js, roles.js, aiService.js, sounds.js
â”‚   â”‚   â”œâ”€â”€ data/                  # mockData.js, templateLibrary.js
â”‚   â”‚   â”œâ”€â”€ App.jsx                # Route definitions + RBAC matrix
â”‚   â”‚   â””â”€â”€ index.css              # CSS variables, dark theme, responsive
â”‚   â”œâ”€â”€ vite.config.js             # base: '/' (production)
â”‚   â””â”€â”€ (no .env â€” API key server-side di auth/config.php)
â”œâ”€â”€ auth/                          # PHP auth backend
â”‚   â”œâ”€â”€ config.php                 # DB, session config, security headers
â”‚   â”œâ”€â”€ auth.php                   # require_auth, session hijacking, CSRF
â”‚   â”œâ”€â”€ login.php                  # POST API login + dual rate limiter
â”‚   â”œâ”€â”€ register.php               # POST API register (status=pending)
â”‚   â”œâ”€â”€ session.php                # GET session check + CSRF token
â”‚   â””â”€â”€ logout.php                 # POST logout + activity logging
â”œâ”€â”€ backend/controller/
â”‚   â”œâ”€â”€ api/
â”‚   â”‚   â”œâ”€â”€ ruangan.php            # CRUD ruangan + trash management
â”‚   â”‚   â”œâ”€â”€ admin.php              # Admin: user mgmt, restore/force_delete
â”‚   â”‚   â”œâ”€â”€ quiz.php               # API kuis + analytics + anti-cheat
â”‚   â”‚   â””â”€â”€ gemini.php             # Backend proxy Gemini API
â”‚   â””â”€â”€ logic/
â”‚       â”œâ”€â”€ LoginRegisterLogic.php  # Auth business logic
â”‚       â”œâ”€â”€ RuanganLogic.php        # Ruangan + soft delete + trash
â”‚       â”œâ”€â”€ RateLimiter.php         # Dual rate limiting (IP + session)
â”‚       â”œâ”€â”€ ActivityLogger.php      # Audit trail
â”‚       â””â”€â”€ GarbageCollector.php    # Auto-clean: activity_log, orphaned files, trashed rooms
â”œâ”€â”€ db/
â”‚   â”œâ”€â”€ migration.php              # CLI-only version-based migration (v1-v6)
â”‚   â””â”€â”€ README.md                  # Arsitektur data documentation
â”œâ”€â”€ storage/
â”‚   â”œâ”€â”€ ruangan/                   # File JSON silabus per ruangan
â”‚   â””â”€â”€ chat/                      # File JSON riwayat chat AI per murid
â”œâ”€â”€ scripts/
â”‚   â”œâ”€â”€ gc.php                     # CLI manual trigger untuk Garbage Collector
â”‚   â””â”€â”€ scan-secrets.sh            # Security: pre-commit secret scanning
â”œâ”€â”€ hooks/pre-commit               # Git pre-commit hook
â”œâ”€â”€ .github/workflows/             # CI: scan-secrets.yml
â”œâ”€â”€ build.sh                       # Build frontend â†’ copy to root XAMPP
â”œâ”€â”€ info.md                        # Changelog project
â””â”€â”€ README.md                      # Dokumentasi project ini
```

---

## ðŸ“‹ Prasyarat

- **XAMPP/LAMPP** (Apache + MySQL) â€” [download](https://www.apachefriends.org/)
- **Node.js v22+** â€” [download](https://nodejs.org/) (via nvm direkomendasikan)
- **Git** â€” [download](https://git-scm.com/)

---

## âš™ï¸ Cara Instalasi

### 1. Klon Repositori

```bash
git clone https://github.com/username/FlacTopus.git
cd FlacTopus
```

### 2. Pindahkan ke XAMPP htdocs

```bash
# Linux/Mac
cp -r . /opt/lampp/htdocs/FlacTopus
```

### 3. Setup Database

```bash
# Jalankan migrasi (CLI-only, otomatis buat tabel + data demo)
php db/migration.php
```

### 4. Setup API Key AI (Opsional)

```bash
# API key disimpan di auth/config.php (server-side, tidak di frontend)
# Edit auth/config.php â†’ set GEMINI_API_KEY
```

> âš ï¸ Tanpa API Key, aplikasi tetap berjalan dalam *mode simulasi*.

### 5. Build Frontend

```bash
cd frontend
npm install
npm run build
```

Atau gunakan script build:

```bash
bash build.sh
```

---

## ðŸš€ Cara Penggunaan

### Production Mode

```bash
# Pastikan Apache & MySQL sudah menyala
# Buka browser:
http://localhost/FlacTopus/
```

### Development Mode (Hot Reload)

```bash
cd frontend
npm install
npm run dev
# Buka http://localhost:5173/FlacTopus/
```

### Akun Demo

| Akun | Email | Password | Role | Status |
| --- | --- | --- | --- | --- |
| Admin | `admin@example.com` | `password123` | admin | active |
| Guru | `guru@example.com` | `password123` | teacher | active |
| Murid | `murid@example.com` | `password123` | student | active |

---

## ðŸ” Sistem Keamanan

Keamanan dibangun berdasarkan referensi project **MEeL** dan diimplementasikan secara menyeluruh:

### 1. Session Hijacking Detection
- Kolom `last_session_id` di tabel `users`
- Setiap request dicek â†’ jika session ID berbeda â†’ session dihancurkan otomatis

### 2. Dual Rate Limiting (IP + Session)

| Context | Maks Percobaan | Jendela Waktu | Keterangan |
| --- | --- | --- | --- |
| Login | 5 per IP | 15 menit | Anti brute force password |
| Register | 3 per IP | 1 jam | Anti spam akun |

- **Session-based:** `$_SESSION['login_fail_count']` â€” lock 5 menit setelah 5 gagal
- **IP-based:** Tabel `login_attempts` â€” track semua percobaan
- **Loopback exemption:** Localhost bebas rate limit untuk development

### 3. Activity Logger (Audit Trail)
Semua aktivitas dicatat ke tabel `activity_log`: login, logout, register, approve, reject, change_role, delete_user, reset_password, rate_limited.

### 4. Secure Cookie
- `httponly = true` â†’ JavaScript tidak bisa baca
- `samesite = 'Lax'` â†’ cookie tidak dikirim saat cross-site
- `secure = dynamic` â†’ otomatis `true` jika HTTPS

### 5. Security Headers

| Header | Fungsi |
| --- | --- |
| `X-Content-Type-Options: nosniff` | Cegah MIME sniffing |
| `X-Frame-Options: DENY` | Cegah clickjacking |
| `Referrer-Policy: strict-origin-when-cross-origin` | Kontrol referrer |
| `Permissions-Policy` | Blokir kamera, mikrofon, lokasi |
| `Cross-Origin-Opener-Policy: same-origin` | Isolasi origin |

### 6. Soft Delete & Recovery
- Guru **soft delete** ruangan â†’ data tersimpan 30 hari
- Admin bisa **pulihkan** atau **hapus permanen** dari tab "Ruangan Terhapus"
- **GarbageCollector** otomatis hard delete setelah 30 hari

### 7. Input Validation & Protection
- Password: Bcrypt (`password_hash()` + `password_verify()`)
- CSRF: Token wajib untuk semua POST request (`X-CSRF-Token` header)
- SQL Injection: Prepared statements (PDO, `EMULATE_PREPARES => false`)
- Register: Role di-override server-side (selalu `student`)

---

## ðŸ‘¥ RBAC (Role-Based Access Control)

| Role | Deskripsi | Akses |
| --- | --- | --- |
| `guest` | Belum login | Landing page, login, register |
| `student` | Murid terdaftar (aktif) | Kelas yang diikuti, belajar, kuis |
| `teacher` | Guru terdaftar (aktif) | Semua akses student + buat/hapus ruangan, edit silabus |
| `admin` | Administrator | Kelola user, pulihkan ruangan terhapus, activity log |

### RBAC Detail per Aksi

| Aksi | Guest | Student | Teacher (pembuat) | Ketua Kelas | Admin |
| --- | --- | --- | --- | --- | --- |
| Lihat ruangan | âŒ | Ruangan diikuti | Ruangan sendiri | â€” | âŒ (privacy) |
| Buat ruangan | âŒ | âŒ | âœ… | âŒ | âŒ |
| Hapus ruangan | âŒ | âŒ | âœ… (soft delete) | âŒ | âŒ |
| Rename ruangan | âŒ | âŒ | âœ… (sendiri) | âŒ | âŒ |
| Edit silabus | âŒ | âŒ | âœ… (sendiri) | âŒ | âŒ |
| Lihat members | âŒ | âŒ | âœ… (sendiri) | âœ… (sendiri) | âŒ |
| Kick murid | âŒ | âŒ | âœ… (sendiri) | âŒ | âŒ |
| Analytics | âŒ | âŒ | âœ… (sendiri) | âœ… (sendiri) | âŒ |
| **Kelola User** | âŒ | âŒ | âŒ | âŒ | âœ… |
| **Lihat Ruangan Terhapus** | âŒ | âŒ | âŒ | âŒ | âœ… |
| **Restore Ruangan** | âŒ | âŒ | âŒ | âŒ | âœ… |
| **Force Delete Ruangan** | âŒ | âŒ | âŒ | âŒ | âœ… |
| **Activity Log** | âŒ | âŒ | âŒ | âŒ | âœ… |

### Flow Autentikasi

1. User buka app â†’ status `guest`
2. Register â†’ **selalu role `student`** â†’ status `pending`
3. Admin approve â†’ status `active`
4. Login â†’ **admin redirect ke `/admin`**, guru/murid redirect ke `/classes`
5. Session PHP dibuat (cookie `FlacTopus`, httponly, 2 jam lifetime)
6. Session hijacking check â†’ setiap request cek `session_id()` di DB
7. Idle 30 menit â†’ auto-logout
8. Double session prevention â†’ user sudah login â†’ redirect

---

## ðŸ—ƒï¸ Database Schema

### Tabel `users`
| Kolom | Tipe | Keterangan |
| --- | --- | --- |
| `id` | INT UNSIGNED PK | Auto increment |
| `name` | VARCHAR(100) | Nama lengkap |
| `email` | VARCHAR(150) UNIQUE | Dipakai login |
| `password_hash` | VARCHAR(255) | Bcrypt |
| `role` | ENUM('student','teacher','admin') | Default: 'student' |
| `status` | ENUM('pending','active','rejected') | Default: 'pending' |
| `last_session_id` | VARCHAR(128) | Session hijacking detection |
| `created_at` | TIMESTAMP | Auto |

### Tabel `ruangan`
| Kolom | Tipe | Keterangan |
| --- | --- | --- |
| `id` | INT UNSIGNED PK | Auto increment |
| `nama` | VARCHAR(150) | Nama ruangan/mapel |
| `kode_ruangan` | CHAR(6) UNIQUE | Kode join murid |
| `user_id` | INT UNSIGNED FK | Guru pembuat (CASCADE) |
| `theme_color` | VARCHAR(50) | Tema warna UI (default: #0f172a) |
| `created_at` | TIMESTAMP | Auto |
| `last_active_at` | TIMESTAMP | Reset timer 2 jam |
| `deleted_at` | TIMESTAMP NULL | Soft delete timestamp |
| `deleted_by` | INT UNSIGNED NULL | ID user yang menghapus |

### Tabel `class_members`
| Kolom | Tipe | Keterangan |
| --- | --- | --- |
| `id` | INT UNSIGNED PK | Auto increment |
| `ruangan_id` | INT UNSIGNED FK | CASCADE |
| `user_id` | INT UNSIGNED FK | CASCADE |
| `joined_at` | TIMESTAMP | Auto |
| `last_seen_at` | TIMESTAMP NULL | Heartbeat terakhir |
| `role` | ENUM('member','admin') | Admin = Ketua Kelas |
| `is_marked` | TINYINT(1) | Tanda khusus murid |
| `pinned_at` | TIMESTAMP NULL | Waktu dipin |

### Tabel `quiz_attempts`
| Kolom | Tipe | Keterangan |
| --- | --- | --- |
| `id` | INT UNSIGNED PK | Auto increment |
| `ruangan_id` | INT UNSIGNED FK | Kelas tempat kuis |
| `user_id` | INT UNSIGNED FK | Murid yang mengerjakan |
| `node_id` | VARCHAR(100) | ID node Skill Tree |
| `node_label` | VARCHAR(255) | Judul node |
| `score` | INT | Nilai 0-100 |
| `total_questions` | INT | Total soal |
| `correct_answers` | INT | Jawaban benar |
| `wrong_answers` | JSON NULL | Pertanyaan salah |
| `tab_switches` | INT | Deteksi pindah tab (anti-cheat) |
| `created_at` | TIMESTAMP | Auto |

### Tabel `syllabus` | `login_attempts` | `activity_log` | `schema_version`
Tabel pendukung untuk pointer file JSON, rate limiting, audit trail, dan migrasi.

> **Catatan desain:** Isi skill tree (nodes/edges) disimpan sebagai **file JSON per ruangan** di `storage/ruangan/`, bukan di kolom DB. DB hanya menyimpan pointer kecil.

---

## ðŸ”§ API Endpoints

### Auth (`auth/*.php`)
| Endpoint | Method | Deskripsi |
| --- | --- | --- |
| `auth/session.php` | GET | Cek status login + ambil CSRF token |
| `auth/login.php` | POST | Login + dual rate limiter |
| `auth/register.php` | POST | Register â†’ status=pending |
| `auth/logout.php` | POST | Logout + activity logging |

### Ruangan (`backend/controller/api/ruangan.php`)
| Aksi | Method | Role | Deskripsi |
| --- | --- | --- | --- |
| `list` | GET | teacher/student | Daftar ruangan aktif |
| `trash` | GET | admin | Daftar ruangan terhapus + sisa hari |
| `create` | POST | teacher | Buat ruangan baru |
| `join` | POST | student | Gabung via kode 6 karakter |
| `delete` | POST | pemilik | **Soft delete** (30 hari retention) |
| `restore` | POST | admin | Pulihkan dari trash |
| `force_delete` | POST | admin | Hapus permanen dari trash |
| `rename` | POST | pemilik | Ubah nama ruangan |
| `kick` | POST | pemilik | Keluarkan murid |
| `set_admin` | POST | pemilik | Atur ketua kelas |
| `toggle_mark` | POST | pemilik | Tandai murid |
| `toggle_pin` | POST | pemilik | Pin murid |
| `touch` | POST | anggota | Keep-alive |
| `syllabus` | GET/POST | anggota/pemilik | Baca/simpan skill tree |
| `heartbeat` | POST | anggota | "Ada orang disini?" |

### Admin (`backend/controller/api/admin.php`)
| Aksi | Method | Role | Deskripsi |
| --- | --- | --- | --- |
| `list` | GET | admin | Daftar semua user + filter |
| `stats` | GET | admin | Statistik user per role & status |
| `approve` | POST | admin | Setujui user pending |
| `reject` | POST | admin | Tolak user pending |
| `change_role` | POST | admin | Ubah role user |
| `delete` | POST | admin | Hapus user permanen |
| `reset_password` | POST | admin | Reset password user |
| `kick` | POST | admin | Keluarkan anggota dari ruangan |
| `restore` | POST | admin | Pulihkan ruangan dari trash |
| `force_delete` | POST | admin | Hapus permanen dari trash |
| `activity_logs` | GET | admin | Audit trail + filter + pagination |
| `activity_stats` | GET | admin | Statistik activity log |

### Quiz (`backend/controller/api/quiz.php`)
| Aksi | Method | Role | Deskripsi |
| --- | --- | --- | --- |
| `analytics` | GET | guru/ketua | Rangkuman kelas |
| `analytics_trend` | GET | guru/ketua | Grafik tren nilai |
| `analytics_participation` | GET | guru/ketua | Partisipasi murid |
| `analytics_leaderboard` | GET | guru/ketua | Peringkat murid |
| `analytics_mistakes` | GET | guru/ketua | Soal sering salah |
| `analytics_cheating` | GET | guru/ketua | Deteksi pindah tab |
| `student_progress` | GET | murid | Progress kuis murid |
| `chat_history` | GET | guru | Riwayat chat AI murid |
| `submit` | POST | murid | Submit jawaban kuis |
| `save_chat` | POST | murid/guru | Simpan riwayat chat AI |

---

## ðŸ“± Responsive Design

| Breakpoint | Perubahan |
| --- | --- |
| â‰¤ 480px | Glass panel padding kompak, auth form 1 kolom |
| â‰¤ 640px | Header stack vertikal, stats grid 2 kolom |
| â‰¤ 768px | Side-panel full-width, quiz 1 kolom, admin tabs scroll |
| Touch devices | Semua tombol/input min-height 44px |

---

## ðŸ”„ Database Migration

```bash
# Jalankan migrasi (CLI-only)
php db/migration.php

# Output:
# âœ… Database project_lomba (MySQL)
# ðŸ“‹ v1: Schema awal (users, ruangan, class_members, syllabus)
# ðŸ“‹ v2: login_attempts (rate limiting)
# ðŸ“‹ v3: activity_log (audit trail)
# ðŸ“‹ v4: theme_color, role, is_marked, pinned_at
# ðŸ“‹ v5: quiz_attempts (rekam jawaban murid)
# ðŸ“‹ v6: deleted_at, deleted_by (soft delete)
# âœ… Database sudah versi terbaru (v6).
```

| Fitur | Keterangan |
| --- | --- |
| CLI Only | `PHP_SAPI !== 'cli'` â†’ 403 Forbidden di browser |
| Version-based | Tabel `schema_version` lacak versi |
| Idempotent | Bisa dijalankan berulang kali tanpa error |
| Safe | Tidak DROP/DELETE data yang ada |

---

## ðŸ¤ Kontribusi

1. **Fork** repositori ini
2. Buat branch fitur baru: `git checkout -b fitur-baru`
3. Commit perubahan: `git commit -m 'Menambahkan fitur baru'`
4. Push ke branch: `git push origin fitur-baru`
5. Buat **Pull Request**

> âš ï¸ Pastikan `npm run lint` (oxlint) tidak mengembalikan error sebelum submit PR.

---

## ðŸ“ Catatan Teknis

- **Build workflow:** `bash build.sh` â†’ Vite build â†’ copy `index.html` + `node-assets/` ke root â†’ XAMPP serve
- **Root `index.html` & `node-assets/`** adalah artefak build (di-gitignore) â€” sumber selalu di `frontend/`
- **Storage silabus:** File JSON di `storage/ruangan/<id>.json` (di-deny .htaccess)
- **AI Key:** `GEMINI_API_KEY` di `auth/config.php` (server-side, tidak ter-expose ke frontend)
- **Password:** Semua di-hash bcrypt; demo password = `password123`
- **Timezone:** MySQL timezone = WIB (+07:00)
- **Register:** Selalu role `student` â€” guru/admin ditambahkan via Panel Admin
- **Soft Delete:** Ruangan yang dihapus guru tersimpan 30 hari sebelum dihapus permanen oleh GarbageCollector

---

*Project ini dikembangkan untuk kompetisi **OSCAR 3.0 Web Development Competition** oleh tim yang beranggotakan siswa SMA/SMK se-JABODETABEK.*

