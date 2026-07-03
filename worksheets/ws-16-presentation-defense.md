# WS-16: Presentation & Defense (UAS)

> **Bab 16 — Presentasi & Pertahanan Ilmiah**

---

## Ringkasan Materi

### Scientific Defense Model

```
Research Work → Presentation → Questioning → Defense → Evaluation → Acceptance
```

### Presentasi ≠ Ringkasan Paper

| Paper | Presentasi |
|-------|-----------|
| Dibaca (self-paced) | Didengar (presenter-paced) |
| Detail lengkap | Ide kunci + highlight |
| Tabel numerik detail | Grafik visual + angka kunci |
| Pembaca bisa re-read | Audiens dengar sekali |

**Prinsip:** Presentasi membutuhkan **reformulasi**, bukan kompresi. Medium berbeda = pendekatan berbeda.

### Claim-Evidence-Reasoning (CER)

Setiap jawaban defense harus memiliki:
1. **Claim** — Pernyataan yang dijawab
2. **Evidence** — Data/fakta pendukung
3. **Reasoning** — Logika yang menghubungkan evidence ke claim

**Contoh:**
| Pertanyaan | Bad Answer | Good Answer (CER) |
|-----------|-----------|-------------------|
| "Kenapa hanya 3 dataset?" | "Tiga sudah cukup" | "3 dataset mewakili variasi: small-clean, medium-clean, medium-noisy [E]. Generalisasi perlu validasi lanjut — listed as limitation [R]" |
| "Hasil DS-3 menurun?" | "Itu outlier" | "Ya, karena distribusi heavy-tail melanggar asumsi Gaussian [E]. Ini menunjukkan boundary condition metode [R]" |
| "Effect size?" | "p=0.003, jadi signifikan" | "Cohen's d=1.2 (large effect) [E] — bukan hanya signifikan tapi substansial [R]" |

### Slide Design — One Slide, One Message

**Optimal 9-Slide Plan (15 menit):**

| # | Slide | Waktu | Pesan |
|---|-------|-------|-------|
| 1 | Title + context | 1 min | Apa ini tentang apa |
| 2 | Problem + motivation | 2 min | Mengapa penting |
| 3 | Gap + RQ | 1.5 min | Apa yang belum terjawab |
| 4 | Method overview | 2 min | Bagaimana dijawab (diagram) |
| 5 | Key result — tabel | 2 min | Temuan utama |
| 6 | Key result — grafik | 2 min | Pola visual |
| 7 | Interpretation + failure | 2 min | Apa artinya |
| 8 | Limitation + future | 1.5 min | Batasan & arah |
| 9 | Conclusion + contribution | 1 min | Closing message |

### Anticipatory Defense

Prediksi pertanyaan berdasarkan kategori:

| Kategori | Contoh Pertanyaan |
|---------|------------------|
| Problem | "Mengapa masalah ini penting?" |
| Gap | "Bagaimana dengan studi X yang sudah menjawab ini?" |
| Method | "Mengapa metode ini, bukan Y?" |
| Results | "Bagaimana menjelaskan anomali di DS-3?" |
| Generalization | "Apakah bisa diterapkan di domain lain?" |

### Tiga Prinsip Jawaban

1. **Direct** — Jawab dulu, elaborasi kemudian
2. **Data-based** — Tunjuk evidence spesifik
3. **Honest** — Akui limitasi jika memang ada

### Jebakan Kognitif

1. "Presentasi = semua yang ada di paper" → terlalu padat
2. "Slide cantik = presentasi bagus" → konten > estetika
3. "Tidak bisa jawab = gagal" → "I don't know, but..." menunjukkan kejujuran
4. "Tidak perlu latihan — saya paham riset saya" → latihan = menemukan celah

---

## Template A.16 — Defense Preparation Sheet

```
DEFENSE PREPARATION

Slide Deck Plan:
  Total slides   : 10 slide 
  Time per slide :  ± 1.5 menit
  Total time     : 15 menit

Slide Outline:
| #  | Pesan Utama                                            | Visual                               | Waktu     |
| -- | ------------------------------------------------------ | ------------------------------------ | --------- |
| 1  | Judul penelitian dan identitas peneliti                | Title Slide                          | 1 menit   |
| 2  | Permasalahan keamanan jaringan dan intrusion detection | Diagram serangan jaringan            | 2 menit   |
| 3  | Research gap dan tujuan penelitian                     | Tabel penelitian terdahulu           | 1.5 menit |
| 4  | Metodologi penelitian                                  | Flowchart preprocessing dan training | 2 menit   |
| 5  | Dataset NSL-KDD dan preprocessing data                 | Diagram cleaning dataset             | 1.5 menit |
| 6  | Hasil evaluasi model                                   | Tabel accuracy, precision, recall    | 2 menit   |
| 7  | Grafik performa model                                  | Accuracy graph dan ROC Curve         | 2 menit   |
| 8  | Analisis statistik                                     | ANOVA, Friedman Test, Effect Size    | 1.5 menit |
| 9  | Keterbatasan penelitian dan failure analysis           | Tabel limitation                     | 1 menit   |
| 10 | Kesimpulan dan kontribusi penelitian                   | Summary slide                        | 1 menit   |


Anticipatory Defense Matrix:
| Kategori           | Pertanyaan Potensial                                                                    | Jawaban (CER)            
| Problem       | Mengapa penelitian intrusion detection system penting untuk diteliti?                   | Claim: Keamanan jaringan komputer menjadi isu penting pada sistem digital modern. **Evidence:** Banyak serangan jaringan seperti DoS, Probe, dan unauthorized access yang dapat mengganggu sistem. **Reasoning:** Sistem IDS dibutuhkan untuk mendeteksi serangan lebih cepat sehingga keamanan jaringan dapat ditingkatkan.                                                                                       |
| Gap            | Mengapa masih perlu membandingkan algoritma jika penelitian sebelumnya sudah ada?       | Claim: Penelitian sebelumnya menunjukkan hasil performa algoritma yang berbeda-beda. Evidence: Beberapa jurnal menunjukkan Random Forest unggul, sementara penelitian lain menunjukkan performa berbeda tergantung preprocessing dan dataset. Reasoning: Karena hasil penelitian terdahulu tidak selalu sama, perlu dilakukan pengujian ulang untuk mengetahui model terbaik pada skenario penelitian ini. |
| Method         | Mengapa menggunakan Decision Tree, Random Forest, dan SVM sebagai algoritma penelitian? | Claim: Ketiga algoritma merupakan metode machine learning yang sering digunakan pada klasifikasi intrusion detection. Evidence: Jurnal rujukan penelitian menggunakan algoritma berbasis klasifikasi untuk membandingkan performa model. Reasoning: Pemilihan tiga algoritma tersebut memungkinkan dilakukan analisis komparatif terhadap model dengan karakteristik berbeda.                              |
| Results        | Mengapa Random Forest memperoleh hasil terbaik dibanding model lain?                    | Claim: Random Forest memberikan performa paling stabil pada proses klasifikasi. Evidence: Accuracy sebesar 99.61% menjadi hasil tertinggi, didukung hasil ANOVA dan Friedman Test yang menunjukkan perbedaan signifikan antar model. Reasoning: Metode ensemble learning pada Random Forest mampu mengurangi overfitting sehingga model lebih baik dalam melakukan generalisasi data.                      |
| Generalization | Apakah hasil penelitian ini dapat diterapkan pada dataset atau sistem lain?             | Claim: Hasil penelitian dapat menjadi referensi, namun belum dapat digeneralisasi secara penuh. Evidence: Penelitian hanya menggunakan dataset NSL-KDD sebagai dataset eksperimen. Reasoning: Untuk memastikan generalisasi yang lebih luas, penelitian selanjutnya perlu menggunakan dataset lain seperti UNSW-NB15 atau CICIDS2017.                                                                      |


Latihan:
  Latihan 1: [tanggal] — [catatan timing & feedback]
  Latihan 2: [tanggal] — [catatan timing & feedback]
  Latihan 3: [tanggal] — [catatan timing & feedback]
```

---

## Latihan 1 — Slide Outline

Rencanakan presentasi 15 menit untuk riset Anda.

| # | Pesan Utama | Visual yang Digunakan | Waktu |
|---|-------------|----------------------|-------|
| 1 | Judul penelitian dan gambaran umum intrusion detection | Cover slide | 1 min |
| 2 | Ancaman keamanan jaringan semakin meningkat sehingga dibutuhkan IDS | Ilustrasi cyber attack | 2 min |
| 3 | Belum diketahui algoritma terbaik untuk klasifikasi intrusion detection | Tabel gap penelitian | 1.5 min |
| 4 |Dataset NSL-KDD digunakan sebagai sumber data penelitian |Diagram dataset | 1 min |
| 5 |Proses preprocessing: cleaning, encoding, outlier handling, normalisasi |Flowchart preprocessing |2 min |
| 6 |Training model menggunakan Decision Tree, Random Forest, dan SVM |Diagram machine learning pipeline |2 min |
| 7 |Hasil evaluasi accuracy, precision, recall, F1-score, dan AUC |Tabel hasil model |2 min |
| 8 |Hasil statistik ANOVA dan Friedman Test |Grafik statistik |1.5 min |
| 9 |Kesimpulan penelitian dan rekomendasi penelitian berikutnya |Closing slide | 2 min |

**Total waktu estimasi:** ____ menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | Problem | Mengapa memilih topik intrusion detection? | Keamanan jaringan menjadi isu penting pada sistem komputer modern | Banyak serangan jaringan meningkat setiap tahun | IDS membantu mendeteksi serangan secara otomatis |
| 2 | Method | Mengapa menggunakan dataset NSL-KDD? | Dataset NSL-KDD merupakan dataset benchmark intrusion detection | Dataset banyak digunakan pada penelitian IDS | Memudahkan perbandingan dengan penelitian terdahulu |
| 3 |Method |Mengapa memilih Decision Tree, Random Forest, dan SVM? |Ketiga algoritma populer pada klasifikasi machine learning |Banyak jurnal menggunakan tiga model tersebut |Digunakan untuk membandingkan performa model |
| 4 |Results |Mengapa SVM menggunakan subset data? |SVM kernel RBF memiliki kompleksitas komputasi tinggi pada data besar |Training full dataset membutuhkan resource besar |Subset representatif digunakan agar eksperimen efisien |
| 5 |Results |Mengapa Random Forest menghasilkan performa terbaik? |Random Forest menggunakan ensemble learning sehingga lebih stabil |Accuracy 99.61% tertinggi dibanding model lain |Ensemble membantu mengurangi overfitting dan meningkatkan generalisasi |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|
| 1 | Mengapa tidak menggunakan algoritma lain seperti KNN atau Naive Bayes? | Penelitian difokuskan pada tiga algoritma yang paling sering digunakan pada penelitian intrusion detection berdasarkan jurnal referensi yang digunakan | [✓] Direct [✓] Data-based [✓] Honest |
| 2 |Mengapa dilakukan preprocessing sebelum training model? |Preprocessing dilakukan untuk meningkatkan kualitas data melalui cleaning, duplicate removal, outlier handling, encoding, dan normalisasi agar model memperoleh data optimal | [✓ ] Direct [✓ ] Data-based [✓ ] Honest |
| 3 |Bagaimana membuktikan Random Forest memang lebih baik secara ilmiah? |Dilakukan pengujian statistik menggunakan ANOVA dan Friedman Test dengan hasil p-value < 0.05 yang menunjukkan adanya perbedaan signifikan antar model | [✓ ] Direct [✓ ] Data-based [✓ ] Honest |

**Pertanyaan yang paling sulit dijawab:**
> Mengapa algoritma SVM tidak menggunakan seluruh dataset seperti dua model lainnya?

**Apa yang perlu disiapkan lebih baik:**
> Menyiapkan penjelasan teknis mengenai kompleksitas komputasi SVM kernel RBF serta alasan penggunaan subset representatif pada dataset besar.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Penelitian machine learning tidak hanya berfokus pada proses training model, tetapi harus memperhatikan preprocessing data, validasi, analisis statistik, dan interpretasi hasil agar kesimpulan penelitian memiliki dasar ilmiah yang kuat.

**Yang akan selalu diterapkan:**
> Pada penelitian berikutnya, setiap proses eksperimen harus terdokumentasi dengan baik, menggunakan data yang valid, serta selalu melakukan evaluasi model berdasarkan analisis statistik agar hasil penelitian lebih dapat dipercaya.
