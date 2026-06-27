# WS-15: Scientific Writing

> **Bab 15 — Penulisan Ilmiah**

---

## Ringkasan Materi

### Scientific Argument Flow

```
Problem → Gap → RQ → Method → Result → Analysis → Conclusion → Contribution
```

Paper ilmiah adalah **satu argumen utuh** dari masalah ke kontribusi. Setiap node harus terhubung logis ke node sebelum dan sesudahnya.

### Struktur IMRAD

| Section | Peran | Pertanyaan Kunci |
|---------|-------|-----------------|
| **Introduction** | Motivasi + frame | Why is this needed? |
| **Method** | Deskripsi (reproducible) | How was it done? |
| **Results** | Laporan objektif | What was found? |
| **Discussion** | Interpretasi + refleksi | What does it mean? |
| **Conclusion** | Ringkasan + kontribusi | So what? |

### Logical Flow — "Red Thread"

Setiap paragraf menjawab satu pertanyaan dan memicu pertanyaan berikutnya. Alur logis ini harus terasa di tiga level:
1. **Antar-kalimat** dalam paragraf
2. **Antar-paragraf** dalam section
3. **Antar-section** dalam paper

### Internal Consistency

Setiap elemen yang dijanjikan di Introduction harus hadir di Discussion/Conclusion.

**Consistency Matrix:**
```
           Intro  Method  Result  Discuss  Conclude
RQ1          ✓      ✓       ✓       ✓        ✓
RQ2          ✓      ✓       ✓       ✗ ←      ✓
Metrik-X     ✗      ✗       ✓ ←     ✗        ✗
```
**Masalah:** RQ2 dibahas di semua bagian kecuali Discussion. Metrik-X muncul di Result tapi tidak diperkenalkan di Method.

### Writing Quality Triad

| Kualitas | Deskripsi | Contoh Buruk → Baik |
|----------|----------|---------------------|
| **Clarity** | Dipahami sekali baca | "Performa meningkat" → "Accuracy meningkat dari 85.3% ke 89.7%" |
| **Precision** | Istilah eksak, tanpa ambiguitas | "signifikan" → "signifikan secara statistik (p=0.003, d=1.2)" |
| **Conciseness** | Setiap kata menambah informasi | Hapus kalimat redundan, filler words |

### Urutan Penulisan yang Disarankan

1. **Method & Results** — paling stabil, tulis pertama
2. **Discussion** — interpretasi berdasarkan hasil
3. **Introduction** — frame sesuai temuan aktual
4. **Abstract & Conclusion** — terakhir

### Target Jumlah Kata

| Section | Target |
|---------|--------|
| Introduction | 500–700 |
| Related Work | 700–1000 |
| Method | 800–1200 |
| Results | 500–800 |
| Discussion | 600–900 |
| Conclusion | 200–400 |

### Jebakan Kognitif

1. "Lebih panjang = lebih lengkap" → conciseness lebih berharga
2. "Introduction harus ditulis pertama" → justru ditulis terakhir
3. "Jargon teknis = lebih ilmiah" → clarity lebih penting
4. "Discussion = ringkasan Results" → Discussion = interpretasi + konteks

---

## Template A.15 — Paper Structure Checklist

```
PAPER STRUCTURE CHECKLIST

Title   : Perbandingan Algoritma Decision Tree, Random Forest, dan Support Vector Machine untuk Deteksi Intrusi Jaringan Menggunakan Dataset NSL-KDD
Target  : [✓ ] Jurnal  [ ] Konferensi  [✓ ] Laporan

Section Check:
  [✓ ] Abstract — masalah, metode, hasil utama, kontribusi (max 250 kata)
  [✓ ] Introduction — konteks → gap → RQ → kontribusi → struktur paper
  [✓ ] Related Work — concept-centric, gap positioning
  [✓ ] Method — reproducible: desain, variabel, metrik, setup, prosedur
  [✓ ] Results — tabel + grafik + observasi (tanpa interpretasi)
  [✓ ] Discussion — interpretasi, perbandingan, implikasi, limitation
  [✓ ] Conclusion — jawaban RQ, kontribusi, future work

Consistency Matrix:
  [✓ ] RQ di Introduction = RQ di Method = RQ di Conclusion
  [✓ ] Variabel di Method = variabel di Results
  [✓ ] Klaim di Discussion didukung data di Results
  [✓ ] Limitasi di Discussion di-address di Conclusion/Future Work

Writing Quality:
  [✓ ] Clarity — mudah dipahami tanpa re-read
  [✓ ] Precision — tidak ada istilah ambigu
  [✓ ] Conciseness — tidak ada kalimat redundan
```

---

## Latihan 1 — Paper Outline

Buat outline paper untuk riset Anda menggunakan struktur IMRAD.

| Section | Konten Utama (2-3 kalimat) | Target Kata |
|---------|---------------------------|------------|
| Abstract | Penelitian membandingkan tiga algoritma machine learning untuk intrusion detection menggunakan dataset NSL-KDD. Hasil menunjukkan Random Forest memiliki performa terbaik. | 200-250 |
| Introduction | Menjelaskan pentingnya keamanan jaringan komputer, ancaman intrusion attack, serta kebutuhan algoritma klasifikasi yang akurat. | 500-700 |
| Related Work |Membahas penelitian sebelumnya mengenai IDS berbasis machine learning khususnya Decision Tree, Random Forest, dan SVM. | 700-1000 |
| Method |Menjelaskan preprocessing dataset, cleaning, encoding, train test split, normalisasi, cross validation, grid search, training model, dan evaluasi. | 800-1200 |
| Results |Menampilkan accuracy, precision, recall, F1-score, confusion matrix, ROC Curve, dan hasil statistik. | 500-800 |
| Discussion |Menjelaskan perbandingan performa model, interpretasi statistik, keterbatasan model, serta failure analysis. | 600-900 |
| Conclusion |Menyimpulkan model terbaik serta rekomendasi penelitian berikutnya. | 200-400 |

---

## Latihan 2 — Consistency Matrix

Buat consistency matrix untuk memverifikasi internal consistency paper Anda.

|  | Intro | Method | Result | Discussion | Conclusion |
|--|-------|--------|--------|-----------|-----------|
| RQ1 | ✓ | ✓ | ✓ | ✓ | ✓ |
| RQ2 | ✓ | ✓ | ✓ | ✓ | ✓ |
| Accuracy |✓ |✓ |✓ |✓ |✓ |
| Precision |✓ |✓ |✓ |✓ |✓ |
| Recall |✓ |✓ |✓ |✓ |✓ |
| F1 Score |✓ |✓ |✓ |✓ |✓ |
| Variabel Independent |✓ |✓ |✓ |✓ |✓ |
| Kontribusi Penelitian |✓ |✓ |✓ |✓ |✓ |

**Isi setiap sel:** ✓ (ada & konsisten), ✗ (missing), ~ (ada tapi inkonsisten)

**Inkonsistensi yang ditemukan:**
> Tidak ditemukan inkonsistensi karena seluruh komponen penelitian telah terhubung secara konsisten dari awal hingga akhir penelitian.

**Tindakan perbaikan:**
> Memastikan seluruh pembahasan pada bab hasil dan pembahasan tetap menggunakan metrik evaluasi yang sama seperti pada metodologi penelitian.

---

## Latihan 3 — Writing Quality Check

Ambil satu paragraf dari tulisan Anda (atau tulis paragraf baru) dan evaluasi kualitasnya.

**Paragraf asli:**
> (tempel paragraf Anda di sini)

| Kriteria | Evaluasi | Perbaikan |
|----------|---------|-----------|
| Clarity | Kalimat cukup jelas namun terlalu umum | Menambahkan konteks intrusion detection system |
| Precision |Tidak menjelaskan ukuran performa |Menambahkan metrik accuracy, precision, recall |
| Conciseness |Kalimat masih terlalu sederhana |Membuat struktur kalimat lebih akademik |

**Paragraf setelah perbaikan:**
> (tulis paragraf yang sudah diperbaiki)
Penelitian ini bertujuan membandingkan performa tiga algoritma machine learning yaitu Decision Tree, Random Forest, dan Support Vector Machine dalam mendeteksi intrusi jaringan komputer menggunakan dataset NSL-KDD. Evaluasi dilakukan menggunakan metrik accuracy, precision, recall, F1-score, serta AUC untuk menentukan algoritma dengan performa terbaik dalam sistem intrusion detection.

## Refleksi

> Apa perbedaan antara menulis "tentang" riset dan menulis sebagai "argumen" riset? Bagaimana urutan penulisan (Method → Discussion → Introduction) mengubah kualitas tulisan?

> Menulis laporan penelitian tidak hanya menjelaskan apa yang telah dikerjakan, tetapi harus membangun sebuah argumen ilmiah yang menunjukkan hubungan logis antara masalah penelitian, metode yang digunakan, hasil eksperimen, analisis statistik, serta kontribusi penelitian.
Urutan penulisan yang dimulai dari metodologi, hasil, pembahasan, lalu pendahuluan membantu peneliti menghasilkan tulisan yang lebih konsisten karena seluruh isi penelitian dibangun berdasarkan hasil eksperimen yang benar-benar diperoleh.
> Dalam penelitian ini, proses penulisan menjadi lebih terarah karena setiap tahap eksperimen mulai dari preprocessing, training model, cross validation, hingga analisis statistik telah terdokumentasi dengan baik sehingga mudah disusun menjadi laporan ilmiah yang sistematis.
