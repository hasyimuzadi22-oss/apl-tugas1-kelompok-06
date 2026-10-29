# BAB I Pendahuluan

## 1.1 Gambaran Subsistem dan Layanan Inti

Kelompok ini (I-6) ditugaskan menganalisis **Layanan jadwal kuliah dan ruang**, yang berada di bawah subsistem **Academic Management** pada Smart Campus UMI. Layanan ini mencakup empat fungsi utama:

- Menampilkan **jadwal pribadi** mahasiswa/dosen
- Memproses **perubahan jadwal** (misalnya karena bentrok atau permintaan dosen)
- Menyediakan **informasi ketersediaan ruang**
- Mendeteksi dan menangani **bentrok jadwal**, baik bentrok mata kuliah maupun bentrok pemakaian ruang

Layanan ini umumnya diakses melalui SIAKAD atau sistem akademik sejenis di lingkungan UMI.

## 1.2 Ruang Lingkup

Analisis dibatasi hanya pada layanan jadwal dan ruang, bukan keseluruhan subsistem Academic Management. Yang dibahas meliputi:

- Alur melihat jadwal
- Alur pengajuan dan persetujuan perubahan jadwal
- Mekanisme pengecekan ruang kosong
- Logika deteksi bentrok jadwal

Hal-hal di luar itu — seperti KRS, nilai, atau pembayaran — tidak dibahas karena merupakan layanan inti kelompok lain sesuai pembagian tugas.

## 1.3 Sumber Data

Data untuk layanan jadwal kuliah dan ruang dikumpulkan melalui:

1. **Pengalaman pengguna** — mencoba langsung fitur jadwal di SIAKAD, mencatat alur penggunaan, kendala yang ditemui, dan tangkapan layar sebagai bukti.
2. **Informasi publik** — merujuk pada situs umi.ac.id, panduan akademik, dan pengumuman resmi terkait jadwal dan penggunaan ruang.
3. **Wawancara singkat** dengan minimal 5 responden (mahasiswa serta staf/pengelola akademik terkait jadwal), dicatat sebagai R1–R5 tanpa identitas pribadi.
4. **Observasi langsung** terhadap kondisi ruang kelas dan proses penanganan bentrok jadwal di kampus.
