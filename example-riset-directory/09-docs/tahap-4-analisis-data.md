# Tahap 4 — Analisis Hasil dan Visualisasi

**Status:** Selesai
**Bergantung pada:** [tahap-3-pengujian-k6.md](tahap-3-pengujian-k6.md)
**Lokasi kode:** `penelitian_deteksi_intrusi_FIX_SVM.py`
---

## Tujuan

Melakukan analisis terhadap hasil pengujian tiga algoritma machine learning, yaitu Decision Tree, Random Forest, dan Support Vector Machine (SVM), berdasarkan hasil Cross Validation, pengujian pada data testing, serta analisis statistik untuk menentukan algoritma yang memiliki performa terbaik dalam mendeteksi intrusi jaringan.

---

## Deliverable

- [x] Analisis hasil 10-Fold Cross Validation
- [x] Analisis hasil GridSearchCV
- [x] Analisis Accuracy
- [x] Analisis Precision
- [x] Analisis Recall
- [x] Analisis F1-Score
- [x] Analisis Area Under Curve (AUC)
- [x] Analisis Confusion Matrix
- [x] Analisis ROC Curve
- [x] Visualisasi Perbandingan Accuracy
- [x] Visualisasi ROC Curve
- [x] Analisis Statistik (Friedman Test, Repeated Measures ANOVA, Wilcoxon Signed Rank Test, Confidence Interval)
- [x] Penyimpanan hasil evaluasi dalam format CSV dan TXT

---

## Desain Analisis

### Tahapan Analisis

```
Hasil Cross Validation
        │
        ▼
Evaluasi Data Testing
        │
        ▼
Perhitungan Accuracy
Precision
Recall
F1-Score
AUC
        │
        ▼
Confusion Matrix
        │
        ▼
ROC Curve
        │
        ▼
Analisis Statistik
        │
        ▼
Visualisasi
        │
        ▼
Kesimpulan Penelitian
```



## Analisis Performa Model

Model dievaluasi menggunakan beberapa metrik berikut.

| Metrik | Fungsi |
|---|---|
| Accuracy | Mengukur tingkat ketepatan klasifikasi. |
| Precision | Mengukur ketepatan prediksi positif. |
| Recall | Mengukur kemampuan model mendeteksi data positif. |
| F1-Score | Menggabungkan Precision dan Recall. |
| AUC | Mengukur kemampuan klasifikasi model. |
| Confusion Matrix | Menampilkan jumlah prediksi benar dan salah. |
| ROC Curve | Membandingkan performa seluruh algoritma. |

---

## Hasil Analisis

### Hasil Cross Validation (10-Fold)

| Algoritma | Mean Accuracy |
|---|---:|
| Decision Tree | **99,49%** |
| Random Forest | **99,57%** |
| Support Vector Machine | **98,29%** |

Random Forest memperoleh rata-rata akurasi tertinggi dengan standar deviasi paling kecil sehingga menunjukkan performa yang paling stabil selama proses Cross Validation.

---

### Hasil Evaluasi pada Data Testing

| Algoritma | Accuracy | Precision | Recall | F1-Score | AUC |
|---|---:|---:|---:|---:|---:|
| Decision Tree | 99,58% | 99,54% | 99,49% | 99,52% | 0,9961 |
| Random Forest | **99,61%** | **99,55%** | **99,56%** | **99,55%** | **0,9997** |
| Support Vector Machine | 99,09% | 99,29% | 98,63% | 98,96% | 0,9993 |

Berdasarkan hasil pengujian, algoritma Random Forest memperoleh nilai Accuracy, Recall, F1-Score, dan AUC tertinggi dibandingkan dua algoritma lainnya.

---

### Analisis Statistik

Untuk memastikan bahwa perbedaan performa antar algoritma tidak terjadi secara kebetulan, dilakukan beberapa pengujian statistik, yaitu:

- Friedman Test
- Repeated Measures ANOVA
- Wilcoxon Signed Rank Test
- Confidence Interval 95%

Hasil analisis menunjukkan bahwa Random Forest memiliki performa yang secara statistik lebih baik dibandingkan Decision Tree dan Support Vector Machine (SVM).

---

## Visualisasi

Visualisasi yang dihasilkan selama penelitian meliputi:

```
perbandingan_model.png
roc_curve.png
```

Grafik Accuracy digunakan untuk membandingkan tingkat akurasi masing-masing algoritma, sedangkan ROC Curve digunakan untuk melihat kemampuan klasifikasi model berdasarkan nilai AUC.

---


## Output Analisis

Seluruh hasil analisis berhasil disimpan dalam beberapa file berikut.

```
hasil_lengkap.txt
hasil_cv_10fold.csv
hasil_perbandingan_model.csv
perbandingan_model.png
roc_curve.png
```

---


## Kesimpulan Tahap Analisis

Berdasarkan hasil Cross Validation, pengujian data testing, visualisasi, dan analisis statistik, algoritma **Random Forest** memberikan performa terbaik dalam mendeteksi intrusi jaringan menggunakan dataset NSL-KDD.

Random Forest memperoleh nilai Accuracy sebesar **99,61%**, Recall sebesar **99,56%**, F1-Score sebesar **99,55%**, serta nilai AUC sebesar **0,9997**. Selain menghasilkan performa terbaik, Random Forest juga menunjukkan kestabilan model yang lebih baik dibandingkan Decision Tree dan Support Vector Machine (SVM), sehingga algoritma tersebut dipilih sebagai model terbaik dalam penelitian ini.

---

## Catatan

- Analisis dilakukan menggunakan Python pada Google Colab.
- Seluruh visualisasi dibuat menggunakan Matplotlib.
- Evaluasi model dilakukan menggunakan library Scikit-learn.
- Analisis statistik dilakukan untuk memastikan perbedaan performa antar algoritma memiliki signifikansi secara ilmiah.
- Hasil analisis digunakan sebagai dasar penyusunan laporan penelitian dan manuskrip jurnal.
