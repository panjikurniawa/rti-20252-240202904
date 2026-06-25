# WS-08: Proposal Integration (UTS)

> **Bab 8 — Proposal & Checkpoint**

---

## Ringkasan Materi

### Proposal = Satu Argumen Utuh

Proposal riset bukan kumpulan bab yang independen. Ia adalah **satu argumen** yang mengalir dari masalah ke rencana solusi. Jika satu koneksi putus, seluruh proposal kehilangan koherensi.

### Integration Map — 6 Koneksi Kritis

```
Problem (Bab 2) → Gap (Bab 3) → RQ & H (Bab 4) → Metrik (Bab 5) → Sistem (Bab 6) → Eksperimen (Bab 7)
```

| Koneksi | Pertanyaan Verifikasi |
|---------|----------------------|
| Problem → Gap | Apakah gap muncul dari analisis literatur terhadap masalah? |
| Gap → RQ | Apakah RQ langsung menjawab gap yang teridentifikasi? |
| RQ → Metrik | Apakah setiap variabel di RQ punya metrik terdefinisi? |
| Metrik → Sistem | Apakah setiap metrik bisa diukur oleh komponen sistem? |
| Sistem → Eksperimen | Apakah desain eksperimen menggunakan sistem sebagai instrumen? |

### Koherensi Vertikal + Horizontal

- **Vertikal** — Alur logis atas-ke-bawah (problem → experiment). Setiap section menjawab pertanyaan yang diangkat section sebelumnya dan memunculkan pertanyaan baru.
- **Horizontal** — Konsistensi terminologi (nama variabel di RQ = di hipotesis = di metrik = di desain)

**Operasionalisasi Red Thread** (benang merah):
```
Bab 2 (Problem) → | memperkenalkan masalah X + evidensi |
                          ↓ menimbulkan pertanyaan: "apa akar gap-nya?"
Bab 3 (Gap)     → | menjawab pertanyaan tadi + membuka "lalu apa yang perlu diteliti?" |
                          ↓
Bab 4 (RQ/H)    → | menjawab gap dengan pertanyaan spesifik + prediksi terukur |
                          ↓
Bab 5-7 (Method)→ | menjawab RQ melalui desain eksperimen yang tepat |
```
Jika ada lompatan (section B tidak menjawab pertanyaan section A), red thread putus.

### Jebakan Kognitif

| Jebakan | Deskripsi |
|---------|----------|
| "Selling" Introduction | Menulis promosi, bukan menyajikan data dan gap |
| Copy-paste Methodology | Menyalin deskripsi tekstbook tanpa menyesuaikan ke RQ |
| Optimistic Timeline | Meremehkan waktu implementasi; selalu tambah buffer 30-50% |
| No Possibility of Failure | Mengimplikasikan hasil pasti sukses — proposal jujur mengakui H₀ mungkin tidak ditolak |

### Struktur Proposal

1. **Pendahuluan** — Latar belakang + problem statement (Bab 1-2)
2. **Tinjauan Pustaka** — Literature review + gap + baseline (Bab 3)
3. **RQ / Kontribusi / Hipotesis** — (Bab 4)
4. **Metodologi** — Metrik + sistem + desain eksperimen (Bab 5-7)
5. **Timeline & Output**

### Istilah Penting

- **Integration Map** — Diagram 6 koneksi kritis antar komponen proposal
- **Vertical Coherence** — Alur logis atas-ke-bawah
- **Horizontal Coherence** — Konsistensi terminologi di semua bagian
- **Checkpoint** — Titik self-assessment sebelum transisi dari desain ke eksekusi

---

## Template A.8 — Integration Checklist

```
PROPOSAL INTEGRATION CHECKLIST

Koneksi Vertikal (Flow Atas-Bawah):
  [✓ ] Problem → Gap: masalah terdokumentasi di literatur
  [✓ ] Gap → RQ: pertanyaan menjawab gap spesifik
  [✓ ] RQ → Hypothesis: hipotesis memprediksi jawaban
  [✓ ] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [✓ ] Hypothesis → Metric: metrik mengukur variabel dalam hipotesis
  [✓ ] Metric → System: komponen sistem menghasilkan/mengukur metrik
  [✓ ] System → Experiment: desain eksperimen menggunakan sistem

Koneksi Horizontal (Konsistensi):
  [✓ ] Istilah sama di semua bagian
  [✓ ] Variabel di RQ = variabel di hipotesis = metrik di desain
  [✓ ] Scope tidak berubah dari masalah ke eksperimen

Cognitive Trap Checklist:
  [✓ ] Tidak ada paragraf "promosi" di pendahuluan (hanya data & gap)
  [✓ ] Metodologi disesuaikan ke RQ, bukan copy-paste textbook
  [✓ ] Timeline sudah ditambah buffer 30-50% dari estimasi awal
  [✓ ] Proposal mengakui kemungkinan H0 tidak ditolak (honest uncertainty)
  [✓ ] Tidak ada klaim "pasti berhasil" atau "meningkatkan signifikan"

Rubrik Self-Assessment:
| Kriteria     | 1 (Lemah)                                        | 2 (Cukup)                                     | 3 (Baik)                                           | Skor |
|------------- |--------------------------------------------------|-----------------------------------------------|----------------------------------------------------|------|
| Koherensi    | >2 koneksi vertikal terputus                     | 1-2 koneksi lemah, argumen masih bisa diikuti | Semua 6 koneksi terhubung, red thread jelas        | 3     |
| Specificity  | Variabel/metrik masih abstrak, tidak ada angka   | Sebagian metrik terdefinisi numerik           | Semua metrik + threshold + unit pengukuran jelas   | 3     |
| Feasibility  | Timeline >6 bulan tanpa memperhitungkan sumber   | Timeline 3-6 bulan dengan asumsi tertentu     | Timeline 1-3 bulan realistis dengan rencana detail |  3    |
| Rigor        | Baseline tidak jelas atau straw man              | 1-2 baseline dengan justifikasi partial       | 2+ baseline SOTA + justifikasi pemilihan lengkap   |   3   |
```

---

## Latihan 1 — Kompilasi Proposal Mini

Kumpulkan hasil dari WS-02 sampai WS-07 menjadi satu ringkasan proposal.

| Komponen | Sumber | Isi (1-2 kalimat) |
|----------|--------|-------------------|
| Problem Statement | WS-02 | Sistem deteksi intrusi berbasis machine learning telah banyak digunakan, namun belum diketahui algoritma mana yang memberikan performa terbaik dalam mendeteksi berbagai jenis serangan jaringan komputer. |
| Gap | WS-03 | Penelitian sebelumnya menunjukkan penggunaan beberapa algoritma machine learning pada IDS, tetapi masih diperlukan analisis komparatif untuk mengetahui algoritma yang paling efektif dalam mendeteksi intrusi jaringan. |
| RQ | WS-04 | Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD berdasarkan metrik evaluasi model? |
| Hipotesis | WS-04 | H₁: Random Forest memiliki performa lebih baik dibandingkan Decision Tree dan SVM berdasarkan akurasi, presisi, recall, F1-Score, dan AUC. |
| Variabel & Metrik | WS-05 | IV = jenis algoritma machine learning; DV = performa model; metrik = akurasi, presisi, recall, F1-Score, AUC, serta waktu pemrosesan. |
| Sistem | WS-06 |Sistem dibangun dengan modul preprocessing data, modul classifier (Decision Tree, Random Forest, SVM), serta modul evaluasi untuk mengukur performa model secara otomatis. |
| Desain Eksperimen | WS-07 |Penelitian menggunakan comparison study dengan menguji tiga algoritma pada dataset NSL-KDD menggunakan preprocessing dan lingkungan pengujian yang sama agar hasil perbandingan adil. |

---

## Latihan 2 — Integration Checklist

Verifikasi 6 koneksi kritis. Isi dengan merujuk tabel di Latihan 1.

| Koneksi | Status | Bukti |
|---------|--------|-------|
| Problem → Gap | ✓ |Masalah berasal dari kebutuhan mengetahui algoritma machine learning yang paling efektif untuk deteksi intrusi jaringan. |
| Gap → RQ | ✓ |Research Question secara langsung menguji apakah Random Forest lebih unggul dibanding algoritma lain. |
| RQ → Hypothesis | ✓ |Hipotesis memprediksi bahwa Random Forest akan memberikan hasil evaluasi lebih baik dibanding baseline. |
| Hypothesis → Metric |✓ |Hipotesis diukur menggunakan akurasi, presisi, recall, F1-Score, AUC, dan waktu pemrosesan. |
| Metric → System |✓ |Sistem memiliki modul evaluasi yang dapat menghasilkan seluruh metrik performa model secara otomatis. |
| System → Experiment |✓ |Sistem digunakan sebagai alat eksperimen untuk menguji performa tiga algoritma dalam kondisi pengujian yang identik. |

**Koneksi mana yang paling lemah?** Problem → Gap
**Bagaimana cara memperkuatnya?**
> Menambahkan lebih banyak referensi penelitian terdahulu agar alasan pentingnya analisis komparatif antar algoritma menjadi lebih kuat.

**Konsistensi horizontal — apakah istilah dan scope konsisten?** [✓ ] Ya / [ ] Tidak
> Jika tidak, di bagian mana terjadi inkonsistensi? Seluruh istilah seperti Random Forest, Decision Tree, SVM, dataset NSL-KDD, serta metrik evaluasi digunakan secara konsisten dari awal hingga desain eksperimen.

---

## Latihan 3 — Rubrik Self-Assessment

Evaluasi proposal mini menggunakan rubrik.

| Kriteria | Skor (1-3) | Justifikasi |
|----------|-----------|-------------|
| Koherensi | 3 |Semua bagian proposal saling terhubung mulai dari problem statement hingga desain eksperimen. |
| Specificity | 3 |Variabel, dataset, algoritma, dan metrik evaluasi telah didefinisikan dengan jelas dan spesifik. |
| Feasibility |3 |Penelitian realistis dilakukan karena menggunakan dataset publik dan algoritma machine learning yang umum digunakan. |
| Rigor |3 |Penelitian menggunakan tiga baseline yang jelas dan membandingkannya dengan metode evaluasi yang sama sehingga hasil lebih valid. |

**Skor total:** 12 / 12

**Apakah proposal siap untuk fase eksekusi?** [✓ ] Ya / [ ] Belum
> Jika belum, apa yang perlu diperbaiki? Proposal telah memiliki alur penelitian yang konsisten, variabel yang jelas, serta rancangan eksperimen yang sesuai dengan tujuan penelitian sehingga siap untuk tahap implementasi dan pengujian.

---

## Refleksi

> Dari seluruh proses WS-01 sampai WS-08, bagian mana yang paling mudah dan paling sulit? Mengapa? Apa yang akan dilakukan berbeda jika mengulang dari awal?

**Bagian termudah:** Menentukan variabel penelitian dan metrik evaluasi karena jurnal yang digunakan sudah menjelaskan algoritma, dataset, dan ukuran performa secara rinci.
**Bagian tersulit:** Menentukan gap penelitian dan menyusun research question karena harus memastikan pertanyaan penelitian benar-benar sesuai dengan tujuan penelitian dan tidak menyimpang dari isi jurnal.
**Yang akan dilakukan berbeda:**
> Jika mengulang dari awal, saya akan membaca jurnal secara menyeluruh terlebih dahulu agar dapat memahami hubungan antara masalah penelitian, metode, dan eksperimen dengan lebih baik.
> Saya juga akan lebih teliti menjaga konsistensi antara problem statement, research question, variabel, dan desain eksperimen agar seluruh proposal tetap berada pada satu jalur penelitian yang sama.
