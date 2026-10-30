# Tiga Desain Struktur 

1. Desain Fitur Jadwal Pribadi (*Personal Schedule Dashboard*)
   - **Deskripsi Fungsional:** Halaman atau antarmuka khusus yang dirancang secara personal bagi setiap pengguna (mahasiswa maupun dosen) untuk melihat daftar mata kuliah, kegiatan akademik, dan slot waktu yang menjadi tanggung jawab atau pilihan mereka dalam satu tampilan terpusat.
   - **Komponen Antarmuka:**
     - Tampilan kalender mingguan atau bulanan (*grid view*).
     - Indikator warna yang berbeda untuk setiap mata kuliah atau status kehadiran.
     - Tombol pintas untuk melihat detail silabus, tautan kelas daring, atau lokasi ruangan fisik secara spesifik.
   - **Tujuan Arsitektur:** Memudahkan pengguna memantau agenda harian mereka tanpa harus menyaring data dari seluruh jadwal program studi yang ada di kampus.

2. Desain Fitur Perubahan Jadwal & Informasi Ruang (*Schedule Updates & Room Information*)
   - **Deskripsi Fungsional:** Modul yang menangani pengumuman, pembaruan (*rescheduling*), pembatalan kelas, serta direktori ketersediaan ruang kelas secara *real-time*.
   - **Komponen Antarmuka:**
     - Panel notifikasi/pemberitahuan langsung (*live banner*) jika terjadi perpindahan jam atau ruangan.
     - Fitur direktori gedung dan ruangan kampus yang menampilkan status ruangan (sedang dipakai, kosong, atau dalam pemeliharaan) beserta kapasitas dan fasilitasnya (proyektor, AC, kapasitas kursi).
   - **Tujuan Arsitektur:** Mengakomodasi fleksibilitas operasional kampus ketika dosen berhalangan hadir atau ketika terjadi pemindahan lokasi kuliah secara mendadak.

3. Desain Fitur Deteksi & Validasi Bentrok Jadwal (*Conflict Detection & Validation Engine*)
   - **Deskripsi Fungsional:** Sistem otomatis di balik layar (*backend logic* dan antarmuka validasi) yang bertugas mendeteksi secara dini potensi terjadinya tumpang tindih waktu, dosen, maupun penggunaan ruang kelas.
   - **Komponen Antarmuka:**
     - Peringatan visual berwarna merah atau *popup warning* saat admin akademik atau mahasiswa mencoba memilih jadwal yang waktunya bersinggungan.
     - Matriks pengecekan ketersediaan ruangan yang langsung mengunci (*lock*) slot ruangan begitu sebuah kelas dikonfirmasi.
   - **Tujuan Arsitektur:** Mencegah terjadinya kesalahan alokasi sumber daya kampus (seperti dua kelas memakai satu ruangan di jam yang sama) sebelum jadwal tersebut disahkan dan dipublikasikan ke sistem utama.
