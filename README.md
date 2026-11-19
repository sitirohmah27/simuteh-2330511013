# SIMUTEH: Sistem Inspeksi Mutu Daun Teh

Nama: Siti Rohmah Ramadhanti
NIM: 2330511013
SEED: 1013
Mata kuliah: Computer Vision

Repositori ini berisi kode, hasil, dan notebook praktikum SIMUTEH. Tujuannya menilai
mutu daun teh dari citra: mengukur persentase luas bercak dan menentukan kelas daun
(Sehat, Bercak Ringan, Bercak Berat). Data berupa 60 citra sintetis yang dibangkitkan
dengan SEED 1013.

## Struktur repositori

```
notebook/   B1-B5 (Pertemuan 1-4), P5_tepi, P6_morfologi
src/        praproses.py, utils_cv.py, utils_tepi.py, bercak.py,
            buat_dataset_sintetis.py
hasil/      tabel CSV, gambar PNG, param_praproses.json, param_bercak.json
data/       citra sintetis (dibangkitkan lewat skrip, tidak disertakan di ZIP)
laporan/    laporan praktikum
requirements.txt
```

## Cara menjalankan (Google Colab)

```
!git clone https://github.com/sitirohmah27/simuteh-2330511013.git
%cd simuteh-2330511013
!pip install -q -r requirements.txt
!python src/buat_dataset_sintetis.py
!jupyter nbconvert --execute --inplace notebook/P5_tepi.ipynb
!jupyter nbconvert --execute --inplace notebook/P6_morfologi.ipynb
```

Skrip `buat_dataset_sintetis.py` membangkitkan 60 citra di `data/sintetis` secara
deterministik (SEED 1013). Semua keluaran tersimpan di `hasil/`.

## Isi per tahap

| Tahap | Notebook | Isi |
|---|---|---|
| P1-P4 | B1-B5 | Praproses: resize, CLAHE kanal V, penapis median; parameter di `hasil/param_praproses.json` |
| P5 | P5_tepi | Gradien (Sobel, Prewitt, Laplacian, LoG), Canny, sigma dan ambang, ambang otomatis dan persentil, evaluasi tepi (presisi, recall, F1, toleransi 2 piksel) |
| P6 | P6_morfologi | Erosi, dilasi, opening, closing, gradien morfologi, elemen penstruktur, komponen terhubung, ukuran bercak, modul bercak dan evaluasinya |

## Modul bercak (`src/bercak.py`)

Alur: mask daun (Otsu pada saturasi) -> bercak awal (median + k x MAD pada kanal R)
-> opening lalu closing -> komponen terhubung konektivitas 8 -> penyaringan
(luas, kebulatan, rasio aspek) -> persentase luas bercak dan kelas.

Parameter akhir (`hasil/param_bercak.json`): kanal R, k = 4,0, SE elips 5x5,
luas minimum 20 piksel, kebulatan minimum 0,5, rasio aspek maksimum 1,8,
batas ringan 0,1% dan batas berat 2,0%, skala 0,4375 mm per piksel.

## Ringkasan hasil

- Canny pada kanal R setelah praproses memberi F1 tepi 0,984, lebih tinggi dari kanal Gray (0,890).
- Pembersihan morfologi (opening lalu closing) menurunkan komponen bercak palsu secara besar; penyaringan bentuk menurunkan galat jumlah bercak.
- Evaluasi 60 citra: galat absolut rerata persentase bercak 0,504, korelasi 0,928, akurasi kelas 0,917.

