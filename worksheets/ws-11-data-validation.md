# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [✓ ] Semua skenario tercakup (Decision Tree, Random Forest, SVM)
  [✓ ] Jumlah run sesuai rencana (10 fold × 3 model = 30 fold total)
  [✓ ] Tidak ada file output hilang
      Missing: 0 dari 30 fold (10 fold per model)

Format Consistency:
  [✓ ] Semua file format sama (CSV/JSON/...)
  [✓ ] Header konsisten
  [✓ ] Tipe data konsisten (numerik tetap numerik)
      Format file yang digunakan:
      - hasil_cv_10fold.csv       (data 10-fold per model)
      - hasil_perbandingan_model.csv (ringkasan evaluasi final)
      - perbandingan_model.png    (visualisasi bar chart)
      - roc_curve.png             (ROC curve comparison)
      - hasil_lengkap.txt         (log output lengkap)

Range & Logic:
  [✓ ] Nilai dalam range masuk akal (semua accuracy dalam [0,1])
  [✓ ] Tidak ada waktu negatif
  [✓ ] Metrik 0–100%, tidak di luar range
      Anomali ditemukan:
      - SVM membutuhkan waktu komputasi jauh lebih lama (46 detik untuk
        training final, 179 detik untuk grid search) dibanding Decision
        Tree (0,66 detik) dan Random Forest (16,58 detik).
      - Hal ini bukan kesalahan data, melainkan karakteristik inheren
        kernel RBF pada dataset berskala besar (77.057 record training).
        SVM juga dilatih pada subset 30.000 data, bukan data penuh.
      - Keputusan: data diterima, anomali waktu SVM didokumentasikan
        sebagai keterbatasan komputasi di bagian limitation penelitian.

Cross-Validation:
  [✓ ] Run identik → hasil mendekati (std kecil: DT ±0.07%, RF ±0.05%,
      SVM ±0.30% — semua dalam batas variabilitas normal)
  [✓ ] Trend konsisten dengan ekspektasi teori:
      Urutan performa: Random Forest > Decision Tree > SVM
      Konsisten dengan jurnal referensi (Sari et al., 2024) yang juga
      menemukan Random Forest sebagai model terbaik untuk deteksi intrusi.

Keputusan:
  [✓ ] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)
     
---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Fold Direncanakan | Fold Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| Decision Tree | 10 (fold CV) | 10 | 0 | Tidak ada masalah |
| Random Forest | 10 (fold CV) | 10 |  | Tidak ada masalah |
|SVM |10 (fold CV, subset 15.000 data) |10 |0 |Tidak masalah |


**Total expected:** 30 fold | **Total actual:** 30 fold | **Missing:** 0

**Keputusan untuk data missing:**
> eluruh proses eksperimen berhasil dijalankan sehingga tidak ditemukan
data yang hilang. Semua 30 fold (10 per model) berhasil tercatat dan
disimpan di file hasil_cv_10fold.csv. Tidak diperlukan pengujian ulang.
---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| fold | Decision Tree |Random Forest | SVM |
|-----|-------------|----------------|--------|
| 1| 99.416% |99.637% | 97.800% |
| 2 | 999.611% | 99.611% | 98.067% |
| 3 | 99.364% |99.468% | 98.267% |
| 4 | 99.468% | 99.520% | 98.467% |
| 5 | 99.481% | 99.546% |97.800% |
| 6 | 99.429% | 99.585% | 98.267% |
| 7 | 99.468% | 99.572% | 98.600% |
| 8 | 99.585% | 99.624% | 98.467% |
| 9 | 99.507% | 99.598% | 98.467% |
| 10| 99.572% | 99.559% | 98.667% |
 


**Deteksi outlier:**
-Decision Tree:
Q1 = 99.439% | Q3 = 99.555% | IQR = 0.117%
Batas bawah = 99.264% | Batas atas = 99.731%
Outlier terdeteksi: Tidak ada ✓
-Random Forest:
Q1 = 99.549% | Q3 = 99.607% | IQR = 0.058%
Batas bawah = 99.461% | Batas atas = 99.695%
Outlier terdeteksi: Tidak ada ✓
-SVM:
Q1 = 98.117% | Q3 = 98.467% | IQR = 0.350%
Batas bawah = 97.592% | Batas atas = 98.992%
Outlier terdeteksi: Tidak ada ✓

**Investigasi (untuk setiap outlier):**

| Model | Temuan | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| Decision Tree | Tidak ada outlier, std ±0.07% | Data stabil, model deterministik dengan parameter entropy, max_depth=20 | Data diterima|
| Random Forest | Tidak ada outlier, std terkecil ±0.05% |Sifat ensemble (200 pohon) meredam variabilitas antar-fold | Data diterima |
| SVM | Tidak ada outlier, tapi std tertinggi ±0.30% | SVM dievaluasi pada subset 15.000 data per fold, bukan data penuh — variabilitas lebih tinggi karena ukuran data lebih kecil | Data diterima, dicatat sebagai keterbatasan komputasi |

Catatan penting tentang SVM:
Variabilitas SVM (±0.30%) lebih tinggi dari DT dan RF bukan karena
instabilitas algoritma, melainkan karena evaluasi CV-nya menggunakan
subset data yang lebih kecil (15.000 dari 77.057 record training).
Ini bukan anomali yang perlu dihapus, melainkan temuan yang perlu
didokumentasikan sebagai limitation penelitian.



## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul
**2. Format:** [✓ ] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check (anomali):** Tidak ditemukan nilai di luar range evaluasi.
**4. Logic check:** [✓ ] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [✓ ] Data siap analisis / [ ] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Data yang benar belum tentu menjadi data yang dapat dipercaya. Data dianggap dapat dipercaya apabila sudah melalui proses validasi, pengecekan konsistensi, serta dipastikan sesuai dengan prosedur penelitian yang telah ditetapkan. Walaupun proses eksperimen dilakukan secara otomatis menggunakan program Python, validasi formal tetap diperlukan untuk memastikan tidak terjadi kesalahan pada proses preprocessing, training model, maupun evaluasi hasil. Dalam penelitian ini, validasi dilakukan pada dua level: (1) validasi hasil 10-fold cross-validation per model menggunakan metode IQR untuk mendeteksi outlier, dan (2) validasi konsistensi format seluruh file output. Dengan melakukan validasi data yang terstruktur, hasil penelitian menjadi lebih valid, lebih akurat, dan dapat dipertanggungjawabkan secara ilmiah.
