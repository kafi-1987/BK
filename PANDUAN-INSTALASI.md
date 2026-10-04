# PANDUAN INSTALASI — Buku Tamu Digital Guru BK

Ada **2 bagian**: Backend (Google Apps Script) lalu Frontend (GitHub Pages). Kerjakan berurutan.

## BAGIAN 1 — BACKEND (Google Apps Script)

1. Buka https://script.google.com → **Proyek baru**.
2. Ganti nama file `Code.gs` menjadi `Kode`, hapus isinya, lalu **tempel seluruh isi `Kode.gs`**. Simpan (Ctrl+S).
3. Pilih fungsi **`setupAppEnvironment`** di dropdown → ▶ **Run**. Klik *Review permissions* dan izinkan akses Drive & Sheets.
   - ⚠️ Jalankan **HANYA SEKALI**. (Bila terlanjur dua kali, fungsi akan menolak dan memberi tahu.)
4. Buka **Execution log**. Catat baris berikut (hanya tampil sekali):
   ```
   Username : superadmin
   Password : BK-xxxxxxxx
   ```
5. Pilih fungsi **`pasangTrigger`** → ▶ Run (sekali). Ini memasang pembersihan sampah otomatis (30 hari) dan backup mingguan.
6. **Deploy → New deployment → Web app**
   - Execute as: **Me**
   - Who has access: **Anyone**
   - Klik Deploy, lalu **salin URL yang berakhiran `/exec`**.
7. Cek di Google Drive: folder `📁 Buku Tamu BK SMAN 6 Palangkaraya` dan Spreadsheet `DB_BukuTamuBK` sudah terbuat.

> Setiap kali Anda mengubah `Kode.gs`, lakukan **Deploy → Manage deployments → ✏️ → Version: New version → Deploy**. URL tidak berubah.

## BAGIAN 2 — FRONTEND (GitHub Pages)

### Langkah 0 — Isi URL backend (WAJIB sebelum upload)
1. Ekstrak `buku-tamu-bk.zip`. Hasilnya folder **`buku-tamu-bk`**.
2. Buka `buku-tamu-bk/js/config.js` dengan Notepad. Ganti
   `https://script.google.com/macros/s/XXXX/exec` dengan URL `/exec` dari Bagian 1 langkah 6. Simpan.

### Langkah 1 — Folder kerja
Folder yang di-`git init` adalah **`buku-tamu-bk`** itu sendiri (folder yang langsung berisi `index.html`).
**Jangan** masuk lebih dalam dan **jangan** naik satu level.

Windows: buka folder `buku-tamu-bk` di File Explorer → klik address bar → ketik `powershell` → Enter. Lalu cek:
```
dir
```
Harus terlihat `index.html`, `css`, `js`, `assets`. Jika tidak, Anda berada di folder yang salah.

### Langkah 2 — Git & GitHub
Panduan ini dikerjakan **bertahap bersama saya di chat** (instal Git, buat repository publik, push, token, aktifkan Pages). Mulai dengan:
```
git --version
```
Kirim screenshot hasilnya, lalu kita lanjut satu langkah per satu langkah.

Ringkasan akhir: setelah `git push -u origin main`, buka repo → **Settings → Pages → Deploy from a branch → main / (root) → Save**, centang **Enforce HTTPS**. Situs: `https://USERNAME.github.io/NAMA-REPO/`

## UJI
1. Buka situs → isi formulir Siswa → ambil selfie → kirim. Tiket `BK-YYYYMMDD-0001` harus muncul.
2. Cek Spreadsheet (sheet `Tamu_Siswa`) dan Drive (folder bulan berisi foto).
3. Buka `#/admin/login` → masuk `superadmin` → **ganti password** saat diminta.
4. Menu **Log & Pengaturan → QR Code** → unduh poster dan cetak.

## CATATAN PENTING
- Kamera hanya jalan di **HTTPS** (GitHub Pages sudah HTTPS). Bila kamera ditolak, tamu bisa memakai tombol *Ambil / Pilih Foto*.
- QR Code memuat pustaka kecil dari cdnjs, jadi butuh internet saat membuat QR.
- Kuota GAS: ±100 tamu/hari aman. Pembuatan foto per tamu 1 file Drive.
- Akun terkunci 15 menit setelah 5 kali salah password; sesi berakhir setelah 60 menit tidak aktif.
- Ekspor Excel berformat `.xls` (dibuka normal di Excel/Sheets); ekspor PDF memakai dialog cetak browser → *Simpan sebagai PDF*.

## MASALAH UMUM
| Gejala | Solusi |
|---|---|
| Banner "Backend belum terhubung" | `GAS_URL` di `js/config.js` belum diisi |
| Halaman 404 di GitHub Pages | `index.html` tidak di root repo → push ulang dari folder `buku-tamu-bk` |
| "Sheet ... tidak ditemukan" | `setupAppEnvironment()` belum dijalankan |
| Perubahan kode GAS tidak berlaku | Buat **New version** pada deployment |
| Situs lama setelah push | Ctrl+Shift+R |
