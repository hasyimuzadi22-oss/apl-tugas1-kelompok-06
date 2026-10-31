# ADR-001: Pemeriksaan bentrok dilakukan secara sinkron saat pengajuan perubahan jadwal

## Status

Proposed

## Context

Perubahan jadwal yang disetujui tanpa pengecekan bentrok dapat menyebabkan dua kelas terjadwal di ruang atau waktu yang sama, yang sulit diperbaiki setelah berjalan.

## Decision

Kami akan melakukan pemeriksaan bentrok jadwal dan ruang secara langsung (sinkron) begitu pengajuan perubahan dikirim, sebelum status perubahan disetujui.

## Consequences

**Untung:**

- Bentrok dapat dicegah sejak awal.
- Koreksi manual berkurang.

**Rugi:**

- Proses pengajuan perubahan jadi sedikit lebih lambat karena harus menunggu hasil pemeriksaan.

## Compliance

- Ditinjau tiap awal semester.
- Diuji dengan skenario pengajuan perubahan jadwal yang sengaja dibuat bentrok.

---

[← Kembali ke daftar ADR](README.md)
