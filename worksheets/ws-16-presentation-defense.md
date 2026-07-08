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
| 2 | Ancaman keamanan jaringan meningkat — dibutuhkan IDS yang adaptif | Ilustrasi cyber attack / diagram serangan | 2 min |
| 3 | Penelitian terdahulu sudah ada tapi skema berbeda → gap penelitian ini | Tabel gap penelitian (Sari et al. 2024 vs penelitian ini) | 1.5 min |
| 4 |Dataset NSL-KDD: 148.517 record, gabung KDDTrain++KDDTest+, split 70:30 |Tabel ringkasan dataset & preprocessing| 1 min |
| 5 |Preprocessing: cleaning (610 duplikat, 37.825 outlier IQR), encoding, normalisasi MinMaxScaler |Flowchart preprocessing 5 langkah |2 min |
| 6 |Training 3 model: DT, RF, SVM — dengan 10-fold CV dan GridSearchCV |Diagram machine learning pipeline |2 min |
| 7 |Hasil evaluasi: RF terbaik (99.61%), DT (99.58%), SVM (99.09%) |Tabel metrik + bar chart accuracy |2 min |
| 8 |Uji statistik: Friedman p=0.00013, W=0.895 (large effect) |Tabel uji statistik + post-hoc Wilcoxon |1.5 min |
| 9 |Kesimpulan: RF signifikan terbaik; SVM kurang efisien untuk data besar |Closing slide + future work | 2 min |

**Total waktu estimasi:** 15 menit

---

## Latihan 2 — Anticipatory Defense

Prediksi 5 pertanyaan yang mungkin diajukan penguji, lalu siapkan jawaban CER.

| # | Kategori | Pertanyaan | Claim | Evidence | Reasoning |
|---|----------|-----------|-------|----------|-----------|
| 1 | Problem | Mengapa memilih topik intrusion detection? | Keamanan jaringan adalah isu kritis di era digital | Serangan siber (DDoS, malware, intrusi) menyebabkan kerugian finansial dan reputasi (Maxwell et al., 2018). IDS tradisional berbasis rule-based tidak mampu mendeteksi serangan baru | Machine learning mampu belajar dari pola historis dan mendeteksi anomali baru secara adaptif — solusi lebih efektif daripada rule-based (Bororing, 2024) |
| 2 | Method | Mengapa menggunakan dataset NSL-KDD? | Dataset NSL-KDD merupakan dataset benchmark intrusion detection | Dataset mencakup 41 fitur jaringan, 4 kategori serangan (DoS, Probe, R2L, U2R), dan lalu lintas normal. Digunakan Sari et al. (2024) sebagai jurnal rujukan sehingga hasil bisa dibandingkan langsung | NSL-KDD merupakan versi yang lebih bersih dari KDD Cup 99 (menghapus duplikat, lebih representatif), memungkinkan pelatihan model pada skenario realistis |
| 3 |Method |Mengapa memilih Decision Tree, Random Forest, dan SVM? |Ketiga algoritma mewakili tiga karakteristik berbeda dan relevan untuk analisis komparatif |Sari et al. (2024) menggunakan ketiga algoritma yang sama pada NSL-KDD. DT (interpretable), RF (ensemble, robust), SVM (margin-based, kernel trick) |Pemilihan ini memungkinkan perbandingan fair antara model tree-based vs margin-based, serta validasi langsung terhadap jurnal rujukan |
| 4 |Results |Mengapa SVM menggunakan subset data? |SVM kernel RBF memiliki kompleksitas komputasi O(n²-n³) yang tidak efisien pada data besar |Training SVM penuh (77.057 record) menyebabkan proses macet >2 jam di Google Colab. Subset 30.000 untuk training final dan 15.000 untuk CV/grid search masih representatif (>38% data training) |Penggunaan subset adalah praktik umum dalam penelitian ML ketika resource komputasi terbatas. Keterbatasan ini didokumentasikan secara transparan di bagian limitation |
| 5 |Results |Mengapa Random Forest menghasilkan performa terbaik? |Random Forest unggul karena ensemble 200 pohon meredam variabilitas dan mencegah overfitting |RF: accuracy 99.61%, AUC 0.9997, std ±0.05% (paling stabil). Friedman test: χ²=17.897, p=0.00013, Kendall's W=0.895 (large effect). Post-hoc: RF vs DT p=0.00781, RF vs SVM p=0.00195 — semua signifikan |Ensemble dari 200 decision tree mengkombinasikan prediksi yang beragam sehingga error individual saling mengkompensasi — berbeda dari DT tunggal yang rentan overfitting |

---

## Latihan 3 — Simulasi Q&A

Minta teman/kolega mengajukan 3 pertanyaan tentang riset Anda. Catat pertanyaan dan evaluasi jawaban Anda.

| # | Pertanyaan | Jawaban Saya | Evaluasi |
|---|-----------|-------------|---------|
| 1 | Mengapa tidak menggunakan algoritma lain seperti KNN atau Naive Bayes? | Penelitian difokuskan pada tiga algoritma yang paling sering digunakan pada penelitian intrusion detection berdasarkan jurnal referensi (Sari et al., 2024). Pemilihan DT, RF, dan SVM memungkinkan perbandingan langsung dengan hasil jurnal rujukan sehingga kebaruan penelitian ini bisa diposisikan dengan jelas | [✓] Direct [✓] Data-based [✓] Honest |
| 2 |Mengapa dilakukan preprocessing sebelum training model? |Preprocessing dilakukan untuk meningkatkan kualitas data: 610 duplikat dan 37.825 outlier (IQR) dihapus, fitur kategorikal di-encode dengan one-hot encoding, dan seluruh fitur dinormalisasi ke [0,1] dengan MinMaxScaler. Tanpa preprocessing, model SVM yang sensitif terhadap skala data akan menghasilkan performa suboptimal | [✓ ] Direct [✓ ] Data-based [✓ ] Honest |
| 3 |Bagaimana membuktikan Random Forest memang lebih baik secara ilmiah? |Dilakukan uji Friedman test (χ²=17.897, p=0.00013) dan repeated-measures ANOVA (F=156.49, p<0.0001) menggunakan data 10-fold cross-validation. Effect size Kendall's W=0.895 (large effect) — artinya perbedaannya bukan hanya signifikan secara statistik tapi substansial secara praktis. Post-hoc Wilcoxon (Bonferroni-corrected): RF vs DT p=0.00781 (d=-1.16), RF vs SVM p=0.00195 (d=3.98) — semua signifikan | [✓ ] Direct [✓ ] Data-based [✓ ] Honest |

**Pertanyaan yang paling sulit dijawab:**
> Mengapa algoritma SVM tidak menggunakan seluruh dataset seperti dua model lainnya?

**Apa yang perlu disiapkan lebih baik:**
> SVM dengan kernel RBF memiliki kompleksitas komputasi O(n²) hingga O(n³) terhadap jumlah data. Pada dataset dengan 77.057 record training, proses training SVM penuh menyebabkan Colab macet lebih dari 2 jam tanpa hasil. Subset 30.000 record (>38% data training) dipilih sebagai kompromi antara representativitas data dan efisiensi komputasi. Keterbatasan ini didokumentasikan secara transparan di bagian limitation, sehingga pembaca tahu bahwa perbandingan SVM dengan DT/RF tidak sepenuhnya setara dari sisi jumlah data training.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-16 — dari paradigma riset hingga presentasi — bagian mana yang paling mengubah cara Anda berpikir tentang riset? Apa satu hal yang akan selalu Anda terapkan di riset berikutnya?

**Insight terbesar:**
> Dari seluruh proses WS-01 sampai WS-16, insight terbesar yang saya dapatkan adalah bahwa penelitian machine learning yang valid bukan hanya soal "model mana yang accuracy-nya paling tinggi" — tapi soal bagaimana membuktikan secara ilmiah bahwa perbedaan itu nyata, bukan
kebetulan. Sebelum mengerjakan rangkaian WS ini, saya akan puas dengan melihat RF=99.61% dan DT=99.58% lalu langsung menyimpulkan "RF lebih baik". Sekarang saya tahu bahwa tanpa Friedman test (p=0.00013) dan effect size (Kendall's W=0.895), klaim itu tidak lebih dari observasi deskriptif — bukan kesimpulan ilmiah yang bisa dipertahankan di depan penguji. Angka yang terlihat bagus belum tentu bermakna secara statistik, dan angka yang signifikan secara statistik belum tentu relevan secara praktis (statistical significance ≠ practical significance). Dua hal ini adalah insight yang paling mengubah cara saya melihat hasil eksperimen.

**Yang akan selalu diterapkan:**
> Pada setiap penelitian berikutnya, saya akan selalu memastikan bahwa setiap klaim perbandingan ("A lebih baik dari B") didukung minimal tiga hal secara bersamaan: (1) uji signifikansi statistik (p-value) untuk membuktikan perbedaan bukan kebetulan, (2) effect size untuk mengukur seberapa besar perbedaan yang sebenarnya terjadi, dan (3) confidence interval untuk menunjukkan rentang ketidakpastian
estimasi. Tanpa ketiganya, hasil eksperimen hanya terlihat meyakinkan secara permukaan tapi tidak akan bisa dipertahankan ketika dihadapkan pada pertanyaan penguji yang kritis maupun peer-review yang ketat.
