# WS-14: Analysis, Interpretation & Failure Analysis

> **Bab 14 — Analisis Data, Interpretasi & Failure Analysis**

---

## Ringkasan Materi

### Data → Knowledge Model

```
Data → Analysis → Interpretation → Explanation → Knowledge
```

Tiga level yang berbeda:
- **Analysis** — "Apa yang terjadi?" (deskriptif + inferensial)
- **Interpretation** — "Apa artinya?" (konteks RQ + literatur)
- **Failure Analysis** — "Mengapa tidak berhasil?" (boundary conditions)

### Beyond p-value

**Statistical significance ≠ practical significance.** Selalu laporkan:
1. p-value (signifikansi statistik)
2. Effect size (besarnya efek)
3. Confidence interval (rentang ketidakpastian)

| Effect Size (Cohen's d) | Interpretasi |
|-------------------------|-------------|
| < 0.2 | Small |
| 0.2 – 0.8 | Medium |
| > 0.8 | Large |

### Pemilihan Uji Statistik

| Kondisi | Uji yang Tepat |
|---------|---------------|
| 2 grup, normal, paired | Paired t-test |
| 2 grup, non-normal | Wilcoxon signed-rank |
| > 2 grup, normal | One-way ANOVA + post-hoc |
| > 2 grup, non-normal | Kruskal-Wallis + post-hoc |
| 2 variabel kontinu | Pearson (normal) / Spearman (rank) |

### Failure Analysis as Contribution

Hipotesis yang ditolak adalah **temuan yang berharga**:

| Dataset | New (F1) | Baseline (F1) | p-value | Cohen's d |
|---------|---------|--------------|---------|-----------|
| DS-1 (small, clean) | 94.2±1.1 | 89.3±1.5 | <0.001 | **3.7** |
| DS-4 (medium, noisy) | 78.3±3.2 | 82.1±2.8 | 0.008 | **-1.3** |
| DS-5 (large, noisy) | 71.6±4.1 | 80.5±3.0 | <0.001 | **-2.5** |

**Insight:** Metode baru unggul di data bersih tapi gagal di data noisy → asumsi Gaussian dilanggar → **boundary condition** ditemukan → hybrid approach direkomendasikan.

**Partial failure + deep analysis = kontribusi lebih kaya daripada full success tanpa analisis.**

### Limitation Types

| Jenis | Contoh |
|-------|--------|
| Internal validity | Confounders yang tidak dikontrol |
| External validity | Generalisasi ke domain lain |
| Construct validity | Metrik mengukur apa yang dimaksud? |
| Statistical limitation | Sample size, asumsi distribusi |

### Jebakan Kognitif

1. "Signifikan statistik = penting secara praktis" → cek effect size
2. "Hipotesis tidak didukung → cari sudut baru" → p-hacking
3. "Kegagalan tidak perlu dilaporkan detail" → missed insight
4. "Limitasi cukup disebutkan, tidak perlu dianalisis" → kedalaman hilang

---

## Template A.14 — Analysis & Interpretation Report

```
ANALYSIS & INTERPRETATION

1. Statistik Deskriptif:
| Skenario      | Mean Accuracy | Std    | Median | Min    | Max    | n  |
| ------------- | ------------- | ------ | ------ | ------ | ------ | -- |
| Decision Tree | 99.49%        | ±0.07% | 99.50% | 99.41% | 99.61% | 10 |
| Random Forest | 99.57%        | ±0.05% | 99.57% | 99.50% | 99.66% | 10 |
| SVM           | 98.29%        | ±0.30% | 98.30% | 97.80% | 98.66% | 10 |


2. Uji Hipotesis:
   Uji yang digunakan  : One Way ANOVA dan Friedman Test
   Justifikasi          : Penelitian membandingkan tiga algoritma berbeda dengan data hasil cross validation sebanyak 10 fold pada masing-masing model. Oleh karena itu digunakan pengujian statistik untuk mengetahui apakah terdapat perbedaan performa yang signifikan antar model.
   Hasil: p = 0.00013 (χ² = 17.897), effect size (d/r/η²) = Kendall's W = 0.895 
   CI 95%               : [99.42%, 99.56%]

3. Keputusan:
   [✓] H₀ ditolak → H₁ diterima
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       : RQ mempertanyakan efektivitas Random Forest dibanding Decision Tree dan SVM. Hasil Friedman test (p<0.001) dan post-hoc Wilcoxon membuktikan Random Forest signifikan lebih unggul dari kedua model lain, menjawab RQ secara definitif
   Practical significance: Meski selisih mean akurasi DT vs RF kecil (0.99490 vs 0.99572, selisih 0.08 poin), konsistensi RF lebih tinggi (Std lebih kecil: 0.00051 vs 0.00079) — RF lebih stabil antar fold. Selisih RF vs SVM jauh lebih besar dan jelas relevan secara praktis (SVM ±1.3 poin lebih rendah, dengan variabilitas 6x lebih besar)
   Perbandingan literatur: Pola hasil ini (Random Forest > Decision Tree > / >> SVM) konsisten dengan jurnal referensi (Sari et al., 2024) yang juga menemukan Random Forest sebagai model terbaik, meski besaran akurasi absolut berbeda karena perbedaan skema split data

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   | Internal validity |Parameter model terbatas pada eksperimen tertentu |Performa dapat berubah pada konfigurasi lain |Menggunakan Grid Search |
   |External validity | Dataset hanya menggunakan NSL-KDD| Sulit digeneralisasi ke dataset lain | Penelitian lanjutan menggunakan UNSW-NB15 atau CICIDS|
   |Computational limitation | SVM memerlukan komputasi tinggi | Waktu training lebih lama | Menggunakan subset representatif |
   |Statistical limitation | Dataset tunggal | Generalisasi statistik terbatas | Menambah dataset pada penelitian lanjutan |

6. Failure Analysis (jika H₀ tidak ditolak):
   Penyebab potensial  : Kombinasi: (1) SVM dilatih pada subset data yang lebih kecil dari DT/RF, dan (2) kernel RBF SVM secara inheren lebih sensitif terhadap jumlah data latih untuk menemukan decision boundary optimal dibanding model tree-based
   Boundary condition   : SVM cenderung bekerja optimal pada dataset berukuran kecil hingga menengah, tetapi kurang efisien ketika jumlah data semakin besar.
   Insight              : Trade-off waktu-akurasi: SVM butuh waktu pelatihan terlama (46-180 detik) namun hasilnya justru paling rendah dan paling tidak stabil (Std tertinggi) — menunjukkan SVM bukan pilihan efisien untuk kasus ini, baik dari sisi akurasi maupun efisiensi komputasi
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 3  (Decision Tree, Random Forest, SVM) |
| Apakah data berpasangan (paired)? |Ya, karena berasal dari fold cross validation yang sama |
| Apakah distribusi normal? (uji normalitas) |Diasumsikan mendekati normal berdasarkan cross validation |
| **Uji yang dipilih:** |One Way ANOVA dan Friedman Test |
| **Justifikasi:** |Membandingkan performa tiga model menggunakan data 10-fold |

**Effect size yang akan dilaporkan:** [✓] Cohen's d / [ ] Eta-squared / [ ] Lainnya: [✓] Cohen’s d (pairwise comparison)/[✓]Confidence Interval

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| Random Forest | 99.57% ± 0.05% | 10 |
| Decision Tree | 99.49% ± 0.07% | 10 |
|SVM | 98.29% ± 0.30% | 10|

p = 0.045, Cohen's d = 0.74, CI 95% = [0.03, 2.77]

| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | p-value < 0.05 sehingga signifikan |
| Effect size | Kendall’s W = 0.895 menunjukkan efek besar |
| Practical significance |Random Forest memberikan performa terbaik |
| Hubungan ke RQ |Menjawab tujuan penelitian |
| Perbandingan literatur |Konsisten dengan penelitian terdahulu |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru Anda mendapat F1 = 83.2%, baseline = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Tidak, seluruh model memiliki performa tinggi |
| Kemungkinan penyebab? | SVM membutuhkan komputasi tinggi pada dataset besar |
| Boundary condition? | SVM kurang optimal pada dataset dengan jumlah record besar |
| Insight yang bisa diambil? | Random Forest lebih stabil untuk intrusion detection |
| Apakah layak dilaporkan? Mengapa? | Ya, karena menunjukkan keterbatasan masing-masing model |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Statistical | Dataset hanya satu sumber | Generalisasi terbatas |
|Computational |Training SVM lebih lama |Eksperimen membutuhkan waktu lebih besar |
|Dataset |Tidak membandingkan dataset lain |Validasi eksternal terbatas |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Dalam penelitian, model dengan akurasi tinggi belum tentu langsung dianggap terbaik tanpa proses analisis statistik. Pengujian statistik seperti ANOVA dan Friedman Test membantu memastikan bahwa perbedaan performa yang terjadi memang signifikan secara ilmiah.
Failure analysis juga penting karena membantu memahami keterbatasan model tertentu. Pada penelitian ini dapat disimpulkan bahwa Random Forest menjadi model terbaik, sedangkan SVM memiliki keterbatasan pada efisiensi komputasi ketika digunakan pada dataset berukuran besar.
> Dengan demikian, penelitian tidak hanya menghasilkan model dengan performa terbaik, tetapi juga memberikan pemahaman mengenai kondisi penggunaan masing-masing algoritma.
