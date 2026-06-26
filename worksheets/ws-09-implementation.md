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
  CPU     : Intel Core i5 / AMD Ryzen 5 (menggunakan Google Colab CPU Runtime)
  RAM     : 12 GB (Google Colab Standard)
  GPU     : Tidak digunakan (CPU Only)
  Storage : Google Drive + Colab Temporary Storage

Software:
  OS        : Linux Ubuntu (Environment Google Colab)
  Runtime   : Python 3.11
  Framework : Scikit-Learn, Pandas, NumPy, Matplotlib


Dependencies:
| Library | Version | Sumber | Hash/Checksum |
|---------|---------|--------|---------------|
| pandas  |  2.x    | Google Colab | Default package |
| numpy   |  1.x    | Google Colab | Default package |
| scikit-learn | 1.x | Google Colab | Default package |
| matplotlib | 3.x | Google Colab | Default package |
| seaborn | 0.x | Google Colab | Default package |

Konfigurasi:
  Config file     : penelitian_final_proposal.py
  Random seed     : 42
  Hyperparameters : GridSearchCV untuk Decision Tree, Random Forest, dan SVM

Reproducibility Check:
  [✓ ] Dependency terdokumentasi (requirements.txt / lock file)
  [✓ ] Seed ditetapkan di semua level (Python, NumPy, framework)
  [✓ ] Config di version control
  [✓ ] README instruksi reproduksi lengkap
```

---

## Latihan 1 — Environment Specification

Dokumentasikan environment untuk eksperimen Anda (boleh environment saat ini atau yang direncanakan).

| Komponen | Spesifikasi |
|----------|------------|
| CPU | Google Colab CPU Runtime |
| RAM | 12 GB |
| GPU | Tidak digunakan |
| OS | Linux Ubuntu (Google Colab Environment) |
| Runtime |Python 3.11 |
| Framework |Scikit-Learn |
| Random Seed |42 |

**Dependencies (minimal 5):**

| Library | Version | Alasan Dibutuhkan |
|---------|---------|-------------------|
| pandas | 2.x | Membaca dan memproses dataset |
|numpy |1.x |Operasi numerik dan array |
|scikit-learn |1.x |Training model machine learning |
|matplotlib |3.x |Membuat visualisasi grafik |
|seaborn |0.x |Membantu analisis visual tambahan |

---

## Latihan 2 — Repeatability Test Plan

Rancang tes repeatability sederhana: jalankan kode yang sama 3× di environment yang sama.

| Run | Seed | Metrik Utama | Hasil Sama? |
|-----|------|-------------|-------------|
| 1 | 42 | Accuracy | — |
| 2 |42 |Accuracy | [✓ ] Ya / [ ] Tidak |
| 3 |42 |Accuracy | [✓ ] Ya / [ ] Tidak |

**Jika hasil berbeda, kemungkinan penyebab:**

> Penyebab umum non-repeatability:
> - **Thermal throttling** — CPU/GPU overheating pada run berturut-turut → clock speed turun → waktu eksekusi berubah
> - **Background process** — antivirus scan, update OS, atau cloud sync aktif saat run berlangsung
> - **Cache dari run sebelumnya** — hasil tersimpan di memori/disk sehingga run berikutnya tidak menjalankan komputasi penuh
> - **Random state tidak dikontrol di semua level** — Python seed di-set, tapi NumPy/PyTorch/TensorFlow punya seed independen

Perbedaan hasil eksperimen biasanya terjadi karena kondisi runtime yang berubah, proses background pada Google Colab, cache yang belum dibersihkan, atau random seed yang tidak dikunci secara konsisten pada setiap library yang digunakan.

**Checklist kontrol yang sudah diterapkan:**
- [✓ ] Random seed di-set di semua level
- [✓ ] Tidak ada background process yang mengganggu
- [✓ ] Cache dibersihkan antar-run
- [✓ ] Config file yang sama untuk semua run

---

## Latihan 3 — README Eksperimen

Tulis README minimum untuk eksperimen Anda (6 komponen wajib).

```
# Judul Eksperimen: Analisis Implementasi Machine Learning untuk Deteksi Intrusi pada Jaringan Komputer

## 1. Environment
> Eksperimen dilakukan menggunakan Google Colab dengan Python 3.11, CPU runtime, dan library Scikit-Learn.

## 2. Installation
> Install library menggunakan command:
pip install pandas numpy scikit-learn matplotlib seaborn

## 3. Data
> Dataset yang digunakan adalah NSL-KDD yang berisi data trafik jaringan normal dan data serangan.
File:
- KDDTrain+.txt
- KDDTest+.txt

## 4. Execution
> Menjalankan file eksperimen pada Google Colab:
python penelitian_final_proposal.py
atau menjalankan setiap cell secara berurutan pada notebook.

## 5. Configuration
> Parameter eksperimen:
- Train Test Split = 70:30
- Cross Validation = 10 Fold
- Random Seed = 42
- Hyperparameter Tuning = GridSearchCV
Model:
- Decision Tree
- Random Forest
- Support Vector Machine


## 6. Expected Output
> Output yang dihasilkan:
- Accuracy
- Precision
- Recall
- F1 Score
- AUC Score
- Confusion Matrix
- Classification Report
- ROC Curve
- CSV hasil evaluasi model
```

---

## Refleksi

> Apakah eksperimen Anda saat ini bisa direproduksi oleh orang lain tanpa bantuan Anda? Komponen apa yang masih hilang?

**Level saat ini:** [✓ ] Repeatability / [✓ ] Reproducibility / [ ] Belum keduanya
**Komponen yang belum terdokumentasi:**
> Eksperimen sudah dapat direproduksi oleh peneliti lain karena dataset, library, konfigurasi parameter, serta tahapan implementasi telah dijelaskan secara sistematis. Dokumentasi yang masih dapat ditingkatkan adalah pembuatan file requirements.txt agar versi dependency dapat dikunci secara lebih detail.
