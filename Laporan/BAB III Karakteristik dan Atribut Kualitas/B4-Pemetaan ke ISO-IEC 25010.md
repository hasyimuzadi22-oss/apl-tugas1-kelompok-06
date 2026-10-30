## B4. Pemetaan ke ISO/IEC 25010
 
| No. | Karakteristik Pendorong | Karakteristik Mutu Produk ISO/IEC 25010 | Subkarakteristik | Dasar Pemetaan dari B2 dan B3 |
|---|---|---|---|---|
| 1 | Akurasi (Deteksi Bentrok Jadwal) | Functional Suitability (Kesesuaian Fungsional) | Functional Correctness | B2 menetapkan target sistem mendeteksi 100% kasus bentrok pada minimal 20 skenario uji. B3 menggambarkan Komponen Validasi Bentrok yang dipanggil secara sinkron oleh Server Aplikasi Jadwal sebelum perubahan disimpan ke Basis Data Akademik. |
| 2 | Ketersediaan (Jam Sibuk Awal Semester) | Performance Efficiency (Efisiensi Kinerja) | Time Behaviour dan Capacity | B2 menetapkan target 95% halaman jadwal tampil dalam < 3 detik saat diakses 1.000 pengguna bersamaan. B3 menempatkan Server Aplikasi Jadwal pada server cloud kampus (struktur alokasi) yang menangani seluruh permintaan tampilan dan pengajuan perubahan jadwal. |
| 3 | Konsistensi Data (Lintas Modul) | Reliability (Keandalan) | Fault Tolerance | B2 menetapkan target perubahan jadwal tercermin di seluruh tampilan dalam < 5 detik setelah disetujui. B3 menggambarkan satu Basis Data Akademik terpusat yang diakses oleh Server Aplikasi Jadwal maupun Komponen Validasi Bentrok, sehingga seluruh tampilan membaca sumber data yang sama. |
 
