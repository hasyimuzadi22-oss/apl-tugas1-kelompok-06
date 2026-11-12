# U2. Skenario Atribut Kualitas

## 1. Pendahuluan

Skenario atribut kualitas merupakan gambaran kebutuhan kualitas yang harus dipenuhi oleh Layanan *Academic Management* (khususnya sub-modul Jadwal Kuliah dan Ruang) pada Sistem Informasi Akademik (SIAKAD) Universitas Muslim Indonesia (UMI). Skenario ini disusun berdasarkan tiga *Architectural Significant Requirements* (ASR) pada U1, yaitu keakuratan deteksi bentrok (*Performance Efficiency*), kemudahan akses informasi jadwal (*Usability*), serta keandalan pencatatan dan konsistensi data (*Reliability*).

Tujuan penyusunan skenario ini adalah memastikan sistem mampu memberikan layanan yang cepat, mudah digunakan, dan dapat diandalkan dalam mengelola operasional penjadwalan perkuliahan

---

## 2. Skenario Atribut Kualitas

### 2.1 ASR-1: Performance Efficiency (Performa & Deteksi Bentrok)

* **Sumber Stimulus:** Admin Akademik atau Dosen.
* **Stimulus:** Mengajukan penyusunan jadwal perkuliahan baru atau permohonan perubahan jadwal (*rescheduling*) secara dinamis.
* **Lingkungan:** Sistem berada dalam kondisi operasional normal maupun periode penyusunan jadwal di awal semester.
* **Artefak:** Modul Jadwal Kuliah dan Ruang (*Validation Engine* dan *Database Service*).
* **Respon:** Sistem melakukan verifikasi otomatis secara sinkron atas ketersediaan ruang, jam mengajar dosen, jadwal mahasiswa (termasuk lintas semester dan laboratorium terhadap teori), serta kapasitas fisik ruangan, lalu menolak transaksi jika ditemukan potensi bentrok sebelum data disimpan ke basis data.
* **Ukuran Respon:** Sistem menolak $100\%$ potensi bentrok (ruang, dosen, dan jadwal mahasiswa) serta kasus ketidaksesuaian kapasitas ruang, dengan durasi proses validasi transaksi backend $\le 500\text{ ms}$.

### 2.2 ASR-2: Usability (Kebergunaan)

* **Sumber Stimulus:** Mahasiswa dan Dosen (Pengguna Akhir).
* **Stimulus:** Mencari informasi jadwal pribadi, lokasi ruang kelas, perubahan jadwal (*rescheduling*), serta detail alokasi mata kuliah melalui perangkat seluler maupun komputer.
* **Lingkungan:** Sistem berada dalam kondisi operasional normal dan diakses secara harian oleh mahasiswa serta dosen.
* **Artefak:** Dasbor Jadwal Pribadi (*Personal Schedule Dashboard*), *API Gateway*, dan antarmuka pengguna (*Frontend Mobile/Web*).
* **Respon:** Sistem menampilkan tampilan jadwal secara visual yang jelas, terstruktur, konsisten, serta langsung mengirimkan notifikasi instan apabila terjadi perubahan jam atau ruang kepada mahasiswa dan dosen terkait.
* **Ukuran Respon:** Informasi jadwal ditampilkan dengan waktu tanggap kurang dari $1,5$ detik dan dapat ditemukan dalam maksimal $3$ kali klik.

### 2.3 ASR-3: Reliability (Keandalan)

* **Sumber Stimulus:** Admin Akademik / Sistem Backend yang memproses persetujuan perubahan jadwal.
* **Stimulus:** Menyetujui pengajuan perubahan jadwal atau perpindahan ruang yang berdampak pada pembaruan data secara masif di sistem.
* **Lingkungan:** Sistem sedang beroperasi aktif dan diakses oleh banyak pengguna secara bersamaan.
* **Artefak:** Layanan integrasi data terpusat, basis data relasional, dan modul *audit logging*.
* **Respon:** Setiap perubahan jadwal yang disetujui langsung disinkronkan, divalidasi, dan dicerminkan di seluruh tampilan dasbor secara terpusat, dengan data status ruang yang selaras dengan kondisi fisik di lapangan serta riwayat transaksi tercatat utuh.
* **Ukuran Respon:** Sistem mencapai keandalan pencatatan dan sinkronisasi sebesar $99,99\%$ dan memastikan data pembaruan jadwal yang berhasil diproses tidak hilang.

---

## 3. Kesimpulan

Sistem Informasi Akademik (SIAKAD) UMI pada layanan *Academic Management* harus mampu menangani validasi bentrok jadwal, menyediakan informasi jadwal dan perubahan yang mudah diakses, serta menjamin keandalan penyimpanan dan sinkronisasi data. Penerapan atribut *Performance Efficiency*, *Usability*, dan *Reliability* diharapkan dapat meningkatkan kualitas layanan akademik secara keseluruhan.
