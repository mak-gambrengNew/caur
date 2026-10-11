# Gopay PWA

Repo ini membungkus UI `index.html` yang diberikan menjadi Progressive Web App (PWA) yang dapat diinstal dari browser yang mendukung.

## Isi repo

- `index.html` — UI utama beserta alur yang ada pada file sumber.
- `manifest.webmanifest` — nama aplikasi, mode standalone, warna tema, dan ikon.
- `service-worker.js` — cache app shell dan fallback offline dasar.
- `icons/` — ikon 192×192, 512×512, dan maskable 512×512 dari logo GoPay berlatar biru yang diberikan.
- `favicon.png` — ikon browser.

## Jalankan lokal

PWA tidak dapat diuji sepenuhnya jika dibuka langsung melalui `file://`. Jalankan server lokal, misalnya:

```bash
python -m http.server 8080
```

Lalu buka `http://localhost:8080`. `localhost` dianggap secure context oleh browser modern untuk pengujian service worker.

## Deploy

Publikasikan **seluruh isi folder** ke hosting HTTPS, misalnya GitHub Pages, Netlify, atau Vercel. Jangan hanya mengunggah `index.html`; file manifest, service worker, dan folder ikon juga diperlukan.

Setelah deploy:
1. Buka URL HTTPS di Chrome Android.
2. Tunggu service worker aktif.
3. Gunakan tombol **Install PWA** pada layar sambutan jika prompt instalasi tersedia. Jika tidak, buka menu browser (⋮) dan pilih **Install app / Tambahkan ke layar utama**.
4. Jika ikon lama masih muncul, hapus shortcut/aplikasi lama lalu instal ulang atau bersihkan data situs.

## Catatan penting

- PWA memberi pengalaman seperti aplikasi (ikon launcher, jendela standalone, cache dasar), tetapi **bukan APK native**.
- Dukungan instalasi berbeda menurut browser dan perangkat. iOS umumnya menggunakan Share → Add to Home Screen.
- Cache offline hanya mencakup app shell dan berkas lokal. Fitur yang membutuhkan API/backend/jaringan tetap membutuhkan koneksi.
- Service worker memerlukan HTTPS pada hosting publik (atau localhost untuk pengujian).
- Sebelum produksi, uji semua alur pada perangkat fisik dan lakukan audit keamanan, aksesibilitas, performa, serta perilaku offline.


## Manifest PWA

`manifest.webmanifest` berisi identitas aplikasi, URL awal dan cakupan, mode standalone, orientasi portrait, warna tema/latar, kategori, serta ikon biasa dan maskable. Pastikan URL `start_url`, `scope`, dan jalur ikon tetap sesuai jika aplikasi diterbitkan di subfolder, bukan di root domain.
