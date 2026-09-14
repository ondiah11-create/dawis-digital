Dasawisma Digital — PWA tanpa build
====================================

ISI FOLDER
- index.html (seluruh aplikasi)
- manifest.json
- service-worker.js
- icon-192.png dan icon-512.png (tambahkan sendiri)

CARA UPDATE FILE index.html YANG SUDAH ADA DI GITHUB
1. Buka repo GitHub Anda di browser HP, tap file index.html
2. Tap ikon pensil (Edit this file)
3. Di dalam editor, pilih semua teks (tap & tahan lalu "Select All", atau tap sekali lalu Ctrl+A kalau pakai keyboard) dan hapus
4. Paste isi index.html yang baru (hasil tombol "Simpan" di halaman ini)
5. Scroll ke bawah, tap "Commit changes"
6. Netlify otomatis redeploy dalam beberapa detik

AKUN LOGIN AWAL
Username: pengurus
Password: pengurus123
(Akun anggota/pengurus baru dibuat oleh pengurus lewat menu Pengaturan.)

SETUP FIREBASE (untuk Chat, Notifikasi, dan Tagihan — semuanya butuh Firebase yang sama)
1. https://console.firebase.google.com -> Add project -> beri nama bebas -> Create project (gratis)
2. Klik ikon </> (Web app) -> Register app -> copy object firebaseConfig yang muncul
3. Di index.html, cari tulisan "GANTI DENGAN KONFIGURASI FIREBASE ANDA", ganti firebaseConfig dengan hasil copy
4. Firebase Console -> Build -> Firestore Database -> Create database -> mode Production
5. Tab Rules, ganti dengan:

   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /{document=**} {
         allow read, write: if true;
       }
     }
   }

   lalu Publish. (Catatan: rule ini terbuka karena aplikasi tidak pakai Firebase Authentication — cocok untuk grup RT yang saling percaya.)
6. Commit ulang index.html supaya firebaseConfig ter-deploy.

CATATAN PENTING
- Data Warga/Kegiatan/Keuangan tersimpan LOKAL per HP (localStorage) — tidak sinkron antar perangkat.
- Chat, Notifikasi, dan Tagihan tersinkron real-time via Firebase (butuh setup di atas).
- Notifikasi HP hanya muncul saat aplikasi sedang dibuka/baru dibuka (bukan saat aplikasi tertutup total) — itu keterbatasan tanpa server push khusus.
