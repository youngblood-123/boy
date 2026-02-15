# Panduan Instalasi TOTP Authenticator

## Apa Itu?

TOTP Authenticator adalah tool berbasis web untuk menghasilkan kode verifikasi 6 digit (seperti Google Authenticator) langsung di browser. Dibangun dengan HTML, CSS, dan JavaScript murni — **tanpa framework, tanpa build tools, tanpa npm**.

---

## Struktur File

```
website-kamu/
├── index.html          ← Dashboard utama (sudah ada)
├── totp.html           ← Halaman TOTP Authenticator (file baru)
├── background.jpg      ← Asset gambar (sudah ada)
├── logo-kuda.png       ← Asset gambar (sudah ada)
└── ... file lainnya
```

Hanya **2 file HTML** — tidak ada file tambahan yang perlu di-install.

---

## Cara Install ke Website

### Langkah 1: Upload File

Upload file `totp.html` ke **folder yang sama** dengan `index.html` di hosting kamu.

| Hosting | Cara Upload |
|---------|-------------|
| **Vercel** | Push ke Git repository, otomatis deploy |
| **Netlify** | Drag & drop folder ke dashboard Netlify |
| **Shared Hosting (cPanel)** | Upload via File Manager ke folder `public_html/` |
| **GitHub Pages** | Commit file ke repository, aktifkan Pages |
| **EdgeOne / CDN** | Upload ke storage bucket |

### Langkah 2: Selesai!

Tidak ada langkah lain. Kedua file sudah saling terhubung:

- **Dashboard → TOTP**: Klik tombol biru **"TOTP Tool"** di header dashboard
- **TOTP → Dashboard**: Klik link **"← Kembali ke Dashboard"** di atas halaman TOTP

---

## Cara Navigasi

```
┌─────────────────────────────────┐
│  index.html (Dashboard)         │
│                                 │
│  [TOTP Tool]  [Logout]  [Dark] │ ← Klik "TOTP Tool"
│       │                         │
└───────┼─────────────────────────┘
        │
        ▼
┌─────────────────────────────────┐
│  totp.html (TOTP Authenticator) │
│                                 │
│  ← Kembali ke Dashboard        │ ← Klik untuk kembali
│                                 │
│  [Masukkan Secret Key]          │
│  [Generate]                     │
│                                 │
│       123 456                   │ ← Kode TOTP 6 digit
│     [Salin Kode]                │
└─────────────────────────────────┘
```

---

## Cara Menggunakan TOTP

1. Buka halaman TOTP (klik tombol **"TOTP Tool"** di dashboard)
2. Masukkan **Base32 Secret Key** di kolom input
   - Contoh: `JBSWY3DPEHPK3PXP`
   - Secret key biasanya didapat dari aplikasi/layanan yang ingin kamu autentikasi
3. Klik **"Generate"** atau tekan **Enter**
4. Kode 6 digit akan muncul dan **otomatis diperbarui setiap 30 detik**
5. Klik **"Salin Kode"** untuk menyalin ke clipboard

---

## Spesifikasi Teknis

| Parameter | Nilai |
|-----------|-------|
| Standar | RFC 6238 (TOTP) + RFC 4226 (HOTP) |
| Algoritma | HMAC-SHA1 |
| Digit | 6 |
| Periode | 30 detik |
| Encoding | Base32 (RFC 4648) |
| Dependensi | Tidak ada (pure HTML/CSS/JS) |
| Crypto API | Web Crypto API (built-in browser) |
| Kompatibel | Chrome, Firefox, Safari, Edge (modern) |

---

## FAQ

**Q: Apakah perlu install Node.js atau npm?**
A: Tidak. Cukup upload file HTML ke hosting.

**Q: Apakah perlu database?**
A: Tidak. Semua proses berjalan di browser pengguna.

**Q: Apakah secret key dikirim ke server?**
A: Tidak. Semua komputasi TOTP dilakukan 100% di sisi client (browser). Tidak ada data yang dikirim ke server manapun.

**Q: Apakah kompatibel dengan Google Authenticator?**
A: Ya. Menggunakan standar yang sama (RFC 6238, HMAC-SHA1, 6 digit, 30 detik).

**Q: Bagaimana jika saya hosting di subdirectory (misal `/tools/`)?**
A: Pastikan kedua file (`index.html` dan `totp.html`) berada di folder yang sama, atau ubah link `href` di masing-masing file sesuai path relatif.
