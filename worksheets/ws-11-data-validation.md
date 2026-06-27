# WS-11: Data Validation & Integrity

> **Bab 11 — Validasi Data & Integritas**

---

## Ringkasan Materi

### Data Trust Model

```
Raw Data → Data Cleaning → Consistency Check → Validation Process → Trusted Data
```

Data mentah belum bisa dipercaya. Harus melewati pipeline validasi sebelum siap untuk analisis statistik.

### Empat Pilar Data Quality

| Pilar | Deskripsi | Contoh Pelanggaran |
|-------|----------|-------------------|
| **Accuracy** | Nilai dalam range masuk akal | Akurasi = 1.5 (di luar [0,1]) |
| **Consistency** | Format seragam di semua run | Run 1: CSV, Run 2: JSON |
| **Completeness** | Tidak ada data hilang dari plan | 97 dari 100 run tercatat |
| **Validity** | Data sesuai desain eksperimen | Parameter baseline tercampur treatment |

### Proses Validasi Progresif

1. **Format validation** — Tipe file, header, kolom
2. **Range validation** — Nilai dalam batas logis
3. **Consistency validation** — Format seragam antar-run
4. **Logic validation** — Data cocok dengan desain eksperimen

Jika gagal di langkah awal → tidak perlu lanjut.

### Anomaly Detection — 3 Jenis

| Jenis | Deskripsi | Deteksi |
|-------|----------|---------|
| **Statistical outlier** | Nilai di luar distribusi normal | IQR: < Q1-1.5×IQR atau > Q3+1.5×IQR |
| **Contextual anomaly** | Normal absolut, abnormal dalam konteks | Run 1-10: ~91%, Run 11-20: ~88% |
| **Pattern anomaly** | Pola sistematis (bukan random) | Performa menurun berurutan |

**Prinsip:** Detect → Investigate → Document → Decide — **JANGAN langsung hapus.**

### Engineering vs Research Validation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan | Data sesuai spesifikasi bisnis | Data layak untuk analisis statistik |
| Missing data | Impute / set default | Investigasi penyebab → dokumentasi |
| Outlier | Bug → fix | Mungkin temuan → investigasi |
| Dokumentasi | Minimal (log error) | Komprehensif (anomali + keputusan) |

### Jebakan Kognitif

1. "Logging otomatis ≠ data benar" → bisa ada bug di logger
2. "Outlier = hapus" → bisa jadi temuan penting
3. "Dataset kecil tidak perlu validasi" → justru lebih rentan
4. "Mean normal = data benar" → [94, 95, 93, **44**, 94] → mean 84% terlihat wajar

---

## Template A.11 — Data Validation Checklist

```
DATA VALIDATION CHECKLIST

Completeness:
  [✓ ] Semua skenario tercakup
  [✓ ] Jumlah run sesuai rencana
  [✓ ] Tidak ada file output hilang
  Missing: 0 dari 9 data points

Format Consistency:
  [✓ ] Semua file format sama (CSV/JSON/...)
  [✓ ] Header konsisten
  [✓ ] Tipe data konsisten (numerik tetap numerik)
      Format file yang digunakan: CSV, PNG, TXT Log Output

Range & Logic:
  [✓ ] Nilai dalam range masuk akal
  [✓ ] Tidak ada waktu negatif
  [✓ ] Metrik 0–100%, tidak di luar range
  Anomali ditemukan: Proses komputasi algoritma SVM membutuhkan waktu lebih lama dibanding model lain.

Cross-Validation:
  [✓ ] Run identik → hasil mendekati
  [✓ ] Trend konsisten dengan ekspektasi teori
      Urutan performa model: Random Forest, Decision Tree, SVM
      Hal ini sesuai jurnal acuan, di mana Random Forest memberikan performa terbaik dibanding algoritma lain.

Keputusan:
  [✓ ] Data siap analisis
  [ ] Perlu cleaning
  [ ] Perlu re-run (skenario: ____)
     
---

## Latihan 1 — Completeness Check

Verifikasi apakah semua data yang direncanakan sudah terkumpul.

| Skenario | Run Direncanakan | Run Tercatat | Missing | Alasan |
|----------|-----------------|-------------|---------|--------|
| Decision Tree | 3 | 3 | 0 | Tidak ada masalah |
| Random Forest | 3 | 3 |  | Tidak ada masalah |
|SVM |3 |3 |0 |Tidak masalah |


**Total expected:** 9 | **Total actual:** 9 | **Missing:** 0

**Keputusan untuk data missing:**
> Seluruh proses eksperimen berhasil dijalankan sehingga tidak ditemukan data yang hilang dan tidak diperlukan pengujian ulang.

---

## Latihan 2 — Anomaly Investigation

Periksa data Anda untuk anomali. Gunakan metode IQR atau z-score.

**Dataset sampel (atau data Anda sendiri):**

| Run | Accuracy (%) |
|-----|-------------|
| Decision Tree| 99.57% |
| Random Forest | 99.61% |
| SVM | 99.09% |


**Deteksi outlier:**
- Q1 = 99.09 | Q3 = 99.61 | IQR = 0.52
- Batas bawah (Q1 - 1.5×IQR) = 98.31
- Batas atas (Q3 + 1.5×IQR) = 100.39
- Outlier terdeteksi: Tidak ada

**Investigasi (untuk setiap outlier):**

| Outlier | Nilai | Kemungkinan Penyebab | Keputusan |
|---------|-------|---------------------|-----------|
| Tidak ada | — | Seluruh model stabil | Data diterima |

---

## Latihan 3 — Validation Report

Buat laporan validasi ringkas untuk dataset eksperimen Anda.

**1. Completeness:** 100% data terkumpul
**2. Format:** [✓ ] Konsisten / [ ] Ada inkonsistensi: ____
**3. Range check (anomali):** Tidak ditemukan nilai di luar range evaluasi.
**4. Logic check:** [✓ ] Parameter sesuai plan / [ ] Ada ketidaksesuaian: ____

**Kesimpulan:** [✓ ] Data siap analisis / [ ] Perlu tindakan: ____

---

## Refleksi

> Apa perbedaan antara "data yang benar" dan "data yang dipercaya"? Mengapa proses validasi formal diperlukan meskipun data dikumpulkan secara otomatis?

> Data yang benar belum tentu menjadi data yang dapat dipercaya. Data dianggap dapat dipercaya apabila sudah melalui proses validasi, pengecekan konsistensi, serta dipastikan sesuai dengan prosedur penelitian yang telah ditetapkan.
> Walaupun proses eksperimen dilakukan secara otomatis menggunakan program Python, validasi formal tetap diperlukan untuk memastikan tidak terjadi kesalahan pada proses preprocessing, training model, maupun evaluasi hasil.
Dengan melakukan validasi data, hasil penelitian menjadi lebih valid, lebih akurat, dan dapat dipertanggungjawabkan secara ilmiah.
