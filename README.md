# Proyek Klasifikasi Gambar: 10 Jenis Hewan

Proyek ini adalah submission untuk kelas "Belajar Pengembangan Machine Learning" di Dicoding. Tujuannya adalah membangun sebuah model klasifikasi gambar yang mampu mengenali 10 kelas hewan berbeda dengan akurasi tinggi, menggunakan arsitektur Convolutional Neural Network (CNN) dan teknik Transfer Learning.

- **Nama:** Bimoseno Kuma
- **Email:** kuma24@student.ub.ac.id
- **ID Dicoding:** kukuma

---

## Latar Belakang

Klasifikasi gambar merupakan salah satu domain fundamental dalam Computer Vision dengan aplikasi yang luas. Proyek ini bertujuan untuk menerapkan teknik-teknik modern dalam deep learning untuk membangun model yang robust dan akurat. Dengan memanfaatkan model pre-trained **EfficientNetB0** dan pipeline data yang efisien menggunakan `tf.data`, model ini berhasil melampaui target akurasi yang ditetapkan.

## Dataset

Dataset yang digunakan adalah **Animals-10** yang bersumber dari Kaggle. Dataset ini dipilih karena memiliki jumlah gambar yang besar, variasi yang cukup, dan resolusi yang tidak seragam, menjadikannya kasus studi yang baik untuk klasifikasi gambar di dunia nyata.

- **Sumber:** [Animals-10 Dataset on Kaggle](https://www.kaggle.com/datasets/alessiocorrado99/animals10)
- **Total Gambar:** 26,179 gambar.
- **Jumlah Kelas:** 10 kelas.
- **Daftar Kelas:** `cane` (anjing), `cavallo` (kuda), `elefante` (gajah), `farfalla` (kupu-kupu), `gallina` (ayam), `gatto` (kucing), `mucca` (sapi), `pecora` (domba), `ragno` (laba-laba), `scoiattolo` (tupai).

---

## Alur Proyek

Proyek ini mengikuti alur kerja machine learning yang sistematis:

1.  **Persiapan Data:**
    -   Mengunduh dataset dari Kaggle menggunakan Kaggle API.
    -   Membagi dataset menjadi tiga set (train 80%, validation 10%, test 10%) menggunakan `split-folders`.
    -   Membangun pipeline data yang sangat efisien menggunakan `tf.keras.utils.image_dataset_from_directory` dan `tf.data` API, yang mencakup `.cache()` dan `.prefetch()` untuk performa maksimal.

2.  **Pembuatan Model (Transfer Learning):**
    -   Menggunakan arsitektur **Transfer Learning** dengan `EfficientNetB0` sebagai *base model* yang bobotnya dibekukan (`trainable=False`).
    -   Menambahkan lapisan augmentasi data (`RandomFlip`, `RandomRotation`, `RandomZoom`) sebagai bagian dari model untuk membuat model lebih tangguh terhadap variasi gambar.
    -   Menambahkan *classifier head* baru yang terdiri dari `GlobalAveragePooling2D`, `Dense`, dan `Dropout` di atas *base model*.
    -   Menggunakan `sparse_categorical_crossentropy` sebagai fungsi loss yang sesuai dengan output label dari pipeline `tf.data`.

3.  **Pelatihan Model:**
    -   Melatih model pada lingkungan GPU untuk akselerasi.
    -   Menggunakan Callbacks canggih seperti `ModelCheckpoint` untuk menyimpan model terbaik, `EarlyStopping` untuk mencegah overfitting dan menghemat waktu, serta `ReduceLROnPlateau` untuk menyesuaikan *learning rate* secara dinamis.

4.  **Evaluasi:**
    -   Mengevaluasi performa model pada data tes yang belum pernah dilihat untuk mendapatkan metrik akurasi yang sebenarnya.
    * Membuat visualisasi berupa plot histori akurasi/loss dan *Confusion Matrix* untuk analisis performa yang mendalam.

5.  **Deployment:**
    -   Membuat model inferensi terpisah (tanpa lapisan augmentasi) untuk memastikan kompatibilitas dan efisiensi.
    -   Mengekspor model yang telah divalidasi ke dalam tiga format standar: **`SavedModel`**, **`TensorFlow Lite (.tflite)`**, dan **`TensorFlow.js`**.

---

## Hasil Akhir

Model berhasil mencapai performa yang sangat memuaskan dan memenuhi semua kriteria proyek.

-   **Akurasi Akhir pada Data Tes: 96.23%**

### Grafik Pelatihan Model
![Training History](https://res.cloudinary.com/dvb1yjl8g/image/upload/v1750940147/graph_m0fxpg.png)

### Confusion Matrix
![Confusion Matrix](https://res.cloudinary.com/dvb1yjl8g/image/upload/v1750940146/confusionpng_p65op6.png)

---

## Struktur Direktori Submission

Berikut adalah struktur direktori akhir dari proyek
```
Klasifikasi_Gambar/
├── saved_model/
│   ├── saved_model.pb
│   └── variables/
├── tflite/
│   ├── model.tflite
│   └── label.txt
├── tfjs_model/
│   ├── model.json
│   └── group1-shard... .bin
├── notebook.ipynb
├── README.md
└── requirements.txt
```
---

## Cara Menjalankan Proyek

Untuk menjalankan notebook ini dan mereplikasi hasilnya, ikuti langkah-langkah berikut:

1.  **Prasyarat:**
    -   Akun Google dengan akses ke Google Colab.
    -   Akun Kaggle untuk mengunduh file API `kaggle.json`.

2.  **Setup Lingkungan:**
    -   Buka file `notebook.ipynb` di Google Colab.
    -   Pastikan Anda memilih **GPU runtime** (`Runtime > Change runtime type > T4 GPU`).

3.  **Menjalankan Notebook:**
    -   Saat pertama kali dijalankan, notebook akan meminta Anda untuk mengunggah file `kaggle.json`. Lakukan ini untuk mengizinkan Colab mengunduh dataset.
    -   Jalankan semua sel secara berurutan dari atas ke bawah. Proses pelatihan akan memakan waktu beberapa saat, dan semua hasil, termasuk model yang diekspor, akan disimpan di direktori `/content/` di dalam sesi Colab.