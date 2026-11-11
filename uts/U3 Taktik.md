# BAGIAN U3: TAKTIK ARSITEKTUR (Architectural Tactics)

Taktik arsitektur merupakan keputusan desain berskala kecil yang digunakan untuk mengontrol dan memenuhi atribut kualitas spesifik pada Sistem Informasi Akademik (SIAKAD) Universitas Muslim Indonesia (UMI), khususnya pada sub-modul Jadwal Kuliah dan Ruang. Berikut adalah penjelasannya berdasarkan tiga ASR utama.

---

### 1. Taktik Skenario 1: Performance Efficiency (Performa & Akurasi Deteksi Bentrok)

* **Nama Taktik:** Synchronous Validation & Atomic Transaction Control (Validate Input & Maintain Transaction Integrity)
* **Atribut Kualitas:** Performance Efficiency (Time Behaviour & Functional Correctness)
* **Cara Kerja:**
  * Saat Admin Akademik atau Dosen mengajukan penyusunan jadwal baru maupun perubahan jadwal (*rescheduling*), Web Backend tidak langsung menyimpan data ke tabel utama basis data.
  * Permintaan terlebih dahulu dilewatkan ke komponen *Validation Engine* secara sinkron. Mesin validasi ini mengeksekusi kueri pengecekan bentrok (*conflict detection query*) yang mencakup ketersediaan ruang, jam mengajar dosen, jadwal mahasiswa lintas semester, bentrok laboratorium vs. teori, serta batas kapasitas fisik ruangan.
  * Seluruh proses pengecekan dan eksekusi simpan dibungkus dalam satu mekanisme *Atomic Database Transaction* (ACID compliance). Jika ditemukan satu saja potensi bentrok atau *overcapacity*, transaksi dibatalkan (*rollback*) seketika dan pesan kesalahan spesifik dikembalikan ke pengguna.
* **Harga yang Dibayar (Trade-off / Cost):**
  * **Peningkatan Waktu Respon Penulisan (*Latency Overhead*):** Proses validasi sinkron yang ketat menambahkan *overhead* waktu komputasi backend sebelum data berhasil disimpan.
  * **Risiko *Database Lock Contraction*:** Kuncian transaksi (*row/table locking*) saat validasi masif dapat menyebabkan antrean singkat pada proses penulisan data jadwal lainnya jika dilakukan secara bersamaan.

---

### 2. Taktik Skenario 2: Usability (Kemudahan Akses Dasbor & Informasi Jadwal)

* **Nama Taktik:** Support User Initiative & Maintain Data Copies (Read-Model Caching & Instant Push Notification)
* **Atribut Kualitas:** Usability (Operability, Learnability, & User Responsiveness)
* **Cara Kerja:**
  * Untuk memastikan mahasiswa dan dosen dapat mengakses dasbor jadwal pribadi serta rincian alokasi ruang dalam waktu kurang dari 1,5 detik dan maksimal 3 kali klik, sistem menyalin data jadwal yang telah terbit dari basis data utama ke *Redis In-Memory Cache*.
  * Saat pengguna membuka dasbor via aplikasi seluler atau web frontend, sistem membaca langsung data siap pakai dari Redis tanpa perlu melakukan kueri *join* relasional yang berat.
  * Selain itu, saat terjadi pembaruan jadwal/ruang oleh admin, sistem memanfaatkan komponen *Notification Gateway* untuk mengirimkan notifikasi *push* instan secara otomatis ke perangkat mahasiswa dan dosen terdampak.
* **Harga yang Dibayar (Trade-off / Cost):**
  * **Overhead Invalidation Cache:** Memerlukan penerapan logika pembersihan cache (*cache invalidation logic*) yang presisi. Setiap kali jadwal diubah atau disetujui, sistem harus memvalidasi dan memperbarui cache Redis secara tepat waktu agar tidak menampilkan data usang (*stale data*).
  * **Biaya Infrastruktur Layanan Notifikasi:** Membutuhkan integrasi dan pemeliharaan *broker* notifikasi (seperti Firebase Cloud Messaging atau WebSocket server) untuk pengiriman notifikasi secara real-time.

---

### 3. Taktik Skenario 3: Reliability (Keandalan Pencatatan & Sinkronisasi Lintas Modul)

* **Nama Taktik:** State Persistence & Asynchronous Event Audit (Event-Driven Synchronization & Audit Logging)
* **Atribut Kualitas:** Reliability (Fault Tolerance, Data Integrity, & Auditability)
* **Cara Kerja:**
  * Saat pengajuan perubahan jadwal atau alokasi ruang disetujui oleh pihak berwenang, sistem menerbitkan status perubahan tersebut ke *Event Publisher/Message Broker*.
  * Komponen *Sync Worker Service* menerima *event* tersebut dan menyinkronkan status ruang serta dasbor perkuliahan di seluruh modul terkait secara terpusat dalam waktu $< 5$ detik.
  * Pada saat yang sama, seluruh riwayat perubahan (siapa pengubah, waktu perubahan, ruang asal, dan ruang tujuan) dicatat secara *asynchronous* ke dalam *Audit Log Table* tanpa mengganggu alur utama transaksi, guna menjamin keandalan pencatatan hingga 99,99% dan mencegah kehilangan jejak audit.
* **Harga yang Dibayar (Trade-off / Cost):**
  * **Kompleksitas Asinkronus (*Eventual Consistency*):** Terdapat jeda waktu sangat kecil (beberapa milidetik hingga $< 5$ detik) antara persetujuan perubahan dengan konsistensi penuh tampilan di seluruh dasbor pengguna.
  * **Pertumbuhan Volume Data Log:** Pencatatan audit log secara menyeluruh memerlukan kapasitas penyimpanan basis data yang terus bertambah seiring tingginya frekuensi perubahan jadwal.
