# 🎬 Sistem Rekomendasi Film

Sistem rekomendasi film berbasis **content-based filtering** menggunakan TF-IDF dan Cosine Similarity, dibangun dari dataset IMDb Movies. Live demo dapat dicoba di Hugging Face Spaces:

🔗 **[Sistem-Rekomendasi-Film](https://huggingface.co/spaces/Axion28/Sistem-Rekomendasi-Film)**

## 📋 Deskripsi

Project ini membangun sistem rekomendasi film yang dapat:
1. **Merekomendasikan film berdasarkan genre**, diurutkan berdasarkan rating IMDb tertinggi
2. **Merekomendasikan film yang mirip** dengan sebuah judul film tertentu, berdasarkan kemiripan konten (genre, tahun rilis, dan deskripsi)

## 📊 Dataset

Dataset yang digunakan: [IMDb Movies Dataset](https://www.kaggle.com/datasets/amanbarthwal/imdb-movies-data) dari Kaggle.

Kolom yang dipakai setelah proses seleksi fitur:
| Kolom | Deskripsi |
|---|---|
| `Title` | Judul film |
| `Year` | Tahun rilis |
| `Rating` | Rating IMDb |
| `Genre` | Genre film |
| `Description` | Sinopsis/deskripsi film |

## 📁 Struktur File

```
.
├── RekomendasiFilm.ipynb      # Notebook eksplorasi data, preprocessing, dan pembuatan model
├── rekomendasi_film.pkl       # Model hasil training (df, cosine similarity matrix, indices)
└── app.py                     # Aplikasi Hugging Face Space (Gradio/Streamlit)
```

## ⚙️ Alur Kerja

### 1. Data Understanding
Eksplorasi awal dataset: dimensi data, tipe kolom, missing value, statistik rating, distribusi genre, dan jumlah film per tahun rilis.

### 2. Data Preparation
- Menghapus baris dengan `Genre` kosong
- Menghapus judul film duplikat
- Membersihkan whitespace pada judul
- Mengisi nilai kosong pada `Year` dan `Rating` dengan nilai rata-rata
- Memilih fitur relevan: `Title`, `Year`, `Rating`, `Genre`, `Description`

### 3. Modelling
- Menggabungkan `Genre`, `Year`, dan `Description` menjadi satu kolom teks (`combined_features`)
- Mengubah teks menjadi representasi numerik menggunakan **TF-IDF Vectorizer**
- Menghitung kemiripan antar film menggunakan **Cosine Similarity**
- Model (dataframe, matriks cosine similarity, dan index judul) disimpan ke `rekomendasi_film.pkl`

### 4. Fungsi Rekomendasi
- `get_top_anime_by_genre(genre_query, top_n=10)` → menampilkan film dengan genre tertentu, diurutkan berdasarkan rating tertinggi
- `recommend_similar_anime(title, top_n=5)` → menampilkan film yang paling mirip dengan judul film yang diberikan

## 🚀 Cara Menjalankan Secara Lokal

```bash
pip install pandas numpy scikit-learn matplotlib seaborn
jupyter notebook RekomendasiFilm.ipynb
```

Untuk menjalankan ulang seluruh proses, siapkan file `imdb-movies-dataset.csv` di direktori yang sama dengan notebook.

## 🌐 Demo

Aplikasi ini telah di-deploy dan dapat dicoba langsung di Hugging Face Spaces:

👉 **https://huggingface.co/spaces/Axion28/Sistem-Rekomendasi-Film**

## 📝 Catatan

- Pendekatan yang digunakan adalah **content-based filtering**, sehingga rekomendasi murni berdasarkan kemiripan konten film (genre, tahun, deskripsi), bukan berdasarkan preferensi/riwayat pengguna.
- Nilai kosong pada kolom numerik (`Year`, `Rating`) diisi menggunakan nilai rata-rata agar tidak mengurangi jumlah data secara signifikan.
