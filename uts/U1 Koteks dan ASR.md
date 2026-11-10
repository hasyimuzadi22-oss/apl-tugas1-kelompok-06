## 1.1 Ringkasan Layanan
Layanan *Academic Management* (khususnya sub-modul Jadwal Kuliah dan Ruang) merupakan salah satu layanan inti pada Sistem Informasi Akademik (SIAKAD) Universitas Muslim Indonesia (UMI). Layanan ini bertanggung jawab dalam mengelola seluruh siklus alokasi perkuliahan, yang meliputi:
* Pembuatan dan penerbitan jadwal perkuliahan mingguan.
* Pengelolaan dan alokasi ruang kelas fisik beserta fasilitas penunjangnya.
* Pengaturan dan validasi jam mengajar dosen.
* Pengajuan dan persetujuan perubahan jadwal (*rescheduling*) secara dinamis.
* Penayangan dasbor jadwal pribadi (*personal schedule dashboard*) yang tersesuaikan untuk mahasiswa dan dosen.

---

## 1.2 Masalah Utama Layanan dan Bukti Empiris

### A. Masalah Utama
Pengelolaan jadwal perkuliahan pada SIAKAD saat ini berpotensi tinggi memicu **bentrok jadwal mata kuliah, ruang kelas, dan waktu mengajar dosen**. Hal ini terjadi karena proses verifikasi ketersediaan ruang dan jadwal dosen belum terintegrasi secara otomatis dan sinkron saat pengajuan perubahan maupun penyusunan awal. Akibatnya, mahasiswa dan dosen sering kali baru menyadari terjadinya *overlapping* setelah jadwal dipublikasikan, sehingga proses koreksi dilakukan secara manual, memakan waktu lama, dan mengganggu kelancaran perkuliahan awal semester.

### B. Bukti Empiris
1. **Ringkasan Wawancara Responden 1 ($R_1$ - Mahasiswa):**
   > *"Informasi perubahan jadwal atau perpindahan ruang biasanya saya terima terlambat, lewat grup chat atau dari teman, bukan dari SIAKAD. Bentrok jadwal juga baru ketahuan setelah jadwal dipublikasikan atau ketika perkuliahan hendak dimulai, karena sistem tidak memberikan notifikasi apa pun."*

2. **Ringkasan Wawancara Responden 2 ($R_2$ - Dosen / Admin Akademik):**
   > *"Pengajuan perubahan jadwal dari dosen sering disetujui tanpa pengecekan silang otomatis terhadap penggunaan ruangan oleh program studi lain. Verifikasi manual membutuhkan waktu hingga 2 hari kerja karena harus mengecek lembar penggunaan ruang secara terpisah."*

3. **Bukti Penggunaan / Tangkapan Layar:**
   Teridentifikasi dua mata kuliah berbeda (*TIF301 - Arsitektur Perangkat Lunak* dan *TIF305 - Grafika Komputer*) teralokasi di ruangan yang sama (*Lab Komputer 3*) pada slot waktu yang bersamaan (*Jumat, 09.30 WITA*).

---

## 1.3 Stakeholder Register dan Matriks Power/Interest

### A. Stakeholder Register
1. **Admin Akademik (Manajer Bisnis):** Memiliki tanggung jawab mengatur jadwal seluruh prodi, memverifikasi permohonan perubahan, dan mengelola alokasi ruang.
2. **Pengelola Ruang / Fakultas (Manajer Bisnis):** Mengawasi ketersediaan dan status penggunaan ruang kelas/laboratorium fisik agar tidak tumpang tindih.
3. **Dosen (Pengguna Akhir):** Membutuhkan kepastian jadwal mengajar yang akurat, tidak bentrok dengan agenda akademik lain, serta kemudahan dalam mengajukan *rescheduling*.
4. **Mahasiswa (Pengguna Akhir):** Membutuhkan tampilan jadwal pribadi yang konsisten, jelas, akurat, dan bebas bentrok di perangkat seluler maupun desktop.

### B. Kuadran Power / Interest
| Power \ Interest | Interest Rendah / Sedang | Interest Tinggi |
| :--- | :--- | :--- |
| **Power Tinggi** | Pimpinan Akademik, Auditor Mutu *(Keep Satisfied)* | **Admin Akademik, Pengelola Ruang** *(Manage Closely)* |
| **Power Rendah / Sedang** | Tim Operasional / Helpdesk *(Monitor)* | **Dosen, Mahasiswa** *(Keep Informed / Consult)* |

---

## 1.4 Architectural Significance Requirements (ASR)

* **ASR-01 (Akurasi Deteksi Bentrok - Functional Correctness):**
  Saat pengajuan perubahan atau penyusunan jadwal baru, sistem harus memvalidasi secara sinkron dan menolak $100\%$ potensi bentrok ruang, dosen, maupun jadwal mahasiswa sebelum data berhasil disimpan ke basis data.
* **ASR-02 (Ketersediaan Jam Sibuk - Performance & Availability):**
  Pada periode puncak (seperti minggu pertama perkuliahan dan pengisian KRS) dengan beban hingga $1.000$ pengguna bersamaan (*concurrent users*), sistem harus menjaga *availability* $99.9\%$ dengan waktu tanggap server (*response time*) $\le 300\text{ ms}$.
* **ASR-03 (Konsistensi Data Lintas Modul - Reliability & Data Integrity):**
  Setiap perubahan jadwal yang disetujui harus terintegrasi dan tercermin di seluruh tampilan dasbor (mahasiswa, dosen, serta informasi ruang) secara terpusat dalam waktu $< 5\text{ detik}$.

---

## 1.5 Karakteristik Pendorong (Architectural Drivers)

Berdasarkan analisis kebutuhan dan dampak strukturalnya, ditetapkan 3 Karakteristik Pendorong Utama:

1. **Konsistensi Jadwal dan Deteksi Bentrok (Utama):**
   * *Alasan:* Kesalahan jadwal berdampak langsung pada terhentinya operasional kegiatan belajar mengajar di kampus.
   * *Fokus Arsitektur:* Penerapan mesin validasi (*validation engine*) sinkron dan transaksi atomik pada lapisan backend.
2. **Keamanan Akses dan Auditabilitas (Utama):**
   * *Alasan:* Jadwal merupakan data akademik penting; perubahan tanpa wewenang dapat merusak sistem perkuliahan. Seluruh riwayat perubahan harus dapat ditelusuri.
   * *Fokus Arsitektur:* Penerapan *Role-Based Access Control* (RBAC) pada setiap REST API endpoint serta *asynchronous audit logging*.
3. **Kinerja Akses Jadwal (Utama):**
   * *Alasan:* Terdapat lonjakan pengaksesan (*peak traffic*) secara masif pada awal semester.
   * *Fokus Arsitektur:* Penerapan strategi *read-caching* (Redis) dan indeks kueri basis data teroptimasi.
