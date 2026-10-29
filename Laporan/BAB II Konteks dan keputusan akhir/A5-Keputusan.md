## A5. Keputusan Arsitektur (ADR)

### ADR-001: Pemeriksaan bentrok dilakukan secara sinkron saat pengajuan perubahan jadwal

| Bagian | Isi |
|---|---|
| **Status** | Proposed |
| **Context** | Perubahan jadwal yang disetujui tanpa pengecekan bentrok dapat menyebabkan dua kelas terjadwal di ruang atau waktu yang sama, yang sulit diperbaiki setelah berjalan. |
| **Decision** | Kami akan melakukan pemeriksaan bentrok jadwal dan ruang secara langsung (sinkron) begitu pengajuan perubahan dikirim, sebelum status perubahan disetujui. |
| **Consequences** | **Untung:** bentrok dapat dicegah sejak awal, mengurangi koreksi manual. **Rugi:** proses pengajuan perubahan jadi sedikit lebih lambat karena harus menunggu hasil pemeriksaan. |
| **Compliance** | Ditinjau tiap awal semester; diuji dengan skenario pengajuan perubahan jadwal yang sengaja dibuat bentrok. |

### ADR-002: Data ruang dan jadwal disimpan terpusat, bukan disalin ke tiap modul

| Bagian | Isi |
|---|---|
| **Status** | Proposed |
| **Context** | Jika data jadwal/ruang disalin ke masing-masing tampilan (mahasiswa, dosen, admin), perubahan di satu tempat bisa tidak langsung muncul di tempat lain, menyebabkan informasi bentrok yang tidak konsisten. |
| **Decision** | Kami akan menyimpan data jadwal dan ruang pada satu sumber data terpusat yang diakses oleh seluruh tampilan, bukan menyalin data ke masing-masing modul. |
| **Consequences** | **Untung:** konsistensi data terjaga, bentrok terdeteksi lebih akurat. **Rugi:** seluruh tampilan bergantung pada ketersediaan sumber data terpusat ini, sehingga gangguan di sana berdampak luas. |
