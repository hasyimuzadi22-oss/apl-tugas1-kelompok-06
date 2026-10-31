
## Ringkasan Wawancara 3

- **Tanggal:** [26-10-2026]
- **Responden (peran saja):** Dosen Program Studi
- **Pewawancara:** [Dwi Andhika Putra]
- **Layanan yang dibahas:** Jadwal mengajar dan pengajuan perubahan jadwal.

### Pertanyaan dan Ringkasan Jawaban

| Pertanyaan | Ringkasan jawaban |
|---|---|
| Bagaimana proses Ibu mengetahui jadwal dan ruang mengajar setiap semester? | Jadwal diperoleh dari SIAKAD atau pengumuman prodi, namun sesekali ditemukan jadwal mengajar yang berbenturan dengan kelas lain. |
| Bagaimana proses pengajuan perubahan jadwal ketika Ibu berhalangan hadir? | Pengajuan dilakukan secara manual melalui admin, lalu menunggu konfirmasi. Dosen tidak langsung tahu apakah usulan waktunya bentrok. |
| Kendala apa yang muncul saat jadwal pengganti ditetapkan? | Ruang yang diinginkan ternyata sudah terpakai, sehingga harus mencari alternatif waktu atau ruang berulang kali. |
| Seberapa penting pemeriksaan bentrok otomatis saat pengajuan dilakukan? | Sangat penting. Dosen berharap sistem langsung menampilkan peringatan jika waktu, ruang, atau pengajar bertabrakan sebelum pengajuan dikirim. |
| Bagaimana Ibu ingin diberi tahu setelah perubahan disetujui? | Melalui notifikasi di sistem dan perubahan langsung tampil pada jadwal mengajar serta jadwal mahasiswa. |
| Apa harapan Ibu terhadap layanan ini? | Pengajuan perubahan yang cepat, jelas statusnya (diajukan, disetujui, ditolak), dan hanya dapat dilakukan oleh pihak yang berwenang. |

### Temuan yang Dipakai dalam Laporan

| Temuan | Dipakai pada bagian laporan |
|---|---|
| Pengajuan perubahan dilakukan manual dan dosen tidak langsung tahu apakah usulannya bentrok (T3, T7). | Latar belakang 1.1; ASR akurasi deteksi bentrok; ADR-001 (pemeriksaan sinkron saat pengajuan). |
| Pencarian ruang dan waktu pengganti berulang karena ruang sudah terpakai (T5). | B3 fitur Deteksi Bentrok (penguncian slot ruang); Pendorong 1. |
| Dosen membutuhkan status pengajuan yang jelas (diajukan, disetujui, ditolak) (T7). | B3 fitur Perubahan Jadwal; alur persetujuan pada ADR-001. |
| Dosen ingin diberi tahu setelah perubahan disetujui dan melihat perubahan langsung di jadwal (T2). | ASR konsistensi data lintas modul; ADR-002. |
| Perubahan hanya boleh dilakukan pihak berwenang (T8). | Pendorong 2 (RBAC); A2 stakeholder (dosen: konsultasikan perubahan). |
