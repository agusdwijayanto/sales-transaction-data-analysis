# 📊 Analisa & Cleaning Dataset Transaksi Penjualan

Proyek analisa data end-to-end menggunakan Python — mencakup data cleaning, integration, transformation, reduction (PCA), dan text processing (NLP) pada dataset transaksi penjualan berskala 5.000 baris.

![Python](https://img.shields.io/badge/Python-3.x-3776AB?logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-Data%20Analysis-150458?logo=pandas&logoColor=white)
![Scikit-learn](https://img.shields.io/badge/Scikit--learn-MinMaxScaler%20%7C%20PCA-F7931E?logo=scikitlearn&logoColor=white)
![NLTK](https://img.shields.io/badge/NLTK-Text%20Processing-green)
![Matplotlib](https://img.shields.io/badge/Matplotlib-Visualization-11557C)
![Jupyter](https://img.shields.io/badge/Jupyter-Notebook-F37626?logo=jupyter&logoColor=white)

---

## 📌 Tentang Proyek

Proyek ini merupakan studi kasus pengolahan data mentah (raw dataset) menjadi dataset yang bersih dan siap dianalisis, dengan alur kerja khas Big Data / Data Science pipeline:

**Import → Missing Value Analysis → Data Cleaning → Data Integration → Data Transformation → Data Reduction → Text Processing → Visualisasi**

Dataset berisi 5.000 transaksi penjualan lintas 5 kategori produk (Fashion, Gaming, Grocery, Otomotif, Elektronik), lengkap dengan ulasan pelanggan berbahasa Indonesia yang diproses menggunakan teknik NLP dasar.

---

## 🎯 Tujuan Analisa

- Membersihkan data yang mengandung *missing value* menggunakan strategi berbeda sesuai jenis kolom (mean, modus, dan string kustom)
- Membentuk fitur baru (*feature engineering*) yang lebih informatif untuk analisa bisnis
- Menyeragamkan skala data numerik dengan normalisasi
- Mereduksi dimensi data numerik menggunakan **PCA (Principal Component Analysis)**
- Mengekstrak insight dari teks ulasan pelanggan melalui **tokenizing, filtering, dan analisa bigram**
- Menyajikan seluruh temuan dalam bentuk visualisasi yang mudah dibaca

---

## 🗂️ Struktur Dataset

| Kolom | Tipe Data | Keterangan |
|---|---|---|
| `id` | int64 | ID unik transaksi |
| `nama` | object | Nama pelanggan |
| `kategori` | object | Kategori produk |
| `harga` | float64 | Harga satuan produk |
| `jumlah` | float64 | Jumlah barang dibeli |
| `rating` | float64 | Rating kepuasan pelanggan (1-5) |
| `tanggal_transaksi` | datetime | Waktu transaksi |
| `deskripsi` | object | Ulasan singkat pelanggan |

**Ukuran dataset:** 5.000 baris × 8 kolom

---

## 🔧 Alur Pengolahan Data

### 1. Import Dataset
Membaca dataset dengan `pandas` dan menampilkan struktur awal (`head()`, `info()`).

### 2. Missing Value Analysis
Mengidentifikasi kolom dengan data kosong: `rating` (843), `deskripsi` (819), `harga` & `jumlah` (100 masing-masing).

### 3. Data Cleaning
- Kolom numerik → diisi **mean**
- Kolom kategorikal → diisi **modus**
- Kolom deskripsi (teks bebas) → diisi string `"tidak ada deskripsi"`

### 4. Data Integration
Membentuk kolom turunan:
- `total_harga` = `harga` × `jumlah`
- `bulan_transaksi` diekstrak dari `tanggal_transaksi`

### 5. Data Transformation
- Normalisasi `harga` & `jumlah` dengan **MinMaxScaler** (skala 0–1)
- Klasifikasi `rating_label` (buruk / cukup / baik)

### 6. Data Reduction
Reduksi 3 fitur numerik (`harga`, `jumlah`, `rating`) menjadi 2 principal component (`PC1`, `PC2`) menggunakan **PCA**.

### 7. Text Processing
- Tokenizing ulasan pelanggan dengan `nltk.word_tokenize()`
- Filtering stopwords Bahasa Indonesia, tanda baca, dan token pendek (<3 karakter)

### 8. Visualisasi
- Distribusi transaksi per kategori & tren bulanan
- Perbandingan histogram harga sebelum/sesudah normalisasi
- Kata & bigram (pasangan kata) yang paling sering muncul dalam ulasan

---

## 💡 Insight Utama

- Sentimen pelanggan didominasi kepuasan — kata **"puas"** muncul **902 kali**, kata paling sering dalam seluruh ulasan.
- Namun keluhan terkait harga cukup signifikan — bigram **"harga terlalu"** dan **"terlalu mahal"** muncul **872 kali**, menunjukkan ini adalah satu frasa keluhan utuh, bukan kata acak.
- Kelima kategori produk terjual relatif merata (980–1.050 transaksi), dengan **Fashion** sedikit unggul sebagai kategori terlaris.
- Tren transaksi bulanan berfluktuasi antara 655–745 transaksi, tanpa pola musiman yang ekstrem dalam rentang data yang tersedia.
- Normalisasi MinMaxScaler terbukti hanya mengubah skala data, bukan bentuk distribusinya — dikonfirmasi lewat perbandingan histogram sebelum/sesudah.
- PC1 hasil PCA didominasi variasi kolom `harga`, karena skala nilainya (jutaan rupiah) jauh lebih besar dibanding `jumlah` dan `rating`.

---

## 🛠️ Tech Stack

| Kategori | Tools |
|---|---|
| Bahasa | Python 3 |
| Data Wrangling | Pandas, NumPy |
| Machine Learning | Scikit-learn (MinMaxScaler, PCA) |
| Natural Language Processing | NLTK |
| Visualisasi | Matplotlib, Seaborn |
| Environment | Jupyter Notebook |

---

## 📁 Struktur Repository

```
├── dataset_kasus_penjualan.csv     # Dataset mentah
├── analisa_dataset_penjualan.ipynb # Notebook analisa lengkap
└── README.md                       # Dokumentasi proyek
```

---

## ▶️ Cara Menjalankan

```bash
# 1. Clone repository
git clone https://github.com/username/nama-repo.git
cd nama-repo

# 2. Install dependencies
pip install pandas numpy scikit-learn nltk matplotlib seaborn jupyter

# 3. Jalankan notebook
jupyter notebook analisa_dataset_penjualan.ipynb
```

> **Catatan:** Saat pertama kali dijalankan, notebook akan otomatis mengunduh resource `nltk` (`punkt`) — pastikan perangkat terhubung ke internet.

---

## 👤 Author

**Agus Dwijayanto**
Mahasiswa Sistem Informasi — Universitas Pamulang

---

<div align="center">

*Proyek ini dibuat sebagai bagian dari eksplorasi pengolahan data & portofolio pribadi.*

</div>
