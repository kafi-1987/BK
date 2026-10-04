# Buku Tamu Digital Guru BK — SMAN 6 Palangkaraya

Frontend statis (HTML/CSS/JS murni) untuk GitHub Pages. Backend: Google Apps Script (REST API JSON).

## Struktur
```
index.html          ← halaman utama (harus di root repository)
css/style.css
js/config.js        ← ISI GAS_URL DI SINI
js/icons.js  core.js  public.js  admin.js  admin2.js  app.js
assets/logo.svg  favicon.svg
```

## Rute
| Hash | Halaman |
|---|---|
| `#/` | Pilih jenis tamu + formulir |
| `#/selfie` → `#/sukses` | Selfie, kirim, tiket |
| `#/admin/login` | Login petugas |
| `#/admin` | Dashboard |
| `#/admin/tamu` , `#/admin/tamu/ID` | Data tamu, detail & edit |
| `#/admin/users` | Kelola admin (Super Admin) |
| `#/admin/log?tab=qr\|log\|db` | QR, audit log, database & sampah (Super Admin) |

## Ganti logo
Simpan logo Anda sebagai `assets/logo.png`, lalu ubah `LOGO` di `js/config.js` menjadi `'assets/logo.png'`.

## Update setelah perubahan
```
git add .
git commit -m "Update"
git push
```
