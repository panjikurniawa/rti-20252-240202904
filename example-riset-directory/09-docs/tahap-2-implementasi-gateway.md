# Tahap 2 — Implementasi Model Machine Learning


**Status:** Selesai
**Acuan arsitektur:** [tahap-1-arsitektur-dan-skema-database.md](tahap-1-arsitektur-dan-skema-database.md)
**Lokasi kode:** [../05-kode/gateway/](../05-kode/gateway/)
**Lokasi kode:** `penelitian_deteksi_intrusi_FIX_SVM.py`


---

## Tujuan

Mengimplementasikan model machine learning untuk mendeteksi intrusi jaringan menggunakan dataset NSL-KDD dengan membandingkan tiga algoritma klasifikasi, yaitu:

- Decision Tree
- Random Forest
- Support Vector Machine (SVM)

Seluruh implementasi dilakukan menggunakan Python pada Google Colab dengan library Scikit-learn.


## Deliverable

- [x] Import dataset NSL-KDD (KDDTrain+ dan KDDTest+)
- [x] Pemeriksaan missing value
- [x] Penghapusan data duplikat
- [x] Penanganan outlier menggunakan metode IQR
- [x] Konversi label menjadi klasifikasi biner (Normal dan Attack)
- [x] One-Hot Encoding pada fitur kategorikal
- [x] Pembagian data Training (70%) dan Testing (30%)
- [x] Normalisasi data menggunakan MinMaxScaler
- [x] Implementasi algoritma Decision Tree
- [x] Implementasi algoritma Random Forest
- [x] Implementasi algoritma Support Vector Machine (SVM)
- [x] Optimasi parameter menggunakan GridSearchCV
- [x] Validasi model menggunakan 10-Fold Cross Validation
- [x] Evaluasi model menggunakan Accuracy, Precision, Recall, F1-Score, AUC, Confusion Matrix, dan ROC Curve
- [x] Penyimpanan hasil evaluasi dalam format CSV
- [x] Pembuatan visualisasi grafik Accuracy dan ROC Curve

## Hasil Implementasi

Seluruh tahapan implementasi berhasil dijalankan sesuai rancangan penelitian.

Tahapan preprocessing berhasil menghasilkan dataset sebanyak **110.082 record** setelah proses penghapusan missing value, data duplikat, dan outlier.

Model kemudian dilatih menggunakan tiga algoritma machine learning, yaitu Decision Tree, Random Forest, dan Support Vector Machine (SVM). Optimasi parameter dilakukan menggunakan GridSearchCV, kemudian setiap model dievaluasi menggunakan 10-Fold Cross Validation serta pengujian pada data testing.

Hasil evaluasi menunjukkan bahwa algoritma **Random Forest** memperoleh performa terbaik dibandingkan dua algoritma lainnya berdasarkan nilai Accuracy, Precision, Recall, F1-Score, dan AUC.

---

## Catatan Implementasi

- Bahasa pemrograman menggunakan **Python**.
- Lingkungan pengembangan menggunakan **Google Colab**.
- Library utama yang digunakan meliputi:
  - Pandas
  - NumPy
  - Scikit-learn
  - Matplotlib
- Support Vector Machine (SVM) menggunakan subset data saat proses Cross Validation dan GridSearchCV untuk mengurangi waktu komputasi pada dataset yang besar.
- Seluruh hasil penelitian disimpan dalam bentuk:
  - `hasil_lengkap.txt`
  - `hasil_cv_10fold.csv`
  - `hasil_perbandingan_model.csv`
  - `perbandingan_model.png`
  - `roc_curve.png`

## Output Penelitian

Implementasi menghasilkan:

- Model Decision Tree
- Model Random Forest
- Model Support Vector Machine (SVM)
- Hasil Cross Validation
- Hasil Grid Search
- Confusion Matrix
- Classification Report
- Grafik Perbandingan Accuracy
- Grafik ROC Curve
- File CSV hasil evaluasi model
