# WS-02: Problem Statement

> **Bab 2 — Problem Formulation & System Context**

---

## Ringkasan Materi

### Problem Formation Model

Masalah riset melewati 5 tahap transformasi. Melompat langsung dari Reality ke Variable adalah kesalahan paling umum.

```
Reality → Observed Issue (Symptom) → Diagnosed Problem (Root Cause)
→ Researchable Problem (Scoped) → Measurable Variable (Operationalized)
```

### Topic ≠ Problem ≠ Research Problem

| Level | Contoh | Status |
|-------|--------|--------|
| **Topik** | Keamanan IoT | Terlalu luas, tidak bisa diuji |
| **Problem** | MQTT tidak terenkripsi | Spesifik tapi belum riset |
| **Research Problem** | Belum ada studi membandingkan overhead TLS 1.3 vs DTLS pada MQTT di IoT RAM < 64KB | Bisa dirancang eksperimennya |

### Symptom vs Root Cause

Apa yang diamati (gejala) ≠ mengapa terjadi (akar masalah). Gunakan **5 Whys** atau **Fishbone Diagram** untuk menggali.

Contoh: "User meninggalkan checkout" (symptom) → "Waktu loading > 8 detik karena API call sequential" (root cause).

### System Thinking

Setiap masalah riset TI harus terikat pada komponen sistem: **Input → Process → Output → Outcome → Constraints → Stakeholders**.

### Problem Quality Check

Masalah riset yang layak harus memenuhi 5 kriteria:
- **Clarity** — Satu orang membaca akan paham
- **Measurability** — Ada metrik kuantitatif
- **Relevance** — Penting untuk domain
- **Testability** — Bisa gagal (falsifiable)
- **Impact** — Ada kontribusi jika terjawab

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan | Menyelesaikan masalah (*solve*) | Memahami dan membuktikan (*understand & prove*) |
| Masalah | Bug, error, fitur belum ada | Gap dalam pengetahuan |
| Scope | Selesaikan semua yang perlu | Batasi agar bisa dibuktikan |
| Output | Working system | Evidence, paper, replicable findings |

### Istilah Penting

- **Problem Statement** — Formulasi tertulis: konteks sistem + gap + dampak + justifikasi
- **System Context** — Deskripsi lengkap: input, proses, output, outcome, constraints, stakeholders
- **Problem Drift** — Masalah "bermutasi" dari pendahuluan ke metodologi karena statement awal tidak presisi
- **Solution-First Thinking** — Memulai dari solusi tanpa masalah yang jelas — berbahaya dalam riset
- **Operational Definition** — Definisi variabel yang cukup jelas agar peneliti lain bisa mengukur hal yang sama

---

## Template A.2 — Problem Statement Builder

```
PROBLEM STATEMENT BUILDER

Domain & Konteks
  Domain   : Keamanan jaringan komputer (Intrusion Detection System)
  Konteks  : Deteksi intrusi berbasis machine learning pada lingkungan jaringan modern

System Context
  Input       : Data lalu lintas jaringan (fitur koneksi dari dataset seperti NSL-KDD)
  Process     : Preprocessing data (normalisasi, encoding) dan klasifikasi menggunakan algoritma ML (DT, RF, SVM)
  Output      : Prediksi apakah traffic normal atau intrusi
  Outcome     : Peningkatan akurasi dan efektivitas deteksi intrusi
  Constraints : Dataset lama (NSL-KDD), keterbatasan representasi serangan modern, keterbatasan resource komputasi
  Stakeholders: Administrator jaringan, organisasi/perusahaan, pengguna sistem

Fenomena → Problem
  Fenomena yang diamati             : Sistem deteksi intrusi berbasis ML menunjukkan akurasi tinggi (>95%)
  Gejala (symptom) yang terukur     : Nilai akurasi tinggi pada dataset uji (NSL-KDD)
  Masalah yang didiagnosis          : Dataset yang digunakan tidak representatif terhadap kondisi jaringan modern
  Masalah riset (researchable)      : Belum ada evaluasi komparatif performa model ML pada dataset lama vs dataset modern dalam mendeteksi intrusi jaringan
  Variabel yang terukur             : Akurasi, precision, recall, F1-score pada beberapa dataset (NSL-KDD vs dataset modern seperti CICIDS)

Problem Quality Check
  [✓] Clarity — Apakah satu orang membaca akan paham?
  [✓ ] Measurability — Apakah ada metrik kuantitatif?
  [✓ ] Relevance — Apakah penting untuk domain?
  [✓ ] Testability — Apakah bisa gagal?
  [✓ ] Impact — Apakah ada kontribusi jika terjawab?

Problem Statement (1 paragraf):
Meskipun berbagai model machine learning seperti Random Forest, Decision Tree, dan Support Vector Machine menunjukkan akurasi tinggi dalam deteksi intrusi jaringan, evaluasi tersebut umumnya dilakukan menggunakan dataset lama seperti NSL-KDD yang tidak merepresentasikan kondisi jaringan modern. Hal ini menimbulkan keraguan terhadap validitas eksternal dari hasil penelitian. Oleh karena itu, diperlukan studi komparatif untuk mengevaluasi performa model machine learning pada dataset lama dan dataset yang lebih representatif terhadap kondisi nyata, dengan menggunakan metrik kuantitatif seperti akurasi, precision, recall, dan F1-score, guna memastikan bahwa model yang diusulkan benar-benar efektif dalam lingkungan operasional.
```

---

## Latihan 1 — Dari Topik ke Masalah Riset

Pilih satu topik di bidang TI yang diminati. Transformasikan melalui 5 tahap Problem Formation Model.

**Topik awal:** Deteksi intrusi jaringan menggunakan machine learning

| Tahap | Hasil |
|-------|-------|
| Reality | Banyak organisasi menggunakan IDS berbasis machine learning untuk keamanan jaringan |
| Observed Issue (Symptom) | Model ML menunjukkan akurasi tinggi (>95%) pada dataset uji |
| Diagnosed Problem (Root Cause) |Dataset yang digunakan (NSL-KDD) tidak mencerminkan kondisi jaringan modern |
| Researchable Problem |Belum ada evaluasi performa model ML pada dataset lama vs dataset modern |
| Measurable Variable |Akurasi, precision, recall, F1-score pada beberapa dataset |

**Apakah terjebak solution-first thinking?** [ ] Ya / [✓ ] Tidak
> Jika ya, kembali ke tahap mana?
> Tidak relevan (tidak terjebak solution-first thinking)

---

## Latihan 2 — System Context Decomposition

Gambarkan konteks sistem dari masalah riset di Latihan 1.

| Komponen | Deskripsi |
|----------|----------|
| Input | Data lalu lintas jaringan (fitur koneksi, paket data) |
| Process |Preprocessing + klasifikasi menggunakan model ML |
| Output |Label: normal atau intrusi |
| Outcome |Sistem mampu mendeteksi serangan dengan akurasi tinggi |
| Constraints |Dataset lama, keterbatasan generalisasi, resource komputasi |
| Stakeholders |Admin jaringan, organisasi, pengguna |

**Komponen mana yang paling relevan dengan masalah riset?** Input (dataset)

Karena masalah utama ada di kualitas dataset → mempengaruhi hasil

## Latihan 3 — Problem Quality Check

Evaluasi problem statement yang sudah dibuat menggunakan 5 kriteria.

| Kriteria | Skor (1-5) | Justifikasi |
|----------|-----------|-------------|
| Clarity |5 |Masalah jelas dan spesifik |
| Measurability |5 |Menggunakan metrik kuantitatif |
| Relevance |5 |Sangat penting dalam keamanan jaringan |
| Testability |5 |Bisa diuji dengan eksperimen |
| Impact |5 |Berpengaruh pada validitas penelitian ML |

**Skor total:** 25 / 25

**Problem statement versi final (1 paragraf):**
> Meskipun berbagai model machine learning seperti Random Forest, Decision Tree, dan Support Vector Machine menunjukkan akurasi tinggi dalam deteksi intrusi jaringan, evaluasi tersebut umumnya dilakukan menggunakan dataset lama seperti NSL-KDD yang tidak merepresentasikan kondisi jaringan modern. Hal ini menimbulkan keraguan terhadap validitas eksternal dari hasil penelitian. Oleh karena itu, diperlukan studi komparatif untuk mengevaluasi performa model machine learning pada dataset lama dan dataset yang lebih representatif terhadap kondisi nyata, dengan menggunakan metrik kuantitatif seperti akurasi, precision, recall, dan F1-score, guna memastikan bahwa model yang diusulkan benar-benar efektif dalam lingkungan operasional.


---

## Refleksi

> Bandingkan "masalah" yang biasa ditemui saat coding (bug, error) dengan masalah riset. Apa perbedaan fundamental dalam cara mendefinisikan dan mendekati keduanya?

**Jawaban:**
> Masalah dalam coding biasanya bersifat teknis dan langsung terlihat, seperti error atau bug yang harus diperbaiki agar sistem dapat berjalan. Pendekatannya adalah mencari solusi secepat mungkin agar sistem berfungsi kembali.
> Sebaliknya, masalah dalam riset tidak selalu terlihat secara langsung dan sering kali berkaitan dengan gap dalam pengetahuan. Dalam riset, masalah tidak langsung diselesaikan begitu saja, tetapi perlu dipahami penyebabnya dan dibuktikan dengan pengujian yang jelas.
