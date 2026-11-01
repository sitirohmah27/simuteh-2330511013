# SIMUTEH: Evaluasi Praktikum Computer Vision P1-P4

Sistem Pemeriksaan Mutu Daun Teh Berbasis Citra (tahap akuisisi dan praproses).

- Nama: Siti Rohmah Ramadhanti
- NIM: 2330511013
- SEED dataset sintetis: 1013 (4 digit terakhir NIM)

## Cara menjalankan
1. Pasang pustaka: `pip install -r requirements.txt`
2. Bangkitkan dataset dari folder utama repo: `python src/buat_dataset_sintetis.py`
3. Jalankan notebook di folder `notebook/` berurutan: B1, B2, B3, B4, B5
   (jalankan dari folder `notebook/` karena path memakai `../`).
4. Gambar, tabel .csv, dan `param_praproses.json` tersimpan di `hasil/`.

## Struktur
- `src/`: buat_dataset_sintetis.py, utils_cv.py, praproses.py
- `notebook/`: B1_lingkungan sampai B5_praproses
- `hasil/`: gambar, tabel, param_praproses.json
- `laporan/`: laporan dan slide

## Ringkasan hasil
- Kanal terbaik: R (KB tertinggi di kelima kondisi cahaya).
- Rangkaian praproses final: CLAHE (clip 1, tile 4) pada kanal V, lalu median 5x5.
- KB kanal R sebelum -> sesudah praproses naik di semua kondisi (+49% sampai +128%).
- Uji bercak palsu pada kelas sehat: simpangan baku daun turun (rasio 0,42-0,58), tidak ada bercak palsu.

## Catatan
Dataset sintetis, bukan acuan diagnosis penyakit tanaman.
Alat bantu AI generatif dipakai untuk membantu kode dan penjelasan konsep (lihat laporan, bagian Refleksi).
