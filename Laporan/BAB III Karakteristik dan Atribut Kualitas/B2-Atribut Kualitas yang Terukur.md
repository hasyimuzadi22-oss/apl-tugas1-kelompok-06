# B2. Evaluasi dan Karakteristik Pendorong

## 1. Kriteria Pengujian Karakteristik Arsitektur

Untuk menentukan apakah suatu kandidat karakteristik merupakan **Karakteristik Pendorong Utama** (*Architectural Driver*), kandidat tersebut dievaluasi berdasarkan tiga kriteria berikut:

* **(a) Dampak pada Keputusan Struktur:**
  Memaksa adanya keputusan teknis yang fundamental, seperti pemilihan pola arsitektur, pemisahan komponen, atau perancangan model data.

* **(b) Keselarasan dengan Tujuan Pemangku Kepentingan:**
  Berdampak langsung terhadap keberhasilan operasional dan nilai utama yang diharapkan oleh mahasiswa, dosen, serta staf akademik.

* **(c) Dapat Dievaluasi dan Diukur:**
  Memiliki kriteria keberhasilan yang jelas dan dapat diuji melalui skenario pengujian, pengukuran kinerja, atau validasi aturan.

## 2. Matriks Evaluasi Kandidat

| Kandidat Karakteristik | (a) Dampak Struktur | (b) Tujuan Pemangku Kepentingan | (c) Dapat Dievaluasi | Status |
| :--- | :---: | :---: | :---: | :---: |
| **Konsistensi & Deteksi Bentrok** | Ya | Ya | Ya | **Pendorong** |
| **Keamanan & Auditabilitas** | Ya | Ya | Ya | **Pendorong** |
| **Kinerja Akses** | Ya | Ya | Ya | **Pendorong** |
| Ketersediaan Layanan | Tidak langsung | Ya | Ya | Pendukung |
| Kemudahan Pemeliharaan | Tidak langsung | Ya | Ya | Pendukung |
| Kemudahan Penggunaan | Tidak | Ya | Sulit diukur | Pendukung |


## 3. Detail Analisis Karakteristik Pendorong

### Pendorong 1: Konsistensi Jadwal dan Deteksi Bentrok
* **Alasan Pemilihan:** Kesalahan atau bentrok jadwal (baik bentrok ruang, dosen, maupun mahasiswa) berdampak langsung pada terhentinya kegiatan akademik.
* **Dampak Arsitektur:** 
  * Penanganan transaksi data yang ketat untuk menjamin konsistensi.
  * Penerapan mesin validasi (*validation engine*) eksplisit yang memeriksa aturan bentrok sebelum jadwal disimpan.
* **Kriteria Pengujian:** Sistem menolak 100% dari minimal 100 skenario uji penyimpanan jadwal yang memiliki konflik waktu, ruang, atau pengajar, termasuk pada kondisi akses bersamaan (*concurrent write*).

### Pendorong 2: Keamanan Akses dan Auditabilitas
* **Alasan Pemilihan:** Perubahan jadwal hanya boleh dilakukan oleh pihak berwenang. Setiap riwayat perubahan harus dapat ditelusuri untuk kebutuhan pertanggungjawaban.
* **Dampak Arsitektur:**
  * Penerapan lapisan otorisasi berbasis peran (*Role-Based Access Control*) pada setiap titik masuk layanan (*API endpoint*).
  * Penyediaan mekanisme pencatatan log terstruktur (*structured logging*) yang terpisah dan aman dari modifikasi.
* **Kriteria Pengujian:** Pada pengujian beban dengan 1.000 pengguna bersamaan, 95% permintaan jadwal memiliki waktu tanggap server ≤ 300 ms dan 95% halaman jadwal tampil penuh dalam < 3 detik.

### Pendorong 3: Kinerja Akses Jadwal
* **Alasan Pemilihan:** Informasi jadwal harus dapat diakses dengan cepat, terutama pada periode puncak seperti minggu pertama perkuliahan atau masa pengisian KRS.
* **Dampak Arsitektur:**
  * Penggunaan indeks database yang optimal dan strategi *caching* untuk data jadwal yang sering dibaca.
  * Pemisahan jalur kueri (*read*) dan pembaruan (*write*) jika tingkat lalu lintas data sangat tinggi.
* **Kriteria Pengujian:** Waktu tanggap (*response time*) pencarian dan penayangan jadwal tidak melebihi $300\text{ ms}$ saat diakses oleh pengguna secara bersamaan.
