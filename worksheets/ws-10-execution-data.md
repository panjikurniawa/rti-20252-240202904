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
| 1     |Pelatihan Decision Tree | 42 |criterion, max_depth |Selesai |27.7 detik |hasil_perbandingan_model.csv |
| 2     |Pelatihan Random Forest |42  |n_estimators, max_depth |Selesai |64.21 detik |hasil_perbandingan_model.csv |
| 3     |Pelatihan SVM | 42     | kernel=rbf, C, gamma |Selesai |19.45 detik |hasil_perbandingan_model.csv  |
| 4     |Grid Search Decision Tree | 42     |criterion=entropy, max_depth=20 | Selesai  |33.15 detik | hasil_perbandingan_model.csv |
| 5     |Grid Search Random Forest | 42 | n_estimators=200, max_depth=None | Selesai | 257.74 detik |  hasil_perbandingan_model.csv |
| 6     |Grid Search SVM | 42 | C=10, gamma=scale | Selesai | 204.0 detik | hasil_perbandingan_model.csv |
| 7     |Evaluasi Final Decision Tree | 42 | Parameter terbaik DT | Selesai | 0.58 detik | perbandingan_model.png |
| 8     |Evaluasi Final Random Forest | 42 | Parameter terbaik RF | Selesai | 17.64 detik | perbandingan_model.png |
| 9     |Evaluasi Final SVM | 42 | Parameter terbaik SVM | Selesai | 52.25 detik | roc_curve.png |

Jumlah runs per skenario : 3 model algoritma
Total runs               : 9 proses pengujian

DATA LOG (per run):
  Run ID    : run-001
  Timestamp : 27 Juni 2026
  Skenario  : Pengujian perbandingan performa Decision Tree, Random Forest, dan SVM pada sistem deteksi intrusi jaringan
  Input     : Dataset NSL-KDD dengan jumlah data awal 148517 record dan data akhir setelah preprocessing sebanyak 110082 record
  Output    : Accuracy, Precision, Recall, F1-Score, AUC Score, Confusion Matrix, Classification Report, Grafik Accuracy, ROC Curve
  Anomali   : Proses komputasi algoritma SVM membutuhkan waktu lebih lama dibanding model lain karena kompleksitas proses training lebih tinggi
  Catatan   : Random Forest memberikan performa terbaik dibandingkan dua algoritma lainnya berdasarkan seluruh metrik evaluasi
```

---

## Latihan 1 — Execution Plan

Susun execution plan untuk eksperimen Anda. Tentukan skenario, jumlah run, dan seed sebelum eksekusi.

| Run # | Skenario | Seed | Parameter Kunci | Status |
|-------|----------|------|----------------|--------|
| 1 | Cross Validation Decision Tree | 42 |  cv=10 | Selesai |
| 2 | Cross Validation Random Forest | 42 |  cv=10 | Selesai |
| 3 |Cross Validation SVM |42 | subset=15000 |Selesai |
| 4 |Grid Search Decision Tree |42 |criterion, max_depth |Selesai |
| 5 |Grid Search Random Forest |42 |n_estimators, max_depth |Selesai |
| 6 |Grid Search SVM | 42| C, gamma | Selesai |
| 7 |Final Training Decision Tree | 42 | best parameter DT | Selesai |
| 8 |Final Training Random Forest | 42 | best parameter RF | Selesai |
| 9 |Final Training SVM | 42 | best parameter SVM | Selesai |

**Total skenario:** 9
**Run per skenario:** 1 kali
**Total run keseluruhan:** 9 proses eksperimen

---

## Latihan 2 — Data Log Terstruktur

Desain format data log untuk eksperimen Anda. Tentukan field apa saja yang akan dicatat.

**Identitas:**
| Field | Contoh |
|-------|--------|
| Run ID | run-001 |
| Timestamp | 27 Juni 2026 |
|Dataset |NSL-KDD |
|Platform | Google colab |

**Konfigurasi:**
| Field | Contoh |
|-------|--------|
| Seed | 42 |
| Data Split | 70:30 |
|Cross Validation |10 Fold |
|Code Version | Python Notebook Final |

**Hasil:**
| Metrik | Tipe Data | Range Valid |
|--------|----------|-------------|
| Accuracy | float | 0.0 – 1.0 |
|Precision |float |0.0-1.0 |
|Recall |float |0.0-1.0 |
|F1-Score|float |0.0-1.0|
|AUC |float |0.0-1.0|
**Format output:** [✓ ] CSV / [ ] JSON / [ ] Database / [ ] Lainnya: [✓ ] PNG / [✓ ] TXT Log File

---

## Latihan 3 — Anomaly Protocol

Rencanakan bagaimana menangani anomali. Untuk setiap jenis, tentukan langkah yang diambil.

| Jenis Anomali | Contoh | Tindakan |
|---------------|--------|----------|
| Program berhenti | Runtime Google Colab disconnect | Menjalankan ulang program |
| Waktu proses terlalu lama |Training SVM membutuhkan waktu lebih lama |Menunggu proses selesai dan memantau runtime |
| Hasil tidak sesuai |Accuracy berubah terlalu jauh |Mengecek preprocessing dan parameter |
| Error membaca data |Dataset gagal dimuat |Upload ulang dataset |

**Prinsip:** Detect → Investigate → Document → Decide

---

## Refleksi

> Pernahkah Anda melaporkan hasil riset/tugas dari single run? Apa risikonya? Bagaimana multiple run mengubah kepercayaan terhadap hasil?

**Pengalaman sebelumnya:**
> Pada praktik sebelumnya proses pengujian hanya berfokus pada satu hasil accuracy tanpa dokumentasi eksperimen yang lengkap.
**Yang akan dilakukan berbeda:**
> Pada penelitian ini seluruh proses eksperimen dicatat secara lengkap, hasil disimpan dalam beberapa file, serta dilakukan perbandingan tiga algoritma machine learning agar hasil penelitian menjadi lebih valid.
