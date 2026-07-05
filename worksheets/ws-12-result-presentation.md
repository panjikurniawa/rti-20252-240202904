# WS-12: Result Presentation & Visualization

> **Bab 12 — Penyajian Hasil & Visualisasi**

---

## Ringkasan Materi

### Data → Insight Model

```
Validated Data → Structured Presentation → Visualization → Pattern Recognition → Insight
```

Penyajian **mendahului** analisis. Tabel dan grafik membantu peneliti "melihat" data sebelum menghitung. Langsung ke uji statistik tanpa visualisasi berisiko kesimpulan yang secara teknis benar tapi kontekstual salah (Anscombe's Quartet, 1973).

### Tabel = Presisi, Grafik = Pola

Keduanya **saling melengkapi**:
- Tabel: angka presisi, self-contained (dipahami tanpa teks), sortable
- Grafik: pola visual, tren, perbandingan cepat

### Jenis Grafik Berdasarkan Tujuan

| Tujuan | Jenis Grafik |
|--------|-------------|
| Perbandingan antar-skenario | Bar chart (grouped/stacked) |
| Distribusi per-skenario | Box plot / violin plot |
| Tren temporal | Line chart |
| Korelasi dua variabel | Scatter plot |
| Proporsi (total = 100%) | Pie chart (hati-hati!) |

### Contoh Tabel Hasil yang Baik

| Model | Accuracy (%) | F1-Score (%) | Training Time (min) |
|-------|-------------|-------------|---------------------|
| BERT | 88.4 ± 1.2 | 87.1 ± 1.4 | 45.2 ± 3.1 |
| LSTM | 86.1 ± 1.8 | 84.5 ± 2.0 | 12.8 ± 1.2 |
| SVM | 82.3 ± 0.9 | 80.7 ± 1.1 | 0.3 ± 0.1 |

*N=10 per model. Mean ± std. Diurutkan berdasarkan Accuracy.*

### Visualization Bias — Yang Harus Dihindari

| Bias | Deskripsi | Dampak |
|------|----------|--------|
| Truncated axis | Y tidak dari 0 | Memperbesar perbedaan kecil |
| Inconsistent scale | Dua grafik skala beda | Perbandingan menyesatkan |
| Cherry-picked data | Hanya tampilkan yang "menang" | Selektif, tidak jujur |
| 3D effects | Efek 3D tanpa dimensi data ke-3 | Distorsi tanpa informasi |
| Missing error bar | Tidak ada variabilitas | Menyembunyikan ketidakpastian |

### Engineering vs Research Presentation

| Aspek | Engineering | Research |
|-------|-----------|---------|
| Tujuan grafik | Dashboard monitoring | Mendukung argumen ilmiah |
| Informasi wajib | KPI, threshold | Mean, std, CI, N, p-value |
| Bias handling | Less critical | Wajib dihindari (peer-review) |

---

## Template A.12 — Result Presentation Plan

```
RESULT PRESENTATION PLAN

Research Question :  Menentukan algoritma machine learning terbaik untuk
                    mendeteksi intrusi jaringan komputer berdasarkan
                    performa klasifikasi (Decision Tree vs Random Forest vs SVM).
Metrik Utama      : Accuracy, Precision, Recall, F1-Score, AUC, Waktu Eksekusi.

Tabel Hasil:
| Skenario      | Accuracy | F1-Score | Waktu Eksekusi | n |
| ------------- | -------- | -------- | -------------- | - |
| Decision Tree | 99.57% ± 0.05% | 99.55%   | 16.58 detik | 10 |
| Random Forest | 99.49% ± 0.07% | 99.52%   | 0.66 detik  | 10 |
| SVM           | 98.29% ± 0.30% | 98.96%   | 46.10 detik | 10 |


Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama                           | Metrik        |
| - | ------------ | ------------------------------------- | ------------- |
| 1 | Bar Chart    | Membandingkan accuracy  model         | Accuracy      |
| 2 | ROC Curve    | Melihat kemampuan klasifikasi model   | AUC           |
| 3 | Bar Chart    | Membandingkan kecepatan komputasi     | Training Time |


Bias Check:
  [✓] Y-axis mulai dari 0 (atau dijustifikasi secara eksplisit jika dipotong)
  [✓] Error bar/CI ditampilkan (std dari 10-fold CV tersedia di tabel)
  [✓] Semua data disertakan — tidak ada model yang disembunyikan
  [✓] Tidak menggunakan efek 3D tanpa alasan
  [✓] Skala konsisten di semua visualisasi
---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Model         | Accuracy | Precision | Recall | F1-Score | AUC      | Std (10-fold) | Waktu |
| ------------- | -------- | --------- | ------ | -------- | ----------- |------------|---------|
| Random Forest | 99.61%   | 99.55%    | 99.56% | 99.55%   | 0.9997 | ±0.05% | 16.58 dtk |
| Decision Tree | 99.58%   | 99.54%    | 99.48% | 99.52%   | 0.9961  | ±0.07% | 0.66 dtk |
| SVM           | 99.09%   | 99.29%    | 98.63% | 98.96%   | 0.9993 | ±0.30% | 46.10 dtk |


**Checklist tabel:**
- [✓] Self-contained (judul jelas, satuan ada, N tercantum)
- [✓] Mean ± Std dari 10-fold CV tersedia di kolom "Std"
- [✓] Diurutkan berdasarkan metrik utama (Accuracy, tertinggi ke terendah)
- [✓] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan                                 | Data yang Digunakan    |
| - | ------------ | ------------------------------------- | ---------------------- |
| 1 | Bar Chart    | Membandingkan accuracy tiga algoritma | Accuracy final dari test set (30%) |
| 2 | ROC Curve    | Membandingkan kemampuan membedakan normal vs attack | Nilai AUC ketiga model  |
| 3 | Bar Chart    | Membandingkan kecepatan komputasi — trade-off penting | Waktu training final (detik)  |


---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan                      | Jawaban                                                |
| ------------------------------- | ------------------------------------------------------ |
| Apakah Y-axis menyesatkan?      | Ya, menyesatkan. Y-axis dimulai dari 90% membuat perbedaan 0,4 poin (91,2% vs 90,8%) terlihat sangat besar secara visual — padahal secara absolut perbedaannya sangat kecil dan kemungkinan tidak signifikan secara statistik. Ini adalah contoh klasik truncated axis bias yang dibahas dalam materi WS-12. |
| Apakah error bar ditampilkan?   | Tidak ditampilkan. Ini masalah karena tanpa std/CI, pembaca tidak bisa menilai apakah perbedaan 0,4 poin itu nyata atau dalam rentang variabilitas normal. |
| Apakah semua model ditampilkan? | Ya, kedua metode ditampilkan — tidak ada yang disembunyikan. |
| Apa solusi jika bias terjadi?   | (1) Mulai Y-axis dari 0, atau (2) jika dipotong, tambahkan catatan eksplisit "axis truncated at 90%" beserta justifikasi ilmiah. Selalu tambahkan error bar (std atau CI 95%) agar pembaca bisa menilai signifikansi perbedaan. |


**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [✓] Y-axis dari 0 (bar chart accuracy dan waktu)
- [✓] Semua model ditampilkan (tidak cherry-picked)
- [✓] Tidak ada efek 3D

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Dalam penelitian, tabel dan grafik memiliki fungsi yang berbeda namun saling melengkapi. Tabel digunakan untuk melihat nilai numerik secara detail, sedangkan grafik membantu melihat pola dan perbandingan secara visual dengan lebih cepat. Jika hanya menggunakan tabel, pembaca akan sulit melihat pola umum hasil eksperimen. Sebaliknya, jika hanya menggunakan grafik maka detail angka menjadi kurang terlihat — dan seperti yang terjadi dalam penelitian ini, ketika semua model memiliki accuracy >99%, grafik bar saja tidak cukup untuk membedakan performa antar model tanpa tabel pendukung. Pada penelitian ini, visualisasi sangat membantu menunjukkan bahwa algoritma Random Forest memiliki performa terbaik dibanding Decision Tree dan SVM, baik dari sisi accuracy maupun nilai AUC (ROC Curve). Dengan penyajian data yang lengkap — tabel presisi + grafik pola + uji statistik (Friedman test, p=0.00013) — hasil penelitian menjadi lebih mudah dipahami dan lebih kuat secara ilmiah.
