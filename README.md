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

2.  **Pembuatan Model (Arsitektur Sequential & Transfer Learning):**
    -   Membangun model menggunakan **`tf.keras.Sequential`** untuk memenuhi kriteria utama submission.
    -   Menggunakan **Transfer Learning** dengan `EfficientNetB0` (dengan bobot `imagenet` yang dibekukan) sebagai lapisan pertama untuk ekstraksi fitur yang kuat.
    -   Menambahkan **lapisan augmentasi data** (`RandomFlip`, `RandomRotation`, `RandomZoom`) langsung di dalam model `Sequential` untuk meningkatkan robustisitas.
    -   Menambahkan **lapisan kustom `Conv2D` dan `MaxPooling2D`** setelah `EfficientNetB0` sesuai dengan kriteria wajib.
    -   Mendesain *classifier head* yang terdiri dari lapisan `Flatten`, `Dense`, dan `Dropout` untuk melakukan klasifikasi akhir.

3.  **Pelatihan Model:**
    -   Melatih model pada lingkungan GPU untuk akselerasi.
    -   Menggunakan Callbacks canggih seperti `ModelCheckpoint` untuk menyimpan model terbaik, `EarlyStopping` untuk mencegah overfitting, serta `ReduceLROnPlateau` untuk menyesuaikan *learning rate* secara dinamis.

4.  **Evaluasi:**
    -   Mengevaluasi performa model pada data tes untuk mendapatkan metrik akurasi yang sebenarnya.
    -   Membuat visualisasi berupa plot histori akurasi/loss dan *Confusion Matrix* untuk analisis performa yang mendalam.

5.  **Deployment:**
    -   Membuat **model inferensi terpisah** (tanpa lapisan augmentasi) dengan memuat bobot dari model terbaik yang telah dilatih. Ini dilakukan untuk memastikan kompatibilitas dan efisiensi saat konversi.
    -   Mengekspor model inferensi ke dalam tiga format standar: **`SavedModel`**, **`TensorFlow Lite (.tflite)`**, dan **`TensorFlow.js`**.


---

## Hasil Akhir

Model berhasil mencapai performa yang sangat memuaskan dan memenuhi semua kriteria proyek.

-   **Akurasi Akhir pada Data Tes: 96.23%**

### Grafik Pelatihan Model
![Training History](https://res.cloudinary.com/dvb1yjl8g/image/upload/v1751007452/graph_pe2zoq.png)

### Confusion Matrix
![Confusion Matrix](https://res.cloudinary.com/dvb1yjl8g/image/upload/v1751007452/confusionpng_g4ynd7.png)

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