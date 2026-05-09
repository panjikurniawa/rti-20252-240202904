# WS-04: Research Question & Hypothesis

> **Bab 4 — Research Question, Contribution & Hypothesis**

---

## Ringkasan Materi

### RQ Bukan Pertanyaan Biasa

Research Question yang baik secara implisit mengandung cetak biru eksperimen: subjek, baseline, metrik, domain, dataset.

| Kualitas | Contoh |
|----------|--------|
| **Buruk** | "Bagaimana pengaruh deep learning terhadap deteksi malware?" |
| **Baik** | "Apakah CNN menghasilkan F1-Score lebih tinggi dari RF pada CIC-MalMem-2022?" |

Perbedaan: RQ yang baik menyebutkan **metode spesifik**, **metrik terukur**, **baseline**, dan **dataset**.

### Tiga Jenis RQ

| Jenis | Pola | Kebutuhan |
|-------|------|-----------|
| **Comparison** | A vs B → mana lebih baik? | ≥ 2 metode, metrik sama |
| **Improvement** | A' vs A → modifikasi lebih baik? | Pre/post, bukti perbaikan |
| **Exploratory** | Faktor X₁...Xₙ → pengaruh terhadap Y? | Multi-variabel, korelasi/regresi |

### Contribution Statement

Tiga jenis kontribusi: **Improvement** (metode terbukti lebih baik), **Comparison** (perbandingan sistematis yang belum ada), **Novel Approach** (pendekatan baru). Kontribusi harus terhubung langsung dengan gap — kontribusi tanpa gap = klaim tanpa justifikasi.

### Hypothesis H₀ / H₁

- **H₀** (Null) = Tidak ada perbedaan signifikan — asumsi default, harus dibuktikan salah
- **H₁** (Alternative) = Ada perbedaan signifikan — diterima hanya jika H₀ ditolak
- Harus **falsifiable**, mengandung **metrik terukur**, dirumuskan **SEBELUM eksperimen**

### Rantai Operasionalisasi

```
RQ → Variable → Metric → Data → Analysis
```

Jika rantai ini tidak lengkap, RQ belum mature. Bi-directional: RQ yang tidak bisa jadi hipotesis testable harus direvisi mundur.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan pertanyaan | Apa yang harus dibangun? | Apa yang harus dibuktikan? |
| Bentuk jawaban | Sistem yang berfungsi | Bukti empiris terukur |
| Sukses diukur oleh | User satisfaction, uptime | Signifikansi statistik, effect size |
| Jika gagal | Debug dan perbaiki | Laporkan, analisis mengapa |

### Istilah Penting

- **Research Question (RQ)** — Pertanyaan spesifik: variabel terukur + metrik + konteks
- **Contribution Statement** — Apa yang diketahui setelah riset selesai yang sebelumnya belum ada
- **H₀ / H₁** — Null vs Alternative Hypothesis
- **Falsifiability** — Kondisi hipotesis ditolak harus bisa didefinisikan sebelum eksperimen
- **Operationalization** — Proses mewujudkan konsep abstrak menjadi variabel terukur

---

## Template A.4 — RQ-Contribution-Hypothesis

```
RQ-CONTRIBUTION-HYPOTHESIS

Gap Statement  : Banyak penelitian deteksi intrusi masih menggunakan dataset lama seperti NSL-KDD sehingga hasil model belum tentu sesuai dengan kondisi jaringan modern.

Research Question:
  Tipe         : [✓] Comparison  [ ] Improvement  [ ] Exploratory
  Formulasi    : Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD?
  Variabel IV  : Jenis algoritma machine learning (Random Forest, Decision Tree, SVM)
  Variabel DV  :  Performa deteksi intrusi
  Metrik       : Akurasi, presisi, recall, dan F1-Score
  Dataset      : NSL-KDD
  Baseline     : Decision Tree dan SVM

Quality Check RQ:
  [✓ ] Variabel spesifik
  [✓] Metrik jelas
  [✓ ] Baseline ada
  [✓ ] Konteks disebutkan
  [✓ ] Memerlukan eksperimen (bukan hanya survei literatur)

Contribution Statement:
  Apa yang baru diketahui : Penelitian menunjukkan bahwa Random Forest memberikan hasil yang lebih baik dibandingkan Decision Tree dan SVM dalam mendeteksi intrusi jaringan pada dataset NSL-KDD.
  Jenis kontribusi        : [ ] Improvement  [✓ ] Comparison  [ ] Novel approach
  Gap yang diisi          : Evaluasi performa beberapa algoritma machine learning pada deteksi intrusi jaringan.

Hypothesis Pair:
  H₀ : Tidak ada perbedaan signifikan performa antara Random Forest, Decision Tree, dan SVM dalam mendeteksi intrusi pada dataset NSL-KDD.
  H₁ : Random Forest memiliki performa yang lebih baik dibandingkan Decision Tree dan SVM dalam mendeteksi intrusi pada dataset NSL-KDD.
  Threshold              : Akurasi dan F1-Score lebih tinggi dari baseline
  Justifikasi threshold  : Akurasi dan F1-Score dipilih karena dapat menunjukkan kemampuan model dalam mendeteksi serangan secara tepat dan seimbang.
```

---

## Latihan 1 — Dari Gap ke RQ

Gunakan gap yang ditemukan di WS-03. Transformasikan menjadi Research Question.

**Gap dari WS-03:** Banyak penelitian masih menggunakan dataset lama seperti NSL-KDD sehingga performa model belum tentu sesuai dengan kondisi jaringan modern.

**RQ versi pertama (tulis bebas):**
> Apakah Random Forest lebih baik dibandingkan Decision Tree dan SVM untuk mendeteksi intrusi jaringan?

**Evaluasi RQ:**

| Komponen | Ada? | Isi |
|----------|------|-----|
| Metode spesifik | Ya |Random Forest, Decision Tree, SVM |
| Metrik terukur | Ya |Akurasi, presisi, recall, F1-Score |
| Baseline | Ya |Decision Tree dan SVM |
| Dataset/konteks | Ya |Dataset NSL-KDD |

**Tipe RQ:** [✓ ] Comparison / [ ] Improvement / [ ] Exploratory

**RQ versi revisi (setelah evaluasi):**
> Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD berdasarkan nilai akurasi, presisi, recall, dan F1-Score?

---

## Latihan 2 — Hypothesis Pair

Rumuskan pasangan hipotesis dari RQ di Latihan 1.

| Komponen | Isi |
|----------|-----|
| H₀ |Tidak ada perbedaan signifikan performa antara Random Forest, Decision Tree, dan SVM pada dataset NSL-KDD |
| H₁ |Random Forest memiliki performa lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD |
| Metrik |Akurasi, presisi, recall, dan F1-Score |
| Threshold |Nilai evaluasi Random Forest lebih tinggi dibanding baseline |
| Justifikasi threshold |Metrik tersebut digunakan untuk melihat seberapa baik model mendeteksi intrusi jaringan. |

**Apakah hipotesis ini falsifiable?** [✓ ] Ya / [ ] Tidak
> Bagaimana cara membuktikannya salah? Jika hasil pengujian menunjukkan bahwa Random Forest tidak lebih baik atau memiliki performa yang sama dengan Decision Tree dan SVM, maka hipotesis alternatif ditolak.

---

## Latihan 3 — Rantai Operasionalisasi

Lengkapi rantai dari RQ hingga metode analisis.

| Tahap | Isi |
|-------|-----|
| RQ | Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD? |
| Variable (IV) |Jenis algoritma machine learning |
| Variable (DV) |Performa deteksi intrusi |
| Metric |Akurasi, presisi, recall, dan F1-Score |
| Data source |Dataset NSL-KDD |
| Analysis method |Perbandingan hasil evaluasi model menggunakan cross-validation |

**Apakah rantai lengkap?** [✓ ] Ya / [ ] Tidak
> Jika tidak, tahap mana yang perlu direvisi? Tidak ada, karena semua bagian sudah saling berhubungan.

---

## Refleksi

> Ambil satu judul skripsi/paper yang pernah dibaca. Coba ekstrak RQ-nya. Apakah RQ tersebut memenuhi semua komponen (metode, metrik, baseline, konteks)? Jika tidak, apa yang hilang?

**Judul:** Implementasi Machine Learning untuk Deteksi Intrusi pada Jaringan Komputer
**RQ yang diekstrak:** Apakah Random Forest memberikan performa yang lebih baik dibandingkan Decision Tree dan SVM dalam mendeteksi intrusi jaringan?
**Komponen yang hilang:** Paper sudah memiliki metode, dataset, dan metrik evaluasi yang cukup jelas. Namun, penjelasan mengenai alasan pemilihan dataset dan pengujian pada kondisi jaringan modern masih belum banyak dibahas.
