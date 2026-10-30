# B1. Kandidat Karakteristik Arsitektur

Dokumen ini mencatat identifikasi kandidat karakteristik arsitektur sistem pengelolaan jadwal akademik, kriteria pengujian untuk menyaring pendorong utama (*architectural drivers*), serta justifikasi teknis pemilihannya.

---

## 1. Identifikasi Kandidat Karakteristik

Kandidat dibagi menjadi tiga kelompok berdasarkan tingkat prioritas dan dampaknya terhadap arsitektur sistem.

### A. Kandidat Utama
Karakteristik yang berdampak langsung pada fondasi sistem dan sifatnya tidak bisa ditawar.

1. **Konsistensi Jadwal dan Deteksi Bentrok**
   * **Kategori:** Struktural, Eksplisit.
   * **Deskripsi:** Sistem harus menjamin tidak ada tumpang-tindih (*overlap*) antara jadwal dosen, ruang kelas, maupun alokasi waktu mahasiswa.
   * **Implikasi Teknikal:** Menentukan perancangan model data (*relational constraint* / *atomic transaction*) serta logika validasi ketat pada *application layer* sebelum data disetujui.

2. **Keamanan Akses**
   * **Kategori:** Lintas Sektor (*Cross-Cutting*), Eksplisit.
   * **Deskripsi:** Memastikan setiap pengguna hanya dapat melihat atau mengubah data sesuai batasan hak aksesnya.
   * **Implikasi Teknikal:** Memengaruhi arsitektur otentikasi (seperti JWT/OAuth2), skema otorisasi berbasis peran (*RBAC*), serta pengamanan di seluruh *endpoint API*.

3. **Auditabilitas Perubahan Data**
   * **Kategori:** Lintas Sektor (*Cross-Cutting*), Eksplisit.
   * **Deskripsi:** Setiap tindakan manipulasi data (tambah, ubah, hapus jadwal) harus terekam secara permanen untuk kebutuhan penelusuran masalah.
   * **Implikasi Teknikal:** Membutuhkan skema *log* terstruktur (*audit log*) yang mencatat identitas pelaku, waktu kejadian, serta perubahan nilai data (*before/after*) dengan kebijakan retensi penyimpanan tertentu.

4. **Kinerja Akses Jadwal**
   * **Kategori:** Operasional, Eksplisit.
   * **Deskripsi:** Kecepatan penayangan data jadwal saat diakses oleh pengguna dalam jumlah banyak.
   * **Implikasi Teknikal:** Menentukan strategi pembuatan indeks basis data, perancangan kueri yang efisien, hingga penerapan mekanisme *caching* untuk data yang sering dibaca.

---

### B. Kandidat Lanjutan
Karakteristik yang mendukung keandalan operasional dan kemudahan pengembangan jangka panjang.

5. **Ketersediaan Layanan (*Availability*)**
   * **Kategori:** Operasional, Implisit.
   * **Deskripsi:** Layanan harus siap digunakan terutama pada masa kritis seperti sebelum dan selama minggu perkuliahan berlangsung.

6. **Kemudahan Penggunaan (*Usability*)**
   * **Kategori:** Operasional, Implisit.
   * **Deskripsi:** Mahasiswa dan dosen dapat menemukan jadwal perkuliahan secara cepat tanpa alur navigasi yang membingungkan.

7. **Kemudahan Pemeliharaan (*Maintainability*)**
   * **Kategori:** Struktural, Implisit.
   * **Deskripsi:** Kode program dan aturan bisnis mudah disesuaikan ketika ada perubahan regulasi akademik di semester baru.

8. **Kompatibilitas dan Integrasi**
   * **Kategori:** Lintas Sektor, Eksplisit.
   * **Deskripsi:** Kemampuan bertukar data dengan sistem lain (misalnya sistem KRS, sistem kepegawaian, atau presensi) melalui kontrak API yang disepakati bersama.

---

### C. Kandidat Tambahan
Karakteristik pendukung pengalaman pengguna dan ketahanan sistem secara umum.

9. **Responsivitas Antarmuka**
   * **Kategori:** Operasional, Implisit.
   * **Deskripsi:** Tampilan antarmuka sistem dapat menyesuaikan layar dengan baik saat dibuka melalui perangkat seluler maupun komputer desktop.

10. **Pemulihan Kesalahan (*Fault Tolerance & Recovery*)**
    * **Kategori:** Operasional, Implisit.
    * **Deskripsi:** Ketika terjadi kegagalan sistem (seperti kueri gagal atau koneksi terputus), sistem dapat menangkap penanganan kesalahan (*error handling*) secara aman tanpa merusak data.

---

## 2. Kriteria Evaluasi dan Pengujian

Untuk menentukan apakah suatu kandidat layak dikategorikan sebagai **Karakteristik Pendorong (*Architectural Driver*)**, kandidat tersebut harus memenuhi **tiga ciri penguji**:

1. **Dampak Struktural/Teknologi:** Keberadaannya secara langsung menentukan pilihan pola arsitektur, struktur basis data, atau kerangka kerja teknologi yang digunakan.
2. **Keterkaitan dengan Tujuan Pemangku Kepentingan:** Berdampak luas terhadap kepuasan, keamanan, atau keberlangsungan operasional pengguna utama (akademik, dosen, mahasiswa).
3. **Dapat Dievaluasi:** Memiliki kriteria pengukuran yang realistis, baik melalui skenario pengujian beban (*load testing*), pengujian fungsional, maupun audit sistem.

---

## 3. Karakteristik Pendorong Terpilih (*Architectural Drivers*)

Berdasarkan evaluasi kriteria di atas, dipilihlah **tiga pendorong utama** yang menjadi fondasi perancangan arsitektur sistem ini:

### Pendorong 1: Konsistensi dan Deteksi Bentrok
* **Alasan Pemilihan:** Kesalahan jadwal (misalnya dua kelas berada di ruangan yang sama pada jam yang sama) berpotensi menghentikan operasional akademik secara langsung.
* **Fokus Arsitektur:** Penerapan *isolation level* transaksi basis data yang tepat serta modul validasi aturan bisnis (*business rule validation*) di tingkat *backend*.

### Pendorong 2: Keamanan Akses dan Auditability
* **Alasan Pemilihan:** Jadwal kuliah merupakan data krusial; perubahan tanpa wewenang dapat merusak perencanaan perkuliahan. Selain itu, jika terjadi kesalahan entri, sistem harus bisa melacak siapa yang melakukan perubahan dan kapan.
* **Fokus Arsitektur:** Penerapan middleware otorisasi berbasis peran (*RBAC*) pada seluruh *endpoint* serta pemisahan penyimpanan *audit log* agar tidak mudah dimanipulasi.

### Pendorong 3: Kinerja Akses Jadwal
* **Alasan Pemilihan:** Terdapat lonjakan akses yang signifikan (*peak traffic*) pada waktu-waktu tertentu, seperti hari pertama pengisian KRS atau minggu pertama perkuliahan.
* **Fokus Arsitektur:** Optimalisasi pencarian data melalui indeks basis data yang presisi, strategi pemisahan kueri baca/tulis, serta penggunaan *read-cache*.
