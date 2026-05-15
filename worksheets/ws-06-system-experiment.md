# WS-06: System-Experiment Mapping

> **Bab 6 — System Design sebagai Experimental Artifact**

---

## Ringkasan Materi

### Sistem = Instrumen Pengujian, Bukan Produk

Seorang engineer bertanya "apakah sistem bekerja?" — seorang peneliti bertanya "apa yang bisa dibuktikan sistem ini?" Sistem dalam riset adalah **artifact** — objek yang sengaja dibuat untuk menguji klaim spesifik.

### System as Experiment Model

```
RQ → Variable → System Component → Experimental Setup → Output
```

Setiap komponen sistem harus bisa ditelusuri ke variabel riset (top-down), dan setiap pengukuran harus menjawab RQ (bottom-up).

### Mapping Variabel ke Komponen

| Tipe Variabel | Peran di Sistem | Contoh |
|---------------|----------------|--------|
| **IV** (Independent) | Modul yang bisa di-toggle/swap | Algoritma A vs B |
| **DV** (Dependent) | Modul pengukuran | Logger, metrics collector |
| **CV** (Control) | Config yang dikunci | Dataset, parameter tetap |

Jika variabel tidak bisa di-map ke komponen apapun → arsitektur perlu didesain ulang.

### 4 Prinsip Desain Eksperimental

| Prinsip | Pertanyaan Kunci |
|---------|-----------------|
| **Traceability** | Komponen ini melayani variabel yang mana? |
| **Modularity** | Bisakah IV diubah tanpa memengaruhi yang lain? |
| **Controllability** | Apakah CV dieksternalisasi ke config file? |
| **Measurability** | Apakah sistem otomatis menghasilkan data yang dibutuhkan? |

### Variable Isolation melalui Arsitektur

- **Modular architecture** — Pisahkan berdasarkan variabel
- **Configuration-driven** — Ubah config (YAML/JSON), bukan code
- **Feature toggles** — On/off flag untuk ablation study

  Contoh config YAML dengan feature toggles:
  ```yaml
  model:
    type: cnn          # IV: ganti "rf" untuk kondisi baseline
  features:
    use_temporal: true  # toggle komponen temporal
    use_normalization: true  # toggle preprocessing
  experiment:
    seed: 42
    runs: 5
  ```
  Dengan pendekatan ini, berbeda kondisi eksperimen = berbeda satu baris config, **tanpa mengubah kode**.

### Research vs Engineering

| Aspek | Engineering | Research |
|-------|------------|----------|
| Tujuan sistem | Memenuhi kebutuhan user | Menguji hipotesis, menghasilkan bukti |
| Arsitektur | Optimasi performa & skalabilitas | Optimasi isolasi variabel & reprodusibilitas |
| Konfigurasi | Sering hardcoded | Dieksternalisasi ke config file |
| Fitur tambahan | Menambah nilai user | Menambah noise jika tidak terkait RQ |

### Istilah Penting

- **Artifact** — Objek yang sengaja dibuat untuk memecahkan masalah atau menguji proposisi
- **Traceability** — Kemampuan menelusuri hubungan RQ → variabel → komponen → output
- **Variable Isolation** — Mengubah hanya satu variabel sambil menahan yang lain konstan
- **Ablation Study** — Menguji kontribusi tiap komponen dengan melepasnya satu per satu
- **Configuration-driven Execution** — Semua parameter di config file, bukan hardcoded

---

## Template A.6 — Mapping RQ ke Arsitektur Sistem

```
SYSTEM-EXPERIMENT MAPPING

Research Question: Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD?

Variable → Component Mapping:
| Variabel | Tipe | Komponen Sistem | Cara Manipulasi/Pengukuran |
|----------|------|-----------------|---------------------------|
|Jenis algoritma machine learning          | IV   | Modul classifier (RF, DT, SVM)                 |Mengganti algoritma yang digunakan saat pelatihan model                           |
|Performa deteksi intrusi          | DV   |Modul evaluasi dan metrics collector                 |Mengukur akurasi, presisi, recall, F1-Score, dan AUC                           |
|Dataset NSL-KDD          | CV   |Modul dataset dan preprocessing                 |Menggunakan dataset dan pembagian data yang sama pada setiap eksperimen                           |

4 Prinsip Desain:
  [✓ ] Traceability — Setiap komponen bisa ditelusuri ke variabel
  [✓ ] Variable Isolation — IV bisa diubah tanpa mengubah CV
  [✓ ] Measurement Integration — Pengukuran DV built-in
  [✓ ] Reproducibility — Setup bisa direkonstruksi

Experimental Setup:
  Input data     : Dataset NSL-KDD
  Parameter      : Pembagian data 70:30, cross-validation, dan hyperparameter tuning
  Output format  : Akurasi, presisi, recall, F1-Score, dan AUC
```

---

## Latihan 1 — Variable-to-Component Mapping

Gunakan RQ dan variabel dari WS-05. Petakan ke komponen sistem.

**RQ:** Apakah Random Forest menghasilkan performa deteksi intrusi yang lebih baik dibandingkan Decision Tree dan SVM pada dataset NSL-KDD?

| Variabel | Tipe | Komponen Sistem | Cara Manipulasi / Pengukuran |
|----------|------|-----------------|---------------------------|
| jenis algoritma machine learning | IV | Modul classifier | Mengganti algoritma RF, DT, dan SVM |
|Performa model | DV |Modul evaluasi |Mengukur akurasi, presisi, recall, dan F1-Score |
|Dataset NSL-KDD | CV |Modul preprocessing dan dataset |Menggunakan data training dan testing yang sama |

**Apakah semua variabel bisa di-map?** [✓ ] Ya 
> Jika tidak, komponen apa yang perlu ditambahkan? Tidak ada, karena semua variabel sudah memiliki komponen sistem yang sesuai.

---

## Latihan 2 — 4 Prinsip Desain

Evaluasi desain sistem terhadap 4 prinsip.

| Prinsip | Status | Bukti / Penjelasan |
|---------|--------|-------------------|
| Traceability | ✅ |Setiap variabel penelitian memiliki komponen sistem yang jelas |
| Modularity |✅ |Algoritma dapat diganti tanpa mengubah proses preprocessing |
| Controllability |✅ |Dataset dan parameter pengujian dibuat tetap pada setiap eksperimen |
| Measurability |✅ |Sistem menghasilkan metrik evaluasi secara otomatis |

**Prinsip mana yang paling sulit dipenuhi?** Modularity
**Strategi untuk mengatasinya:**
> Sistem dibuat dalam bentuk modul terpisah antara preprocessing, dataset, dan classifier sehingga perubahan algoritma tidak memengaruhi bagian lain pada sistem.

---

## Latihan 3 — Ablation Study Planning

Jika sistem memiliki 3 komponen utama, rencanakan ablation study.

> **Panduan jumlah kondisi:** Untuk 3 komponen (A, B, C), kondisi minimal yang direkomendasikan:
> Full + (-A) + (-B) + (-C) = **4 kondisi dasar**. Jika waktu memungkinkan, tambahkan kombinasi ganda: (-A,-B), (-A,-C), (-B,-C) = **7 kondisi**. Sesuaikan dengan *computational cost* dan tenggat waktu penelitian.

| Kondisi | Komponen A | Komponen B | Komponen C | Hasil yang Diharapkan |
|---------|-----------|-----------|-----------|----------------------|
| Full | ✅ Random Forest | ✅ Normalisasi data | ✅ Feature encoding | Hasil performa terbaik |
| – A | ❌ (ganti DT/SVM) | ✅ | ✅ |Akurasi diperkirakan menurun |
| – B | ✅ | ❌ (tanpa normalisasi) | ✅ |Performa model menjadi kurang stabil |
| – C | ✅ | ✅ | ❌ (tanpa encoding fitur) |Model sulit memproses data kategorikal |

**Komponen mana yang diprediksi paling berkontribusi?** Random Forest
**Mengapa?**
> Random Forest diperkirakan memberi kontribusi paling besar karena pada hasil penelitian algoritma ini memiliki akurasi dan nilai evaluasi tertinggi dibandingkan Decision Tree dan SVM.

---

## Refleksi

> Apa risiko jika sistem dibangun seperti produk (monolitik, fitur lengkap) lalu baru dilakukan eksperimen? Mengapa arsitektur modular penting untuk riset?

**Jawaban:**
> Jika sistem dibuat seperti produk yang terlalu kompleks, proses eksperimen akan menjadi lebih sulit karena banyak komponen saling terhubung. Akibatnya, peneliti akan kesulitan mengetahui bagian mana yang benar-benar memengaruhi hasil penelitian.
> Arsitektur modular penting dalam riset karena setiap komponen dapat diuji atau diganti secara terpisah tanpa mengubah keseluruhan sistem. Dengan cara ini, proses pengujian menjadi lebih jelas, mudah diulang, dan hasil penelitian lebih mudah dianalisis.
