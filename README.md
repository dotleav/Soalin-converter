# Soalin-converter

Konverter docx → paket soal Soalin, jalan di browser (tanpa terminal, tanpa server).
Hasilnya satu file `.patch` yang cocok dengan struktur repo [dotleav/Soalin](https://github.com/dotleav/Soalin).

## Pakai

1. Buka halaman ini, pilih `.docx`, isi Kategori / Nama paket, klik **Konversi**.
2. Ulangi kalau ada beberapa docx. Cek field repo (`owner/repo@branch`, default `dotleav/Soalin@main`).
3. **Unduh .patch**, upload ke root repo Soalin (mis. di Codespaces), lalu:

```bash
git am soalin-hasil-konversi.patch      # langsung jadi commit
# atau
git apply --index soalin-hasil-konversi.patch
git push
```

## Isi patch

- `data/packages/<id>/questions.js` dan `images/packages/<id>/img-*.png` (gambar = binary patch)
- diff `data/manifest.js` (header & format sama dengan `scripts/convert-docx.js`)

`data/manifest.js` (dan `questions.js` kalau sudah ada) diambil dari GitHub saat unduh, jadi patch
dihitung terhadap isi repo terbaru. Kalau repo private/offline, tempel manifest manual di Langkah 3.

Re-convert paket yang sudah ada: hapus dulu `git rm -r data/packages/<id> images/packages/<id>`, commit, baru apply.
