# BAB I. PENDAHULUAN
 
## 1.1 Latar Belakang
 
Layanan jadwal kuliah dan ruang merupakan komponen penting penunjang kegiatan akademik mahasiswa di kampus [1]. Berdasarkan pengamatan terhadap SIAKAD, pengelolaan jadwal saat ini berpotensi menimbulkan bentrok jadwal mata kuliah maupun ruang, karena verifikasi ketersediaan ruang dan jadwal dosen belum sepenuhnya terintegrasi secara otomatis [2]. Mahasiswa dan dosen sering kali baru mengetahui adanya bentrok setelah jadwal dipublikasikan, sehingga perubahan harus dilakukan secara manual dan memakan waktu [3]. Informasi ketersediaan ruang serta status perubahan jadwal pun belum selalu tersampaikan secara *real-time* kepada seluruh pihak terkait [3]. Oleh karena itu, diperlukan perancangan arsitektur perangkat lunak yang andal untuk mendukung layanan jadwal kuliah dan ruang pada subsistem *Academic Management*, agar proses penjadwalan, deteksi bentrok, dan informasi ruang berjalan lebih sistematis dan terpadu [4].
 
## 1.2 Tujuan Dokumen
 
Tujuan dari penyusunan dokumen arsitektur ini adalah:
 
1. Mendokumentasikan Kebutuhan Signifikan Arsitektur (ASR) yang digali dari kondisi nyata pengguna layanan jadwal dan ruang [1].
2. Merumuskan Keputusan Arsitektur (ADR) yang logis, seperti penerapan pemeriksaan bentrok secara sinkron saat pengajuan perubahan jadwal [2].
3. Memetakan rancangan sistem ke dalam tiga struktur arsitektur utama (Modul, *Component & Connector*, dan Alokasi) sebagai pedoman teknis bagi pengembang [1].
4. Menetapkan target metrik atribut kualitas (akurasi, ketersediaan, dan konsistensi data) beserta analisis kompromi (*trade-off*) dari sistem yang dirancang [1].
## 1.3 Ruang Lingkup Sistem
 
Ruang lingkup arsitektur yang dirancang berfokus pada empat fitur utama layanan jadwal kuliah dan ruang:
 
1. **Jadwal Pribadi:** Penyajian jadwal kuliah/mengajar yang dipersonalisasi untuk tiap mahasiswa dan dosen [3].
2. **Perubahan Jadwal:** Alur pengajuan dan persetujuan perubahan jadwal beserta validasi otomatis terhadap potensi bentrok [2].
3. **Informasi Ruang:** Penyediaan data ketersediaan ruang secara *real-time* untuk mendukung penjadwalan maupun penggunaan insidental [3].
4. **Deteksi Bentrok:** Mekanisme pemeriksaan otomatis terhadap bentrok jadwal mata kuliah maupun bentrok pemakaian ruang [2].
 
