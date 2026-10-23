# 🚀 TelDrive Cloud - Unlimited Storage via Telegram

Aplikasi cloud storage pribadi berbasis web (*self-hosted Google Drive alternative*) yang memanfaatkan infrastruktur Telegram sebagai media penyimpanan file tak terbatas (*unlimited storage*) dengan dukungan chunking, enkripsi, dan streaming media.

---

## 🏗️ Tech Stack & Arsitektur

* **Core Engine / Backend:** [Go (Golang)](https://go.dev) — High-throughput streaming I/O, concurrency goroutine, MTProto client (`gotd/td`).
* **Frontend Web UI:** React + TypeScript + Vite — Antarmuka bergaya Google Drive / Material You (embedded ke binary via `//go:embed`).
* **Storage Backend:** Telegram MTProto (Penyimpanan file tak terbatas hingga 2GB/4GB per chunk).
* **Metadata Database:** PostgreSQL (Neon Cloud) — Menyimpan struktur tree folder, indeks chunk file, dan otentikasi user.

---

## 📁 Struktur File

```text
├── docker-compose.yml   # Konfigurasi container Docker TelDrive
├── config.toml          # File konfigurasi utama (port, db, JWT, session, upload encryption)
├── .env                 # Environment variables untuk deployment PaaS/Cloud
└── README.md            # Dokumentasi panduan instalasi dan penggunaan
```

---

## ✨ Fitur Utama

- ⚡ **Unlimited Storage**: File diunggah ke channel/saved message Telegram.
- 🧩 **Smart Chunking**: File berukuran gigabyte dipecah otomatis ke pecahan kecil dan di-assemble saat streaming/download.
- 🎬 **In-Browser Streaming**: Putar video (MP4/MKV) dan audio langsung dari browser via *HTTP Range Requests* tanpa download penuh.
- 🔐 **End-to-End Encryption**: Opsi enkripsi AES-256 pada upload file.
- 🔌 **Rclone Support**: Kompatibel dengan Rclone untuk integrasi mount drive ke OS lokal.

---

## 🚀 Cara Menjalankan

### 1. Jalankan di Server / Komputer Lokal (Docker Compose)

Pastikan Docker sudah terinstall:

```bash
git clone https://github.com/arjuna15/drive_tele.git
cd drive_tele
docker compose up -d
```

Buka browser: `http://localhost:8080`.

---

### 2. Deploy Gratis ke Cloud (PaaS seperti Zeabur / Render)

1. Hubungkan repository GitHub ini (**`arjuna15/drive_tele`**) ke penyedia PaaS (misal: [Zeabur](https://zeabur.com) atau [Render](https://render.com)).
2. Pastikan port diarahkan ke **`8080`**.
3. Pastikan konfigurasi environment variable berikut terpasang (sudah ada di `.env`):
   - `TELDRIVE_DB_DATA_SOURCE`
   - `TELDRIVE_TG_APP_ID`
   - `TELDRIVE_TG_APP_HASH`
   - `TELDRIVE_JWT_SECRET`
   - `TELDRIVE_TG_UPLOADS_ENCRYPTION_KEY`
   - `TELDRIVE_JWT_ALLOWED_USERS`

---

## 🔑 Login Pertama Kali

1. Buka URL web yang telah aktif di browser.
2. Masukkan nomor HP Telegram Anda (format: `+628...`).
3. Buka aplikasi Telegram Anda, salin kode OTP login yang dikirimkan oleh sistem Telegram.
4. Masukkan kode OTP ke browser dan selesai! Web drive siap digunakan.

---

## ⚠️ Lisensi & Catatan

Proyek ini dibangun berdasarkan proyek open-source [tgdrive/teldrive](https://github.com/tgdrive/teldrive). Gunakan untuk keperluan backup dan personal cloud drive pribadi secara bertanggung jawab sesuai syarat dan ketentuan penggunaan Telegram API.
