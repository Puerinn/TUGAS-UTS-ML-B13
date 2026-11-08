# B13 – Karakteristik Kejadian Gempa Indonesia (Milestone 1 UTS)

**Project ID:** B13
**Mata kuliah:** Pembelajaran Mesin (Semester Ganjil TA. 2026–2027)
**Nama Kelompok:** Kelompok 9

**Anggota:**
- Dedi Sanjaya Nainggolan (231111885)
- Erico Adelorenzo Samosir (231112600)
- Andi Aziz Prasetyo (231112637)

## Deskripsi Masalah

Indonesia terletak di pertemuan beberapa lempeng tektonik sehingga gempa terjadi hampir setiap hari dengan karakter yang beragam. Proyek ini mengkaji apakah kejadian gempa membentuk kelompok atau pola yang dapat ditemukan secara otomatis, dan fitur apa yang membawa pola itu (waktu, lokasi, kedalaman, atau magnitudo). Pendekatan yang dipakai adalah unsupervised classical ML: PCA, t-SNE, dan UMAP untuk reduksi dimensi, serta K-Means, GMM, dan DBSCAN untuk clustering, pada katalog USGS wilayah Indonesia periode 2010–2025 dengan magnitudo ≥ 4,0. Proyek ini tidak bertujuan memprediksi gempa.

Pertanyaan analisis:
1. Berapa dimensi efektif data gempa, dan fitur mana yang paling banyak menjelaskan variasinya?
2. Apakah ada kelompok gempa yang dapat ditemukan, dan apakah reduksi dimensi memperbaikinya dibandingkan tanpa reduksi?
3. Apakah fitur waktu (bulan dan jam) membentuk struktur, atau hanya menambah derau?
4. Apakah struktur yang ditemukan pada 2010–2017 masih berlaku pada 2018–2025?
5. Apakah cluster berdasarkan lokasi mengikuti zona seismik dan berkaitan dengan kedalaman?

## Isi Repositori

| Berkas | Keterangan |
|---|---|
| `README.md` | Dokumentasi repositori (file ini) |
| `notebook_uts_gempa_B13.ipynb` | Notebook eksperimen lengkap (bagian 1–8, mengikuti komponen A–I laporan) |
| `Laporan_UTS_B13_Kelompok9.pdf` | Laporan Milestone 1 (PDF untuk dikumpulkan) |
| `Laporan_UTS_B13_Kelompok9.docx` | Versi Word laporan (sumber yang bisa diedit) |
| `gempa_indonesia_bersih.csv` | Data kerja: 25.057 kejadian, hasil penyaringan wilayah dari katalog USGS |
| `tabel_hasil_eksperimen_awal.csv` | Ringkasan hasil eksperimen awal yang dikutip di laporan |
| `hasil_eksperimen_uts.csv` | Tabel hasil lengkap keluaran notebook (semua model, metrik, dan perbandingan ruang yang sama) |
| `requirements.txt` | Library Python yang dibutuhkan |

## Sumber Data

USGS Earthquake Catalog (ComCat), U.S. Geological Survey
- Pencarian: https://earthquake.usgs.gov/earthquakes/search/
- API (FDSN Event Web Service): https://earthquake.usgs.gov/fdsnws/event/1/
- Parameter: format CSV, lintang −11 s.d. 6, bujur 95 s.d. 141, 2010-01-01 s.d. 2025-12-31, magnitudo ≥ 4,0
- Tanggal akses: 6 Oktober 2026
- Pengolahan: data diunduh per tahun (batas 20.000 kejadian per permintaan), 30.435 kejadian mentah; kejadian negara tetangga dibuang lewat kolom `place`, tersisa 25.057 kejadian (`gempa_indonesia_bersih.csv`).

Data USGS bersifat publik. USGS dapat merevisi katalognya sehingga angka dapat sedikit berbeda bila data diunduh ulang.

## Petunjuk Penggunaan

**Opsi 1 – tanpa internet (disarankan, hasil sama dengan laporan):**
1. Letakkan `gempa_indonesia_bersih.csv` di folder yang sama dengan notebook.
2. Pastikan pada sel import (bagian 2.1) `PAKAI_CSV_BERSIH = True` (sudah menjadi nilai bawaan).
3. Jalankan semua sel (Restart & Run all).

**Opsi 2 – unduh dari USGS (perlu internet, 5–15 menit):** ubah `PAKAI_CSV_BERSIH = False`, lalu jalankan semua sel. Data mentah tersimpan ke `usgs_raw.csv`.

**Google Colab:** unggah notebook dan CSV, lalu Runtime → Jalankan semua.
**Lokal:** `pip install -r requirements.txt`, lalu buka notebook dengan Jupyter.

Seed acak tetap (`SEED = 42`). Notebook menyimpan tabel hasil lengkap ke `hasil_eksperimen_uts.csv`. Library `umap-learn` bersifat opsional; jika tidak terpasang, bagian perbandingan UMAP dilewati.

## Ringkasan Temuan

- Dengan 10 fitur, clustering lemah (silhouette ≈ 0,09; ARI bootstrap 0,630) dan PCA butuh 9 dari 10 komponen untuk 90% variansi.
- Struktur yang stabil ada pada lokasi dan kedalaman (silhouette 0,402 latih / 0,417 uji di ruang lokasi–kedalaman; ARI bootstrap 0,994). Keunggulan ini muncul di ruang lokasi–kedalaman itu sendiri, didukung stabilitas bootstrap dan peta DBSCAN.
- DBSCAN (jarak haversine, eps 50 km) menemukan 21 cluster pada data latih dan 25 pada data uji, mengikuti busur subduksi.
- Fitur waktu (bulan, jam) tidak membentuk cluster bermakna; reduksi dimensi tidak memperbaiki clustering.
- Evaluasi memakai split kronologis (latih 2010–2017, uji 2018–2025) untuk mencegah kebocoran dari gempa susulan.

## Tautan

- Notebook Colab: https://colab.research.google.com/drive/16rj53lMoBts1kc1uAMWQ2OqYLpKZWi9e?usp=sharing
- Repositori: https://github.com/Puerinn/TUGAS-UTS-ML-B13
