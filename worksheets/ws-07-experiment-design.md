# WS-07: Experimental Design & Validity

> **Bab 7 — Experimental Design & Validity**

---

## Ringkasan Materi

### Correlation ≠ Causality

Kausalitas membutuhkan 3 syarat:
1. **Covariance** — X dan Y bergerak bersama
2. **Temporal precedence** — X berubah sebelum Y
3. **Elimination of alternatives** — Tidak ada faktor lain yang menjelaskan Y

Controlled experiment adalah satu-satunya metode yang bisa membuktikan kausalitas.

### Empat Jenis Validitas

| Jenis | Pertanyaan | Ancaman Umum |
|-------|-----------|-------------|
| **Internal** | Apakah hubungan IV→DV nyata? | Confounding variable, selection bias |
| **External** | Apakah bisa digeneralisasi? | Dataset terlalu spesifik |
| **Construct** | Apakah mengukur konsep yang benar? | Metrik tidak sesuai |
| **Conclusion** | Apakah kesimpulan statistik valid? | Sample size kecil, uji salah |

Internal dan external validity sering berkonflik: semakin terkontrol (internal kuat) → semakin artificial (external lemah).

### Tiga Tipe Eksperimen dalam Riset TI

| Tipe | Deskripsi | Kapan Digunakan |
|------|----------|----------------|
| **Comparison Study** | Metode A vs B pada kondisi identik | Membandingkan pendekatan berbeda |
| **Ablation Study** | Full system → lepas komponen satu per satu | Mengukur kontribusi tiap komponen |
| **Parameter Study** | Variasikan satu parameter, amati dampak | Uji sensitifitas/robustness |

### Fairness dalam Perbandingan

Perbandingan yang adil = **kondisi identik** untuk semua metode: dataset sama, preprocessing sama, tuning effort sebanding, environment sama, metrik sama.

Contoh tidak adil: Transformer (30 fitur tambahan + Bayesian optimization) vs RF (default params) → hasilnya misleading.

### Threats to Validity = Diidentifikasi Sebelum Eksperimen

Ancaman validitas harus diidentifikasi **sebelum** eksperimen dan mitigasinya dirancang sebagai bagian dari desain — bukan ditulis sebagai boilerplate setelah selesai.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan testing | Memastikan sistem memenuhi requirement | Membuktikan hubungan kausal antar variabel |
| Baseline | Versi sebelumnya (last release) | Metode tervalidasi dari literatur |
| Kegagalan | Bug → fix → release | H₀ tidak ditolak → tetap kontribusi ilmiah |
| Sukses | 100% test pass | Evidence valid — mendukung atau menolak hipotesis |

### Istilah Penting

- **Causality** — Hubungan sebab-akibat (covariance + temporal + elimination)
- **Controlled Experiment** — Ubah satu variabel, kontrol sisanya, amati efek
- **Fairness** — Semua metode diuji pada kondisi yang benar-benar identik
- **Threats to Validity** — Faktor yang bisa melemahkan kesimpulan jika tidak dimitigasi
- **Conclusion Validity** — Validitas statistik: power, sample size, uji yang tepat

---

## Template A.7 — Desain Eksperimen Lengkap

```
EXPERIMENT DESIGN

Research Question : Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD?
Hypothesis        : Random Forest memiliki performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM berdasarkan akurasi, presisi, recall, dan F1-Score.
Tipe Eksperimen   : [✓ ] Comparison  [ ] Ablation  [ ] Parameter

Kondisi Eksperimen:
| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Model baseline menggunakan Decision Tree dan SVM | DT dan SVM | Dataset NSL-KDD, split data 70:30, preprocessing sama |
| Treatment | Model menggunakan Random Forest | Random Forest | Dataset NSL-KDD, split data 70:30, preprocessing sama |

Fairness Checklist:
  [✓ ] Dataset identik untuk semua kondisi
  [✓ ] Preprocessing setara
  [✓ ] Tuning effort setara
  [✓ ] Environment identik
  [✓ ] Metrik evaluasi sama

Threat Analysis:
| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal    | Overfitting pada data training | Menggunakan 10-fold cross-validation |
| External    | Dataset NSL-KDD belum sepenuhnya mewakili jaringan modern | Menyarankan penggunaan dataset terbaru pada penelitian berikutnya |
| Construct   | Akurasi saja belum cukup menggambarkan performa IDS | Menggunakan recall, F1-Score, dan AUC sebagai metrik tambahan |
| Conclusion  | Hasil eksperimen dapat dipengaruhi ukuran dataset | Menggunakan dataset training dan testing yang konsisten |

Statistical Plan:
  Uji statistik   : Perbandingan nilai evaluasi model
  Justifikasi      : Digunakan untuk melihat model dengan performa terbaik
  Alpha            : 0.05
  Effect size min  : Perbedaan akurasi minimal 2%
```

---

## Latihan 1 — Desain Eksperimen

Susun desain eksperimen berdasarkan RQ, variabel, dan sistem dari WS-04 sampai WS-06.

**RQ:** Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD?
**Tipe eksperimen:** [✓ ] Comparison / [ ] Ablation / [ ] Parameter

| Kondisi | Deskripsi | IV Value | CV Settings |
|---------|-----------|----------|-------------|
| Control | Menggunakan model baseline Decision Tree dan SVM | DT dan SVM | Dataset NSL-KDD, preprocessing sama, split data 70:30 |
| Treatment |Menggunakan model Random Forest |Random Forest |Dataset NSL-KDD, preprocessing sama, split data 70:30 |

---

## Latihan 2 — Fairness Checklist

Evaluasi apakah desain eksperimen di Latihan 1 sudah fair.

| Kriteria | Status | Detail |
|----------|--------|--------|
| Dataset identik | ✅ |Semua model menggunakan dataset NSL-KDD |
| Preprocessing setara |✅ |Normalisasi dan encoding dilakukan dengan cara yang sama |
| Tuning effort setara |✅ |Setiap model menggunakan proses pelatihan dan pengujian yang sama |
| Environment identik |✅ |Eksperimen dilakukan pada sistem dan data yang sama |
| Metrik evaluasi sama |✅ |Semua model dievaluasi menggunakan akurasi, presisi, recall, dan F1-Score |

**Ada yang tidak fair?** [✓ ] Tidak
> Jika ya, bagaimana cara memperbaikinya? Tidak ada, karena seluruh model diuji dengan kondisi yang sama.

---

## Latihan 3 — Threat Analysis

Identifikasi ancaman validitas untuk desain eksperimen ini.

| Threat Type | Ancaman Spesifik | Mitigasi |
|-------------|-----------------|----------|
| Internal | Data leakage antara data training dan testing | Menggunakan pembagian data yang terpisah dan cross-validation |
| External |Dataset masih menggunakan NSL-KDD yang cukup lama |Membandingkan hasil dengan dataset yang lebih baru pada penelitian selanjutnya |
| Construct |Akurasi tinggi belum tentu menunjukkan kemampuan deteksi yang baik |Menambahkan recall, F1-Score, dan AUC sebagai metrik evaluasi |
| Conclusion |Jumlah data tertentu bisa memengaruhi hasil evaluasi |Menggunakan proses pengujian yang konsisten pada semua model |

**Ancaman mana yang paling sulit dimitigasi?** External validity
**Mengapa?**
> Karena dataset NSL-KDD belum sepenuhnya mencerminkan pola serangan jaringan modern, sehingga hasil penelitian mungkin berbeda ketika diterapkan pada kondisi nyata.

---

## Refleksi

> Sebuah paper melaporkan "metode kami mengalahkan semua baseline." Apa 3 pertanyaan pertama yang harus diajukan untuk mengevaluasi klaim ini?

**Jawaban:**
1. Apakah semua model diuji menggunakan dataset dan preprocessing yang sama?
2. Apakah baseline yang digunakan masih relevan dan umum dipakai dalam penelitian serupa?
3. Apakah evaluasi dilakukan menggunakan metrik yang cukup lengkap seperti recall, F1-Score, dan AUC, bukan hanya akurasi saja?
