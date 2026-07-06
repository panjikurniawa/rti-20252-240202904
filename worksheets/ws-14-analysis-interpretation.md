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
| Decision Tree | 99.49%        | ±0.07% | 99.50% | 99.36% | 99.61% | 10 |
| Random Forest | 99.57%        | ±0.05% | 99.57% | 99.47% | 99.64% | 10 |
| SVM           | 98.29%        | ±0.30% | 98.37% | 97.80% | 98.67% | 10 |


2. Uji Hipotesis:
   Uji yang digunakan  :  Friedman Test (uji utama) + Repeated-Measures ANOVA (konfirmasi)
   Justifikasi          : 3 grup dibandingkan (DT, RF, SVM), data berpasangan karena dievaluasi pada fold cross-validation yang identik (paired), n=10 per model. Friedman dipilih sebagai uji konservatif untuk data berpasangan dengan n kecil.
   Hasil Friedman: χ² = 17.897, p = 0.00013 (p < 0.001, sangat signifikan)
   Hasil ANOVA         : F = 156.49, p < 0.0001 (konfirmasi konsisten)
   Effect size         : Kendall's W = 0.895 → kategori LARGE

3. Keputusan:
   [✓] H₀ ditolak → H₁ diterima
   [ ] H₀ tidak ditolak

4. Interpretasi:
   Hubungan ke RQ       : RQ penelitian ini menanyakan "bagaimana tingkat efektivitas algoritma Random Forest dibanding Decision Tree dan SVM dalam mendeteksi intrusi jaringan komputer?" Hasil Friedman test (p<0.001) dan post-hoc Wilcoxon (semua pasangan signifikan) membuktikan RF secara statistik lebih baik dari keduanya — RQ terjawab secara definitif.
   Practical significance: Selisih mean RF vs DT kecil secara absolut (99.57% vs 99.49%, selisih 0.08 poin), namun RF lebih konsisten (std ±0.05% vs ±0.07%) dan CI RF tidak overlap dengan CI DT secara penuh. Selisih RF vs SVM jauh lebih besar (±1.3 poin) dan jelas relevan secara praktis — SVM juga 6× lebih tidak stabil. Dari sisi waktu komputasi: DT (0.66 dtk) vs RF (16.58 dtk) vs SVM (46.10 dtk) → DT paling efisien untuk sistem real-time.
   Perbandingan literatur: Pola urutan performa (RF > DT >> SVM) konsisten dengan jurnal referensi (Sari et al., 2024) yang juga menemukan RF sebagai model terbaik untuk deteksi intrusi pada NSL-KDD. Akurasi absolut lebih tinggi (>99%) karena perbedaan skema split data (70:30 acak vs split asli KDDTrain+/KDDTest+).

5. Limitation:
   | Jenis | Ancaman | Dampak | Mitigasi |
   |-------|---------|--------|----------|
   | Internal validity |Split 70:30 acak menghilangkan unseen attack |Akurasi artifisial tinggi (>99%), kurang representatif untuk zero-day attack |Uji lanjutan dengan split asli KDDTrain+/KDDTest+ |
   |External validity | Hanya menggunakan dataset NSL-KDD | Sulit digeneralisasi ke dataset/domain lain | enelitian lanjutan dengan UNSW-NB15 atau CICIDS|
   |Computational limitation | SVM dilatih pada subset (bukan data penuh) | Perbandingan SVM vs DT/RF tidak sepenuhnya setara | Dokumentasikan secara transparan di metode |
   |Statistical limitation | ataset tunggal, satu domain | eneralisasi statistik terbatas | Tambah dataset pada penelitian lanjutan |

6. Failure Analysis (jika H₀ tidak ditolak):
   Penyebab potensial  : (1) SVM dilatih pada subset data lebih kecil (30.000 dari 77.057 record), sehingga perbandingan tidak sepenuhnya setara. (2) Kernel RBF SVM secara inheren lebih sensitif terhadap jumlah data latih dibanding model tree-based.
   Boundary condition   : SVM cenderung kompetitif pada dataset kecil-menengah, namun kurang efisien pada data berskala besar karena kompleksitas komputasi O(n²-n³). Pada dataset ini (77.057 record training), SVM butuh waktu 46-180 detik — vs DT yang hanya 0.66 detik.
   Insight              :Trade-off waktu-akurasi yang jelas: SVM memerlukan waktu komputasi paling lama namun menghasilkan performa terendah dan variabilitas tertinggi (std ±0.30% vs RF ±0.05%). Untuk sistem deteksi intrusi yang membutuhkan respons cepat, Decision Tree adalah pilihan paling efisien (0.66 detik, akurasi 99.58%), sementara Random Forest adalah pilihan terbaik jika waktu training bukan kendala utama.
```

---

## Latihan 1 — Pemilihan Uji Statistik

Tentukan uji statistik yang tepat untuk eksperimen Anda.

| Pertanyaan | Jawaban |
|-----------|---------|
| Berapa grup yang dibandingkan? | 3  (Decision Tree, Random Forest, SVM) |
| Apakah data berpasangan (paired)? |Ya — ketiga model dievaluasi pada fold cross-validation yang identik (paired) |
| Apakah distribusi normal? (uji normalitas) |Terbukti normal berdasarkan uji Shapiro-Wilk (p > 0.05 untuk ketiga model: DT, RF, SVM) — bukan sekadar diasumsikan |
| **Uji yang dipilih:** |Friedman Test (uji utama, non-parametrik, konservatif untuk n kecil) + Repeated-Measures ANOVA (konfirmasi, karena data lolos normalitas) |
| **Justifikasi:** |>2 grup + data berpasangan + n=10 → Friedman sebagai pilihan aman; ANOVA sebagai konfirmasi. Keduanya menghasilkan p < 0.001 → konsisten. |

**Effect size yang akan dilaporkan:** [ ] Cohen's d / [ ] Eta-squared / [ ] Lainnya: [ ] Cohen’s d (pairwise comparison)/[ ]Confidence Interva/l[✓] Kendall's W = 0.895 (effect size global untuk Friedman test) → Large [✓] Cohen's d untuk post-hoc berpasangan (RF vs DT: d=-1.16, RF vs SVM: d=3.98, DT vs SVM: d=4.03) [✓] Confidence Interval 95% per model

---

## Latihan 2 — Interpretasi Hasil

Gunakan data berikut (atau data riil Anda) untuk berlatih interpretasi.

**Data:**
| Model | Accuracy (mean ± std) | n |
|-------|----------------------|---|
| Random Forest | 99.57% ± 0.05% | 10 |
| Decision Tree | 99.49% ± 0.07% | 10 |
|SVM | 98.29% ± 0.30% | 10|



| Aspek | Interpretasi |
|-------|-------------|
| Signifikansi statistik | p = 0.00013 jauh di bawah α=0.05 bahkan α=0.001 → sangat signifikan. Dikonfirmasi oleh ANOVA (F=156.49, p<0.0001). Tidak ada keraguan statistik bahwa perbedaan performa ketiga model adalah nyata, bukan kebetulan. |
| Effect size | Kendall's W = 0.895 → Large effect. Artinya perbedaan antar model bukan hanya signifikan secara statistik, tapi juga substansial secara praktis — terutama antara model tree-based (DT/RF) vs SVM (Cohen's d ≈ 4.0). |
| Practical significance |Selisih RF vs DT kecil (0.08 poin) — mungkin tidak relevan secara praktis untuk semua aplikasi. Tapi RF lebih konsisten (std ±0.05% vs ±0.07%) dan CI tidak overlap. Selisih RF vs SVM besar (±1.3 poin) dan jelas relevan. Dari sisi waktu: DT 0.66 dtk vs RF 16.58 dtk → untuk sistem real-time, DT lebih efisien. |
| Hubungan ke RQ |RQ: "Bagaimana efektivitas Random Forest dibanding Decision Tree dan SVM?" → Terjawab definitif: RF signifikan lebih baik dari keduanya (p<0.001, W=0.895), dengan selisih terbesar terhadap SVM (d=3.98). |
| Perbandingan literatur |Konsisten dengan Sari et al. (2024): RF terbaik untuk deteksi intrusi NSL-KDD. Akurasi lebih tinggi (99.61% vs 96.8%) karena perbedaan skema split, bukan karena metode yang berbeda secara fundamental. |

---

## Latihan 3 — Failure Analysis

Latih kemampuan failure analysis: hipotesis TIDAK didukung. Apa yang bisa dipelajari?

**Skenario:** Metode baru F1 = 83.2%, baseline F1 = 84.7%. p = 0.12 (tidak signifikan).

| Pertanyaan | Jawaban |
|-----------|---------|
| Apakah ini "gagal"? | Bukan gagal total. p = 0.12 berarti tidak ada cukup bukti statistik bahwa metode baru berbeda dari baseline — bukan bukti bahwa metode baru "lebih buruk". Hipotesis tidak terdukung adalah temuan yang valid, bukan kesalahan eksperimen. |
| Kemungkinan penyebab? | (1) Sample size terlalu kecil sehingga power test rendah (sulit mendeteksi perbedaan 1.5 poin F1 yang memang kecil). (2) Metode baru menambah kompleksitas tanpa manfaat F1 yang cukup besar untuk melampaui variabilitas natural data. |
| Boundary condition? | Metode baru mungkin hanya unggul pada kondisi data tertentu (misalnya dataset besar, data noisy, atau kelas imbalanced) yang tidak tercakup dalam eksperimen ini. Tidak bisa disimpulkan "metode tidak berguna" tanpa menguji di berbagai kondisi. |
| Insight yang bisa diambil? | Trade-off: kompleksitas tambahan metode baru tidak sebanding dengan manfaat performa di kondisi ini. Perlu investigasi lebih lanjut: apakah ada kondisi spesifik di mana metode baru unggul? Ini adalah boundary condition yang berharga untuk penelitian selanjutnya. |
| Apakah layak dilaporkan? Mengapa? | Ya, sangat layak. Hasil negatif + analisis boundary condition mencegah peneliti lain mengulang eksperimen yang sama, menghemat waktu komunitas riset. Komunitas ilmiah (ACL, NeurIPS, SIGIR) secara eksplisit mengakui kontribusi hasil negatif yang dianalisis dengan baik. |

**Limitation terkait:**
| Jenis | Ancaman | Dampak |
|-------|---------|--------|
| Statistical | Sample size kecil → low statistical power |Risiko Type II error: gagal mendeteksi perbedaan yang sebenarnya ada |
|Construct validity |F1-score mungkin tidak menangkap semua kualitas metode baru (misal robustness, interpretability, inference speed) |Kesimpulan "tidak berbeda" mungkin hanya berlaku untuk metrik F1, bukan kualitas metode secara keseluruhan |
|External validity |THanya diuji pada satu dataset/kondisi |Tidak bisa digeneralisasi sebelum diuji di kondisi yang lebih beragam |

---

## Refleksi

> Apakah "failure" dalam riset benar-benar gagal, atau justru kontribusi? Bagaimana failure analysis mengubah cara Anda melihat hasil negatif?

> Dalam penelitian, model dengan akurasi tinggi belum tentu langsung dianggap terbaik tanpa proses analisis statistik. Pengujian statistik seperti Friedman Test dan ANOVA membantu memastikan bahwa perbedaan performa yang terjadi memang signifikan secara ilmiah — bukan sekadar kebetulan dari satu kali split data. Failure analysis juga penting karena membantu memahami keterbatasan model tertentu. Pada penelitian ini, SVM menunjukkan performa terendah dengan variabilitas tertinggi, yang mengungkap boundary condition: SVM kurang efisien untuk dataset berskala besar, baik dari sisi waktu komputasi maupun stabilitas performa. Dengan demikian, penelitian tidak hanya menghasilkan model dengan performa terbaik (Random Forest), tetapi juga memberikan pemahaman menyeluruh mengenai kondisi penggunaan masing-masing algoritma — termasuk kapan DT lebih direkomendasikan daripada RF (sistem real-time dengan resource terbatas) dan kapan SVM kurang cocok digunakan.
