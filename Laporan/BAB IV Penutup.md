## Kesimpulan

Dokumen ini merancang arsitektur layanan jadwal kuliah dan ruang pada subsistem Academic Management SIAKAD, yang mencakup empat fitur: jadwal pribadi, perubahan jadwal, informasi ruang, dan deteksi bentrok. Perancangan berangkat dari masalah bahwa verifikasi ketersediaan ruang dan jadwal dosen belum terintegrasi secara otomatis, sehingga bentrok baru diketahui setelah jadwal dipublikasikan dan harus diperbaiki secara manual.

Hasil perancangan dapat disimpulkan sebagai berikut:

1. **Konteks, stakeholder, dan batasan.** Analisis empat konteks (teknis, siklus hidup proyek, bisnis, dan profesional) menunjukkan bahwa arsitektur harus menjamin jadwal yang akurat, menjaga privasi dan tata kelola, bersifat modular, dan mudah dipelihara lintas semester. Admin akademik dan pengelola ruang dikelola secara intensif (*manage closely*), pimpinan akademik dan auditor dijaga kepuasannya (*keep satisfied*), sedangkan mahasiswa dan dosen diinformasikan dan dilibatkan melalui kanal umpan balik. Batasan seperti penggunaan basis data akademik yang sudah ada, akses lintas perangkat, kesiapan sebelum masa pengisian jadwal, dan tim IT yang kecil menuntut arsitektur yang sederhana dan mudah dipantau.

2. **Kebutuhan signifikan dan keputusan arsitektur.** Tiga ASR dirumuskan, yaitu akurasi deteksi bentrok, ketersediaan pada jam sibuk, dan konsistensi data lintas modul. Dua keputusan arsitektur diambil untuk menjawabnya:
   - **ADR-001:** pemeriksaan bentrok dilakukan secara sinkron saat pengajuan perubahan jadwal. Bentrok dicegah sejak awal, dengan konsekuensi proses pengajuan sedikit lebih lambat.
   - **ADR-002:** data jadwal dan ruang disimpan pada satu sumber data terpusat. Konsistensi tampilan terjaga, dengan konsekuensi seluruh tampilan bergantung pada ketersediaan sumber data tersebut.

3. **Karakteristik pendorong.** Evaluasi berdasarkan dampak struktural, keselarasan dengan tujuan stakeholder, dan keterukuran menghasilkan tiga karakteristik pendorong: (1) konsistensi dan deteksi bentrok, (2) keamanan akses dan auditabilitas, dan (3) kinerja akses jadwal. Ketersediaan, kemudahan pemeliharaan, dan kemudahan penggunaan ditetapkan sebagai karakteristik pendukung.

4. **Struktur desain dan ISO/IEC 25010.** Rancangan dipetakan ke tiga struktur desain: Jadwal Pribadi, Perubahan Jadwal dan Informasi Ruang, serta Deteksi dan Validasi Bentrok. Pemetaan ke ISO/IEC 25010 menghubungkan akurasi deteksi bentrok dengan *Functional Suitability*, ketersediaan pada jam sibuk dengan *Performance Efficiency*, dan konsistensi data lintas modul dengan *Reliability*.

5. **Analisis trade-off.** Arsitektur ini mendahulukan keamanan dan integritas data di atas kinerja, konsistensi data di atas ketersediaan, serta kemudahan penggunaan di atas fleksibilitas. Dampak tiap kompromi dikurangi melalui pencatatan audit asinkron, pengindeksan, pencadangan rutin, pemantauan sistem, serta template dan validasi otomatis.

Secara keseluruhan, arsitektur ini memprioritaskan kebenaran dan konsistensi jadwal, keamanan, dan keterlacakan perubahan di atas kecepatan dan fleksibilitas. Pilihan ini sesuai dengan sifat jadwal kuliah sebagai dasar operasional akademik, karena kesalahan di dalamnya jauh lebih mahal daripada jeda pemrosesan beberapa detik.

## Saran

1. **Verifikasi asumsi teknis SIAKAD.** Teknologi internal, skema basis data, dan kemampuan integrasi SIAKAD yang saat ini masih berupa asumsi perlu dikonfirmasi bersama tim IT kampus sebelum implementasi dimulai.

2. **Uji target metrik.** Lakukan pengujian skenario bentrok (termasuk akses bersamaan atau *concurrent write*) dan uji beban pada kondisi jam sibuk awal semester, untuk membuktikan bahwa target akurasi, waktu tanggap, dan konsistensi data benar-benar tercapai.

3. **Mitigasi titik tunggal kegagalan.** Karena pemeriksaan sinkron dan data terpusat membuat seluruh tampilan bergantung pada satu sumber data, siapkan pemantauan, pencadangan rutin, dan prosedur pemulihan yang jelas.

4. **Selesaikan pengujian sebelum periode puncak.** Pengujian dan rilis sebaiknya rampung jauh sebelum masa pengisian jadwal awal semester, mengingat sistem harus siap dan stabil pada periode tersebut.

5. **Tinjau status ADR bersama stakeholder.** ADR-001 dan ADR-002 masih berstatus *Proposed*. Tinjau setiap awal semester dan setiap penambahan modul baru, lalu ubah menjadi *Accepted* setelah disepakati admin akademik, pengelola ruang, dan tim pengembang.

6. **Jaga kesederhanaan operasional.** Pilih komponen yang mudah dipantau dan dipelihara agar sesuai dengan kapasitas tim IT kampus yang terbatas.

7. **Libatkan pengguna akhir.** Sediakan kanal umpan balik bagi mahasiswa dan dosen, serta lakukan sesi tinjauan kebutuhan dengan dosen, agar rancangan tetap sesuai dengan kebutuhan nyata.
