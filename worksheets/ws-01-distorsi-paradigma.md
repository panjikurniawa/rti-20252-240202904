# WS-01: Distorsi & Paradigma

> **Bab 1 — Research Mindset in IT**

---

## Ringkasan Materi

### Research Trust Model

Pengetahuan ilmiah tidak muncul langsung dari kenyataan. Ia melewati **6 tahap transformasi** yang masing-masing rawan distorsi:

```
Reality → Data → Processing → Analysis → Inference → Knowledge
```

Etika mencegah distorsi yang disengaja (fabrikasi, cherry-picking). Validitas mendeteksi distorsi yang tidak disengaja (confounding variable, sampling bias).

### Tiga Jenis Validitas

| Jenis | Pertanyaan | Contoh Ancaman |
|-------|-----------|----------------|
| **Internal Validity** | Apakah hubungan kausal benar ada? | Confounding variable |
| **External Validity** | Apakah bisa digeneralisasi? | Dataset terlalu homogen |
| **Construct Validity** | Apakah mengukur hal yang benar? | Metrik tidak sesuai klaim |

### Paradigma Riset

Mata kuliah ini menggunakan pendekatan **Positivist** (fenomena TI bisa diukur objektif melalui eksperimen terkontrol) diperkuat **Design Science Research** (DSR). Penting untuk membedakan keduanya:

| Paradigma | Cara Kerja | Contoh di TI |
|-----------|-----------|---------------|
| **Positivis** | Uji hipotesis dengan eksperimen terkontrol | Apakah CNN lebih akurat dari RF pada dataset X? |
| **Design Science Research** | Bangun artefak (sistem/model/framework) untuk menguji proposisi | Dapatkah arsitektur hybrid CNN+LSTM membuktikan peningkatan recall ≥5%? |
| **Interpretivis** | Pahami makna melalui konteks & kualitatif | Bagaimana peneliti manafsirkan anomali data sensor IoT? |

Dalam DSR, artefak **bukan tujuan akhir** — ia adalah instrumen untuk menghasilkan pengetahuan. Pertanyaan riset tetap harus difalsifikasi.

### Mode Berpikir Peneliti

**Curious** (mempertanyakan fenomena) → **Critical** (mengevaluasi klaim berdasarkan bukti) → **Systematic** (merancang investigasi terstruktur dan reproducible).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Membuat sistem yang bekerja | Menghasilkan pengetahuan yang valid |
| Pertanyaan khas | "Bagaimana membuatnya jalan?" | "Apakah klaim ini benar?" |
| Ukuran sukses | Sistem berfungsi, client puas | Hipotesis terjawab, temuan tervalidasi |
| Kegagalan | Harus dihindari | Harus dilaporkan (negative result = kontribusi) |

### Istilah Penting

- **Research Mindset** — Pola pikir yang menuntut bukti dan mempertanyakan asumsi
- **Research Ethics** — Prinsip perilaku: kejujuran, objektivitas, keterbukaan, akuntabilitas
- **HARKing** — Hypothesizing After Results are Known — merumuskan hipotesis setelah melihat data
- **Falsifiability** — Hipotesis harus bisa dibuktikan salah

---

## Template A.1 — Research Mindset Self-Assessment

```
Nama Peneliti    : Panji Kurniawan
Tanggal          : 23 April 2026

1. Ketika membaca klaim "metode X 95% akurat":
   - Pertanyaan pertama saya: Apakah akurasi tersebut diuji pada dataset yang representatif terhadap kondisi nyata, dan apakah ada perbandingan yang adil dengan metode lain?
   - Data yang dibutuhkan untuk verifikasi: Confusion matrix, distribusi kelas, detail dataset (jenis & tahun), metode evaluasi (cross-validation), serta baseline model.


2. Posisi paradigma:
   - Pendekatan: [ ] Positivis  [ ] Interpretivis  [ ] Design Science  [ ] Mixed
   - Alasan: Penelitian menguji performa model secara kuantitatif (positivis) sekaligus membangun artefak berupa model machine learning untuk membuktikan efektivitasnya (design science).

3. Identifikasi distorsi:
   - Asumsi tersembunyi:  Dataset NSL-KDD dianggap mewakili kondisi nyata jaringan modern.
   - Sumber bias potensial: Dataset bias (data lama), penghapusan outlier, dan kemungkinan ketidakseimbangan kelas.
   - Langkah mitigasi: Menggunakan dataset tambahan yang lebih modern, melakukan evaluasi lintas dataset, serta melaporkan hasil dengan dan tanpa preprocessing tertentu.

4. Komitmen etika:
   - Data yang tidak akan dimanipulasi: Data outlier dan data yang menurunkan performa model tetap dilaporkan.
   - Batasan yang diakui sejak awal: Dataset yang digunakan bersifat terbatas dan mungkin tidak merepresentasikan kondisi dunia nyata.
```

---

## Latihan 1 — Identifikasi Distorsi

Pilih satu paper riset di bidang TI yang mengklaim "metode X meningkatkan performa." Telusuri setiap tahap Research Trust Model.

> **Panduan pencarian paper:** Gunakan [IEEE Xplore](https://ieeexplore.ieee.org), [ACM Digital Library](https://dl.acm.org), atau Google Scholar. Pilih paper **tahun 2020 ke atas**, di topik yang Anda minati: deteksi anomali, klasifikasi citra, NLP, keamanan siber, IoT, dsb.
>
> **Contoh domain TI:** "Deteksi anomali lalu-lintas jaringan menggunakan CNN — akurasi meningkat 94% vs baseline SVM 87%." Distorsi potensial: apakah dataset normal/anomali seimbang? Apakah hanya diuji pada satu vendor traffic?

**Paper yang dipilih:**
> Judul: Implementasi Machine Learning untuk Deteksi
Intrusi pada Jaringan Komputer
> Penulis (Tahun): Dyan Prawita Sari, Zuhri Halim, Irlon, Bayu Waseso, Saromah (2024)
> Sumber/Link DOI: (https://jurnal.polgan.ac.id/index.php/jmp/article/view/14074)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Menggunakan dataset NSL-KDD sebagai representasi trafik jaringan | Dataset lama → tidak mencerminkan serangan modern (external validity) |
| Data → Processing |Normalisasi, encoding, penghapusan outlier |Outlier bisa merupakan serangan nyata → bias |
| Processing → Analysis |Training model (DT, RF, SVM) + cross-validation |Hyperparameter tuning tidak dijelaskan detail → fairness issue |
| Analysis → Inference |Bandingkan performa berdasarkan akurasi, presisi, recall |Tidak ada uji signifikansi statistik |
| Inference → Knowledge |Klaim Random Forest paling efektif |Over-generalization (hanya 1 dataset) |

**Distorsi paling besar di tahap:** External Validity (dataset tidak representatif terhadap kondisi nyata)

**Dua distorsi spesifik yang teridentifikasi:**
1. Penggunaan dataset NSL-KDD yang tidak mencerminkan kondisi jaringan modern
2. Penghapusan outlier yang berpotensi menghilangkan data serangan pentin

---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Outlier tidak boleh dihapus hanya untuk meningkatkan hasil; harus dilaporkan dua versi |
| Transparansi |Peneliti harus menjelaskan alasan penghapusan outlier dan dampaknya terhadap hasil |
| Peer review |Reviewer akan mempertanyakan validitas jika outlier dihapus tanpa justifikasi kuat |

**Keputusan akhir dan justifikasi:**
> Outlier sebaiknya tidak langsung dihapus. Analisis harus dilakukan dalam dua skenario (dengan dan tanpa outlier), disertai penjelasan apakah outlier merupakan noise atau bagian dari fenomena nyata. Hal ini penting untuk menjaga integritas ilmiah dan menghindari bias dalam interpretasi hasil.

---

## Latihan 3 — Posisi Paradigma

**Topik riset:** Deteksi intrusi jaringan menggunakan machine learning

> **Skala 1–5:** 1 = tidak sesuai sama sekali dengan topik ini, 5 = sangat sesuai dan dominan digunakan pada riset bertopik serupa.

| Kriteria | Positivis | Interpretivis | Design Science |
|----------|-----------|---------------|----------------|
| Kesesuaian dengan topik (1–5) | 5 — fokus pada pengujian performa model | 1 — tidak melibatkan interpretasi manusia | 5 — membangun model sebagai artefak |
| Jenis data yang dikumpulkan | Data numerik (log jaringan, metrik evaluasi) | Data kualitatif tidak digunakan | Hasil uji model dan performa sistem |
| Limitasi paradigma |Terbatas pada dataset, tidak menangkap konteks nyata |Tidak relevan untuk masalah teknis ini |Artefak bisa overfit pada dataset tertentu |

**Paradigma yang dipilih:** Positivis + Design Science
**Alasan:** Penelitian ini menguji performa model secara kuantitatif (positivis) sekaligus membangun artefak berupa model machine learning untuk membuktikan efektivitasnya (design science research).

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelumnya, saya cenderung menerima klaim akurasi tinggi seperti 95% tanpa mempertanyakan konteksnya. Setelah memahami konsep distorsi dalam Research Trust Model, saya menyadari bahwa angka tersebut bisa dipengaruhi oleh banyak faktor seperti pemilihan dataset, preprocessing, dan metode evaluasi.

Sekarang, saya akan mempertanyakan apakah dataset yang digunakan representatif, apakah terdapat bias dalam preprocessing seperti penghapusan outlier, serta apakah hasil tersebut dapat digeneralisasi. Saya juga lebih kritis terhadap klaim performa tinggi dan tidak langsung menganggapnya sebagai bukti keunggulan metode.
> ___________________________________________________
