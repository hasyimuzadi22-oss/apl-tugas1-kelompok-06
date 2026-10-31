
## Ringkasan Wawancara 4

- **Tanggal:** [26-10-2026]
- **Responden (peran saja):** Dosen 
- **Pewawancara:** [Hasyim Muzadi]
- **Layanan yang dibahas:** Informasi ruang dan kebutuhan fasilitas perkuliahan.

### Pertanyaan dan Ringkasan Jawaban

| Pertanyaan | Ringkasan jawaban |
|---|---|
| Bagaimana Bapak biasanya memastikan ruang kuliah tersedia dan sesuai kebutuhan? | Pengecekan dilakukan dengan menghubungi staf atau melihat langsung ke ruangan, karena informasi ruang di sistem belum lengkap. |
| Informasi ruang apa yang paling dibutuhkan? | Kapasitas, ketersediaan proyektor, pendingin ruangan, dan status ruang (kosong, dipakai, atau pemeliharaan). |
| Pernahkah terjadi ruang tidak sesuai dengan jumlah mahasiswa? | Pernah, misalnya kelas besar ditempatkan di ruang berkapasitas kecil sehingga perkuliahan kurang nyaman. |
| Bagaimana kebutuhan ruang untuk kegiatan insidental seperti kuliah pengganti? | Dosen membutuhkan daftar ruang kosong pada waktu tertentu yang dapat dilihat langsung tanpa harus bertanya ke admin. |
| Apa risiko jika informasi ruang tidak diperbarui secara langsung? | Dua kegiatan dapat menggunakan ruang yang sama, atau ruang yang sedang dalam pemeliharaan tetap dipilih. |
| Apa saran Bapak untuk layanan informasi ruang? | Direktori ruang yang diperbarui langsung, dapat dicari berdasarkan waktu, kapasitas, dan fasilitas. |

### Temuan yang Dipakai dalam Laporan

| Temuan | Dipakai pada bagian laporan |
|---|---|
| Informasi ruang di sistem belum lengkap sehingga dosen mengecek langsung ke staf atau ruangan (T4). | Latar belakang 1.1; B3 fitur Informasi Ruang. |
| Informasi ruang yang dibutuhkan: kapasitas, proyektor, pendingin ruangan, dan status ruang (T4). | B3 fitur Informasi Ruang (direktori gedung dan ruang). |
| Kelas besar pernah ditempatkan di ruang berkapasitas kecil (T4). | Aturan validasi kapasitas pada validation engine (B3 fitur Deteksi Bentrok). |
| Daftar ruang kosong pada waktu tertentu dibutuhkan untuk kuliah pengganti (T4). | B3 fitur Informasi Ruang; Pendorong 1. |
| Informasi ruang yang tidak langsung diperbarui berisiko membuat ruang dipakai ganda atau ruang pemeliharaan terpilih (T5). | ASR konsistensi data lintas modul; ADR-002 (data terpusat). |
