## B4. Pemetaan ke ISO/IEC 25010

> Catatan: pemetaan ini didasarkan pada 3 karakteristik pendorong yang konsisten dengan ASR di BAB II (A4). Kalau hasil B1 kelompok memilih karakteristik pendorong yang berbeda, sesuaikan kolom pertama tabel ini.

| Karakteristik Pendorong | Karakteristik Mutu ISO/IEC 25010 | Penjelasan Singkat |
|---|---|---|
| Akurasi deteksi bentrok jadwal | **Functional Suitability** (sub: Functional Correctness) | Sistem harus menghasilkan hasil pemeriksaan bentrok yang benar sesuai data jadwal dan ruang, tanpa salah deteksi (false positive/negative). |
| Ketersediaan sistem saat jam sibuk (awal semester) | **Performance Efficiency** (sub: Time Behaviour) dan **Reliability** (sub: Availability) | Sistem harus tetap responsif dan dapat diakses meski banyak pengguna mengakses jadwal secara bersamaan. |
| Konsistensi data jadwal/ruang lintas modul | **Reliability** (sub: Fault Tolerance) | Perubahan jadwal harus tercermin konsisten di semua tampilan (mahasiswa, dosen, info ruang) agar tidak terjadi informasi yang saling bertentangan. |

**Catatan tambahan:** kelima karakteristik ISO/IEC 25010 lain (Compatibility, Usability, Security, Maintainability, Portability) tidak menjadi pendorong utama untuk layanan ini, tetapi tetap relevan sebagai pertimbangan sekunder — misalnya Usability untuk kemudahan mahasiswa melihat jadwal, dan Security untuk membatasi siapa yang bisa mengajukan perubahan jadwal.
