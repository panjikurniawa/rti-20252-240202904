# Arsitektur, Desain, dan Landasan Teori

**Judul Penelitian:** Analisis Penerapan Algoritma Random Forest dalam
Meningkatkan Akurasi Deteksi Intrusi pada Jaringan Komputer
**Peneliti:** Panji Kurniawan | NIM 240202904
**Status:** Selesai (hasil Tahap 1 — Perancangan Metodologi & Desain Sistem)

---

## 1. Arsitektur Komponen Sistem

Penelitian ini merupakan eksperimen komparatif berbasis simulasi (offline).
Tidak ada sistem real-time — seluruh proses berjalan pada dataset statis NSL-KDD
di lingkungan Google Colab.

```mermaid
graph TB
    subgraph INPUT["INPUT — Dataset NSL-KDD"]
        A1["KDDTrain+.txt<br/>125.973 record"]
        A2["KDDTest+.txt<br/>22.544 record"]
    end

    subgraph PREPROCESSING["PREPROCESSING PIPELINE"]
        B1["Penggabungan Data<br/>Total: 148.517 record"]
        B2["Pembersihan Data<br/>Missing value, duplikat (610),<br/>outlier IQR (37.825)"]
        B3["Transformasi Data<br/>Label encoding (attack=0, normal=1)<br/>One-hot encoding (protocol, service, flag)"]
        B4["Split 70:30<br/>Training: 77.057<br/>Testing: 33.025"]
        B5["Normalisasi<br/>MinMaxScaler — fit pada training saja"]
    end

    subgraph MODELS["MODEL MACHINE LEARNING"]
        C1["Decision Tree<br/>Kondisi A (Baseline)<br/>criterion=entropy, max_depth=20"]
        C2["Random Forest<br/>Kondisi B (Intervensi)<br/>n_estimators=200, max_depth=None"]
        C3["SVM<br/>Kondisi A (Baseline)<br/>kernel=RBF, C=10, gamma=scale"]
    end

    subgraph TUNING["HYPERPARAMETER TUNING"]
        D1["Grid Search CV-5<br/>Decision Tree:<br/>criterion × max_depth"]
        D2["Grid Search CV-5<br/>Random Forest:<br/>n_estimators × max_depth"]
        D3["Grid Search CV-5 (subset)<br/>SVM:<br/>C × gamma"]
    end

    subgraph EVALUATION["EVALUASI MODEL"]
        E1["10-Fold Cross-Validation<br/>pada data training"]
        E2["Evaluasi Test Set<br/>Accuracy, Precision,<br/>Recall, F1-Score, AUC"]
        E3["Confusion Matrix<br/>TP / TN / FP / FN"]
        E4["Uji Statistik<br/>Friedman Test + ANOVA<br/>Post-hoc Wilcoxon<br/>Kendall's W + CI 95%"]
    end

    subgraph OUTPUT["OUTPUT"]
        F1["hasil_cv_10fold.csv"]
        F2["hasil_perbandingan_model.csv"]
        F3["perbandingan_model.png"]
        F4["roc_curve.png"]
        F5["hasil_lengkap.txt"]
    end

    A1 --> B1
    A2 --> B1
    B1 --> B2 --> B3 --> B4 --> B5
    B5 --> C1 & C2 & C3
    C1 --> D1 --> E1
    C2 --> D2 --> E1
    C3 --> D3 --> E1
    E1 --> E2 --> E3 --> E4
    E4 --> F1 & F2 & F3 & F4 & F5
```

---

## 2. Alur Preprocessing Data

```mermaid
flowchart TD
    START(["Dataset NSL-KDD\n148.517 record"])

    START --> MV["Cek Missing Value\nmissing = 0\n→ tidak ada tindakan"]
    MV --> DUP["Hapus Duplikat\n610 baris dihapus\n→ 147.907 record"]
    DUP --> OUT["Hapus Outlier (IQR)\nFitur: duration, src_bytes, dst_bytes\nIQR multiplier: 3×\n37.825 baris dihapus\n→ 110.082 record"]
    OUT --> LABEL["Label Encoding (Biner)\nnormal  → 1\nattack  → 0\n(LabelEncoder, alfabetis)"]
    LABEL --> OHE["One-Hot Encoding\nprotocol_type, service, flag\n41 fitur asli → 122 fitur"]
    OHE --> SPLIT["Train-Test Split 70:30\nstratify=y, random_state=42\nTraining: 77.057 | Testing: 33.025"]
    SPLIT --> NORM["Normalisasi MinMaxScaler\nfit_transform pada X_train\ntransform pada X_test\noutput: rentang 0–1"]
    NORM --> DONE(["Data Siap\n110.082 record | 122 fitur"])
```

---

## 3. Alur Eksperimen dan Evaluasi

```mermaid
flowchart TD
    DATA(["Data Training (70%)\n77.057 record"])
    SUBSET(["Subset SVM\nCV & Grid Search: 15.000\nFinal training: 30.000"])

    DATA --> CV10["10-Fold Cross-Validation\nDecision Tree — data penuh\nRandom Forest — data penuh\nSVM — subset 15.000"]
    DATA --> GS_DT["Grid Search CV-5 (DT)\ncriterion: gini, entropy\nmax_depth: 10, 20, 30, None\n→ best: entropy, depth=20"]
    DATA --> GS_RF["Grid Search CV-5 (RF)\nn_estimators: 100, 200\nmax_depth: 10, 20, None\n→ best: 200, depth=None"]
    SUBSET --> GS_SVM["Grid Search CV-5 (SVM)\nC: 1, 10\ngamma: scale, 0.01\n→ best: C=10, gamma=scale"]

    GS_DT --> TRAIN_DT["Training Final DT\ndata penuh, best params\n⏱ 0.66 detik"]
    GS_RF --> TRAIN_RF["Training Final RF\ndata penuh, best params\n⏱ 16.58 detik"]
    GS_SVM --> TRAIN_SVM["Training Final SVM\nsubset 30.000, best params\n⏱ 46.10 detik"]

    TEST(["Data Testing (30%)\n33.025 record"])
    TRAIN_DT & TRAIN_RF & TRAIN_SVM --> EVAL["Evaluasi pada Test Set\nAccuracy | Precision | Recall\nF1-Score | AUC\nConfusion Matrix"]
    TEST --> EVAL

    CV10 --> STAT["Uji Statistik\nShapiro-Wilk (normalitas)\nFriedman Test (χ²=17.897, p=0.00013)\nRepeated-Measures ANOVA (F=156.49)\nPost-hoc Wilcoxon (Bonferroni)\nKendall's W = 0.895\nCI 95% per model"]
    EVAL --> STAT
    STAT --> RESULT(["Kesimpulan\nH1 diterima:\nRandom Forest signifikan terbaik"])
```

---

## 4. Desain Variabel Penelitian

### 4.1 Variabel Independen (IV)

Algoritma machine learning yang digunakan — bersifat kategorikal dengan 3 kategori:

| Kategori | Algoritma | Kondisi |
|---|---|---|
| Kondisi A (Baseline) | Decision Tree | Model tree-based tunggal, interpretable |
| Kondisi A (Baseline) | Support Vector Machine (SVM) | Model margin-based, kernel RBF |
| **Kondisi B (Intervensi)** | **Random Forest** | Ensemble dari 200 pohon keputusan |

### 4.2 Variabel Dependen (DV)

Performa deteksi intrusi — diukur secara numerik pada test set yang sama (33.025 record):

| Metrik | Tipe Data | Range Valid | Keterangan |
|---|---|---|---|
| Accuracy | float | [0, 1] | Proporsi prediksi benar dari total |
| Precision | float | [0, 1] | TP / (TP + FP) — menghindari false positive |
| Recall | float | [0, 1] | TP / (TP + FN) — menghindari false negative |
| F1-Score | float | [0, 1] | Harmonic mean precision & recall |
| AUC | float | [0, 1] | Area Under ROC Curve |

---

## 5. Skema Dataset NSL-KDD

NSL-KDD terdiri dari **41 fitur asli** yang merepresentasikan karakteristik
koneksi jaringan, dikategorikan sebagai berikut:

```mermaid
erDiagram
    NSL_KDD_RECORD {
        varchar     label           "target: normal / attack (binary)"
        int         duration        "lama koneksi (detik)"
        varchar     protocol_type   "TCP / UDP / ICMP — one-hot encoded"
        varchar     service         "http, ftp, smtp, dll — one-hot encoded"
        varchar     flag            "SF, S0, REJ, dll — one-hot encoded"
        bigint      src_bytes       "bytes dari source ke destination"
        bigint      dst_bytes       "bytes dari destination ke source"
        int         land            "koneksi ke host/port sendiri (1/0)"
        int         wrong_fragment  "jumlah fragment salah"
        int         urgent          "jumlah paket urgent"
        int         hot             "jumlah hot indicators"
        int         num_failed_logins "jumlah percobaan login gagal"
        int         logged_in       "berhasil login (1/0)"
        int         count           "koneksi ke host yang sama (2 detik terakhir)"
        int         srv_count       "koneksi ke service yang sama"
        float       serror_rate     "% koneksi dengan SYN error"
        float       rerror_rate     "% koneksi dengan REJ error"
        float       same_srv_rate   "% koneksi ke service yang sama"
        float       diff_srv_rate   "% koneksi ke service berbeda"
        int         dst_host_count  "koneksi ke destination host"
        float       dst_host_srv_rate "% koneksi ke service yang sama di dst host"
    }

    LABEL_ENCODING {
        varchar     original_label  "normal, neptune, smurf, portsweep, dll"
        int         binary_label    "normal=1, attack=0"
    }

    NSL_KDD_RECORD ||--|| LABEL_ENCODING : "di-encode ke"
```

**Kategori serangan di NSL-KDD:**

| Kategori | Contoh Serangan | Deskripsi |
|---|---|---|
| **DoS** | neptune, smurf, back | Denial of Service — menghabiskan resource |
| **Probe** | portsweep, nmap, satan | Scanning jaringan untuk mengidentifikasi kelemahan |
| **R2L** | ftp_write, guess_passwd | Remote to Local — akses tidak sah dari luar |
| **U2R** | buffer_overflow, rootkit | User to Root — eskalasi privilege |
| **Normal** | — | Trafik jaringan normal |

---

## 6. Landasan Teori Algoritma

### 6.1 Decision Tree

Decision Tree membagi dataset secara rekursif berdasarkan fitur yang paling
informatif (menggunakan kriteria impurity seperti Gini atau Entropy) hingga
terbentuk model berbentuk pohon keputusan yang dapat digunakan untuk klasifikasi.

**Karakteristik:**
- Interpretable — aturan keputusan dapat dibaca langsung
- Cepat saat prediksi (O(log n) terhadap jumlah node)
- Rentan overfitting pada data kompleks

**Parameter terbaik pada penelitian ini:**
```
criterion  = entropy  (Information Gain)
max_depth  = 20
```

**Formula Information Gain:**
```
IG(S, A) = H(S) - Σ (|Sv|/|S|) × H(Sv)
H(S) = -Σ p(c) × log₂(p(c))     (Shannon Entropy)
```

### 6.2 Random Forest

Random Forest adalah metode ensemble yang membangun banyak Decision Tree secara
independen pada subset acak data (bagging) dan fitur (feature randomness), lalu
menggabungkan prediksi melalui majority voting.

**Karakteristik:**
- Mengurangi variance melalui ensemble (mengatasi overfitting DT tunggal)
- Robust terhadap noise dan outlier
- Waktu training lebih lama dari DT tunggal

**Parameter terbaik pada penelitian ini:**
```
n_estimators = 200  (jumlah pohon)
max_depth    = None (pohon tumbuh penuh)
random_state = 42
```

**Formula prediksi (majority voting):**
```
ŷ = mode({ T₁(x), T₂(x), ..., T_B(x) })
di mana T_b adalah pohon ke-b dari B pohon total
```

### 6.3 Support Vector Machine (SVM)

SVM mencari hyperplane dengan margin maksimum yang memisahkan dua kelas data.
Untuk data non-linear, kernel trick (RBF) digunakan untuk memetakan data ke
dimensi yang lebih tinggi di mana pemisahan linear memungkinkan.

**Karakteristik:**
- Efektif di ruang dimensi tinggi
- Kompleksitas komputasi O(n²)–O(n³) — berat untuk data besar
- Sensitif terhadap skala fitur (perlu normalisasi)

**Parameter terbaik pada penelitian ini:**
```
kernel       = rbf   (Radial Basis Function)
C            = 10    (regularization parameter)
gamma        = scale (= 1 / (n_features × X.var()))
probability  = True  (untuk perhitungan AUC)
```

**Catatan implementasi:** SVM dilatih pada subset 30.000 record dari 77.057
data training karena keterbatasan komputasi kernel RBF pada dataset besar.

**Formula kernel RBF:**
```
K(x, x') = exp(-γ × ||x - x'||²)
```

---

## 7. Landasan Teori Evaluasi

### 7.1 Metrik Klasifikasi

Diturunkan dari Confusion Matrix (TP, TN, FP, FN):

```
Accuracy  = (TP + TN) / (TP + TN + FP + FN)
Precision = TP / (TP + FP)
Recall    = TP / (TP + FN)
F1-Score  = 2 × (Precision × Recall) / (Precision + Recall)
```

**Dalam konteks deteksi intrusi:**
- TP = serangan yang berhasil terdeteksi (attack diprediksi attack)
- FN = serangan yang lolos (attack diprediksi normal) — **paling kritis**
- FP = false alarm (normal diprediksi attack)

### 7.2 Uji Statistik

Karena membandingkan lebih dari 2 grup berpasangan (paired, data dari fold yang sama):

| Uji | Fungsi | Hasil |
|---|---|---|
| Shapiro-Wilk | Uji normalitas distribusi 10-fold per model | Ketiga model normal (p > 0.05) |
| Friedman Test | Uji signifikansi perbedaan >2 grup berpasangan | χ²=17.897, **p=0.00013** |
| Repeated-Measures ANOVA | Konfirmasi (data lolos normalitas) | F=156.49, p<0.0001 |
| Kendall's W | Effect size untuk Friedman test | W=0.895 **(Large)** |
| Wilcoxon Signed-Rank | Post-hoc berpasangan (Bonferroni α=0.0167) | Semua pasangan signifikan |
| Confidence Interval 95% | Rentang ketidakpastian mean per model | DT [99.43%,99.55%], RF [99.54%,99.61%], SVM [98.07%,98.51%] |

---

## 8. Keputusan Desain Penelitian

| Aspek | Keputusan | Justifikasi |
|---|---|---|
| Skema split data | Gabung KDDTrain+ + KDDTest+, split ulang 70:30 acak | Sesuai proposal; distribusi lebih homogen |
| Normalisasi | MinMaxScaler (bukan Z-score/StandardScaler) | Sesuai script implementasi; cocok untuk SVM yang sensitif skala |
| Penanganan outlier | IQR multiplier 3× pada duration, src_bytes, dst_bytes | Threshold konservatif agar data serangan (yang secara alami ekstrem) tidak terhapus berlebihan |
| Subset SVM | 15.000 (CV) / 30.000 (final training) | Kernel RBF O(n²–n³) tidak scalable pada 77.057 record — dicatat sebagai limitation |
| Random seed | 42 di semua level | Reproducibility — hasil identik saat dijalankan ulang |
| Uji statistik | Friedman (utama) + ANOVA (konfirmasi) | Data berpasangan (10-fold), >2 grup; Friedman konservatif untuk n kecil |

---

## 9. Mapping ke Implementasi Kode

| Komponen | Implementasi | File |
|---|---|---|
| Preprocessing pipeline | `pandas.get_dummies()`, `LabelEncoder`, `MinMaxScaler`, `train_test_split` | `penelitian_deteksi_intrusi_FIX_SVM.py` STEP 2–8 |
| Subset SVM | `np.random.choice(..., replace=False)` dengan `seed=42` | STEP 9B |
| Cross-validation | `cross_val_score(..., cv=10, n_jobs=-1)` | STEP 10 |
| Grid search | `GridSearchCV(..., cv=5, n_jobs=-1)` | STEP 11–13 |
| Evaluasi metrik | `accuracy_score`, `precision_score`, `recall_score`, `f1_score`, `roc_auc_score` | STEP 14 |
| Visualisasi | `matplotlib.pyplot` — bar chart + ROC curve | STEP 16–17 |
| Uji statistik | `scipy.stats.friedmanchisquare`, `scipy.stats.wilcoxon`, `scipy.stats.shapiro` | Analisis terpisah (WS-14) |

**Acuan lengkap:** [`05-kode/penelitian_deteksi_intrusi_FIX_SVM.py`](../05-kode/)
