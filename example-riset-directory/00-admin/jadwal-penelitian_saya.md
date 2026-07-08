# Jadwal & Log Pelaksanaan Penelitian

**Nama:** Panji Kurniawan
**NIM:** 240202904
**Judul:** Analisis Penerapan Algoritma Random Forest dalam Meningkatkan Akurasi Deteksi Intrusi pada Jaringan Komputer
**Dataset:** NSL-KDD (KDDTrain+ & KDDTest+)
**Platform:** Google Colab (Python 3.11, CPU Runtime)

Catatan kronologis pelaksanaan tiap tahap berdasarkan riwayat eksperimen
dan log output (`hasil_lengkap.txt`).

---

## Log Pelaksanaan

| Tanggal | Tahap | Aktivitas | Referensi |
|---|---|---|---|
| 2026-06-10 s.d. 2026-06-15 | Tahap 1 — Proposal & Revisi | Penyusunan proposal penelitian (UTS Riset Teknologi Informasi); revisi sesuai catatan dosen (hipotesis testable H1/H0, definisi populasi/sampel, baseline kondisi A vs intervensi kondisi B, definisi eksplisit variabel IV dan DV); jadwal penelitian diubah dari 8 bulan menjadi 2 minggu | [01-proposal/UTS_Riset_Teknologi_Informasi_Revisi_Final.docx](../01-proposal/) |
| 2026-06-20 | Tahap 2 — Studi Literatur | Review jurnal rujukan utama: Sari et al. (2024) "Implementasi Machine Learning untuk Deteksi Intrusi pada Jaringan Komputer" (Jurnal Minfo Polgan, Vol.13 No.2); identifikasi gap penelitian (skema split berbeda, penanganan outlier IQR, uji statistik belum dilakukan di jurnal rujukan) | [02-literatur/](../02-literatur/) |
| 2026-06-22 | Tahap 3 — Persiapan Dataset & Environment | Download dataset NSL-KDD (KDDTrain+.txt: 125.973 record, KDDTest+.txt: 22.544 record) dari repository GitHub defcom17; setup Google Colab, verifikasi library (pandas 2.2.2, numpy 1.26.4, scikit-learn 1.4.2, matplotlib 3.8.4, scipy 1.13.0); penulisan script Python awal | [04-data/](../04-data/), [05-kode/](../05-kode/) |
| 2026-06-23 | Tahap 4 — Preprocessing Data | Implementasi pipeline preprocessing: penggabungan KDDTrain+ dan KDDTest+ (total 148.517 record); pengecekan missing value (0 kasus); penghapusan 610 duplikat; penanganan outlier metode IQR pada fitur duration, src_bytes, dst_bytes (37.825 record dihapus); konversi label biner (attack=0, normal=1); one-hot encoding fitur kategorikal (protocol_type, service, flag) → 122 fitur; split 70:30 (77.057 training / 33.025 testing); normalisasi MinMaxScaler (fit pada training saja); data akhir: 110.082 record | [05-kode/penelitian_deteksi_intrusi_FIX_SVM.py](../05-kode/) |
| 2026-06-24 | Tahap 5 — Eksperimen Awal (Error) | Eksekusi script versi pertama — macet pada proses cross-validation SVM (runtime >2 jam 43 menit tanpa hasil) karena SVM kernel RBF dijalankan pada seluruh 77.057 record training; proses dihentikan (Interrupt execution) | [05-kode/](../05-kode/) |
| 2026-06-24 | Tahap 5 — Perbaikan Script | Optimasi script: SVM cross-validation dan grid search menggunakan subset 15.000 record; SVM training final menggunakan subset 30.000 record; DT dan RF tetap menggunakan data penuh; verifikasi sintaks Python; script final diberi nama `penelitian_deteksi_intrusi_FIX_SVM.py` | [05-kode/penelitian_deteksi_intrusi_FIX_SVM.py](../05-kode/) |
| 2026-06-25 | Tahap 6 — Eksekusi Eksperimen Final | Eksekusi script final di Google Colab — selesai dalam ±15 menit; 10-fold cross-validation untuk ketiga model (30 fold total); grid search hyperparameter (DT: 31.38 dtk, RF: 233.12 dtk, GS SVM: 179.97 dtk); parameter terbaik: DT criterion=entropy max_depth=20; RF n_estimators=200 max_depth=None; SVM C=10 gamma=scale; evaluasi final pada test set 33.025 record; semua output tersimpan: hasil_cv_10fold.csv, hasil_perbandingan_model.csv, perbandingan_model.png, roc_curve.png, hasil_lengkap.txt | [04-data/](../04-data/), [06-output/](../06-output/) |
| 2026-06-25 | Tahap 7 — Analisis Statistik | Perhitungan uji statistik dari data 10-fold: uji normalitas Shapiro-Wilk (ketiga model normal, p>0.05); Friedman test (χ²=17.897, p=0.00013 — sangat signifikan); repeated-measures ANOVA (F=156.49, p<0.0001 — konfirmasi konsisten); Kendall's W=0.895 (large effect); post-hoc Wilcoxon Bonferroni-corrected: RF vs DT p=0.00781 d=-1.16, RF vs SVM p=0.00195 d=3.98, DT vs SVM p=0.00195 d=4.03; CI 95%: DT [99.43%, 99.55%], RF [99.54%, 99.61%], SVM [98.07%, 98.51%] | [06-output/](../06-output/), [07-manuskrip/](../07-manuskrip/) |
| 2026-06-26 | Tahap 8 — Penulisan Laporan | Penyusunan bagian Hasil dan Pembahasan (7 sub-bagian: preprocessing, CV, hyperparameter tuning, evaluasi final, uji statistik, confusion matrix, pembahasan); pengisian worksheet WS-09 s.d. WS-16; verifikasi konsistensi angka antar dokumen | [07-manuskrip/Hasil_dan_Pembahasan_Panji.docx](../07-manuskrip/), [08-laporan/](../08-laporan/) |
| 2026-06-27 | Tahap 9 — Finalisasi & Dokumentasi | Review akhir seluruh dokumen; pengisian riset directory (00-admin s.d. 09-docs); push ke GitHub repository `panjikurniawa/rti-20252-240202904` | Seluruh folder repo |

---

## Hasil Utama Penelitian

| Metrik | Decision Tree | Random Forest | SVM |
|---|---|---|---|
| Accuracy (test set) | 99.58% | **99.61%** | 99.09% |
| F1-Score | 99.52% | **99.55%** | 98.96% |
| AUC | 0.9961 | **0.9997** | 0.9993 |
| CV Mean (10-fold) | 99.49% ± 0.07% | **99.57% ± 0.05%** | 98.29% ± 0.30% |
| Waktu Training | 0.66 dtk | 16.58 dtk | 46.10 dtk |

**Uji statistik:** Friedman test χ²=17.897, **p=0.00013**, Kendall's W=0.895 (large effect)
**Kesimpulan:** H1 diterima — Random Forest signifikan lebih baik dari Decision Tree dan SVM

---

## Status Ringkas

- **Tahap 1 — Proposal & Revisi**: ✅ Selesai (revisi sesuai 4 catatan dosen)
- **Tahap 2 — Studi Literatur**: ✅ Selesai (jurnal rujukan diidentifikasi dan dianalisis)
- **Tahap 3 — Persiapan Dataset**: ✅ Selesai (NSL-KDD tersedia, environment siap)
- **Tahap 4 — Preprocessing**: ✅ Selesai (110.082 record, 122 fitur, split 70:30)
- **Tahap 5 & 6 — Eksperimen**: ✅ Selesai (script final, 30 fold CV, grid search, evaluasi)
- **Tahap 7 — Analisis Statistik**: ✅ Selesai (Friedman, ANOVA, Wilcoxon, CI 95%)
- **Tahap 8 — Penulisan Laporan**: ✅ Selesai (Hasil & Pembahasan, WS-09 s.d. WS-16)
- **Tahap 9 — Finalisasi**: ✅ Selesai (dokumentasi lengkap, push ke GitHub)

---

## Checklist Sebelum Pengumpulan

- [x] Proposal direvisi sesuai 4 catatan dosen (hipotesis, populasi/sampel, baseline vs intervensi, IV & DV)
- [x] Script Python final tersedia dan reproducible (seed 42 di semua level)
- [x] Dataset hasil eksperimen tersimpan (CSV, PNG, TXT log)
- [x] Uji statistik formal dilakukan (Friedman test, ANOVA, post-hoc Wilcoxon, CI 95%)
- [x] Worksheet WS-09 s.d. WS-16 selesai dan dikumpulkan
- [x] Laporan Hasil dan Pembahasan selesai (7 sub-bagian, 7 tabel)
- [x] Riset directory lengkap (00-admin s.d. 09-docs)
- [ ] Push semua file ke GitHub repository

---

## Korespondensi

| Tanggal | Pihak | Topik | Status |
|---|---|---|---|
| 2026-06-10 | Dosen pembimbing | Revisi proposal: hipotesis testable, populasi/sampel, baseline vs intervensi, IV & DV | ✅ Selesai direvisi |
| 2026-06-15 | Dosen pembimbing | Konfirmasi jadwal penelitian 2 minggu (dari 8 bulan) | ✅ Disetujui |
