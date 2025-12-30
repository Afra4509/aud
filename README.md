# 🔐 SECURITY ASSESSMENT REPORT  
## Evaluasi Keamanan Sistem Digital SMADA

---

## 📘 Dokumen Informasi

| Keterangan | Detail |
|-----------|--------|
| Judul | Laporan Evaluasi Keamanan Sistem Digital SMADA |
| Jenis Dokumen | Security Observation & Assessment |
| Lingkup | Aplikasi & Website Sekolah |
| Penyusun | Siswa SMADA |
| Tanggal | 30 Desember 2025 |
| Status | Internal – Evaluasi & Rekomendasi |

---

## 📝 Ringkasan Eksekutif (Executive Summary)

Dokumen ini merupakan laporan hasil **observasi dan evaluasi keamanan terbatas** terhadap beberapa sistem digital yang digunakan di lingkungan SMADA, meliputi aplikasi pembelajaran dan website sekolah.

Tujuan utama laporan ini adalah untuk:
- Mengidentifikasi **potensi kerentanan keamanan**
- Memberikan **gambaran risiko teknis**
- Menyampaikan **rekomendasi perbaikan** demi meningkatkan keamanan, stabilitas, dan profesionalisme sistem

Laporan ini disusun secara **objektif, teknis, dan bertanggung jawab**, serta **tidak bertujuan untuk menyalahkan pihak mana pun**, melainkan sebagai bahan evaluasi internal.

---

## 🎯 Tujuan & Ruang Lingkup

### Tujuan
- Menilai kondisi keamanan sistem digital sekolah
- Mengidentifikasi risiko terhadap data dan layanan
- Mendukung peningkatan tata kelola keamanan TI

### Ruang Lingkup Sistem
1. **Aplikasi SMADA E-Learning**
2. **Website smadapas.biz**
3. **Website smadapas.sch.id**

---

## 1️⃣ Aplikasi SMADA E-Learning

### 🔍 Temuan Teknis
- Struktur aplikasi relatif **mudah diekstraksi**
- Mekanisme **autentikasi masih dapat dimodifikasi**
- Website masih dapat diakses melalui **wrapping aplikasi**
- Lock app dan anti-split telah diterapkan, namun:
  - **Sistem perizinan aplikasi belum optimal**
- Aplikasi terdeteksi masih dalam **debug mode**
- Stabilitas sesi pengguna berpotensi terganggu
- **Lapisan keamanan aplikasi masih terbatas**

### ⚠️ Risiko
- Manipulasi autentikasi
- Penyalahgunaan sesi login
- Potensi akses tidak sah terhadap sistem

---

## 2️⃣ Website smadapas.biz

### 🔍 Temuan Teknis
- Masih dapat diakses menggunakan **payload tertentu**
- Potensi **SQL Injection**
- Kredensial administrator **rentan brute force**
- **WAF dan proteksi Cloudflare belum optimal**
- Struktur admin terpisah berdasarkan kelas:
  - `/x-adminnya/`
  - `/xi-adminnya/`
  - `/xii-adminnya/`
- Struktur ini meningkatkan:
  - Kompleksitas sistem
  - Risiko keamanan
- Spesifikasi **VPS/hosting kurang memadai**
- Fitur upload file:
  - Berpotensi SQL Injection
  - Memungkinkan penyisipan file berbahaya
- Hak akses pengguna dapat dimodifikasi

### ⚠️ Risiko
- Pengambilalihan akun
- Eskalasi hak akses
- Kebocoran dan manipulasi data

---

## 3️⃣ Website smadapas.sch.id

### 🔍 Temuan Teknis
- Ditemukan **penyisipan tautan eksternal berbahaya (judol)**
- Terdapat celah penyimpanan atau penyematan link
- **cPanel dengan tingkat keamanan rendah**
- Tidak terdapat lapisan proteksi tambahan:
  - WAF
  - Cloudflare
  - Rate limiting
  - Bot protection
  - CDN
  - Load balancer

---

## 🛡️ DDoS & Error Analysis Summary

**Tanggal Analisis:** 30/12/2025  
**Waktu:** 17.17 WIB  

### 📊 Hasil Pengujian
- Status Website: **ONLINE**
- HTTP Error: **TIDAK TERDETEKSI**
- Server Response: **NORMAL**
- DDoS Risk Level: **LOW**

### ⚠️ Catatan Penting
Walaupun kondisi saat ini tergolong stabil, **tidak adanya lapisan proteksi aktif** menjadikan sistem **rentan jika terjadi serangan di masa mendatang**.

---

## 📈 Ringkasan Risiko Sistem

| Sistem | Status | Tingkat Risiko |
|------|------|---------------|
| SMADA E-Learning | Aktif | Menengah |
| smadapas.biz | Aktif | Tinggi |
| smadapas.sch.id | Aktif | Menengah |

---

## ✅ Rekomendasi Umum

- Menonaktifkan **debug mode** pada sistem produksi
- Memperkuat:
  - Autentikasi
  - Otorisasi
- Restrukturisasi sistem admin website
- Penerapan:
  - WAF
  - Cloudflare
  - Rate limiting
  - Secure file upload
- Audit keamanan berkala
- Pengelolaan kredensial yang lebih ketat

---

## ⚠️ Disclaimer

Laporan ini disusun **untuk tujuan edukasi, evaluasi internal, dan peningkatan keamanan sistem**.  
Tidak dimaksudkan untuk eksploitasi, penyalahgunaan, atau tindakan yang melanggar hukum.

---

## 👤 Penyusun
Disusun oleh:  
**Siswa SMADA**  
Sebagai bentuk kepedulian terhadap keamanan dan kualitas sistem digital sekolah.

---

## 📅 Riwayat Dokumen
- Versi: 1.0  
- Update Terakhir: 30 Desember 2025
