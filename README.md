# Evolusi Perangkat Lunak - Praktikum 02: Manajemen GitHub & Prinsip CI

[![CI Status](https://github.com/el-kocan/evolusi-pl-24-544540-sv-25445/actions/workflows/ci.yml/badge.svg)](https://github.com/el-kocan/evolusi-pl-24-544540-sv-25445/actions)
![Laravel](https://img.shields.io/badge/Laravel-12.x-FF2D20?style=flat&logo=laravel&logoColor=white)
![PHP](https://img.shields.io/badge/PHP-8.3-777BB4?style=flat&logo=php&logoColor=white)
![Vite](https://img.shields.io/badge/Vite-8.x-646CFF?style=flat&logo=vite&logoColor=white)
![TailwindCSS](https://img.shields.io/badge/TailwindCSS-v4-06B6D4?style=flat&logo=tailwindcss&logoColor=white)

Repository ini dibangun untuk memenuhi tugas **Praktikum Pertemuan 02** mata kuliah **Konstruksi & Evolusi Perangkat Lunak**, Program Studi Sarjana Terapan, Sekolah Vokasi, Universitas Gadjah Mada.

---

## 👤 Identitas Mahasiswa

* **NIM:** `24/544540/SV/25445`
* **Mata Kuliah:** Konstruksi & Evolusi Perangkat Lunak
* **Dosen Pengampu:** Galih Malela Damaraji, S.Pd., M.Eng.
* **Tahun Ajaran:** Gasal 2025/2026

---

## 🌿 Model Percabangan (Branching Strategy)

Repository ini menerapkan kaidah Git Flow dengan perlindungan cabang (*Branch Protection Rules*):

```text
main (Production Ready & Protected)
  ▲
  └── dev (Integration Branch & Protected)
        ▲
        └── feature/setup-vite-ui (Feature Work)
```

1. **`main`**: Cabang utama yang selalu dalam kondisi rilis stabil. Tidak boleh di-push langsung (*branch protected*).
2. **`dev`**: Cabang integrasi pengembangan tim. Perubahan digabungkan melalui Pull Request dari cabang fitur (*branch protected*).
3. **`feature/*`**: Cabang kerja spesifik untuk pengembangan fitur atau perbaikan.

### Alur Pull Request:
1. `feature/setup-vite-ui` ➔ `dev` (Pull Request #1)
2. `dev` ➔ `main` (Pull Request #2)

---

## ⚙️ Continuous Integration (GitHub Actions)

Pipeline otomatis dikonfigurasi pada `.github/workflows/ci.yml` dengan **3 Job mandiri** yang berjalan paralel setiap kali terjadi `push` atau `pull_request` ke cabang `main` dan `dev`:

1. **Job 1: `Code Quality & Lint (Laravel Pint)`**
   * Menginisialisasi runner Ubuntu dengan runtime **PHP 8.3**.
   * Memasang dependensi Composer.
   * Menjalankan standarisasi kode dan *linter* otomatis (`./vendor/bin/pint --test`).

2. **Job 2: `Backend Tests (PHPUnit)`**
   * Menginisialisasi runner Ubuntu dengan runtime **PHP 8.3**.
   * Memasang dependensi Composer.
   * Menjalankan suite pengujian unit dan fitur (`php artisan test`).

3. **Job 3: `Frontend Build (Vite)`**
   * Menginisialisasi runner Ubuntu dengan runtime **Node.js 22**.
   * Memasang dependensi frontend melalui `npm ci`.
   * Memvalidasi bahwa *bundle asset* CSS & JS dapat dikompilasi secara bersih (`npm run build`).

---

## 📝 Format Pesan Commit (Conventional Commits)

Seluruh riwayat commit ditulis menggunakan standar **Conventional Commits**:
* `feat:` penambahan fitur baru (misal tampilan antarmuka, aset baru).
* `test:` penambahan atau penyesuaian pengujian unit/fitur.
* `ci:` konfigurasi alur kerja otomasi dan pipeline pengujian.
* `docs:` pembaruan dokumentasi README atau panduan proyek.
* `chore:` konfigurasi build dasar atau pemeliharaan dependensi.

---

## 🚀 Panduan Menjalankan Proyek di Lingkungan Lokal

### Prasyarat:
* PHP >= 8.3
* Composer >= 2.x
* Node.js >= 20.x & npm

### Langkah Instalasi:
```bash
# 1. Clone repository
git clone https://github.com/el-kocan/evolusi-pl-24-544540-sv-25445.git
cd evolusi-pl-24-544540-sv-25445

# 2. Pasang dependensi PHP & salin konfigurasi env
composer install
cp .env.example .env
php artisan key:generate

# 3. Pasang dependensi Node.js dan build aset
npm install
npm run build

# 4. Jalankan pengujian otomatis
php artisan test

# 5. Jalankan server lokal
php artisan serve
```
