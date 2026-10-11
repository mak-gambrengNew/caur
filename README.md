# DompetKu (PWA) + Supabase

Dompet digital dengan saldo, top up, bayar QRIS, dan riwayat transaksi yang tersimpan di server Supabase (project `caur`).

## Isi repo
```
index.html                      aplikasi lengkap (tampilan HP + semua halaman)
assets/asset1.png               logo header kiri atas dashboard
assets/asset2.png               logo "Powered by" di halaman input PIN
supabase/migrations/*.sql       skema tabel + fungsi server (wallet_snapshot, wallet_pay, wallet_topup)
supabase/seed.sql               data contoh (opsional)
```

## Menjalankan
Buka lewat server statis supaya folder `assets/` terbaca, mis. `python3 -m http.server 8000`, lalu buka `http://localhost:8000`.

## Mengganti logo
Timpa file di `assets/` dengan nama yang sama, tanpa mengubah kode.
- `asset1.png`: logo putih/transparan, tampil selebar sekitar 82 dp di header biru. Disarankan 3x (246x120 px) agar tajam.
- `asset2.png`: logo berwarna untuk latar gelap, tampil selebar sekitar 50 dp. Disarankan 420x120 px.

## Supabase
- Aplikasi memanggil fungsi RPC lewat `SB_URL` dan `SB_KEY` (kunci publishable) di `index.html`, pada skrip `dompetku-server`.
- Project baru: jalankan migrasi, lalu `seed.sql` (ganti PIN top up di dalamnya), lalu ubah `SB_URL` dan `SB_KEY`.
- Tabel dikunci RLS tanpa policy; semua akses lewat fungsi `SECURITY DEFINER`.
- Alur: top up memeriksa PIN di server; bayar QRIS memotong saldo dan mencatat riwayat dalam satu langkah; `ref` yang sama tidak dipotong dua kali.

## Catatan keamanan
Belum ada login. Siapa pun yang memegang kunci publik bisa memanggil `wallet_pay`. Tambahkan Supabase Auth atau PIN bayar di server sebelum dipakai umum.
