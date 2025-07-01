Langkah Pengerjaan Proyek

Proyek ini bertujuan untuk memprediksi penutupan saham MNC Bank dengan pendekatan machine learning, khususnya menggunakan algoritma **Linear Regression** dan **K-Nearest Neighbors (KNN)**. Proyek ini dibangun melalui beberapa tahapan utama berikut:

### 1. Business Understanding
Tahap pertama adalah memahami konteks bisnis dan permasalahan yang ingin diselesaikan. Dalam proyek ini, fokus utamanya adalah **memprediksi harga penutupan saham** yang dapat digunakan untuk membantu investor, analis keuangan, atau pihak internal bank dalam mengambil keputusan.
Permasalahan nyata di pasar saham adalah bagaimana memanfaatkan data historis saham untuk memprediksi harga di masa mendatang. Oleh karena itu, proyek ini bertujuan:
- Untuk mengevaluasi performa model AI dalam prediksi harga saham,
- Untuk membandingkan dua pendekatan algoritmik (regresi vs klasifikasi),
- Dan untuk mengidentifikasi model mana yang paling sesuai digunakan dalam kasus ini.

### 2. Data Understanding
Dataset yang digunakan merupakan data historis saham MNC Bank yang terdiri dari fitur:
- **Open**: Harga pembukaan saham
- **High**: Harga tertinggi dalam satu hari
- **Low**: Harga terendah dalam satu hari
- **Close**: Harga penutupan
- **Volume**: Jumlah volume transaksi
Selain itu, dibuat juga fitur tambahan `Label` berupa nilai biner (0 = turun, 1 = naik) sebagai target klasifikasi untuk KNN. Proses analisis awal dilakukan untuk memahami distribusi nilai, hubungan antar fitur, serta melihat pola umum pada data.

### 4. Exploratory Data Analysis (EDA)
Dilakukan eksplorasi terhadap data untuk memahami distribusi, pola, serta kemungkinan anomali pada dataset. Tahapan EDA mencakup:
- **Statistik deskriptif awal**, seperti nilai rata-rata, minimum, maksimum, dan standar deviasi dari masing-masing fitur (Open, High, Low, Close, Volume).
- **Visualisasi distribusi fitur**, misalnya menggunakan histogram atau boxplot untuk melihat apakah ada outlier atau nilai ekstrem yang tidak wajar.
- **Heatmap korelasi**, untuk melihat hubungan antara fitur numerik, terutama sejauh mana `Close` dipengaruhi oleh `Open`, `High`, `Low`, dan `Volume`.
- **Pemeriksaan missing value**, meskipun dalam dataset ini tidak ditemukan nilai kosong, tahap ini tetap dilakukan untuk memastikan kualitas data.
- **Distribusi kelas pada target `Label`**, dilakukan untuk mengetahui apakah data balance (seimbang) antara label naik (1) dan turun (0). Jika tidak seimbang, hal ini dapat mempengaruhi performa model klasifikasi.
EDA membantu menentukan strategi praproses dan pemilihan fitur yang tepat, serta memberi insight awal terhadap perilaku data historis saham.

### 3. Data Preparation
Tahap ini mencakup beberapa proses sebagai berikut:
- **Seleksi Fitur**: Menghapus kolom yang tidak diperlukan dan memilih fitur yang berpengaruh terhadap target.
- **Encoding Label**: Menambahkan kolom `Label` dengan menggunakan logika sederhana apakah harga penutupan naik dibanding hari sebelumnya.
- **Pembagian Data**: Dataset dibagi menjadi data latih dan data uji menggunakan `train_test_split` dari Scikit-Learn dengan proporsi 80:20.
- **Normalisasi (opsional)**: Model Linear Regression tidak wajib dinormalisasi, tetapi bisa digunakan pada model lain.
Tujuannya adalah menyiapkan data agar siap dimasukkan ke dalam model machine learning.

### 4. Modeling
Proses ini mencakup pembangunan dan pelatihan dua model:
- **Linear Regression**
  - Digunakan untuk memprediksi harga penutupan secara langsung.
  - Model dilatih menggunakan fitur numerik (Open, High, Low, Volume).
  - Hasil output berupa nilai prediksi `Close` (berbasis regresi).
- **K-Nearest Neighbors (KNN)**
  - Digunakan untuk klasifikasi arah harga (naik atau turun).
  - Target yang digunakan adalah kolom `Label`.
  - Model memprediksi kelas 0 atau 1 berdasarkan nilai K tetangga terdekat.
Proses pelatihan dan prediksi dilakukan untuk masing-masing model secara terpisah.

### 5. Evaluation
Evaluasi model dilakukan untuk mengukur performa masing-masing pendekatan. Dua kategori evaluasi dilakukan:
- **Evaluasi Regresi (Linear Regression)**
  - Hasil prediksi `Close` dibandingkan dengan nilai aktual.
  - Divisualisasikan menggunakan grafik *Actual vs Predicted*.
  - Dihitung metrik akurasi secara tidak langsung melalui konversi nilai ke label (naik/turun).
- **Evaluasi Klasifikasi (KNN)**
  - Menggunakan metrik:
    - **Accuracy**
    - **Precision**
    - **Recall**
    - **F1-score**
  - Ditampilkan juga **confusion matrix** dalam bentuk teks dan visualisasi heatmap.
Hasil evaluasi menunjukkan bahwa model Linear Regression memiliki performa yang lebih baik (akurasi 71.24%) dibanding KNN (akurasi 43.01%).

### 6. Kesimpulan dan Rekomendasi
Dari hasil modeling dan evaluasi, diperoleh kesimpulan bahwa **Linear Regression lebih cocok digunakan** dalam konteks dataset ini dibandingkan KNN. Hal ini dapat disebabkan oleh pola hubungan antar fitur yang cenderung linier, sehingga pendekatan regresi mampu menangkap tren lebih baik dibanding klasifikasi berbasis jarak.
Adapun rekomendasi pengembangan lanjutan adalah:
- Meningkatkan jumlah data historis (lebih panjang dan lebih luas),
- Menambahkan fitur teknikal seperti Moving Average, RSI, dll,
- Mencoba model lain seperti Random Forest, XGBoost, atau LSTM,
- Dan melakukan tuning parameter pada setiap algoritma.


