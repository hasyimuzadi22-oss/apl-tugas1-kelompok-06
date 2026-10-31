# ADR-002: Data ruang dan jadwal disimpan terpusat, bukan disalin ke tiap modul

## Status

Proposed

## Context

Jika data jadwal/ruang disalin ke masing-masing tampilan (mahasiswa, dosen, admin), perubahan di satu tempat bisa tidak langsung muncul di tempat lain, menyebabkan informasi bentrok yang tidak konsisten.

## Decision

Kami akan menyimpan data jadwal dan ruang pada satu sumber data terpusat yang diakses oleh seluruh tampilan, bukan menyalin data ke masing-masing modul.

## Consequences

**Untung:**

- Konsistensi data terjaga.
- Bentrok terdeteksi lebih akurat.

**Rugi:**

- Seluruh tampilan bergantung pada ketersediaan sumber data terpusat ini, sehingga gangguan di sana berdampak luas.

## Compliance

- Diperiksa melalui code review setiap penambahan modul baru yang mengakses data jadwal/ruang.

---

[← Kembali ke daftar ADR](README.md)
