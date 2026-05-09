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
   - Pertanyaan pertama saya:Apakah dataset yang digunakan benar-benar sesuai dengan kondisi nyata, dan apakah metode pembandingnya diuji secara adil?
   - Data yang dibutuhkan untuk verifikasi: Saya ingin melihat detail dataset, pembagian data, confusion matrix, dan bagaimana model tersebut diuji.

2. Posisi paradigma:
   - Pendekatan: [✓ ] Positivis  [ ] Interpretivis  [✓ ] Design Science  [ ] Mixed
   - Alasan: “Penelitian ini menggunakan data dan pengujian angka untuk melihat performa model, sekaligus membuat model machine learning sebagai solusi deteksi intrusi.

3. Identifikasi distorsi:
   - Asumsi tersembunyi:  Penelitian menganggap dataset NSL-KDD masih cocok untuk kondisi jaringan saat ini.
   - Sumber bias potensial: Dataset bias (data lama), penghapusan outlier, dan kemungkinan ketidakseimbangan kelas.
   - Langkah mitigasi: Penelitian sebaiknya memakai dataset yang lebih baru dan membandingkan hasil sebelum dan sesudah preprocessing.

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
> Judul: Implementasi Machine Learning untuk Deteksi Intrusi pada Jaringan Komputer
> Penulis (Tahun): Dyan Prawita Sari et al.(2024)
> Sumber/Link DOI: (https://jurnal.polgan.ac.id/index.php/jmp/article/view/14074)

| Tahap | Apa yang Dilakukan | Potensi Distorsi |
|-------|-------------------|-----------------|
| Reality → Data | Menggunakan dataset NSL-KDD sebagai representasi trafik jaringan | Dataset lama → tidak mencerminkan serangan modern (external validity) |
| Data → Processing |Normalisasi, encoding, penghapusan outlier |Outlier bisa merupakan serangan nyata → bias |
| Processing → Analysis |Training model (DT, RF, SVM) + cross-validation |Hyperparameter tuning tidak dijelaskan secara rinci, sehingga berpotensi menyebabkan ketidakadilan dalam perbandingan model (fairness issue) |
| Analysis → Inference |Bandingkan performa berdasarkan akurasi, presisi, recall |Tidak ada uji signifikansi statistik |
| Inference → Knowledge |Klaim Random Forest paling efektif |Over-generalization (hanya 1 dataset) |

**Distorsi paling besar di tahap:** External Validity (dataset tidak representatif terhadap kondisi nyata) 
Akurasi tinggi bisa jadi karena dataset yang digunakan sudah cukup mudah dipelajari oleh model, jadi belum tentu hasilnya sama di kondisi nyata.

**Dua distorsi spesifik yang teridentifikasi:**
1. Dataset NSL-KDD sudah cukup lama sehingga belum tentu sesuai dengan kondisi jaringan sekarang.
2. Beberapa outlier mungkin sebenarnya bagian dari pola serangan sehingga tidak seharusnya langsung dihapus.
---

## Latihan 2 — Analisis Kasus Etika

Skenario: Seorang peneliti menemukan bahwa jika 3 data point outlier dihapus, hasil eksperimennya menjadi signifikan. Dengan outlier, hasilnya tidak signifikan.

| Perspektif | Analisis |
|------------|---------|
| Kejujuran ilmiah | Outlier tidak boleh dihapus hanya untuk meningkatkan hasil; harus dilaporkan dua versi |
| Transparansi |Peneliti perlu menjelaskan kenapa outlier dihapus dan bagaimana pengaruhnya terhadap hasil penelitian.|
| Peer review |Reviewer akan mempertanyakan validitas jika outlier dihapus tanpa justifikasi kuat |

**Keputusan akhir dan justifikasi:**
> Outlier sebaiknya tidak langsung dihapus. Analisis harus dilakukan dalam dua skenario (dengan dan tanpa outlier), disertai penjelasan apakah outlier merupakan noise atau bagian dari fenomena nyata. Hal ini penting supaya hasil penelitian tetap jujur dan tidak menyesatkan.

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
**Alasan:** Penelitian ini menggunakan data dan pengujian untuk melihat performa model, sekaligus membuat model machine learning untuk mendeteksi intrusi jaringan.

---

## Refleksi

> Sebelum membaca materi ini, apakah pernah mempertanyakan klaim "95% akurat"? Setelah memahami rantai distorsi, pertanyaan apa yang sekarang akan diajukan saat membaca paper?

**Jawaban:**
> Sebelumnya, saya biasanya langsung percaya kalau ada penelitian yang mengklaim akurasi tinggi seperti 95%. Setelah mempelajari materi ini, saya sadar kalau akurasi tinggi belum tentu berarti modelnya benar-benar bagus karena hasilnya bisa dipengaruhi dataset dan cara pengujiannya.
> Sekarang, saya akan mempertanyakan apakah dataset yang digunakan representatif, apakah terdapat bias dalam preprocessing seperti penghapusan outlier, serta apakah hasil tersebut dapat digeneralisasi. Sekarang saya jadi lebih hati-hati saat melihat klaim akurasi tinggi dan tidak langsung percaya begitu saja.
