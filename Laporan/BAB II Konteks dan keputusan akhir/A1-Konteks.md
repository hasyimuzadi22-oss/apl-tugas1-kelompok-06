# A1. Analisis Empat Konteks Arsitektur

## 1. Ringkasan Empat Konteks

| No | Konteks | Uraian |
|----|---------|--------|
| 1 | Konteks Teknis | Layanan diasumsikan diakses melalui peramban pada ponsel dan komputer. Rancangan mengusulkan antarmuka web responsif, layanan aplikasi, validasi domain jadwal, dan penyimpanan terpusat. Teknologi internal yang digunakan SIAKAD belum diverifikasi. |
| 2 | Konteks Siklus Hidup Proyek | Layanan perlu dirancang, diuji, dirilis, dipantau, dan dipelihara lintas semester. Aturan jadwal dapat berubah mengikuti kebijakan akademik. Oleh karena itu, aturan validasi dan akses data perlu dipisahkan agar dapat diuji dan diperbarui dengan risiko yang lebih rendah. |
| 3 | Konteks Bisnis | Tujuan utama adalah membantu mahasiswa dan dosen memperoleh jadwal yang benar, serta membantu admin mengelola perubahan dan ruang tanpa bentrok. Nilai bisnis berasal dari pengurangan kesalahan informasi, transparansi perubahan, dan efisiensi koordinasi. |
| 4 | Konteks Profesional | Rancangan harus menghormati privasi, kewenangan perubahan jadwal, dan tata kelola kampus. Keputusan penting harus terdokumentasi. Kebutuhan dan batasan yang belum terverifikasi harus dinyatakan sebagai asumsi, bukan fakta. |

## 2. Keterkaitan Konteks

| No | Konteks | Kebutuhan | Dampak pada Arsitektur |
|----|---------|-----------|------------------------|
| 1 | Konteks Bisnis | Kebutuhan akan jadwal yang akurat | Mendorong penerapan validasi bentrok |
| 2 | Konteks Profesional | Kebutuhan akan privasi dan tata kelola | Mendorong penerapan otorisasi dan audit |
| 3 | Konteks Teknis | Kebutuhan akan sistem yang terstruktur | Mendorong pemisahan modul |
| 4 | Konteks Siklus Hidup Proyek | Kebutuhan pemeliharaan jangka panjang | Mendorong pengujian otomatis dan dokumentasi keputusan |
