# WS-09: Implementation & Environment

> **Bab 9 — Implementasi Riset & Kontrol Lingkungan**

---

## Ringkasan Materi

### Implementasi Riset ≠ Coding Biasa

Tujuan implementasi riset bukan membuat software yang berfungsi, melainkan membangun **instrumen pengukuran yang konsisten**. Setiap modul harus di-mapping ke variabel (dari Bab 6), parameter harus config-driven, dan logging aktif dari hari pertama.

> **Mengapa reproducibility penting?** Sains dibangun di atas prinsip verifikasi — temuan harus bisa dikonfirmasi oleh peneliti lain. _Replicability crisis_ yang terjadi di banyak paper riset ML/AI disebabkan oleh environment tidak terdokumentasi: orang lain tidak bisa reproduksi, hasil diragukan, kepercayaan terhadap temuan hilang. Prinsip: **dokumentasi environment = snapshot kredibilitas riset Anda.**

### Reproducible Implementation Model

```
Design → Implementation → Environment Setup → Execution Consistency → Reproducibility → Trustworthy Result
```

Setiap transisi memiliki syarat:
- Design → Implementation: kode sesuai mapping variabel-ke-komponen
- Implementation → Environment: versi, dependency, seed, path, OS eksplisit
- Environment → Consistency: seed terkunci, urutan deterministik
- Consistency → Reproducibility: dokumentasi lengkap
- Reproducibility → Trust: siapa pun ikuti dokumentasi → hasil sama/serupa

### Repeatability vs Reproducibility

| Level | Peneliti | Environment | Hasil |
|-------|---------|-------------|-------|
| **Repeatability** | Sama | Sama | Sama persis |
| **Reproducibility** | Berbeda | Berbeda (ikuti docs) | Sama/serupa |

Capai **repeatability** dulu, baru **reproducibility**.

### Engineering vs Research Perspective

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Sistem berfungsi untuk user | Instrumen pengukuran konsisten |
| Dependency | Update ke terbaru | Lock di versi spesifik |
| Testing | Unit, integration, E2E | Repeatability test (run ulang → sama?) |
| Dokumentasi | User guide, API docs | Environment spec, execution steps, expected output |
| Config | Default masuk akal | Setiap parameter eksplisit & adjustable |

### Jebakan Kognitif

1. Menunda environment setup → bug sulit dilacak
2. Tidak pakai version control → hasil tidak bisa direkonstruksi
3. Menolak Docker/container → "di laptop saya bisa" saat review
   - **Docker** = teknologi container yang "membungkus" aplikasi beserta seluruh dependency-nya dalam satu unit terisolasi. Hasilnya: kode berjalan identik di laptop, server, maupun reviewer lain. Intro singkat: `docker run -v $(pwd):/workspace environment-image python run_experiment.py`
4. 3× hasil sama ≠ repeatable (bisa cache/state tersimpan)

### Dependency Locking

Mengandalkan "install library terbaru" berbahaya: versi berbeda = perilaku berbeda = hasil tidak reproducible. Praktik:
- **Python**: buat `requirements.txt` dengan versi eksplisit: `scikit-learn==1.3.2`, lalu kunci dengan `pip freeze > requirements.txt`
- **Conda**: gunakan `conda env export > environment.yml` untuk snapshot lengkap
- **Node.js/R/Julia**: gunakan `package-lock.json` / `renv.lock` / `Project.toml` — semua fungsi serupa: lock versi + hash

### Istilah Penting

- **Environment Specification** — Deskripsi lengkap: hardware, OS, runtime, library + versi, config, seed
- **Dependency** — Komponen eksternal yang harus di-lock versinya
- **Config-driven** — Parameter dieksternalisasi ke file konfigurasi, bukan hardcode

---

## Template A.9 — Dokumentasi Setup Eksperimen

```
EXPERIMENT SETUP DOCUMENTATION

Hardware:
  CPU     : Google Colab CPU Runtime (Intel Xeon / AMD EPYC — shared)
  RAM     : 12 GB (Google Colab Standard allocation)
  GPU     : Tidak digunakan (CPU Only — semua komputasi di CPU)
  Storage :  Google Colab Temporary Storage (/content/)

Software:
  OS        : Linux Ubuntu 22.04 (Google Colab Environment)
  Runtime   : Python 3.11.x
  Framework : scikit-learn, pandas, numpy, matplotlib, scipy

Dependencies:
| Library | Version | Sumber | cara install |
|---------|---------|--------|---------------|
| pandas  |  2.2.2  | Google Colab default | pip install pandas==2.2.2  |
| numpy   |  1.26.4 | Google Colab default |  pip install numpy==1.26.4 |
| scikit-learn | 1.4.2  | Google Colab default | pip install scikit-learn==1.4.2 |
| matplotlib | 3.8.4  | Google Colab default |  pip install matplotlib==3.8.4 |
| scipy   | 1.13.0 | Google Colab default | pip install scipy==1.13.0 |

Konfigurasi:
  Config file     : penelitian_deteksi_intrusi_FIX_SVM.py
  Random seed     : 42 (dikunci di semua level:
                    train_test_split(..., random_state=42),
                    DecisionTreeClassifier(random_state=42),
                    RandomForestClassifier(random_state=42),
                    SVC(random_state=42),
                    np.random.seed(42))
  Hyperparameters : GridSearchCV untuk Decision Tree, Random Forest, SVM
                    (parameter grid terdokumentasi di script)

Reproducibility Check:
  [✓ ] Dependency terdokumentasi (requirements.txt / lock file)
  [✓ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [✓ ] Config di version control
  [✓ ] README instruksi reproduksi lengkap
  [✓] Dataset dapat didownload otomatis via wget (tercantum di script)
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Google Colab CPU Runtime (shared, tidak ada GPU) |
| RAM | 12 GB (Google Colab Standard) |
| GPU | Tidak digunakan |
| OS | Linux Ubuntu 22.04 (Google Colab Environment) |
| Runtime |Python 3.11.x |
| Framework |scikit-learn 1.4.2 |
| Random Seed |42 (semua level: model, split data, numpy) |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| pandas | 2.2.2 | Membaca dataset CSV, manipulasi DataFrame (read_csv, get_dummies, drop_duplicates) |
|numpy |1.26.4 |Operasi array numerik, random seed (np.random.seed), perhitungan statistik dasar |
|scikit-learn |1.4.2 |Training model (DT, RF, SVM), preprocessing (MinMaxScaler, LabelEncoder), evaluasi (accuracy_score, roc_curve, dll), CV & GridSearchCV |
|matplotlib |3.8.4 |Membuat visualisasi bar chart accuracy dan ROC curve |
|scipy |1.13.0 |Uji statistik: Friedman test, Wilcoxon signed-rank, Shapiro-Wilk, confidence interval (digunakan di analisis WS-14, bukan di script utama)|

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 | Accuracy RF = 0.9961 | Baseline |
| 2 |42 |Accuracy RF = 0.9961 | [✓ ] Ya / [ ] Tidak |
| 3 |42 |Accuracy RF = 0.9961 | [✓ ] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

> Versi library berbeda -> Cek pip show scikit-learn -> Gunakan versi spesifik di requirements.txt
> Random state tidak dikunci di semua level -> Cek apakah np.random.seed(42) ada -> Tambahkan seed di semua komponen stokastik
> Dataset berbeda/berubah -> Bandingkan jumlah record (harus 148.517 awal) -> Download ulang dari URL yang sama (GitHub defcom17)
> Cache Colab dari session lama -> Hasil berbeda meski seed sama -> Runtime → Restart runtime → jalankan ulang dari awal


**Checklist kontrol yang sudah diterapkan:**
- [✓ ] Random seed dikunci di semua level (train_test_split, DT, RF, SVM, numpy)
- [✓ ] Dataset didownload dari URL tetap (raw.githubusercontent.com/defcom17/NSL_KDD)
- [✓ ] Tidak ada state tersimpan antar-run (script dijalankan fresh setiap kali)
- [✓ ] Config file (script Python) sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Analisis Implementasi Machine Learning untuk Deteksi Intrusi pada Jaringan Komputer

## 1. Environment
> Platform  : Google Colab (CPU Runtime, 12GB RAM)
> OS        : Linux Ubuntu 22.04 (Colab environment)
> Python    : 3.11.x

> Dependencies (versi spesifik):
  pandas==2.2.2
  numpy==1.26.4
  scikit-learn==1.4.2
  matplotlib==3.8.4
  scipy==1.13.0


## 2. Installation
> Install library menggunakan command:
pip install pandas==2.2.2 numpy==1.26.4 scikit-learn==1.4.2 \
              matplotlib==3.8.4 scipy==1.13.0

## 3. Data
> Dataset yang digunakan adalah NSL-KDD yang berisi data trafik jaringan normal dan data serangan.
File:
- KDDTrain+.txt (125.973 record, data training asli)
- KDDTest+.txt  (22.544 record, data testing asli)

## 4. Execution
> Menjalankan file eksperimen pada Google Colab:
  python penelitian_deteksi_intrusi_FIX_SVM.py


## 5. Configuration
> Random seed   : 42 (semua level — model, split, numpy)
> Train-test    : 70% training / 30% testing (stratified)
> CV            : 10-fold cross-validation
> Normalisasi   : MinMaxScaler (fit pada training saja)
> SVM subset    : 15.000 (CV & grid search) / 30.000 (final training)

> Best parameters dari grid search:
  Decision Tree : criterion=entropy, max_depth=20
  Random Forest : n_estimators=200, max_depth=None
  SVM           : C=10, gamma=scale


## 6. Expected Output
> Output yang dihasilkan:
hasil_cv_10fold.csv          — 10 nilai akurasi fold per model
  hasil_perbandingan_model.csv — ringkasan metrik evaluasi final
  perbandingan_model.png       — bar chart perbandingan accuracy
  roc_curve.png                — ROC curve ketiga model
  hasil_lengkap.txt            — log output seluruh proses

Nilai yang diharapkan (hasil aktual):
  Decision Tree : Accuracy 99.58%, F1 99.52%, AUC 0.9961
  Random Forest : Accuracy 99.61%, F1 99.55%, AUC 0.9997 ← TERBAIK
  SVM           : Accuracy 99.09%, F1 98.96%, AUC 0.9993

Estimasi waktu:
  Cross-validation : ~2 menit (DT + RF data penuh, SVM subset)
  Grid search      : ~7 menit (DT cepat, RF & SVM lebih lama)
  Final training   : ~1 menit
  Total            : ±10–15 menit
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [✓ ] Repeatability / [✓ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Eksperimen ini sudah mencapai level repeatability (terbukti dari
dua run dengan seed 42 menghasilkan angka identik hingga 7 desimal)
dan mendekati level reproducibility — siapapun yang mengikuti
README di atas dapat mereproduksi hasil yang sama.

Komponen yang masih bisa ditingkatkan untuk reproducibility penuh:
(1) Membuat requirements.txt dengan output pip freeze dari
environment Colab aktual untuk mengunci semua dependency transitif
(bukan hanya 5 library utama), dan (2) mencantumkan versi Python
yang lebih spesifik (misalnya 3.11.7) karena versi minor pun
bisa mempengaruhi perilaku beberapa library.

Pelajaran utama dari WS-09: dokumentasi environment bukan formalitas —
ini yang menentukan apakah hasil penelitian bisa diverifikasi orang lain
atau tidak. Tanpa versi spesifik, orang yang mencoba mereproduksi
bisa mendapat hasil berbeda hanya karena scikit-learn 1.5.x
mengubah default parameter yang tidak kita sadari.
