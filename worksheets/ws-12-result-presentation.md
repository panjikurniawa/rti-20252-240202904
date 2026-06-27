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

Research Question : Menentukan algoritma machine learning terbaik untuk mendeteksi intrusi jaringan komputer berdasarkan performa klasifikasi.
Metrik Utama      : Accuracy, Precision, Recall, F1-Score, AUC, dan Waktu Eksekusi.

Tabel Hasil:
| Skenario      | Accuracy | F1-Score | Waktu Eksekusi | n |
| ------------- | -------- | -------- | -------------- | - |
| Decision Tree | 99.58%   | 99.52%   | 0.58 detik     | 1 |
| Random Forest | 99.61%   | 99.55%   | 17.64 detik    | 1 |
| SVM           | 99.09%   | 98.96%   | 52.25 detik    | 1 |


Visualisasi yang Direncanakan:
| # | Jenis Grafik | Pesan Utama                           | Metrik        |
| - | ------------ | ------------------------------------- | ------------- |
| 1 | Bar Chart    | Membandingkan accuracy antar model    | Accuracy      |
| 2 | ROC Curve    | Melihat performa klasifikasi model    | AUC           |
| 3 | Bar Chart    | Membandingkan waktu proses tiap model | Training Time |


Bias Check:
  [ ] Y-axis mulai dari 0 (atau dijustifikasi)
  [ ] Error bar/CI ditampilkan
  [ ] Semua data disertakan (tidak cherry-picked)
  [ ] Tidak menggunakan 3D tanpa alasan
``[✓] Sumbu Y dimulai dari angka logis
  [✓] Seluruh data ditampilkan
  [✓] Tidak menggunakan efek visual berlebihan
  [✓] Tidak ada data yang disembunyikan
---

## Latihan 1 — Tabel Hasil

Buat tabel hasil eksperimen Anda (boleh dengan data simulasi jika belum punya data riil).

| Model         | Accuracy | Precision | Recall | F1-Score | Waktu       |
| ------------- | -------- | --------- | ------ | -------- | ----------- |
| Random Forest | 99.61%   | 99.55%    | 99.56% | 99.55%   | 17.64 detik |
| Decision Tree | 99.58%   | 99.54%    | 99.48% | 99.52%   | 0.58 detik  |
| SVM           | 99.09%   | 99.29%    | 98.63% | 98.96%   | 52.25 detik |


**Checklist tabel:**
- [✓ ] Self-contained (judul jelas, satuan ada, N tercantum)
- [✓ ] Mean ± std (bukan single number)
- [✓ ] Diurutkan berdasarkan metrik utama
- [✓ ] Format konsisten di semua baris

---

## Latihan 2 — Rencana Visualisasi

Rencanakan 2-3 grafik untuk menyajikan data dari Latihan 1. Setiap grafik = satu pesan.

| # | Jenis Grafik | Pesan                                 | Data yang Digunakan    |
| - | ------------ | ------------------------------------- | ---------------------- |
| 1 | Bar Chart    | Membandingkan accuracy tiga algoritma | Accuracy seluruh model |
| 2 | ROC Curve    | Membandingkan kemampuan klasifikasi   | Nilai AUC model        |
| 3 | Bar Chart    | Membandingkan kecepatan komputasi     | Waktu proses model     |


---

## Latihan 3 — Bias Detection

Evaluasi visualisasi berikut untuk bias (skenario dari contoh):

**Skenario:** Metode A = 91.2%, Metode B = 90.8%. Bar chart dengan Y-axis mulai dari 90%.

| Pertanyaan                      | Jawaban                                                |
| ------------------------------- | ------------------------------------------------------ |
| Apakah Y-axis menyesatkan?      | Tidak, grafik menampilkan rentang nilai yang wajar     |
| Apakah error bar ditampilkan?   | Tidak, karena hanya menggunakan satu hasil final       |
| Apakah semua model ditampilkan? | Ya, seluruh model dimasukkan                           |
| Apa solusi jika bias terjadi?   | Menggunakan skala konsisten dan menampilkan semua data |


**Evaluasi grafik Anda sendiri dari Latihan 2:**
- [✓ ] Semua bias check lulus
- [ ] Ada yang perlu diperbaiki: ____

---

## Refleksi

> Mengapa tabel dan grafik keduanya diperlukan — tidak cukup salah satu saja? Pernahkah Anda membuat grafik yang (tanpa sengaja) menyesatkan?

> Dalam penelitian, tabel dan grafik memiliki fungsi yang berbeda namun saling melengkapi. Tabel digunakan untuk melihat nilai numerik secara detail, sedangkan grafik membantu melihat pola dan perbandingan secara visual dengan lebih cepat.
Jika hanya menggunakan tabel, pembaca akan sulit melihat pola umum hasil eksperimen. Sebaliknya, jika hanya menggunakan grafik maka detail angka menjadi kurang terlihat.
> Pada penelitian ini, visualisasi sangat membantu menunjukkan bahwa algoritma Random Forest memiliki performa terbaik dibanding Decision Tree dan SVM, baik dari sisi accuracy maupun nilai AUC.
Dengan penyajian data yang baik, hasil penelitian menjadi lebih mudah dipahami dan lebih kuat untuk mendukung analisis ilmiah.
