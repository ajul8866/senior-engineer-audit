# Senior Engineer Audit

Skill untuk mengaudit bug fungsional dan keamanan melalui enam fase, dengan konfirmasi temuan dan pemeriksaan ulang oleh agen independen. Hasilnya berupa laporan bug bounty yang didukung bukti dan disiapkan untuk pengiriman manual.

Paket ini berisi instruksi bagi agen AI. Alur lengkap ada di [SKILL.md](SKILL.md), sedangkan format catatan, template laporan, dan kriteria siap kirim ada di [references/reporting.md](references/reporting.md).

## Cara kerja

1. **Petakan basis kode.** Kenali komponen, entrypoint, aliran data, batas kepercayaan, pengujian, dan cakupan program.
2. **Cari bug per area.** Telusuri perilaku nyata dan catat area yang sudah diperiksa, pengecualian, serta pemeriksaan yang terhalang.
3. **Konfirmasi setiap kandidat.** Agen baru yang bukan penemu mencoba membuktikan atau menyangkal dugaan menggunakan kode dan reproduksi.
4. **Tulis catatan terstruktur.** Simpan bukti, prasyarat, dampak, severity, putusan validator, dan hubungan duplikat.
5. **Verifikasi ulang setiap catatan.** Agen baru yang berbeda dari penemu dan validator pertama memeriksa klaim serta bukti secara independen.
6. **Tulis laporan akhir.** Buat laporan per temuan yang memenuhi kriteria, disertai indeks, cakupan pemeriksaan, keterbatasan, dan pekerjaan tertunda.

## Kebutuhan

- Agen AI yang dapat membaca berkas dan menjalankan pemeriksaan lokal yang relevan.
- Dukungan subagen dengan konteks baru untuk dua tahap verifikasi independen. Jika fitur ini tidak tersedia, status verifikasi harus tetap ditandai belum lengkap.
- Basis kode yang akan diaudit serta runtime dan dependensi yang diperlukan untuk reproduksi.
- Scope, pengecualian, dan aturan program untuk menentukan kelayakan laporan bug bounty. Jika belum tersedia, audit lokal tetap dapat berjalan dengan kelayakan bounty berstatus belum diketahui.

Pengujian target live mengikuti otorisasi dan aturan program yang tersedia. Utamakan reproduksi lokal dengan akun dan data sintetis.

## Cara pakai

Clone repositori ini:

```sh
git clone https://github.com/ajul8866/senior-engineer-audit.git
```

Berikan lokasi skill dan proyek kepada agen. Ganti path contoh berikut dengan lokasi sebenarnya:

```text
Baca /path/ke/senior-engineer-audit/SKILL.md, lalu jalankan alur enam fase
untuk repositori /path/ke/proyek.

Aturan program: /path/ke/program-rules.md.
Simpan hasil di /path/ke/hasil-audit, di luar repositori target.

Gunakan agen independen untuk mengonfirmasi setiap kandidat dan agen baru
yang berbeda untuk memverifikasi ulang setiap catatan. Siapkan laporan
bug bounty sesuai template program untuk dikirim manual.
```

Jika skill sudah terdaftar di lingkungan agen, gunakan `$senior-engineer-audit` untuk memanggilnya. Berkas [agents/openai.yaml](agents/openai.yaml) menyediakan metadata tampilan dan contoh pemanggilan.

## Hasil audit

```text
hasil-audit/
├── index.md
├── coverage.md
├── records/
│   └── C-001.md
├── evidence/
│   └── C-001/
└── reports/
    └── C-001.md
```

- `index.md`: ringkasan putusan, tautan laporan, keterbatasan, dan pekerjaan tertunda.
- `coverage.md`: area yang diperiksa beserta bukti, pengecualian, dan penghalangnya.
- `records/`: seluruh kandidat, termasuk dugaan yang ditolak, duplikat, dan kandidat dengan bukti belum cukup.
- `evidence/`: PoC dan bukti yang telah disanitasi.
- `reports/`: laporan untuk temuan yang lolos kriteria siap kirim.

Laporan siap kirim memerlukan bukti teknis, dua tahap verifikasi independen, reproduksi yang memadai, kelayakan sesuai aturan program, dampak yang didukung bukti, penanganan duplikat, dan sanitasi bukti. Bug fungsional tanpa dampak yang memenuhi kriteria bounty tetap dicatat sebagai observasi internal.

Bahasa dan format laporan mengikuti permintaan pengguna atau program. Skill menghasilkan laporan serta rekomendasi perbaikan; pengiriman laporan dilakukan manual. Cakupan yang tercatat membantu menunjukkan pekerjaan yang belum selesai, tanpa menjamin semua bug ditemukan atau laporan diterima program.
