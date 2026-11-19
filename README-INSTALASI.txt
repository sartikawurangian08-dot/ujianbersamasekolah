APLIKASI UJIAN BERSAMA V3.1 — PAKET PWA SIAP DEPLOYMENT

PERSYARATAN HOSTING
- PHP 8.1 atau lebih baru
- MySQL 5.7+ / MariaDB 10.4+
- Ekstensi PDO MySQL aktif
- SSL/HTTPS aktif
- Hosting Linux/cPanel disarankan

LANGKAH INSTALASI CPANEL
1. Login cPanel sekolah.
2. Buka MySQL® Databases, buat database, user, lalu hubungkan user ke database dengan ALL PRIVILEGES.
3. Buka phpMyAdmin, pilih database, lalu Import file database.sql.
4. Buka File Manager > public_html. Buat folder ujian (atau folder sesuai subdomain).
5. Upload Aplikasi_Ujian_Bersama_V2.zip lalu Extract. Pastikan index.php berada langsung di folder /ujian, bukan di subfolder bersarang.
6. Salin config.example.php menjadi config.php. Edit empat nilai database: db_host, db_name, db_user, db_pass. Host umumnya localhost, tetapi ikuti data dari penyedia hosting.
7. Buka https://DOMAIN-SEKOLAH/ujian/ untuk memastikan halaman login tampil.
8. Buat admin pertama dengan cara menjalankan hash password melalui PHP CLI atau buat file sementara create_admin.php berisi:
   <?php echo password_hash('PASSWORD-KUAT-ANDA', PASSWORD_DEFAULT);
   Jalankan sekali, salin hash yang keluar, lalu hapus create_admin.php.
   Di phpMyAdmin jalankan:
   INSERT INTO users(name,username,password_hash,role,active)
   VALUES('Administrator','admin','TEMPEL_HASH_DI_SINI','admin',1);
   Jangan gunakan password contoh. Hapus file sementara setelah selesai.
9. Login, buka Ubah Password, lalu buat akun guru, pengawas, dan siswa.
10. Buat mata pelajaran, jadwal ujian, dan soal. Uji dengan akun dummy sebelum ujian resmi.

CATATAN PENTING
- Cookie sesi disetel secure=true. Sistem harus dijalankan melalui HTTPS.
- Paket ini merupakan versi operasional awal untuk staging/pilot. Sebelum ujian resmi berskala besar, lakukan uji beban, audit keamanan independen, backup-restore test, dan uji pemulihan koneksi.
- PWA tidak mengunci perangkat. Safe Exam Browser harus dikonfigurasi terpisah dan diuji di perangkat sekolah.
- Auto-save membutuhkan koneksi internet aktif; paket ini belum menyediakan sinkronisasi offline penuh.
- Guru dan admin berbagi kewenangan pengelolaan soal/ujian dalam versi ini. Pembatasan kepemilikan data guru dapat diperketat pada pengembangan berikutnya.
- Fitur pengacakan opsi menyajikan opsi dalam urutan berbeda; kunci tetap berdasarkan label jawaban. Uji skenario acak sebelum ujian nyata.
- Ekspor CSV tersedia untuk rekap hasil. Koreksi esai dilakukan oleh guru/admin.
- Backup database secara rutin sebelum dan setelah setiap periode ujian.


PWA / PEMASANGAN DI HP
- Upload seluruh isi folder aplikasi ke hosting HTTPS. Jangan hanya mengunggah index.php.
- Android: buka link aplikasi di Chrome. Pilih menu ⋮ > Install app / Tambahkan ke layar utama.
- iPhone/iPad: buka link melalui Safari > tombol Bagikan > Add to Home Screen / Tambahkan ke Layar Utama.
- Admin, guru, dan pengawas menggunakan link yang sama; menu akan menyesuaikan peran akun.
- PWA tetap membutuhkan internet untuk login, membuka ujian, dan menyimpan jawaban. Cache offline hanya menyediakan halaman informasi saat koneksi terputus; ujian offline belum didukung.
- Setelah update, bila ikon/tampilan lama masih muncul, tutup aplikasi dan muat ulang. Service worker memakai cache versi baru.
- Pastikan domain menggunakan HTTPS dan file assets/icons tersedia.

CATATAN PEMERIKSAAN V3
- Cookie sesi secure disesuaikan dengan HTTPS agar localhost HTTP dapat dipakai untuk pengujian; produksi wajib HTTPS.
- Perbaikan pemeriksaan ID peserta saat mengakhiri ujian.
- Nilai total dihitung ulang setelah koreksi esai.
- Dashboard disesuaikan untuk peran siswa dan petugas serta memiliki akses cepat dan aktivitas terbaru.
- Manifest, ikon instalasi Android/iOS, dan service worker diperbarui. Data halaman login/ujian tidak dimasukkan ke cache agar tidak menyimpan konten privat.


PANDUAN LENGKAP PEMULA: lihat PANDUAN-DEPLOYMENT-PEMULA.txt.
