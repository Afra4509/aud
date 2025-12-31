# SMADA Security Hardening & Prevention Guide

## Ringkasan
Dokumen ini disusun sebagai panduan **pencegahan dan penguatan keamanan sistem digital SMADA** berdasarkan hasil evaluasi teknis dan observasi terbatas terhadap aplikasi dan website yang digunakan dalam ekosistem sekolah.

Tujuan utama dokumen ini adalah:
- Mencegah insiden keamanan di masa depan
- Melindungi data siswa, guru, dan institusi
- Meningkatkan profesionalitas dan keandalan sistem
- Menurunkan risiko reputasi dan hukum

Dokumen ini **bukan laporan kesalahan personal**, melainkan panduan teknis untuk perbaikan sistem.

---

## Ruang Lingkup
Panduan ini mencakup:
- Aplikasi E-Learning (Mobile & Web)
- Website `smadapas.biz`
- Website `smadapas.sch.id`
- Infrastruktur server & jaringan
- Manajemen akun dan akses
- Proteksi terhadap serangan umum (OWASP Top 10, DDoS, Bot, Malware)

---

## 1. Pengamanan Aplikasi E-Learning

### 1.1 Build & Distribusi Aplikasi
**Masalah umum:**
- Aplikasi mudah diekstraksi
- Mode debug masih aktif
- Kode dan konfigurasi terekspos

**Pencegahan efektif:**
- Gunakan **release build** (non-debug)
- Aktifkan:
  - Code obfuscation (ProGuard / R8)
  - Anti-tampering & integrity check
- Nonaktifkan:
  - Debug flag
  - Logging sensitif di production
- Validasi signature aplikasi saat runtime

---

### 1.2 Autentikasi & Sesi
**Masalah umum:**
- Autentikasi dapat dimodifikasi
- Manajemen sesi tidak stabil

**Pencegahan efektif:**
- Terapkan **token-based authentication (JWT / session token)**
- Session timeout otomatis
- Validasi token di server (bukan client)
- Implementasi **single-session per user**
- Deteksi anomali login (IP / device change)

---

### 1.3 Isolasi Aplikasi
**Masalah umum:**
- Aplikasi dapat diakses via web wrapping

**Pencegahan efektif:**
- Backend **menolak request non-application**
- Validasi:
  - User-Agent
  - App signature
  - Custom application headers
- Rate-limit request API

---

## 2. Pengamanan Website smadapas.biz

### 2.1 Struktur & Arsitektur
**Masalah umum:**
- Banyak endpoint admin terpisah
- Kompleksitas tinggi, attack surface besar

**Pencegahan efektif:**
- Satukan panel admin dalam **satu endpoint**
- Gunakan role-based access control (RBAC)
- Batasi akses admin berdasarkan IP / VPN

---

### 2.2 Autentikasi & Kredensial
**Masalah umum:**
- Username/password mudah ditebak
- Rentan brute force

**Pencegahan efektif:**
- Password policy kuat:
  - Minimum 12 karakter
  - Kombinasi huruf, angka, simbol
- Hash password dengan **bcrypt / argon2**
- Aktifkan:
  - Login rate limiting
  - Account lockout sementara
- Wajibkan pergantian password berkala

---

### 2.3 SQL Injection & Input Validation
**Masalah umum:**
- Input tidak difilter
- Upload file tidak aman

**Pencegahan efektif:**
- Gunakan **prepared statements**
- Validasi input server-side
- Nonaktifkan dynamic SQL
- Escape & sanitize semua input

---

### 2.4 Upload File Security
**Masalah umum:**
- Upload file berbahaya (HTML/PHP trigger)

**Pencegahan efektif:**
- Whitelist MIME type & extension
- Rename file secara acak (UUID)
- Simpan file di luar web root
- Scan file dengan antivirus server-side
- Nonaktifkan eksekusi file upload

---

## 3. Pengamanan Website smadapas.sch.id

### 3.1 Pencegahan Malware & Judol Injection
**Masalah umum:**
- Penyisipan link eksternal / judol

**Pencegahan efektif:**
- Audit seluruh file website
- Reinstall core CMS (jika ada)
- Ganti seluruh kredensial:
  - cPanel
  - FTP
  - Database
- Nonaktifkan editor file publik
- Batasi permission file (`644/755`)

---

### 3.2 cPanel & Server
**Masalah umum:**
- Pengamanan default (lemah)

**Pencegahan efektif:**
- Aktifkan:
  - ModSecurity
  - ImunifyAV / Imunify360
- Update OS & service rutin
- Nonaktifkan login root langsung
- Gunakan SSH key authentication

---

## 4. Proteksi Infrastruktur & Jaringan

### 4.1 DDoS & Traffic Protection
**Kondisi saat ini:**
- Risiko DDoS rendah, proteksi minim

**Pencegahan efektif (WAJIB):**
- Aktifkan **Cloudflare**
- Gunakan:
  - WAF
  - Rate Limiting
  - Bot Management
  - CDN
- Gunakan HTTPS di seluruh domain
- Aktifkan HTTP security headers

---

### 4.2 Monitoring & Logging
- Centralized log
- Audit login & perubahan data
- Alert otomatis untuk aktivitas abnormal
- Backup harian (offsite)

---

## 5. Manajemen Akses & Organisasi

### 5.1 Akses Administrator
- Prinsip **least privilege**
- Tidak berbagi akun admin
- Log semua aktivitas admin
- 2FA untuk akun penting

---

### 5.2 Prosedur Keamanan
- SOP respon insiden
- Audit keamanan berkala
- Pengetesan keamanan terkontrol
- Edukasi keamanan untuk operator sistem

---

## Penutup
Dokumen ini disusun sebagai **panduan pencegahan** agar sistem digital SMADA:
- Lebih aman
- Lebih stabil
- Lebih profesional
- Siap menghadapi ancaman nyata di masa depan

Keamanan bukan tentang siapa yang salah, melainkan **bagaimana sistem diperbaiki dan diperkuat bersama**.

---

**Disusun oleh:**  
Siswa SMADA  
Sebagai bentuk kepedulian terhadap keamanan dan reputasi institusi
