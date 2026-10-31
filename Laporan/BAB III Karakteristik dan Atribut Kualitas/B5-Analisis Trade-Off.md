## B5. Analisis Trade-Off

Sistem ini mencakup empat fitur: jadwal pribadi, perubahan jadwal, informasi ruang, dan deteksi bentrok. Analisis berikut membahas tiga pasangan karakteristik yang saling memengaruhi, lalu menetapkan karakteristik mana yang didahulukan beserta alasannya.

### Ringkasan

| No | Pasangan Karakteristik | Didahulukan | Dikorbankan (sebagian) | Keputusan Terkait |
|---|---|---|---|---|
| 1 | Akurasi deteksi bentrok vs Kecepatan respons | **Akurasi deteksi bentrok** | Kecepatan pengajuan perubahan | ADR-001 |
| 2 | Konsistensi data vs Ketersediaan | **Konsistensi data** | Ketersediaan saat sumber data terganggu | ADR-002 |
| 3 | Keamanan & auditabilitas vs Kinerja akses jadwal | **Keamanan & auditabilitas** | Kecepatan akses | RBAC dan audit log |

---

### 1. Akurasi Deteksi Bentrok vs Kecepatan Respons

| Aspek | Penjelasan |
|---|---|
| **Hubungan** | Agar bentrok tidak lolos, setiap pengajuan perubahan jadwal harus diperiksa terhadap jadwal dosen, jadwal kelas, dan pemakaian ruang sebelum disetujui. Pemeriksaan yang menyeluruh dan dilakukan langsung (sinkron) membutuhkan waktu pemrosesan. Pemeriksaan yang ditunda atau dilakukan di belakang layar akan lebih cepat, tetapi bentrok baru ketahuan setelah perubahan disetujui. |
| **Dampak** | Admin akademik dan dosen harus menunggu hasil pemeriksaan sebelum pengajuan diproses, sehingga proses terasa sedikit lebih lambat, terutama saat banyak pengajuan masuk bersamaan di awal semester. Sebaliknya, jika pemeriksaan dilewati demi kecepatan, dua kelas bisa terjadwal di ruang atau waktu yang sama dan harus dikoreksi manual setelah jadwal dipublikasikan. |
| **Yang didahulukan** | **Akurasi deteksi bentrok.** |
| **Alasan** | Bentrok jadwal berdampak langsung pada terhentinya kegiatan perkuliahan dan sulit diperbaiki setelah berjalan, sedangkan jeda pemeriksaan hanya berlangsung sesaat. Keputusan ini dituangkan dalam ADR-001. Dampak kecepatannya dapat ditekan dengan indeks basis data pada kolom waktu dan ruang, serta kueri pemeriksaan yang efisien. |

### 2. Konsistensi Data vs Ketersediaan

| Aspek | Penjelasan |
|---|---|
| **Hubungan** | Agar perubahan jadwal langsung tercermin di tampilan mahasiswa, dosen, dan informasi ruang, seluruh tampilan membaca satu sumber data terpusat. Konsekuensinya, jika sumber data ini bermasalah, semua tampilan ikut terganggu. Menyalin data ke tiap modul akan meningkatkan ketersediaan, tetapi membuka peluang data yang berbeda antartampilan. |
| **Dampak** | Gangguan pada basis data akademik terpusat berdampak luas karena menjadi titik tunggal kegagalan, terutama pada jam sibuk awal semester. Sebaliknya, jika memakai salinan data, mahasiswa bisa melihat ruang atau jam lama sementara admin sudah menyetujui perubahan, dan bentrok bisa tidak terdeteksi. |
| **Yang didahulukan** | **Konsistensi data.** |
| **Alasan** | Data yang tidak sinkron dapat menyebabkan bentrok tidak terdeteksi dan informasi yang menyesatkan, yang justru merusak tujuan utama sistem. Keputusan ini dituangkan dalam ADR-002. Risiko titik tunggal kegagalan dikurangi dengan pemantauan, pencadangan rutin, prosedur pemulihan, dan uji beban sebelum periode puncak. |

### 3. Keamanan & Auditabilitas vs Kinerja Akses Jadwal

| Aspek | Penjelasan |
|---|---|
| **Hubungan** | Otorisasi berbasis peran (RBAC) pada setiap endpoint dan pencatatan audit log (pelaku, waktu, data sebelum dan sesudah perubahan) menambah beban pemrosesan pada setiap permintaan. Di sisi lain, kinerja akses jadwal menuntut waktu tanggap yang cepat saat banyak pengguna membuka jadwal bersamaan. |
| **Dampak** | Setiap permintaan menjadi sedikit lebih lambat karena harus melewati pemeriksaan hak akses, dan setiap perubahan jadwal menambah proses penulisan log. Pemakaian *read-cache* untuk mempercepat tampilan jadwal juga harus dijaga agar tidak menampilkan data lama setelah ada perubahan yang disetujui. |
| **Yang didahulukan** | **Keamanan akses dan auditabilitas.** |
| **Alasan** | Perubahan jadwal hanya boleh dilakukan oleh pihak berwenang, dan setiap perubahan harus dapat ditelusuri untuk pertanggungjawaban serta kebutuhan auditor. Jeda beberapa milidetik jauh lebih murah daripada perubahan jadwal tanpa wewenang atau tanpa jejak. Dampak kinerja dapat ditekan dengan pencatatan audit secara asinkron, indeks basis data, pemisahan jalur baca dan tulis, serta *cache* yang dibersihkan otomatis setiap kali perubahan disetujui. Pemeriksaan bentrok tetap membaca sumber data terpusat, bukan *cache*, agar akurasi tidak terganggu. |

---

Urutan prioritas karakteristik pada sistem ini adalah: **(1) akurasi deteksi bentrok, (2) konsistensi data, (3) keamanan dan auditabilitas, lalu (4) kinerja dan ketersediaan**. Alasan utamanya, kesalahan pada jadwal kuliah berdampak langsung pada operasional akademik dan sulit diperbaiki setelah dipublikasikan, sedangkan keterlambatan respons atau gangguan singkat dampaknya jauh lebih kecil dan dapat dimitigasi melalui optimasi, pemantauan, dan pencadangan.
