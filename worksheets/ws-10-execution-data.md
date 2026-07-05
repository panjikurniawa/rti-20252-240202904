# WS-10: Experiment Execution & Data Collection

> **Bab 10 — Eksekusi Eksperimen & Pengumpulan Data**

---

## Ringkasan Materi

### Experiment Execution Pipeline

```
Design → Execution Plan → Controlled Execution → Data Collection → Data Logging → Dataset for Analysis
```

### Multiple Run = Non-Negotiable

Single run **tidak pernah cukup** untuk klaim ilmiah. Minimum 5-10 run per skenario dengan seed berbeda. Multiple run menghasilkan:
- Mean, std, confidence interval
- Distribusi hasil → uji statistik
- Variabilitas → error bar di grafik

### Execution Plan

Setiap eksperimen harus memiliki plan sebelum eksekusi:
- Daftar skenario
- Jumlah run per skenario
- Random seed per run (pre-determined!)
- Urutan eksekusi (randomisasi/counterbalancing)
- Pre-execution checklist

### Data Logging Komprehensif

Setiap run menghasilkan log terstruktur:
1. **Identitas** — Run ID, timestamp, skenario
2. **Konfigurasi** — Semua parameter, seed, code version
3. **Hasil** — Semua metrik, output detail
4. **Metadata** — Waktu eksekusi, resource usage, warning/error

Format: CSV/JSON/database — **bukan stdout yang di-copy-paste**.

### Engineering vs Research Execution

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Run | Sekali (deploy) | Multiple (min 5-10, seed berbeda) |
| Logging | Error log, access log | Semua parameter, metrik, metadata |
| Anomali | Bug → fix → redeploy | Investigasi → dokumentasi → analisis |
| Urutan | Tidak penting | Bisa bias — perlu randomisasi |

### Anomali = Dokumentasi, Bukan Hapus

Run gagal/anomali tidak boleh dihapus tanpa dokumentasi. Bisa jadi:
- **Bug** → fix & re-run (dokumentasikan!)
- **Batas kemampuan metode** → DNF = temuan
- **Data yang bias** jika hanya simpan run "berhasil"

### Jebakan Kognitif

1. "Satu angka cukup" → tanpa distribusi, tidak bisa diuji
2. "Seed tidak penting" → bahkan algoritma deterministik bisa dipengaruhi library stokastik
3. "Run gagal langsung hapus" → kehilangan temuan potensial
4. "Semua run harus hari ini" → thermal throttling, fatigue

---

## Template A.10 — Execution Plan & Data Log

```
EXECUTION PLAN

| Run # | Skenario | Seed | Parameter | Status | Waktu | Output File |
|-------|----------|------|-----------|--------|-------|-------------|
| 1     |Cross-Val Decision Tree | 42 |cv=10, data penuh (77.057 record) |Selesai |27.22 detik |hasil_cv_10fold.csv |
| 2     |Cross-Val Random Forest |42  |cv=10, n_estimators=100, data penuh  |Selesai |58.83 detik |hasil_cv_10fold.csv |
| 3     |Cross-Val SVM  | 42     | cv=10, subset=15.000 record |Selesai |16.20 detik |hasil_cv_10fold.csv  |
| 4     |Grid Search Decision Tree | 42     |criterion=[gini,entropy], max_depth | Selesai  |31.38 detik | - |
| 5     |Grid Search Random Forest | 42 | n_estimators=[100,200], max_depth | Selesai | 233.12 detik | - |
| 6     |Grid Search SVM  | 42 | C=[1,10], gamma=[scale,0.01], sub=15.000 | Selesai | 179.97 detik | - |
| 7     |Final Training DT | 42 | criterion=entropy, max_depth=20  | Selesai | 0.66 detik | hasil_perbandingan_model.csv |
| 8     |Final Training RF | 42 | n_estimators=200, max_depth=None | Selesai | 16.58 detik |hasil_perbandingan_model.csv |
| 9     |Final Training SVM  | 42 | C=10, gamma=scale, subset=30.000 record | Selesai | 46.10 detik | hasil_perbandingan_model.csv |

Jumlah skenario    : 9 proses (3 CV + 3 Grid Search + 3 Final Training)
Fold per model     : 10 fold (CV) → total 30 fold untuk 3 model
Total run overall  : 30 fold CV + 6 proses GS + 3 final training

DATA LOG (per run):
  Run ID    : run-001
  Timestamp : 27 Juni 2026
  Skenario  : Perbandingan performa Decision Tree, Random Forest, SVM
              pada sistem deteksi intrusi jaringan (NSL-KDD)
  Input     : Dataset NSL-KDD — data awal 148.517 record,
              data akhir setelah preprocessing 110.082 record,
              split 70:30 → training 77.057 / testing 33.025 record
  Output    : Accuracy, Precision, Recall, F1-Score, AUC,
              Confusion Matrix, Classification Report,
              Bar Chart, ROC Curve, CSV hasil, TXT log
  Anomali   : SVM membutuhkan waktu komputasi jauh lebih lama
              (46 detik final training, 180 detik grid search)
              dibanding DT (0.66 dtk) dan RF (16.58 dtk).
              Penyebab: kompleksitas kernel RBF O(n²-n³) pada
              dataset besar. Ditangani dengan subset data.
  Catatan   : Random Forest memberikan performa terbaik (Accuracy
              99.61%, AUC 0.9997) pada semua metrik evaluasi.
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | Cross-Validation Decision Tree | 42 |  cv=10, data penuh (77.057 record) | Selesai |
| 2 | Cross-Validation Random Forest | 42 |  cv=10, n_estimators=100, data penuh | Selesai |
| 3 |Cross-Validation SVM |42 | cv=10, subset=15.000 record |Selesai |
| 4 |Grid Search Decision Tree |42 |criterion=[gini,entropy], max_depth=[10,20,30,None] |Selesai |
| 5 |Grid Search Random Forest |42 |n_estimators=[100,200], max_depth=[10,20,None] |Selesai |
| 6 |Grid Search SVM | 42| C=[1,10], gamma=[scale,0.01], subset=15.000 | Selesai |
| 7 |Final Training Decision Tree | 42 | criterion=entropy, max_depth=20 | Selesai |
| 8 |Final Training Random Forest | 42 | n_estimators=200, max_depth=None | Selesai |
| 9 |Final Training SVM | 42 | C=10, gamma=scale, subset=30.000 record | Selesai |

**Total skenario:**  9 proses eksperimen
Fold per model (CV): 10 fold × 3 model = 30 fold total
Prinsip multiple run terpenuhi melalui 10-fold cross-validation
(setiap model dievaluasi 10 kali pada subset data berbeda,
menghasilkan distribusi performa yang bisa diuji secara statistik)

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | run-001 |
| Timestamp | 27 Juni 2026 |
|Dataset |NSL-KDD (KDDTrain+ + KDDTest+, digabung lalu split 70:30) |
|Platform | Google Colab (Python 3, CPU runtime) |

**Konfigurasi:**
| Field | Nilai |
|-------|--------|
| Random Seed | 42 (dikunci di semua proses: train_test_split, semua model, np.random) |
| Data Split | 70% training (77.057) : 30% testing (33.025) |
|Cross Validation |10-fold (stratified, data training saja) |
|Normalisasi | MinMaxScaler — fit pada training, transform pada testing |
|SVM CV subset size | 15.000 record (dari 77.057 training) |
|SVM Final training subset | 30.000 record (dari 77.057 training) |
|Code Version | penelitian_deteksi_intrusi_FIX_SVM.py (versi final) |

**Hasil:**
| Metrik | Tipe Data | Range Valid | Nilai Aktual (RF) |
|--------|----------|-------------|--------------------|
| Accuracy | float | 0.0 – 1.0 |0.9961|
|Precision |float |0.0-1.0 |0.9955 |
|Recall |float |0.0-1.0 |0.9956 |
|F1-Score|float |0.0-1.0|0.9955 |
|AUC |float |0.0-1.0|0.9997 |
|Waktu training | float (detik) | >0 |16.58 dtk|
**Format output:** [✓ ] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: [✓ ] PNG / [✓ ] TXT Log File

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Waktu proses ekstrem | Training SVM 46 detik (final) dan 180 detik (grid search) — jauh lebih lama dari DT (0.66 dtk) dan RF (16.58 dtk) | Dokumentasikan sebagai karakteristik komputasi SVM kernel RBF, bukan error. Gunakan subset data (15.000 untuk CV/GS, 30.000 untuk final training) sebagai solusi |
| Program berhenti / disconnect |Google Colab disconnect saat menjalankan SVM penuh (pernah terjadi — macet 2 jam 43 menit) |Interrupt execution → restart runtime → jalankan ulang script yang sudah dioptimalkan dengan subset SVM |
| Hasil tidak sesuai ekspektasi |Accuracy sangat tinggi (>99%) — lebih tinggi dari jurnal rujukan (96.8%) |Investigasi penyebab: ditemukan bahwa penggabungan KDDTrain+ dan KDDTest+ lalu split acak 70:30 menghilangkan tantangan "unseen attack" pada test set asli → didokumentasikan sebagai limitation penelitian |
| Error membaca dataset |FileNotFoundError: KDDTrain+.txt not found |Upload ulang dataset ke Colab atau gunakan cell wget untuk download otomatis dari GitHub |
|Run ke-n hasilnya sangat berbeda | Belum terjadi — std semua model kecil (DT ±0.07%, RF ±0.05%) | Jika terjadi: cek seed consistency, periksa apakah ada data leakage, dokumentasikan fold yang anomali |

**Prinsip:** Detect → Investigate → Document → Decide
(anomali SVM tidak dihapus, melainkan diinvestigasi dan didokumentasikan
sebagai keterbatasan komputasi yang valid)

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Pada praktik sebelumnya, proses pengujian hanya berfokus pada satu hasil accuracy tanpa dokumentasi eksperimen yang lengkap. Risikonya: hasil dari single run bisa saja kebetulan sangat baik atau sangat buruk karena variabilitas random — tanpa multiple run, klaim "model A lebih baik dari model B" tidak bisa dibuktikan secara statistik.
**Yang akan dilakukan berbeda:**
> Dalam penelitian ini, prinsip multiple run diterapkan melalui 10-fold cross-validation (setiap model dievaluasi 10 kali pada subset berbeda), menghasilkan distribusi performa yang kemudian diuji menggunakan Friedman test (p=0.00013) dan repeated-measures ANOVA (F=156.49, p<0.0001). Hasilnya: klaim "Random Forest lebih baik" bukan sekadar satu angka, melainkan kesimpulan yang terbukti signifikan secara statistik dengan effect size besar (Kendall's W = 0.895). Perbedaan utama dari approach sebelumnya: semua proses kini terdokumentasi lengkap dalam log file (hasil_lengkap.txt), semua parameter tercatat (termasuk subset size SVM yang sering tidak disebutkan), dan anomali (waktu SVM yang ekstrem, hasil accuracy >99%) tidak dihapus melainkan diinvestigasi dan didokumentasikan sebagai temuan atau keterbatasan.
