# U7. ARCHITECTURAL DECISION RECORDS (ADR)

Dokumen *Architectural Decision Record* (ADR) ini mencatat keputusan-keputusan arsitektur penting yang diambil dalam perancangan **Sub-Modul Jadwal Kuliah dan Ruang** pada **Sistem Informasi Akademik (SIAKAD) Universitas Muslim Indonesia (UMI)**. Setiap ADR memuat konteks permasalahan, keputusan yang ditetapkan, serta konsekuensi teknis yang ditimbulkan.

---

## ADR-001: Implementasi Validation Engine Sinkron & Message Queueing (RabbitMQ) untuk Deteksi Bentrok & Sinkronisasi Notifikasi

* **Title**: ADR-001: Penerapan Validation Engine Sinkron dengan Atomic Transaction Control serta Message Queueing berbasis RabbitMQ untuk Sinkronisasi Jadwal dan Notifikasi Asinkron
* **Status**: Accepted
* **Context**:
  Proses penyusunan dan pengajuan perubahan jadwal perkuliahan (*rescheduling*) pada SIAKAD UMI sebelumnya rawan memicu bentrok jadwal mata kuliah, ruang kelas, jadwal laboratorium vs teori, waktu mengajar dosen, serta ketidaksesuaian kapasitas ruang terhadap jumlah mahasiswa terdaftar (ASR-01). Selain itu, perubahan jadwal yang disetujui berpotensi memicu lonjakan beban jaringan (*traffic spike*) saat ribuan mahasiswa dan dosen mengakses dasbor secara serentak pada periode puncak/awal semester (ASR-02). Jika pemrosesan perubahan dan pengiriman notifikasi dilakukan secara langsung (*synchronous write & push*), sistem berisiko mengalami *HTTP 504 Gateway Timeout* dan ketidaksinkronan data status ruang.
* **Decision**:
  1. Mengimplementasikan **Validation Engine secara sinkron** di lapisan backend yang dibungkus *Atomic Database Transaction (ACID)* untuk memvalidasi 100% ketersediaan ruang, jam mengajar dosen, jadwal mahasiswa (termasuk lintas semester dan lab vs teori), serta kapasitas fisik ruangan sebelum transaksi disimpan (*commit*) ke basis data utama.
  2. Mengimplementasikan **RabbitMQ sebagai Message Broker** dengan pola *Event-Driven Architecture (EDA)*. Setiap transaksi perubahan jadwal yang berhasil disetujui akan menerbitkan *event* ke antrean asinkron (*message queue*) untuk diproses oleh *background worker* guna menyinkronkan data lintas modul dan mengirimkan *push notification* via Firebase Cloud Messaging (FCM).
* **Consequences**:
  * **Positif**: Terhindar 100% dari potensi jadwal bentrok dan *overcapacity* ruang kelas sebelum data tersimpan, sistem terbebas dari risiko *crash* saat lonjakan akses jadwal di awal semester, waktu tanggap *frontend* dasbor tetap konsisten $\le 300\text{ ms}$, dan mampu menampung 1.000+ pengguna serentak dengan *downtime* 0% (*availability* 99,9%).
  * **Negatif**: Proses validasi sinkron yang ketat menambah sedikit *overhead* waktu komputasi penulisan (*latency overhead* backend $\le 500\text{ ms}$), serta terdapat jeda waktu sangat kecil (*eventual consistency delay* $<5\text{ detik}$) sebelum seluruh pengguna menerima notifikasi konfirmasi perubahan jadwal secara resmi.

---

## ADR-002: Separasi Read-Model (Redis Caching) dan Relational Database Transaction (ACID) untuk Layanan Jadwal SIAKAD UMI

* **Title**: ADR-002: Penggunaan Redis In-Memory Caching untuk Pembacaan Dasbor Jadwal Pribadi & Transaksi RDBMS (ACID) untuk Manajemen Ruang dan Audit Logging
* **Status**: Accepted
* **Context**:
  Sistem membutuhkan performa pencarian dan penayangan informasi dasbor jadwal pribadi (*Personal Schedule Dashboard*) bagi mahasiswa dan dosen yang cepat ($<1{,}5\text{ detik}$ dan $\le 3\text{ kali klik}$) pada perangkat seluler maupun desktop (ASR-02). Di sisi lain, sistem harus menjamin keandalan pencatatan transaksi perubahan jadwal, konsistensi status penggunaan ruang kelas fisik, serta *audit trail* agar tidak ada riwayat perubahan yang hilang (*reliability* 99,99%) (ASR-03).
* **Decision**:
  1. Menggunakan **Redis In-Memory Caching** untuk melayani kueri pembacaan dasbor jadwal perkuliahan mingguan dan ketersediaan ruang secara terpisah (*read-model*), sehingga *frontend* membaca data langsung dari *cache* tanpa melakukan *query join* relasional yang berat.
  2. Menggunakan **Relational Database Management System (RDBMS - MySQL Cluster)** dengan dukungan transaksi ACID untuk modul validasi jadwal, alokasi master ruang, dan pencatatan *audit log* transaksi perubahan.
* **Consequences**:
  * **Positif**: Dasbor jadwal pribadi dan rincian alokasi ruang dapat diakses secara instan dengan waktu tanggap $<1{,}5\text{ detik}$ tanpa membebani basis data relasional utama. Data transaksi perubahan jadwal dan *audit log* tersimpan secara permanen, aman, dan terstruktur tanpa risiko kehilangan data (*persistence & reliability* 99,99%).
  * **Negatif**: Memerlukan penerapan logika pembersihan memori (*cache invalidation logic*) yang presisi pada Redis setiap kali terjadi persetujuan perubahan jadwal atau penyesuaian status ruang fisik oleh admin/pengelola ruang, guna mencegah tampilan data lama (*stale data*).
