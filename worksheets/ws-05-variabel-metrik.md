# WS-05: Variabel & Metrik

> **Bab 5 — Metric, Measurement & Data**

---

## Ringkasan Materi

### Measurement Alignment Model

Setiap pengukuran yang valid harus bisa ditelusuri melalui rantai ini tanpa lompatan logis:

```
Problem → Concept → Variable → Metric → Data → Result
```

### Operationalization = Keputusan Desain

Menerjemahkan konsep abstrak menjadi variabel terukur bukan proses mekanis. "Code quality" yang diukur via SonarQube code smells membawa asumsi implisit. Setiap operasionalisasi harus didokumentasikan dan dijustifikasi.

### Empat Tipe Data (NOIR)

| Tipe | Ciri | Contoh | Operasi Valid |
|------|------|--------|---------------|
| **Nominal** | Kategori, tanpa urutan | Jenis algoritma (RF, SVM, CNN) | Modus, chi-square |
| **Ordinal** | Urutan, interval tidak sama | Skala Likert (1-5) | Median, Spearman |
| **Interval** | Jarak bermakna, tanpa nol absolut | Suhu Celsius | Mean, Pearson, t-test |
| **Ratio** | Jarak bermakna + nol absolut | Waktu eksekusi (ms) | Semua operasi |

Tipe data menentukan uji statistik yang valid. Kebanyakan metrik performa TI = ratio; persepsi pengguna = ordinal.

### Kriteria Pemilihan Metrik

- **Representative** — Mewakili konsep yang diteliti
- **Sensitive** — Cukup peka menangkap perbedaan bermakna (hindari ceiling effect)
- **Feasible** — Bisa dikumpulkan dalam batasan waktu dan biaya

### Pre-registration

Metrik harus ditentukan **sebelum** eksperimen. Memilih metrik setelah melihat data = **p-hacking**. Metrik tambahan yang ditemukan kemudian dilaporkan sebagai *exploratory*, bukan *confirmatory*.

### Primary vs Secondary Metric

- **Primary Metric** — Langsung terikat ke hipotesis, menentukan kesimpulan
- **Secondary Metric** — Pendukung, dilaporkan di samping primary; statusnya suplementer

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Pemilihan metrik | Berdasarkan kebiasaan/tool yang ada | Berdasarkan construct validity |
| Anomali | Dihapus untuk laporan bersih | Diinvestigasi — bisa jadi temuan |
| Kapan dipilih | Setelah sistem jadi (monitoring) | Sebelum eksperimen (by design) |

### Istilah Penting

- **Operationalization** — Transformasi konsep abstrak menjadi variabel terukur
- **Construct Validity** — Sejauh mana pengukuran benar-benar mengukur konsep yang dimaksud
- **Measurement Scale** — Klasifikasi data (NOIR) yang menentukan analisis valid
- **Multi-metric Evaluation** — Menggunakan beberapa metrik untuk menangkap konsep kompleks

---

## Template A.5 — Definisi Variabel, Metrik & Justifikasi

```
VARIABLE & METRIC DEFINITION

Research Question: Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD?


| Variabel | Tipe | Konsep | Metrik | Skala | Satuan | Cara Mengukur | Justifikasi |
|----------|------|--------|--------|-------|--------|---------------|-------------|
|Jenis algoritma machine learning          | IV   |Pendekatan klasifikasi intrusi        |Random Forest, Decision Tree, SVM        |Nominal       |—         | Membandingkan algoritma yang digunakan dalam eksperimen               |Digunakan untuk melihat pengaruh jenis algoritma terhadap hasil deteksi intrusi             |
|Performa deteksi intrusi          | DV   |Kemampuan model mendeteksi serangan        |Akurasi, presisi, recall, dan F1-Score        |Ratio       |Persen (%)        | Menghitung hasil evaluasi model pada dataset pengujian               |Metrik ini dapat menunjukkan seberapa baik model mendeteksi intrusi jaringan             |
|Dataset NSL-KDD          | CV   |Sumber data pengujian model        |Jumlah data latih dan data uji        |Ratio       |Data record        |Dataset dibagi menjadi data training dan testing               |Digunakan agar pengujian model dilakukan pada data yang sama dan lebih adil             |

Alignment Check:
  RQ → Concept → Variable → Metric → Data → Result
  [✓ ] Setiap langkah terdokumentasi
  [✓ ] Tidak ada "lompatan logis"
  [✓ ] Metrik mengukur apa yang dimaksud (construct validity)
```

---

## Latihan 1 — Operationalization Chain

Gunakan RQ dari WS-04. Definisikan variabel dan metriknya.

**RQ:** Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD?

| Variabel | Tipe | Konsep Abstrak | Metrik Konkret | Skala (NOIR) | Satuan |
|----------|------|---------------|----------------|-------------|--------|
| Jenis algoritma | IV | Pendekatan machine learning | RF, DT, dan SVM | Nominal | — |
|Performa model | DV |Kemampuan mendeteksi intrusi |Akurasi, presisi, recall, F1-Score |Ratio |Persen (%) |
|Dataset NSL-KDD | CV |Sumber data eksperimen |Jumlah data training dan testing |Ratio |Record data |

**Apakah ada lompatan logis dalam rantai?**  [✓ ] Tidak
> Jika ya, di mana? Tidak ada, karena variabel, metrik, dan data yang digunakan sudah sesuai dengan research question.

---

## Latihan 2 — Evaluasi Metrik

Evaluasi metrik DV yang dipilih di Latihan 1 menggunakan 3 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Representative | 5 |F1-Score dan recall cukup mewakili kemampuan model dalam mendeteksi intrusi jaringan |
| Sensitive |4 |Perbedaan performa antar model masih dapat terlihat dari hasil evaluasi |
| Feasible |5 |Data dan metrik dapat diperoleh langsung dari hasil pengujian model |

**Apakah perlu secondary metric?** [✓ ] Ya 
> Jika ya, apa dan mengapa? AUC dan waktu pemrosesan dapat digunakan sebagai secondary metric untuk melihat kemampuan model dalam membedakan data normal dan serangan, serta melihat efisiensi proses deteksi.

**Contoh kasus ceiling effect untuk metrik ini:**
> Jika semua model memiliki akurasi di atas 99%, maka perbedaan performa antar model akan sulit terlihat hanya dari metrik akurasi.

---

## Latihan 3 — Data Quality Check

Bayangkan data yang akan dikumpulkan dari eksperimen. Evaluasi 4 dimensi kualitas data.

| Dimensi | Pertanyaan | Jawaban | Strategi Mitigasi |
|---------|-----------|---------|------------------|
| Completeness | Apakah semua data point terkumpul? |Sebagian besar data tersedia lengkap pada dataset NSL-KDD |Memastikan tidak ada data penting yang hilang sebelum preprocessing |
| Consistency | Apakah ada kontradiksi internal? |Data memiliki format yang cukup konsisten |Melakukan pengecekan data sebelum pelatihan model |
| Validity | Apakah benar-benar mengukur yang dimaksud? |Dataset berisi data normal dan data serangan jaringan |Menggunakan metrik evaluasi yang sesuai seperti recall dan F1-Score |
| Representativeness | Apakah sampel mewakili populasi target? |Dataset cukup sering digunakan dalam penelitian IDS, tetapi masih tergolong dataset lama |Membandingkan hasil dengan dataset yang lebih baru pada penelitian selanjutnya |

---

## Refleksi

> Mengapa memilih metrik setelah melihat data dianggap p-hacking? Apa bedanya dengan eksplorasi data yang sah?

**Jawaban:**
> Memilih metrik setelah melihat hasil data bisa membuat penelitian menjadi tidak objektif karena peneliti dapat memilih metrik yang memberikan hasil terbaik saja. Hal ini dapat membuat kesimpulan penelitian menjadi bias.
> Berbeda dengan eksplorasi data yang sah, eksplorasi dilakukan untuk memahami pola data atau menemukan informasi tambahan, bukan untuk mengganti metrik utama yang sudah ditentukan sejak awal penelitian.
