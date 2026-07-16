# Tahap 3 — Pengujian Model Machine Learning

**Status:** Selesai 
**Bergantung pada:** [tahap-2-implementasi-gateway.md](tahap-2-implementasi-gateway.md)
**Lokasi kode:** `penelitian_deteksi_intrusi_FIX_SVM.py`

---

## Tujuan

Melakukan pengujian terhadap tiga algoritma machine learning untuk mengetahui algoritma yang memiliki performa terbaik dalam mendeteksi intrusi jaringan menggunakan dataset NSL-KDD.

Algoritma yang diuji meliputi:

- **Decision Tree**
- **Random Forest**
- **Support Vector Machine (SVM)**

Pengujian dilakukan menggunakan metode **10-Fold Cross Validation**, **GridSearchCV**, dan evaluasi pada data testing.


## Deliverable

- [x] Pengujian Decision Tree
- [x] Pengujian Random Forest
- [x] Pengujian Support Vector Machine (SVM)
- [x] Validasi menggunakan 10-Fold Cross Validation
- [x] Optimasi parameter menggunakan GridSearchCV
- [x] Pengujian menggunakan data testing
- [x] Perhitungan Accuracy
- [x] Perhitungan Precision
- [x] Perhitungan Recall
- [x] Perhitungan F1-Score
- [x] Perhitungan Area Under Curve (AUC)
- [x] Confusion Matrix
- [x] Classification Report
- [x] Visualisasi Perbandingan Accuracy
- [x] Visualisasi ROC Curve
- [x] Penyimpanan hasil dalam format CSV dan TXT

      
## Desain Pengujian

### Algoritma yang Dibandingkan

| Algoritma | Keterangan |
|---|---|
| Decision Tree | Algoritma pembanding pertama (baseline). |
| Random Forest | Algoritma utama yang dianalisis. |
| Support Vector Machine (SVM) | Algoritma pembanding kedua. |


### Tahapan Pengujian

Dataset NSL-KDD
        │
        ▼
Preprocessing
        │
        ▼
Train-Test Split (70 : 30)
        │
        ▼
Normalisasi Data
        │
        ▼
GridSearchCV
        │
        ▼
10-Fold Cross Validation
        │
        ▼
Training Model
        │
        ▼
Testing Model
        │
        ▼
Evaluasi Model


### Parameter Pengujian
Model dievaluasi menggunakan beberapa parameter berikut :

| Parameter | Fungsi |
|---|---|
| Accuracy | Mengukur ketepatan klasifikasi. |
|  Precision | Mengukur ketepatan prediksi positif. |
| Recall | Mengukur kemampuan mendeteksi data positif. | 
| F1-Score | Kombinasi Precision dan Recall. |
| AUC | Mengukur kemampuan klasifikasi model. |
| Confusion Matrix | Menampilkan hasil klasifikasi benar dan salah. |
| ROC Curve | Membandingkan performa ketiga algoritma. |

### Hasil PengujianPengujian berhasil dilakukan terhadap ketiga algoritma machine learning.

### Hasil Cross Validation

| Algoritma | Mean Accuracy |
|---|---|
| Decision Tree | **99,49%** |
|  Random Forest |**99,57%** |
| SVM | **98,29%** | 


### Hasil Pengujian Data Testing

| Algoritma | Accuracy | Precision | Recall | F1-Score | AUC |
|---|---:|---:|---:|---:|---:|
| Decision Tree | 99,58% | 99,54% | 99,49% | 99,52% | 0,9961 |
| Random Forest | **99,61%** | **99,55%** | **99,56%** | **99,55%** | **0,9997** |
| SVM | 99,09% | 99,29% | 98,63% | 98,96% | 0,9993 |


## Kesimpulan Tahap Pengujian

Berdasarkan hasil pengujian menggunakan 10-Fold Cross Validation dan data testing, algoritma **Random Forest** memperoleh performa terbaik dibandingkan Decision Tree dan Support Vector Machine (SVM). Random Forest menghasilkan nilai Accuracy, Recall, F1-Score, dan AUC tertinggi sehingga dipilih sebagai algoritma yang paling efektif dalam mendeteksi intrusi jaringan menggunakan dataset NSL-KDD.

---


## Catatan Implementasi

- Seluruh eksperimen dilakukan menggunakan **Python** pada **Google Colab**.
- Optimasi parameter dilakukan menggunakan **GridSearchCV**.
- Validasi model menggunakan **10-Fold Cross Validation**.
- Support Vector Machine (SVM) menggunakan subset data saat proses Cross Validation dan GridSearchCV untuk mengurangi waktu komputasi pada dataset yang besar.
- Hasil pengujian divisualisasikan dalam bentuk grafik Accuracy dan ROC Curve untuk mempermudah analisis performa masing-masing algoritma.
