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
Jumlah data awal  : 148517 records

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
| One Hot Encoding | Protocol, Service, Flag | Mengubah kategori menjadi fitur numerik | Algoritma membutuhkan data numerik |


Normalization:
  Metode    : StandardScaler (Z-Score Normalization)
  Alasan    : Menyamakan skala data agar model SVM bekerja lebih optimal
  Parameter : Training set saja

Leakage Check:
  [✓ ] Parameter normalisasi dari training set saja
  [✓ ] Tidak ada informasi test set dalam preprocessing
  [✓ ] Cross-validation dilakukan setelah split

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
|Outlier |37825 |Metode IQR |Mengurangi noise pada data |


**Jumlah data sebelum cleaning:** 148517
**Jumlah data setelah cleaning:** 110082
**Persentase data yang hilang/berubah:** 25.88%

---

## Latihan 2 — Normalisasi Decision

Tentukan apakah data Anda perlu normalisasi, dan jika ya, metode apa yang tepat.

| Variabel | Range Asli | Distribusi | Outlier? | Metode Normalisasi | Alasan |
|----------|-----------|-----------|----------|-------------------|--------|
| duration | 0 – sangat besar | Tidak merata | Ya| StandardScaler | Menyamakan skala |
|src_bytes |Nilai tinggi bervariasi |Tidak normal |Ya |StandardScaler |Mengurangi perbedaan rentang |
|dst_bytes |Nilai tinggi bervariasi | Tidak normal | Ya |StandardScaler | Mempermudah training model |
|label | 1-0 | Sudah numerik | Tidak | Tidak perlu |Sudah dalam bentuk target|

**Apakah normalisasi diperlukan?** [✓ ] Ya / [ ] Tidak
**Justifikasi:**
> Normalisasi diperlukan karena dataset memiliki banyak fitur numerik dengan skala berbeda. Tanpa normalisasi, algoritma seperti SVM dapat menghasilkan performa yang kurang optimal karena sensitif terhadap perbedaan skala antar fitur.

**Leakage check:**
- [✓ ] Parameter dihitung dari training set saja
- [✓ ] Normalisasi diterapkan setelah train-test split

---

## Latihan 3 — Preprocessing Report

Buat ringkasan preprocessing lengkap — dokumentasi yang cukup bagi orang lain untuk mereplikasi.

```
PREPROCESSING SUMMARY

1. Dataset: NSL-KDD Dataset
2. Data awal: 148517 records, 41 features
3. Cleaning:
   - Missing values: 0 kasus, metode: tidak diperlukan penanganan
   - Duplikat: 610 kasus, tindakan: dihapus
   - Error: 37825 kasus, tindakan: dihapus menggunakan metode IQR
4. Transformation: Label encoding pada target klasifikasi
                   One Hot Encoding pada fitur kategorikal
5. Normalisasi: StandardScaler (Z-Score) (metode), parameter dari training set
6. Data akhir: 110082 records, 122 features + 1 label
7. Leakage check: [✓ ] Lulus / [ ] Ada masalah
```

---

## Refleksi

> Apakah Anda pernah melakukan normalisasi "karena biasa dilakukan" tanpa mempertimbangkan apakah benar-benar diperlukan? Apa risiko over-preprocessing?

> Pada beberapa eksperimen machine learning, proses normalisasi sering dilakukan karena dianggap sebagai langkah standar. Namun sebenarnya tidak semua model membutuhkan normalisasi. Jika preprocessing dilakukan secara berlebihan, terdapat risiko perubahan distribusi data yang justru dapat memengaruhi performa model.
Dalam penelitian ini, normalisasi dilakukan karena salah satu algoritma yang digunakan adalah SVM yang sangat sensitif terhadap skala data. Oleh karena itu preprocessing dilakukan secukupnya agar kualitas data tetap terjaga tanpa menyebabkan distorsi berlebihan.
> Dengan preprocessing yang terstruktur, proses eksperimen menjadi lebih valid dan hasil penelitian dapat dipercaya.
