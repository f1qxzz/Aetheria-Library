# 📚 Aetheria Library

## 📖 Project Overview

**Aetheria Library** adalah aplikasi web PHP Native untuk mengelola operasional perpustakaan: katalogisasi buku, manajemen anggota, peminjaman, pengembalian, dan denda otomatis.

### 🔍 Masalah yang Diselesaikan
- ❌ Pengelolaan peminjaman manual → ✅ Sistem digital terintegrasi
- ❌ Tracking ketersediaan buku tidak akurat → ✅ Real-time inventory tracking
- ❌ Denda keterlambatan manual → ✅ Auto-calculation denda
- ❌ Riwayat tidak terstruktur → ✅ Database terpusat dengan audit trail
- ❌ Approval peminjaman lambat → ✅ Approval workflow bertingkat

### 💼 Use Cases Utama

| Role | Use Case |
|------|----------|
| **Admin** | Approve peminjaman, manage pengguna, lihat laporan |
| **Petugas** | Kelola buku & kategori, validasi peminjaman/return, track denda |
| **Anggota** | Cari & ajukan peminjaman, lihat riwayat, bayar denda |

---

## 🎯 Features

**Admin:**
- Dashboard dengan stats (total buku, anggota, peminjaman)
- CRUD pengguna (admin, petugas)
- Approve/reject peminjaman
- Lihat laporan & denda

**Petugas:**
- CRUD buku & kategori
- Validate peminjaman & pengembalian  
- Kelola denda anggota
- Lihat laporan

**Anggota:**
- Browse & cari katalog buku
- Ajukan peminjaman (status: Pending → Approved → Peminjaman)
- Request return buku
- Lihat riwayat & denda
- Tulis ulasan buku

---

## 🛠 Tech Stack

| Layer | Teknologi | Fungsi |
|-------|-----------|--------|
| **Backend** | PHP 7.4+ | Server-side logic |
| **Database** | MySQL 5.7+ | Data storage |
| **Frontend** | HTML5, CSS3, JS ES6+ | Client-side UI |
| **Icons** | Font Awesome 6.x | UI icons |
| **Server** | XAMPP/Apache 2.4+ | Local & production |
| **Tools** | Git, VS Code | Development |

---

## 📁 Project Structure

```
Aetheria-Library/
├── 📄 index.php                 ← Landing page
├── 📄 login.php                 ← Login page
├── 📄 register.php              ← Register anggota
├── 📄 logout.php                ← Logout handler
├── 📄 api_search.php            ← AJAX search API
├── 📄 setup.php                 ← DB initialization
│
├── 📂 config/
│   └── 📄 database.php          ← DB connection & helpers
│
├── 📂 includes/
│   ├── 📄 session.php           ← Auth & session management
│   └── 📄 upload_helper.php     ← File upload utilities
│
├── 📂 admin/                    ← Admin Dashboard
│   ├── 📄 dashboard.php         ├─ Stats & quick actions
│   ├── 📄 pengguna.php          ├─ CRUD users
│   ├── 📄 transaksi.php         ├─ Approve/reject loans
│   ├── 📄 denda.php             ├─ Fine management
│   ├── 📄 laporan.php           └─ Reports
│   └── 📂 includes/
│       ├── 📄 header.php
│       └── 📄 nav.php
│
├── 📂 petugas/                  ← Petugas Dashboard
│   ├── 📄 dashboard.php         ├─ Dashboard
│   ├── 📄 buku.php              ├─ CRUD books
│   ├── 📄 kategori.php          ├─ Categories
│   ├── 📄 anggota.php           ├─ Member management
│   ├── 📄 transaksi.php         ├─ Validate loan/return
│   ├── 📄 denda.php             └─ Fine tracking
│   └── 📂 includes/
│       ├── 📄 header.php
│       └── 📄 nav.php
│
├── 📂 anggota/                  ← Member Dashboard
│   ├── 📄 dashboard.php         ├─ Dashboard
│   ├── 📄 katalog.php           ├─ Book catalog
│   ├── 📄 pinjam.php            ├─ Request loan
│   ├── 📄 riwayat.php           ├─ Loan history
│   ├── 📄 kembali.php           ├─ Return book
│   ├── 📄 ulasan.php            └─ Write review
│   └── 📂 includes/
│       ├── 📄 header.php
│       └── 📄 nav.php
│
├── 📂 assets/
│   ├── 📂 css/
│   │   ├── 📄 style.css, index.css, login.css, etc.
│   │   ├── 📂 admin/        ├─ Admin-specific styles
│   │   ├── 📂 petugas/      ├─ Petugas-specific styles
│   │   └── 📂 anggota/      └─ Member-specific styles
│   ├── 📂 js/
│   │   └── 📄 script.js     ← Global JS utilities
│   └── 📂 img/              ← Images & media
│
├── 📂 uploads/              ← Dynamic uploaded files
│   ├── 📂 cover/            ├─ Book covers
│   ├── 📂 foto_anggota/     └─ Member photos
│
└── 📄 README.md             ← Documentation (this file)
```

### 📂 Penjelasan Folder

| Folder | Fungsi |
|--------|--------|
| `config/` | Database connection & global constants |
| `includes/` | Shared helpers (session, upload, auth) |
| `admin/` | Admin dashboard & management pages |
| `petugas/` | Librarian dashboard & operations |
| `anggota/` | Member portal & borrowing features |
| `assets/css/` | Stylesheets organized by role |
| `assets/js/` | Client-side scripts (validation, AJAX) |
| `uploads/` | Cover images & member photos |

---

## 📄 Penjelasan File Penting

### config/database.php
- **Fungsi:** Database connection & global helpers
- **Isi utama:**
  - `getConnection()` — Koneksi MySQLi ke `perpus_30`
  - `safe_query()`, `get_val()` — Query helper aman
  - `DENDA_PER_HARI = 1000` — Fine constant (Rp)
- **Keterkaitan:** Include di semua file yang perlu database

### includes/session.php
- **Fungsi:** Authentication & session management
- **Isi utama:**
  - `initSession()` — Start session
  - `isAdmin()`, `isPetugas()`, `isAnggotaLoggedIn()` — Role checks
  - `requireAdmin()`, `requireAnggota()` — Protect pages
  - `logout()` — Clear session & redirect
- **Keterkaitan:** Called di setiap page untuk auth validation

### index.php (Landing Page)
- **Fungsi:** Homepage publik dengan catalog buku populer & terbaru
- **Isi utama:**
  - Fetch stats: total buku, anggota, peminjaman
  - Query buku populer (by transaction count)
  - Query buku terbaru
  - Display gallery dengan responsive grid
- **Keterkaitan:** Entry point publik, link ke login/register/anggota

### login.php
- **Fungsi:** Central authentication untuk semua roles
- **Isi utama:**
  - Form: username + password
  - Validate di table `pengguna` (admin/petugas) & `anggota` (member)
  - Set `$_SESSION` variables sesuai role
  - Redirect ke dashboard masing-masing role
- **Keterkaitan:** Dari index, register → ke role dashboards

### register.php
- **Fungsi:** Self-service registration untuk anggota baru
- **Isi utama:**
  - Form: nama, email, username, password, foto (optional)
  - Insert ke table `anggota`
  - Validate: email unique, username unique, password strength
  - Upload foto ke `uploads/foto_anggota/`
- **Keterkaitan:** Redirect ke login.php setelah berhasil

### admin/dashboard.php
- **Fungsi:** Admin dashboard dengan stats & quick approval actions
- **Isi utama:**
  - Stats: total buku, anggota, buku tersedia, peminjaman aktif
  - List pending loans dengan inline approve/reject buttons
  - Recent transactions table
- **Keterkaitan:** Query `transaksi`, `buku`, `anggota` tables
- **Logika:** Click "Setujui" → status='Peminjaman' | Click "Tolak" → status='Ditolak'

### admin/transaksi.php
- **Fungsi:** Transaction approval & management
- **Isi utama:**
  - List all transactions dengan status filtering
  - Approve pending loans (status='Pending' → 'Peminjaman')
  - Reject loans (→ 'Ditolak')
  - Mark returns (status='Pengembalian' → 'Dikembalikan')
- **Keterkaitan:** Update `transaksi`, `buku`, `denda` tables

### anggota/katalog.php
- **Fungsi:** Book catalog for members to browse & search
- **Isi utama:**
  - List all books dengan paging (12 per page)
  - Search: keyword matching judul/pengarang
  - Filter by category
  - Show only='tersedia' books
- **Keterkaitan:** Link ke pinjam.php untuk request loan

### anggota/pinjam.php
- **Fungsi:** Loan request form & creation
- **Isi utama:**
  - Form: select book, optional return deadline extension
  - Validate: book available, max 3 concurrent loans, no outstanding fines
  - Create `transaksi` record with status='Pending'
  - Update book status to 'dipinjam'
- **Keterkaitan:** Insert `transaksi`, update `buku` status

### anggota/riwayat.php
- **Fungsi:** Member loan history & status tracking
- **Isi utama:**
  - List all member transactions (paginated)
  - Display status with color coding (Pending/Dipinjam/Ditolak/Dikembalikan)
  - Show due date & days remaining/overdue
  - Show applicable fines
  - Button untuk return request
- **Keterkaitan:** Query `transaksi`, `buku`, `denda` tables

### anggota/kembali.php
- **Fungsi:** Return request for borrowed books
- **Isi utama:**
  - List current active loans (status='Peminjaman')
  - Form: select book, submit return request
  - Update status to 'Pengembalian'
  - Auto-calculate fine jika late
- **Keterkaitan:** Update `transaksi`, create/update `denda` records

### assets/css/admin/dashboard.css
- **Fungsi:** Styling for admin dashboard (layout, cards, tables, badges)
- **Komponen utama:**
  - CSS Variables: `--soft-purple`, `--neutral-800`, `--shadow-md`, dll
  - `.srow` — stats grid (3 columns)
  - `.sc` — stat cards (white with backdrop-filter)
  - `.dc` — data cards (recent transactions)
  - `.status-badge` — status labels (success/danger/warning)
  - Responsive: grid 3 cols → 1 col on mobile
- **Keterkaitan:** Loaded by admin/dashboard.php

### assets/js/script.js
- **Fungsi:** Global client-side utilities
- **Fungsi utama:**
  - `searchBooks()` — AJAX search via api_search.php
  - `validateForm()` — Client-side form validation
  - `togglePassword()` — Show/hide password input
  - `approveTransaction()` — AJAX approve via admin/transaksi.php
  - `showMessage()` — Display alerts/notifications
- **Keterkaitan:** Loaded di semua pages untuk form handling & AJAX

---

## ⚙️ Installation

### 📋 Prasyarat
- XAMPP (Apache + PHP 7.4+ + MySQL 5.7+)
- Git
- Browser modern (Chrome, Firefox)

### 🚀 Setup Step-by-Step

**1. Clone Repository**
```bash
cd C:\xampp\htdocs
git clone https://github.com/yourname/perpustakaan-digital.git Aetheria-Library
cd Aetheria-Library
```

**2. Start XAMPP Services**
- Buka XAMPP Control Panel
- Click "Start" untuk Apache & MySQL
- Tunggu status "Running"

**3. Create Database**
```bash
# Via phpMyAdmin (http://localhost/phpmyadmin)
# OR via MySQL CLI:
mysql -u root
CREATE DATABASE perpus_30 CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
EXIT;
```

**4. Run Setup Script**
```
Buka: http://localhost/Aetheria-Library/setup.php
```

**5. Verify Installation**
```
http://localhost/Aetheria-Library                 # Homepage
http://localhost/Aetheria-Library/login.php       # Login page
http://localhost/Aetheria-Library/register.php    # Register page
```

---

## 🔐 Environment Configuration (.env)

**File:** `config/database.php`

```php
define('DB_HOST', 'localhost');      // MySQL host
define('DB_USER', 'root');           // MySQL username
define('DB_PASS', '');               // MySQL password
define('DB_NAME', 'perpus_30');      // Database name
define('DENDA_PER_HARI', 1000);      // Fine per day (Rp)
```

| Variable | Fungsi | Contoh |
|----------|--------|--------|
| `DB_HOST` | MySQL server address | `localhost` atau `192.168.1.10` |
| `DB_USER` | MySQL username | `root` |
| `DB_PASS` | MySQL password | `password123` (if set) |
| `DB_NAME` | Database name | `perpus_30` |
| `DENDA_PER_HARI` | Fine per day (IDR) | `1000` = Rp 1.000/hari |

---

## ▶️ Running Project

### 🏃 Development Mode

```bash
# 1. Start XAMPP (Apache + MySQL)
# 2. Open browser: http://localhost/Aetheria-Library
# 3. Browse atau login dengan akun test:

# Admin:
# - Username: admin
# - Password: admin123
# - Go to: http://localhost/Aetheria-Library/admin/dashboard.php

# Petugas:
# - Username: petugas
# - Password: petugas123
# - Go to: http://localhost/Aetheria-Library/petugas/dashboard.php

# Anggota (Member):
# - Register di http://localhost/Aetheria-Library/register.php
# - Go to: http://localhost/Aetheria-Library/anggota/dashboard.php
```

### 📍 Main URLs

| Role | Page | URL |
|------|------|-----|
| **Public** | Homepage | `http://localhost/Aetheria-Library` |
| **Public** | Login | `http://localhost/Aetheria-Library/login.php` |
| **Public** | Register | `http://localhost/Aetheria-Library/register.php` |
| **Admin** | Dashboard | `http://localhost/Aetheria-Library/admin/dashboard.php` |
| **Petugas** | Dashboard | `http://localhost/Aetheria-Library/petugas/dashboard.php` |
| **Anggota** | Dashboard | `http://localhost/Aetheria-Library/anggota/dashboard.php` |

---

## 🔄 Alur Sistem

### 👤 User Flow (Anggota/Member)

```
1. REGISTER / LOGIN
   ├─ New: register.php → insert to table `anggota`
   └─ Existing: login.php → set $_SESSION → redirect anggota/dashboard.php

2. BROWSE KATALOG
   └─ anggota/katalog.php: search, filter kategori, paging

3. AJUKAN PEMINJAMAN
   └─ anggota/pinjam.php: create transaksi (status='Pending')

4. TUNGGU APPROVAL (Admin)
   ├─ Status='Pending' → Admin approve
   ├─ Admin click "Setujui" → status='Peminjaman'
   └─ Member bisa ambil buku di perpustakaan

5. MONITOR DEADLINE
   └─ anggota/riwayat.php: lihat status, due date, remaining days

6. KEMBALIKAN BUKU
   ├─ anggota/kembali.php: request return
   ├─ Update status='Pengembalian'
   ├─ Auto-calculate fine jika late
   └─ Petugas validate fisik & close transaksi

7. BAYAR DENDA (if late)
   └─ Komunikasi dengan petugas untuk pembayaran
```

### Database Flow

```
anggota    → transaksi → buku
   ↓            ↓          ↓
  User     Loan Record   Inventory
           ↓
         denda (if late)
```

### Admin Approval Flow

```
Member request loan (Pending)
    ↓
Admin see di admin/transaksi.php
    ↓
Admin click "Setujui"
    ├─ Update transaksi: status='Peminjaman'
    ├─ Update buku: status='dipinjam'
    └─ Member can take book
    
    OR
    
Admin click "Tolak"
    ├─ Update transaksi: status='Ditolak'
    └─ Loan cancelled
```

---

## 🧪 Testing

Checklist manual testing:

**Authentication:**
- [ ] Register anggota baru
- [ ] Login & redirect correct dashboard
- [ ] Logout clear session

**Loan Workflow:**
- [ ] Browse & search katalog
- [ ] Request loan (status=Pending)
- [ ] Admin approve → status=Peminjaman
- [ ] Request return → status=Pengembalian
- [ ] Petugas validate → status=Dikembalikan

**Fine Calculation:**
- [ ] Return late → fine auto-apply
- [ ] Fine = days_late × Rp1.000
- [ ] Member see fine di riwayat

**Responsive:**
- [ ] Desktop: full layout
- [ ] Mobile: stack vertically, hamburger menu

---

## 📦 Dependencies Breakdown

### 🔧 Core PHP Extensions

| Dependency | Fungsi | Digunakan Di |
|------------|--------|-------------|
| **MySQLi** (built-in) | Database connection & queries | config/database.php |
| **Sessions** (built-in) | User authentication & state | includes/session.php |
| **File Upload** (built-in) | Image upload handling | register.php, petugas/buku.php |
| **Date/Time** (built-in) | Calculate deadlines & fines | admin/transaksi.php, denda.php |

### 🎨 Frontend Libraries

| Library | Version | Fungsi | Digunakan Di |
|---------|---------|--------|-------------|
| **Font Awesome** | 6.x | Icons (check, x, clock, dll) | template files |
| **Inter Font** | - | Typography | assets/css/style.css |
| **Plus Jakarta Sans** | - | Headlines | header.php |

### 🔒 Security Dependencies

**Saat ini:**
- Session-based auth (native PHP)
- MySQLi prepared statements (prevent SQL injection)

**Recommended untuk future:**
- `bcrypt` untuk password hashing: `password_hash($pwd, PASSWORD_BCRYPT)`
- `CSRF tokens` untuk form protection
- `Content Security Policy` headers

---

## ⚠️ Troubleshooting

### Error: "Koneksi database gagal"
**Solusi:**
- Pastikan MySQL running di XAMPP
- Check `config/database.php` credentials
- Create database: `CREATE DATABASE perpus_30 CHARACTER SET utf8mb4;`

### Error: "Headers already sent"
**Solusi:**
- `session_start()` harus di baris pertama, sebelum HTML output
- Hapus whitespace sebelum `<?php`

### Login gagal
**Solusi:**
- Verify username/password di database
- Check table: `SELECT * FROM pengguna WHERE username='admin';`

### Image/Cover tidak muncul
**Solusi:**
- Set folder permissions: `chmod -R 777 uploads/`
- Verify file path relative ke root (misal: `uploads/cover/book1.jpg`)

### Fine tidak auto-calculate
**Solusi:**
- Check constant: `var_dump(DENDA_PER_HARI);` should be 1000
- Test date logic: `datediff(today, tgl_kembali_rencana)`

---

## 🧑‍💻 Contributing & License

### 📝 Contributing

1. Fork repository
2. Create feature branch: `git checkout -b feature/nama-fitur`
3. Commit changes: `git commit -m "Deskripsi perubahan"`
4. Push to branch: `git push origin feature/nama-fitur`
5. Open Pull Request

### 📜 License

MIT License © 2026 Aetheria Library

