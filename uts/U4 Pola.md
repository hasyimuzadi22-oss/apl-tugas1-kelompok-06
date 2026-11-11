# BAGIAN U4: POLA ARSITEKTUR (Architectural Patterns)

Pola arsitektur merupakan kerangka desain tingkat makro (*high-level architectural pattern*) yang mendefinisikan struktur organisasi sistem secara keseluruhan untuk mendukung taktik-taktik yang telah dipilih pada bagian U3.

---

### 1. Pola Utama yang Digunakan: *Layered Architecture* (N-Tier Architecture) dengan *Microservices-ready Modules*

* **Deskripsi Pola:** 
  Sistem Informasi Akademik (SIAKAD) UMI pada layanan *Academic Management* memisahkan tanggung jawab sistem ke dalam beberapa lapisan logis yang jelas (*separation of concerns*):
  * **Presentation Layer:** Antarmuka web dan seluler tempat mahasiswa dan dosen mengakses *Personal Schedule Dashboard*.
  * **API Gateway & Business Logic Layer:** Lapisan penanganan routing, autentikasi berbasis RBAC, serta penempatan *Validation Engine* untuk memproses aturan bisnis penjadwalan secara ketat.
  * **Data & Caching Layer:** Lapisan penyimpanan relasional utama (MySQL dengan kendali ACID) yang dikombinasikan dengan *Redis In-Memory Cache* untuk mempercepat akses baca (*read operations*).

---

### 2. Kesesuaian Pola Arsitektur dengan Karakteristik Pendorong (ASR)

* **Mendukung ASR-01 (Functional Correctness & Validation):**
  Lapisan logika bisnis menggunakan pola terpusat pada *Validation Engine* untuk memastikan setiap transaksi perubahan jadwal mematuhi batasan aturan akademik secara atomik sebelum mencapai basis data.

* **Mendukung ASR-02 (Performance & Availability):**
  Integrasi *Redis Cache Layer* pada arsitektur data memungkinkan pembacaan dasbor jadwal secara masif tanpa membebani basis data relasional utama, menjaga waktu tanggap $\le 300\text{ ms}$ di tengah lonjakan trafik pengguna.

* **Mendukung ASR-03 (Reliability & Data Integrity):**
  Penerapan basis data transaksional yang dipadukan dengan modul sinkronisasi asinkron memastikan integritas data status ruang dan catatan audit tetap terjaga sebesar $99,99\%$.
