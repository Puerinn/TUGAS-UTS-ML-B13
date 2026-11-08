B13 – Karakteristik Kejadian Gempa Indonesia (Milestone 1 UTS)
Reduksi dimensi dan pencarian pola (unsupervised, classical ML) pada katalog gempa USGS, wilayah Indonesia, 2010–2025, M ≥ 4,0.

Kelompok: 9
Anggota: Dedi Sanjaya Nainggolan (231111885) Erico Adelorenzo Samosir (231112600) Andi Aziz Prasetyo (231112637)
Isi repositori
Berkas	Keterangan
notebook_uts_gempa_B13.ipynb	Notebook eksperimen lengkap (bagian 1–8, mengikuti komponen A–I laporan)
Laporan_UTS_B13_Kelompok9.pdf	Laporan Milestone 1 (PDF untuk dikumpulkan)
Laporan_UTS_B13_Kelompok9.docx	Versi Word laporan (sumber yang bisa diedit)
gempa_indonesia_bersih.csv	Data kerja: 25.057 kejadian, hasil penyaringan wilayah dari katalog USGS
tabel_hasil_eksperimen_awal.csv	Ringkasan hasil eksperimen awal yang dikutip di laporan
requirements.txt	Library yang dibutuhkan
Sumber data
USGS Earthquake Catalog (ComCat): https://earthquake.usgs.gov/earthquakes/search/ API: https://earthquake.usgs.gov/fdsnws/event/1/ (format CSV, lintang −11 s.d. 6, bujur 95 s.d. 141, 2010-01-01 s.d. 2025-12-31, magnitudo ≥ 4,0). Data USGS bersifat publik. USGS dapat merevisi katalognya sehingga angka dapat sedikit berbeda bila data diunduh ulang.

Cara menjalankan
Opsi 1 – tanpa internet (disarankan, hasil sama dengan laporan):

Letakkan gempa_indonesia_bersih.csv di folder yang sama dengan notebook.
Pada sel import (bagian 2.1) ubah PAKAI_CSV_BERSIH = True.
Jalankan semua sel (Restart & Run all).
Opsi 2 – unduh dari USGS (perlu internet, 5–15 menit): biarkan PAKAI_CSV_BERSIH = False, jalankan semua sel. Data mentah tersimpan ke usgs_raw.csv.

Google Colab: unggah notebook dan CSV, lalu Runtime → Jalankan semua. Lokal: pip install -r requirements.txt, lalu buka notebook. Seed acak tetap (SEED = 42). Notebook menyimpan tabel hasil lengkap ke hasil_eksperimen_uts.csv.

Ringkasan temuan
Dengan 10 fitur, clustering lemah (silhouette ≈ 0,09) dan PCA butuh 9 dari 10 komponen.
Struktur yang stabil ada pada lokasi dan kedalaman (silhouette 0,402 latih / 0,417 uji di ruang lokasi–kedalaman; ARI bootstrap 0,994).
Fitur waktu (bulan, jam) tidak membentuk cluster bermakna; reduksi dimensi tidak memperbaiki clustering.
Evaluasi: split kronologis (latih 2010–2017, uji 2018–2025) untuk mencegah kebocoran dari gempa susulan.
