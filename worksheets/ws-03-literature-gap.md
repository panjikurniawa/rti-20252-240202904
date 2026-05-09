# WS-03: Literature Mapping & Gap

> **Bab 3 — Literature Review, Research Gap & Baseline**

---

## Ringkasan Materi

### Literature Review = Positioning, Bukan Ringkasan

Literature review bukan merangkum paper satu per satu. Pendekatan yang benar adalah **concept-centric** — organisasi berdasarkan tema, metode, atau variabel. Tujuan: menemukan **pola, kontradiksi, dan gap**.

**Perbandingan pendekatan Author-centric vs Concept-centric:**

| Aspek | Author-centric (Hindari) | Concept-centric (Gunakan) |
|-------|--------------------------|---------------------------|
| Struktur | Per penulis/paper ("Rahman et al. menyatakan...") | Per konsep/metode ("Pendekatan berbasis transformer") |
| Tujuan | Ringkasan isi paper | Perbandingan metode & identifikasi gap |
| Contoh paragraph | "Rahman (2023) pakai CNN. Lee (2022) pakai LSTM. Zhang (2021) pakai RF." | "Tiga pendekatan dominan: CNN digunakan oleh 4 paper untuk representasi fitur visual; LSTM untuk data sekuensial; RF sebagai baseline klasik." |
| Hasil akhir | Daftar paper | Peta pengetahuan + gap yang teridentifikasi |

### Empat Jenis Research Gap

| Jenis Gap | Deskripsi | Contoh |
|-----------|----------|--------|
| **Performance Gap** | Performa belum memadai | Akurasi deteksi hanya 78% pada kasus tertentu |
| **Method Gap** | Pendekatan belum diterapkan | Belum ada yang pakai transformer untuk task ini |
| **Data Gap** | Dataset terbatas/tidak representatif | Semua studi pakai dataset sintetis |
| **Context Gap** | Belum diuji pada konteks berbeda | Belum ada evaluasi di negara berkembang |

Gap terkuat = kombinasi 2+ jenis.

### Systematic Search Strategy

1. **Database utama**: IEEE Xplore, ACM DL, Scopus
   - Akses IEEE/ACM melalui jaringan kampus atau VPN institusi
   - Alternatif bebas biaya: Google Scholar, ResearchGate ([researchgate.net](https://www.researchgate.net)), arXiv ([arxiv.org](https://arxiv.org))
2. **Boolean query** yang terdokumentasi eksplisit
   - Contoh: `("anomaly detection" OR "intrusion detection") AND ("deep learning" OR "neural network") NOT ("medical imaging")`
   - Gunakan tanda kutip untuk frasa eksak; AND/OR/NOT mengontrol scope
3. **Snowballing** — dua arah:
   - **Backward snowballing**: buka daftar referensi di paper kunci → telusuri paper yang dikutip
   - **Forward snowballing**: di Google Scholar, klik "Cited by" di bawah paper kunci → temukan paper yang mengutipnya
   - Ulangi 1–2 tingkat untuk membangun cakupan komprehensif
4. Klaim "belum ada penelitian" harus didukung **bukti pencarian**

### Baseline Selection — 3 Kriteria

| Kriteria | Pertanyaan |
|----------|-----------|
| **Relevan** | Apakah menyelesaikan masalah yang sama? |
| **Representatif** | Apakah mewakili common practice? |
| **State-of-the-Art** | Apakah terbaru/terbaik? |

Membandingkan deep learning 2024 dengan decision tree sederhana tanpa justifikasi = **straw man comparison** (perbandingan tidak jujur).

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan baca literatur | Mencari solusi yang sudah ada | Memahami apa yang belum terjawab |
| Cara membaca paper | Tutorial, how-to | Metode, limitasi, gap |
| Baseline | Framework terpopuler | State-of-the-art yang rigorous |
| Dokumentasi pencarian | Tidak diperlukan | Wajib (reproducible) |

### Istilah Penting

- **Concept-centric** — Organisasi literatur berdasarkan konsep/metode, bukan per penulis
- **Snowballing** — Backward (telusuri referensi) + Forward (cari yang mengutip paper kunci)
- **Research Position** — Pernyataan eksplisit posisi riset terhadap studi sebelumnya
- **Straw man comparison** — Memilih baseline lemah agar metode sendiri terlihat lebih baik

---

## Template A.3 — Literature Mapping & Gap Identification

```
LITERATURE MAPPING

Topik      : Deteksi intrusi jaringan menggunakan machine learning
Database   : Google Scholar dan IEEE Xplore
Query      : ("intrusion detection" OR "network intrusion detection") AND ("machine learning" OR "random forest" OR "SVM")
Tahun      : 2020–2024
Hasil awal : 15 paper → Screening → 5 paper final

Literature Matrix (concept-centric):

| Study | Tahun | Method | Data | Result | Limitation |
|-------|-------|--------|------|--------|------------|
|Dyan Prawita Sari et al.| 2024  |Random Forest, DT, SVM |NSL-KDD |Random Forest akurasi 96.8% | Dataset masih menggunakan NSL-KDD yang cukup lama|
|Singh et al. | 2021 |Supervised Learning | KDD Cup / NSL-KDD | Machine learning efektif untuk IDS | Belum membahas serangan modern secara mendalam |
|Bororing | 2024 | ML Anomaly Detection | Traffic jaringan | Deteksi anomali meningkat | False positive masih cukup tinggi |
|Bhanu et al. | 2020 | Decision Tree | IoT Dataset | Model ringan dan mudah diterapkan | Performa menurun pada data yang kompleks |
|Heizmann et al. | 2022 | Implementasi Machine Learning | Multi dataset | ML membantu proses deteksi otomatis | Generalisasi model masih menjadi tantangan |

Pola yang ditemukan:
  Metode dominan     :  Supervised learning seperti Random Forest, Decision Tree, dan SVM
  Dataset umum       : NSL-KDD dan KDD Cup
  Limitasi berulang  : Banyak penelitian masih memakai dataset lama dan belum menguji kondisi jaringan modern


GAP IDENTIFICATION

Gap 1: [Jenis: performance / method / data / context]
  Deskripsi    : Banyak penelitian masih menggunakan dataset lama seperti NSL-KDD
  Bukti        : Sebagian besar paper pada literature mapping masih memakai dataset NSL-KDD atau KDD Cup
  Signifikansi : Dataset lama belum tentu sesuai dengan pola serangan jaringan saat ini, sehingga hasil penelitian bisa berbeda ketika diterapkan pada kondisi nyata.

Gap 2: [Jenis: Context Gap]
  Deskripsi    : Model belum banyak diuji pada lingkungan jaringan modern dan serangan terbaru
  Bukti        :  Penelitian lebih banyak fokus pada data simulasi dibanding pengujian pada kondisi jaringan nyata
  Signifikansi : Pengujian pada konteks modern penting untuk mengetahui apakah model masih efektif digunakan saat ini


Baseline Selection:
| Baseline | Relevansi | Representatif | Source |
|----------|-----------|---------------|--------|
|  Random Forest  | Sama-sama digunakan untuk deteksi intrusi  | Banyak dipakai pada penelitian IDS berbasis ML  | Dyan Prawita Sari et al., 2024 |
| Support Vector Machine (SVM) | Digunakan untuk klasifikasi traffic jaringan |  Menjadi metode pembanding yang cukup umum digunakan | Singh et al., 2021 |
```

---

## Latihan 1 — Concept-Centric Literature Table

Gunakan topik riset dari WS-02. Cari minimal 5 paper relevan menggunakan database akademik.

> **Panduan pencarian:**
> - Database: IEEE Xplore, ACM DL, Google Scholar, atau ResearchGate
> - Tulis query Boolean yang digunakan: contoh `("object detection" OR "image classification") AND ("edge computing") NOT ("medical")`. Dokumentasikan query secara eksplisit.
> - Akses gratis: buka Google Scholar → cari judul paper → klik [PDF] jika tersedia, atau akses lewat campus VPN

**Topik riset:** Deteksi intrusi jaringan menggunakan machine learning
**Query pencarian:** ("intrusion detection" OR "network intrusion detection") AND ("machine learning" OR "random forest" OR "SVM")
**Database:** Google Scholar dan IEEE Xplore

| # | Study | Tahun | Method | Dataset | Result | Limitasi |
|---|-------|-------|--------|---------|--------|----------|
| 1 | Dyan Prawita Sari et al. | 2024 | Random Forest, Decision Tree, SVM | NSL-KDD | Random Forest memperoleh akurasi tertinggi sebesar 96.8% | Dataset masih memakai NSL-KDD yang sudah cukup lama |
| 2 | Singh et al. | 2021 | Supervised Learning | KDD Cup / NSL-KDD | Machine learning cukup efektif untuk IDS | Belum banyak membahas serangan terbaru |
| 3 | Bororing | 2024 | Machine Learning Anomaly Detection | Traffic jaringan | Deteksi anomali meningkat | False positive masih cukup tinggi |
| 4 | Bhanu et al. | 2020 | Decision Tree | IoT Dataset | Model mudah diterapkan dan ringan | Performa menurun pada data yang kompleks |
| 5 | Heizmann et al. | 2022 | Implementasi ML | Multi dataset | ML membantu proses deteksi otomatis | Generalisasi model masih menjadi tantangan |

**Pola yang terlihat — Metode dominan:** Sebagian besar penelitian menggunakan metode supervised learning seperti Random Forest, Decision Tree, dan SVM untuk mendeteksi intrusi jaringan.
**Limitasi yang berulang:** Banyak penelitian masih memakai dataset lama seperti NSL-KDD sehingga hasil pengujian belum tentu sesuai dengan kondisi jaringan modern saat ini.

---

## Latihan 2 — Gap Identification

Berdasarkan tabel di Latihan 1, identifikasi gap.

| Jenis Gap | Ditemukan? | Gap Statement |
|-----------|-----------|---------------|
| Performance Gap | [✓ ] Ya  | Performa model dapat berubah ketika diuji pada dataset atau kondisi jaringan yang berbeda |
| Method Gap |  [x] Tidak | Metode seperti Random Forest dan SVM sudah cukup sering digunakan |
| Data Gap | [✓ ] Ya  |Banyak penelitian masih menggunakan dataset lama seperti NSL-KDD |
| Context Gap | [✓ ] Ya  |Belum banyak pengujian model pada kondisi jaringan modern dan serangan terbaru |

**Gap utama yang dipilih:** Data Gap dan Context Gap
**Mengapa gap ini penting (bukan sekadar "belum ada yang meneliti")?**
> Penggunaan dataset lama dapat membuat hasil penelitian terlihat bagus, tetapi belum tentu memberikan hasil yang sama ketika diterapkan pada jaringan nyata. Jika model hanya diuji menggunakan data lama, kemampuan deteksi terhadap serangan modern masih belum dapat dipastikan. Karena itu, pengujian menggunakan dataset yang lebih baru penting untuk melihat apakah model benar-benar efektif digunakan saat ini.

---

## Latihan 3 — Baseline Selection

Pilih 2 baseline dari literatur yang sudah dibaca.

| # | Baseline | Mengapa Relevan | Mengapa Representatif | Apakah SOTA? | Sumber |
|---|----------|----------------|----------------------|-------------|--------|
| 1 | Random Forest | Sama-sama digunakan untuk deteksi intrusi jaringan | Banyak digunakan dalam penelitian IDS berbasis machine learning | Bukan SOTA terbaru, tetapi masih sering digunakan | Dyan Prawita Sari et al., 2024 |
| 2 |Support Vector Machine (SVM) | Digunakan untuk klasifikasi traffic jaringan | Menjadi metode pembanding yang umum dipakai | Bukan SOTA | Singh et al., 2021 |

**Apakah pemilihan baseline ini bisa dianggap straw man?**  [✓ ] Tidak
> Justifikasi: Baseline yang dipilih masih relevan dan sering digunakan dalam penelitian deteksi intrusi jaringan, sehingga perbandingan tetap adil dan tidak menggunakan metode yang terlalu lemah.

---

## Refleksi

> Apa perbedaan antara "belum ada yang meneliti ini" (klaim tanpa bukti) dengan research gap yang valid? Bagaimana cara membuktikan bahwa sebuah gap benar-benar ada?

**Jawaban:**
> Pernyataan “belum ada yang meneliti ini” tidak bisa langsung dianggap benar tanpa adanya bukti dari pencarian literatur. Research gap yang valid harus didukung dari beberapa penelitian sebelumnya dan menunjukkan bagian mana yang masih kurang atau belum banyak dibahas.
> Gap penelitian dapat dibuktikan dengan membandingkan beberapa paper yang relevan, misalnya banyak penelitian masih memakai dataset lama atau belum menguji model pada kondisi jaringan modern. Dari situ bisa terlihat bagian mana yang masih perlu diteliti lebih lanjut.
