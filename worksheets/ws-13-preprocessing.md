# WS-13: Data Preprocessing

> **Bab 13 — Preprocessing & Persiapan Data untuk Analisis**

---

## Ringkasan Materi

### Data Refinement Pipeline

```
Raw Data → Cleaning → Transformation → Normalization → Processed Data → Analysis Ready
```

Setiap tahap memiliki tujuan berbeda. **Preprocessing bukan langkah teknis biasa** — setiap keputusan preprocessing adalah keputusan riset yang bisa mengubah kesimpulan.

### Empat Prinsip Preprocessing

| Prinsip | Deskripsi |
|---------|----------|
| **Consistency** | Metode sama untuk data yang sama |
| **Transparency** | Setiap langkah terdokumentasi |
| **Reproducibility** | Orang lain bisa mengulang dengan hasil sama |
| **Minimal Distortion** | Ubah sesedikit mungkin; jika normalisasi tidak perlu, jangan lakukan |

### Cleaning Triad

| Masalah | Strategi | Risiko |
|---------|---------|--------|
| **Missing values** | | |
| — Listwise deletion | Missing < 5%, random | Data loss |
| — Mean/median imputation | Sedikit missing, dist. normal | Mengurangi variabilitas |
| — Model-based imputation | Banyak missing, pola sistematis | Introduces dependency |
| — Flag & separate | Missing karena alasan substantif | Kompleksitas analisis |
| **Duplikat** | Identifikasi → verifikasi → hapus | False positive (data mirip ≠ duplikat) |
| **Error format** | Standardisasi tipe, encoding | Kehilangan informasi saat konversi |

### Normalisasi — Kapan & Metode Mana

| Metode | Formula | Output | Sensitif Outlier? |
|--------|---------|--------|-------------------|
| Min-max | (x-min)/(max-min) | [0, 1] | Ya |
| Z-score | (x-mean)/std | Unbounded | Lebih robust |
| Robust scaling | (x-median)/IQR | Unbounded | Paling robust |

**Kunci:** Parameter normalisasi harus dihitung dari **training set saja** — bukan seluruh data. Pelanggaran = **data leakage**.

### Data Leakage Prevention

Data leakage terjadi ketika informasi dari test set "bocor" ke preprocessing:
- Normalisasi parameter dari seluruh dataset ← **SALAH**
- Cross-validation dilakukan sebelum split ← **SALAH**
- Feature selection menggunakan label test set ← **SALAH**

### Jebakan Kognitif

1. "Preprocessing cuma teknis — tidak perlu detail" → bisa ubah kesimpulan
2. "Lebih banyak preprocessing = lebih bersih = lebih baik" → over-processing distorsi data
3. "Normalisasi selalu diperlukan" → belum tentu, tergantung metode analisis
4. "Imputation sama untuk semua situasi" → strategi harus sesuai konteks

---

## Template A.13 — Preprocessing Documentation Log

```
PREPROCESSING LOG

Dataset           : NSL-KDD Dataset
Jumlah data awal  : 148.517 records

Cleaning:
| Masalah       | Jumlah Kasus | Penanganan                  | Justifikasi                                          |
| ------------- | ------------ | --------------------------- | ---------------------------------------------------- |
| Missing Value | 0            | Tidak ada tindakan          | Dataset tidak memiliki data kosong                   |
| Duplikat      | 610 data     | Menghapus data duplikat     | Menghindari bias pengulangan data                    |
| Outlier       | 37825 data   | Menghapus dengan metode IQR | Mengurangi data ekstrem yang dapat memengaruhi model |


Transformation:
| Transformasi     | Variabel                | Detail                                  | Alasan                             |
| ---------------- | ----------------------- | --------------------------------------- | ---------------------------------- |
| Label Encoding   | Label                   | Normal → 1, Attack → 0                  | Mengubah label menjadi numerik     |
| One Hot Encoding | protocol_type, Service, Flag | Mengubah kategori menjadi fitur numerik | Algoritma machine learning membutuhkan data numerik |


Normalization:
  Metode    : MinMaxScaler (Min-Max Normalization)
  Formula   : (x - min) / (max - min)
  Output    : Nilai dalam rentang [0, 1]
  Alasan    : Menyamakan skala seluruh fitur numerik agar setiap fitur
              berkontribusi seimbang dalam model, khususnya SVM yang
              sangat sensitif terhadap perbedaan skala antar fitur.
  Parameter : Dihitung dari training set saja (fit_transform pada X_train,
              transform saja pada X_test) — mencegah data leakage.

Leakage Check:
  [✓] Parameter normalisasi dari training set saja
      (scaler.fit_transform(X_train) → scaler.transform(X_test))
  [✓] Tidak ada informasi test set dalam preprocessing
  [✓] Cross-validation dilakukan setelah split 70:30


Jumlah data akhir : 110082 records
Script tersedia   : [✓ ] Ya →Google Colab Notebook path: ____ | [ ] Belum
```

---

## Latihan 1 — Cleaning Plan

Periksa dataset Anda (atau dataset contoh) dan dokumentasikan masalah yang ditemukan.

| Masalah | Jumlah Kasus | Penanganan | Justifikasi |
|---------|-------------|------------|-------------|
| Missing Value | 0 | Tidak ada tindakan | Dataset lengkap |
|Data Duplikat |610 |Menghapus duplicate rows |Menghindari pengulangan data |
|Outlier |37825 |Metode IQR (Interquartile Range) pada fitur duration, src_bytes, dst_bytes |Mengurangi noise dan nilai ekstrem yang dapat memengaruhi decision boundary model |


**Jumlah data sebelum cleaning:** 148517
**Jumlah data setelah cleaning:** 110082
**Persentase data yang hilang/berubah:** 25.88%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| duration | 0 – sangat besar | Tidak merata | Ya| MinMaxScaler | Menyamakan skala ke [0,1]; setelah IQR, outlier ekstrem sudah dibuang |
|src_bytes |Nilai tinggi bervariasi |Tidak normal |Ya | MinMaxScaler |Mengurangi perbedaan rentang antar fitur |
|dst_bytes |Nilai tinggi bervariasi | Tidak normal | Ya |MinMaxScaler | Mempermudah training model, khususnya SVM |
|label | 0 atau 1 | Sudah numerik | Tidak | Tidak perlu |Sudah dalam bentuk target biner |

**Apakah normalisasi diperlukan?** [✓ ] Ya / [ ] Tidak
**Justifikasi:**
> Normalisasi diperlukan karena dataset memiliki banyak fitur numerik dengan skala yang sangat berbeda (contoh: fitur duration bernilai 0–58.329, sementara fitur flag hasil one-hot encoding bernilai 0–1). Tanpa normalisasi, algoritma seperti SVM yang berbasis jarak/margin akan didominasi oleh fitur dengan nilai besar, sehingga performa model menjadi suboptimal. MinMaxScaler dipilih karena setelah penghapusan outlier dengan metode IQR, tidak ada lagi nilai ekstrem yang signifikan sehingga sensitivitas MinMaxScaler terhadap outlier tidak menjadi masalah.
> 
**Leakage check:**
- [✓ ] Parameter MinMaxScaler (nilai min dan max) dihitung dari training set saja menggunakan fit_transform(X_train)
- [✓ ] Normalisasi pada data testing hanya menggunakan transform(X_test) — bukan fit_transform
- [✓ ] Normalisasi dilakukan setelah train-test split 70:30

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: NSL-KDD Dataset (gabungan KDDTrain+ dan KDDTest+)
2. Data awal: 148.517 records, 41 fitur asli
3. Cleaning:
   - Missing values: 0 kasus, metode: tidak diperlukan penanganan
   - Duplikat: 610 kasus, tindakan: dihapus
   - Outlier        : 37.825 kasus → dihapus menggunakan metode IQR
                      pada fitur duration, src_bytes, dst_bytes
                      (batas: Q1 - 3×IQR sampai Q3 + 3×IQR)
4. Transformation:
    - Label encoding   : Label dikategorikan biner
                        attack → 0, normal → 1
                        menggunakan LabelEncoder dari scikit-learn
     - One-Hot Encoding : Fitur kategorikal (protocol_type, service, flag)
                        diubah menjadi fitur numerik biner
                        menggunakan pd.get_dummies()
                        Jumlah fitur bertambah dari 41 → 122 fitur
5. Train-Test Split:
   - Rasio : 70% training (77.057 records) : 30% testing (33.025 records)
   - Metode: train_test_split(stratify=y, random_state=42)                        
6. Normalisasi:
   - Metode  : MinMaxScaler (Min-Max Normalization)
   - Formula : (x - min) / (max - min) → output rentang [0, 1]
   - Parameter (min, max) dihitung HANYA dari training set:
     X_train_scaled = scaler.fit_transform(X_train)
     X_test_scaled  = scaler.transform(X_test)
6. Data akhir: 110.082 records, 122 fitur + 1 label
7. Leakage check: [✓ ] Lulus / [ ] Ada masalah
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Pada beberapa eksperimen machine learning, proses normalisasi sering dilakukan karena dianggap sebagai langkah standar. Namun sebenarnya tidak semua model membutuhkan normalisasi. Jika preprocessing dilakukan secara berlebihan, terdapat risiko perubahan distribusi data yang justru dapat memengaruhi performa model. Dalam penelitian ini, normalisasi (MinMaxScaler) dilakukan karena salah satu algoritma yang digunakan adalah SVM yang sangat sensitif terhadap skala data. Selain itu, Decision Tree dan Random Forest juga mendapat manfaat dari skala fitur yang seragam. Oleh karena itu preprocessing dilakukan secukupnya agar kualitas data tetap terjaga tanpa menyebabkan distorsi berlebihan. Dengan preprocessing yang terstruktur dan terdokumentasi, proses eksperimen menjadi lebih valid, dapat direplikasi, dan hasil penelitian dapat dipercaya.
