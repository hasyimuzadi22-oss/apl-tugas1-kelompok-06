# B1. Kandidat Karakteristik Arsitektur

### Kandidat Utama
* **Konsistensi jadwal dan deteksi bentrok** (Struktural, Eksplisit)
  Menentukan model data dan aturan validasi sistem.
* **Keamanan akses** (Lintas Sektor, Eksplisit)
  Berdampak pada mekanisme autentikasi, otorisasi, serta perlindungan seluruh *endpoint*.
* **Auditabilitas perubahan** (Lintas Sektor, Eksplisit)
  Memerlukan pencatatan log terstruktur dan kebijakan retensi data.
* **Kinerja akses jadwal** (Operasional, Eksplisit)
  Menentukan strategi indeks basis data serta optimasi kueri.

### Kandidat Lanjutan
* **Ketersediaan layanan** (Operasional, Implisit) — Layanan harus tetap aktif sebelum dan selama periode perkuliahan.
* **Kemudahan penggunaan** (Operasional, Implisit) — Pengguna dapat menemukan informasi jadwal dengan cepat.
* **Kemudahan pemeliharaan** (Struktural, Implisit) — Fleksibel terhadap perubahan aturan bisnis yang bisa berubah tiap semester.
* **Kompatibilitas / Integrasi** (Lintas Sektor, Eksplisit) — Pertukaran data antar sistem harus berjalan sesuai kontrak/API yang disepakati.

### Kandidat Tambahan
* **Responsivitas antarmuka** (Operasional, Implisit) — Akses optimal baik melalui perangkat seluler maupun desktop.
* **Pemulihan kesalahan** (Operasional, Implisit) — Sistem mampu mendeteksi kegagalan dan memiliki penanganan yang jelas.

---

## Kriteria Penilaian Karakteristik

Suatu karakteristik dikategorikan sebagai **pendorong (driver)** apabila memenuhi tiga syarat berikut:
1. Berdampak langsung pada keputusan struktur atau pilihan teknologi.
2. Selaras dengan tujuan utama para *stakeholder*.
3. Dapat diukur atau dievaluasi melalui skenario pengujian tertentu.

*Konsistensi, keamanan/audit, dan kinerja akses telah memenuhi ketiga kriteria di atas.*

---

## Karakteristik Pendorong Terpilih

1. **Konsistensi & Deteksi Bentrok**
   Kesalahan pada penjadwalan berdampak langsung pada kelancaran seluruh kegiatan akademik.
2. **Keamanan & Auditabilitas**
   Setiap perubahan data wajib dilakukan oleh pihak yang berwenang dan memiliki rekam jejak yang dapat ditelusuri.
3. **Kinerja Akses**
   Informasi jadwal harus dapat diakses dengan cepat, terutama pada periode puncak (*traffic peak*).
