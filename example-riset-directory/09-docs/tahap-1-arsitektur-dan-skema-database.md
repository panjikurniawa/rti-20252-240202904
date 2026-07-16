# Tahap 1 — Perancangan  Penelitian, dan Persiapan Dataset

**Status:** Selesai

---

## 1. Komponen Sistem

1.  **Google Colab**
   - Digunakan sebagai lingkungan pengembangan dan pelaksanaan seluruh eksperimen machine learning menggunakan Python.
2. **Dataset NSL-KDD**
   - Digunakan sebagai sumber data utama penelitian.
   - Dataset terdiri atas data lalu lintas jaringan normal dan berbagai jenis serangan jaringan.
   - Dataset diperoleh dari NSL-KDD (KDDTrain+ dan KDDTest+).
3. **Library Machine Learning**
   - Pandas untuk pengolahan data.
   - NumPy untuk komputasi numerik.
   - Scikit-learn untuk preprocessing, pelatihan model, dan evaluasi.
   - Matplotlib untuk visualisasi hasil penelitian.

## 2. Alur Resolusi Kunci (Mitigasi)

```
Studi Literatur
        │
        ▼
Pengumpulan Dataset NSL-KDD
        │
        ▼
Preprocessing Data
(Missing Value, Duplikat,
Outlier, Encoding,
Normalisasi)
        │
        ▼
Pembagian Data
(Training 70% : Testing 30%)
        │
        ▼
Implementasi Algoritma
Decision Tree
Random Forest
Support Vector Machine
        │
        ▼
Grid Search
Hyperparameter Tuning
        │
        ▼
10-Fold Cross Validation
        │
        ▼
Evaluasi Model
Accuracy
Precision
Recall
F1-Score
AUC
Confusion Matrix
ROC Curve
        │
        ▼
Analisis Statistik
        │
        ▼
Kesimpulan
```

## 3. Persiapan Dataset

Dataset yang digunakan adalah **NSL-KDD**, yang merupakan dataset benchmark untuk penelitian Intrusion Detection System (IDS).

Tahapan preprocessing meliputi:

- Pemeriksaan missing value.
- Penghapusan data duplikat.
- Penanganan outlier menggunakan metode Interquartile Range (IQR).
- Konversi label menjadi klasifikasi biner (normal dan attack).
- One-Hot Encoding pada fitur kategorikal.
- Normalisasi data menggunakan MinMaxScaler.
- Pembagian data menjadi data training (70%) dan data testing (30%).

  
## 4. Algoritma yang Digunakan

Penelitian membandingkan tiga algoritma machine learning, yaitu:

| Algoritma | Fungsi |
|---|---|---|---|
| Decision Tree | Sebagai algoritma baseline pertama. |
| Random Forest | Algoritma utama yang dianalisis dalam penelitian. |
| Support Vector Machine (SVM) | Sebagai algoritma baseline kedua untuk perbandingan performa. |


## 5. Metrik Evaluasi

Model dievaluasi menggunakan beberapa metrik, yaitu:

| Metrik | Tujuan |
|  Accuracy | Mengukur tingkat ketepatan klasifikasi. |
| Precision | Mengukur ketepatan prediksi data positif. |
| Recall | Mengukur kemampuan mendeteksi seluruh data positif. |
| F1-Score | Menggabungkan Precision dan Recall. |
| AUC | Mengukur kemampuan model membedakan dua kelas. |
| Confusion Matrix | Mengetahui jumlah prediksi benar dan salah. |
| ROC Curve | Membandingkan performa klasifikasi setiap algoritma. |

## 6. Keputusan Penelitian

1. Dataset yang digunakan adalah **NSL-KDD**.
2. Penelitian menggunakan pendekatan klasifikasi biner (Normal dan Attack).
3. Algoritma yang dibandingkan terdiri atas **Decision Tree, Random Forest, dan Support Vector Machine (SVM)**.
4. Optimasi parameter dilakukan menggunakan **GridSearchCV**.
5. Validasi model menggunakan **10-Fold Cross Validation**.
6. Evaluasi model menggunakan Accuracy, Precision, Recall, F1-Score, AUC, Confusion Matrix, dan ROC Curve.
7. Seluruh implementasi dilakukan menggunakan **Python pada Google Colab** dengan library **Scikit-learn**.
