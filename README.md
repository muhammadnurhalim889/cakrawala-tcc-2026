# 🎓 Cakrawala — Sistem Akademik Cerdas Berbasis AI

**Trunodjoyo Creative Competition 2026 — Vibe Code (Web Application Development)**
Tema: *Shaping Tomorrow: Digital Innovation, Artificial Intelligence, and Sustainable Communities*

Cakrawala adalah sistem akademik mahasiswa yang mengintegrasikan Artificial Intelligence untuk membantu mahasiswa memantau performa akademik secara proaktif, dan membantu admin/dosen mengidentifikasi mahasiswa yang butuh perhatian lebih cepat — sekaligus mendorong budaya kampus yang lebih paperless dan suportif lewat fitur mentoring sebaya.

---

## ✨ Fitur Utama

### Dashboard Admin
- **Ringkasan** — statistik akademik + **dashboard dampak keberlanjutan** (estimasi kertas dihemat) + **AI Insight level kelas** (analisis pola & rekomendasi untuk seluruh angkatan, bertenaga Gemini AI)
- **Upload Nilai** — input nilai per kelas/mata kuliah
- **Pengumuman** — buat, ubah, hapus pengumuman (target kelas tertentu atau semua kelas)
- **Kelola Kelas** — CRUD kelas & mata kuliah
- **Data Mahasiswa** — CRUD mahasiswa, termasuk ubah kredensial login, pencarian, dan export CSV
- **Pengaturan Akun** — ganti username/password admin

### Dashboard Mahasiswa
- **Profil** — ringkasan data akademik
- **Nilai Saya** — transkrip, visualisasi tren IPK ("growth rings"), **AI Academic Advisor** (rekomendasi belajar personal + referensi materi), cetak/simpan PDF
- **Pengumuman** — otomatis terfilter sesuai kelas
- **Tanya AI** — chatbot akademik interaktif (Gemini AI), riwayat percakapan otomatis kedaluwarsa setelah 7 hari
- **Mentoring** — mahasiswa berprestasi (IPK > 3.4) dapat mendaftar jadi mentor sebaya

### Lainnya
- Mode gelap (dark mode)
- Desain responsif, accessible di mobile

---

## 🤖 Peran Artificial Intelligence

| Fitur | Model AI | Fungsi |
|---|---|---|
| AI Academic Advisor | Gemini (via Cloudflare Worker proxy) | Menganalisis nilai mahasiswa, memberi rekomendasi & referensi belajar personal |
| AI Insight Level Kelas | Gemini | Menganalisis data agregat tiap kelas, memberi insight & saran tindakan untuk admin |
| Chatbot Akademik | Gemini | Asisten tanya-jawab interaktif untuk mahasiswa |

Seluruh fitur AI memiliki **fallback rule-based** — jika API AI tidak dapat diakses, sistem tetap memberi analisis dasar berbasis aturan, sehingga aplikasi tidak pernah gagal total.

---

## 🏗️ Arsitektur & Teknologi

```
┌─────────────────────┐      ┌──────────────────────┐      ┌─────────────────┐
│  sistem-akademik-ai  │─────▶│  Firebase Realtime DB │      │   Gemini API     │
│  .html (frontend)    │      │  (data akademik)      │      │  (generative AI) │
│  hosted: GitHub Pages│      └──────────────────────┘      └────────▲─────────┘
└──────────┬───────────┘                                             │
           │                                                          │
           └─────────────────────▶ Cloudflare Worker (proxy) ─────────┘
                                    (menghindari CORS, menyembunyikan API key)
```

- **Frontend**: HTML, CSS, vanilla JavaScript (tanpa framework — ringan & cepat dimuat)
- **Database**: [Firebase Realtime Database](https://firebase.google.com/) — NoSQL, sinkronisasi data real-time
- **AI Proxy**: [Cloudflare Workers](https://workers.cloudflare.com/) — menjalankan pemanggilan Gemini API di sisi server, menghindari pembatasan CORS browser dan mencegah API key terekspos ke pengguna akhir
- **AI Model**: Google Gemini (`gemini-3.5-flash`)
- **Hosting**: GitHub Pages

---

## 📈 Skalabilitas

- **Firebase Realtime Database** menskalakan otomatis mengikuti pertumbuhan data (dari puluhan hingga ribuan mahasiswa) tanpa perubahan arsitektur
- **Cloudflare Workers** berjalan di *edge network* global, sehingga latensi tetap rendah walau jumlah pengguna bertambah dari berbagai lokasi
- Struktur data berbasis path (`kelas/`, `mahasiswa/`, `pengumuman/`, `chat/`) dirancang agar operasi baca/tulis tetap efisien (O(1) per path) walau volume data bertambah besar
- Frontend tanpa framework berat menjaga waktu muat tetap cepat meski fitur terus ditambah

---

## 🚀 Cara Menjalankan

1. Buka [`sistem-akademik-ai.html`](./sistem-akademik-ai.html) langsung di browser, **atau**
2. Akses versi live: `[isi URL GitHub Pages di sini]`

**Akun demo:**
- Admin: hubungi tim pengembang / lihat kredensial demo di dokumen presentasi
- Mahasiswa: login menggunakan NIM & kata sandi akun (dibuat lewat dashboard Admin)

### Menjalankan backend sendiri (opsional)
Proyek ini menggunakan Firebase & Cloudflare Worker milik tim pengembang. Untuk menjalankan instance sendiri:
1. Buat project [Firebase](https://console.firebase.google.com), aktifkan Realtime Database
2. Deploy `worker.js` ke [Cloudflare Workers](https://workers.cloudflare.com), isi API key Gemini dari [Google AI Studio](https://aistudio.google.com/apikey)
3. Update konstanta `FIREBASE_URL` dan `GEMINI_PROXY_URL` di `sistem-akademik-ai.html`

---

## 🖼️ Cuplikan Layar

[*(https://ibb.co.com/LzxXvRd6)*]/ADMIN
[*(https://ibb.co.com/S7MjFK6S)*]/USER

---

## 👥 Tim Pengembang

- [Isi nama & instansi tim di sini]

---

## 📄 Lisensi

Proyek ini dibuat untuk keperluan Trunodjoyo Creative Competition 2026 (UKM Triple-C, Universitas Trunodjoyo Madura).
