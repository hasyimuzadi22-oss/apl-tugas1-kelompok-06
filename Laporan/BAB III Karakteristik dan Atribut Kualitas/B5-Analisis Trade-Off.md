## Analisis Trade-off: Layanan Penilaian Tugas

Sistem ini mencakup empat fungsi: rubrik, penilaian dosen, umpan balik, dan rekap nilai tugas.

### 1. Keamanan & Integritas Data vs Kinerja

| Aspek | Penjelasan |
|---|---|
| **Hubungan** | Kontrol keamanan seperti otorisasi per peran, enkripsi, dan pencatatan audit (siapa mengubah nilai, kapan, dari berapa ke berapa) menambah beban pemrosesan pada setiap permintaan. |
| **Dampak** | Penyimpanan dan penampilan nilai menjadi sedikit lebih lambat, terutama saat dosen menginput banyak nilai sekaligus menjelang batas waktu atau saat rekap diakses banyak pengguna. |
| **Yang didahulukan** | **Keamanan dan integritas data.** |
| **Alasan** | Nilai adalah data akademik yang sensitif dan berdampak langsung pada kelulusan mahasiswa. Nilai yang bisa diubah tanpa jejak, atau terlihat oleh pihak yang tidak berhak, jauh lebih merugikan daripada jeda beberapa detik. Dampak kinerja dapat ditekan dengan optimasi lain, misalnya pencatatan audit secara asinkron dan pengindeksan data. |

### 2. Konsistensi Data vs Ketersediaan

| Aspek | Penjelasan |
|---|---|
| **Hubungan** | Agar rekap nilai selalu akurat, setiap perubahan nilai atau bobot rubrik harus langsung tercermin di rekap dan tampilan mahasiswa. Hal ini membutuhkan sumber data tunggal dan transaksi yang ketat, sehingga sistem lebih rentan berhenti ketika sumber data bermasalah. Menyalin data ke banyak tempat (cache atau replika) akan meningkatkan ketersediaan, tetapi memungkinkan tampilan yang berbeda-beda. |
| **Dampak** | Jika basis data utama terganggu, penilaian dan penampilan rekap ikut terganggu. Sebaliknya, jika memakai salinan data, mahasiswa bisa melihat nilai lama sementara dosen sudah merevisinya. |
| **Yang didahulukan** | **Konsistensi data.** |
| **Alasan** | Nilai yang salah atau tidak sinkron dapat memicu keberatan akademik dan koreksi manual yang mahal. Gangguan singkat pada layanan masih bisa diterima karena penilaian tidak bersifat *real-time critical*. Pendekatan ini sejalan dengan ADR-002 (data terpusat), dan risikonya dikurangi dengan pencadangan rutin dan pemantauan sistem. |

### 3. Fleksibilitas Rubrik vs Kemudahan Penggunaan

| Aspek | Penjelasan |
|---|---|
| **Hubungan** | Semakin bebas dosen menyusun rubrik (jumlah kriteria, bobot, skala, deskripsi level), semakin rumit antarmuka dan aturan perhitungannya. |
| **Dampak** | Rubrik yang terlalu bebas membuat pembuatan rubrik lama, rawan salah bobot (misalnya total tidak 100%), dan rekap antar kelas sulit dibandingkan. Rubrik yang terlalu kaku tidak mengakomodasi karakteristik mata kuliah yang berbeda. |
| **Yang didahulukan** | **Kemudahan penggunaan.** |
| **Alasan** | Pengguna utama adalah dosen dengan waktu terbatas. Sistem yang rumit akan ditinggalkan atau diisi asal-asalan. Fleksibilitas tetap diberikan secara terbatas lewat template rubrik siap pakai yang dapat disesuaikan, dengan validasi otomatis seperti total bobot harus 100%. |

---
