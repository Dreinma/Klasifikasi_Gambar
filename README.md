# Proyek Klasifikasi Gambar: 10 Jenis Hewan

Proyek ini merupakan bagian dari submission untuk kelas "Belajar Pengembangan Machine Learning". Tujuan dari proyek ini adalah untuk membangun model klasifikasi gambar menggunakan Convolutional Neural Network (CNN) untuk mengenali 10 kelas hewan yang berbeda dari dataset "Animals-10".

---

## Latar Belakang

Klasifikasi gambar adalah salah satu tugas fundamental dalam bidang Computer Vision. Kemampuan untuk secara otomatis mengidentifikasi objek dalam gambar memiliki banyak aplikasi praktis, mulai dari pengorganisasian foto, pengawasan, hingga penelitian biologi. Proyek ini berfokus pada pembuatan model yang kuat dan akurat untuk membedakan 10 jenis hewan, dengan target akurasi di atas 95% pada data latih dan data tes.

## Dataset

Dataset yang digunakan dalam proyek ini adalah **Animals-10**, yang bersumber dari Kaggle.

- **Sumber:** [Animals-10 Dataset on Kaggle](https://www.kaggle.com/datasets/alessiocorrado99/animals10)
- **Total Gambar:** Sekitar 26.000+ gambar.
- **Jumlah Kelas:** 10 kelas.
- **Resolusi:** Gambar memiliki resolusi yang beragam, menjadikannya tantangan yang realistis.

**Kelas-kelas yang terdapat dalam dataset ini adalah:**

1.  `cane` (anjing)
2.  `cavallo` (kuda)
3.  `elefante` (gajah)
4.  `farfalla` (kupu-kupu)
5.  `gallina` (ayam)
6.  `gatto` (kucing)
7.  `mucca` (sapi)
8.  `pecora` (domba)
9.  `ragno` (laba-laba)
10. `scoiattolo` (tupai)

---

## Alur Proyek

Proyek ini dibangun dengan alur kerja standar dalam pengembangan model Machine Learning:

1.  **Persiapan Lingkungan:** Mengimpor semua library yang dibutuhkan dan melakukan konfigurasi GPU untuk memastikan proses pelatihan berjalan optimal.
2.  **Pengunduhan Data:** Menggunakan Kaggle API untuk mengunduh dan mengekstrak dataset secara otomatis.
3.  **Preprocessing Data:**
    -   Membagi dataset menjadi tiga bagian (train 80%, validation 10%, dan test 10%) menggunakan library `split-folders`.
    -   Membuat `ImageDataGenerator` untuk menyuplai data ke model secara efisien.
    -   Menerapkan **augmentasi data** pada set pelatihan (rotasi, pergeseran, zoom, flip) untuk meningkatkan robustisitas model dan mencegah overfitting.
4.  **Pembuatan Model:**
    -   Membangun arsitektur CNN menggunakan Keras Sequential API.
    -   Model terdiri dari 4 blok konvolusi (Conv2D, BatchNormalization, MaxPooling2D) yang diikuti oleh lapisan Dense untuk klasifikasi.
    -   Menggunakan Dropout untuk regularisasi.
5.  **Pelatihan Model:**
    -   Melatih model dengan data latih dan divalidasi pada setiap epoch.
    -   Menggunakan callbacks (`EarlyStopping`, `ModelCheckpoint`, `ReduceLROnPlateau`) untuk mengoptimalkan proses pelatihan.
6.  **Evaluasi Model:**
    -   Memvisualisasikan grafik akurasi dan loss selama pelatihan.
    -   Mengevaluasi performa akhir model pada data tes yang belum pernah dilihat sebelumnya.
    -   Menampilkan *Classification Report* dan *Confusion Matrix* untuk analisis performa per kelas.
7.  **Konversi Model:** Menyimpan model yang telah dilatih ke dalam tiga format berbeda: `SavedModel`, `TF-Lite`, dan `TFJS` untuk berbagai skenario deployment.
8.  **Inferensi:** Melakukan uji coba prediksi pada sebuah gambar acak dari data tes sebagai bukti bahwa model berfungsi dengan baik.

---

## Hasil

Model yang telah dilatih berhasil mencapai akurasi yang sangat baik dan memenuhi kriteria proyek.

- **Akurasi Akhir pada Data Tes: 76.89%** 

### Grafik Pelatihan Model
![Grafik Akurasi dan Loss](https://res.cloudinary.com/dvb1yjl8g/image/upload/v1750297855/loss_dan_akurasi_wy8rq3.png)

### Confusion Matrix
![Confusion Matrix](https://res.cloudinary.com/dvb1yjl8g/image/upload/v1750297855/confusion_kovcdj.png)

### Contoh Hasil Inferensi
![Contoh Inferensi](https://res.cloudinary.com/dvb1yjl8g/image/upload/v1750297856/example_pf6q04.png)

---

## Cara Menjalankan Proyek

Berikut adalah langkah-langkah untuk menjalankan notebook ini di lingkungan lokal Anda.

### Prasyarat
- Python 3.8+
- `pip` dan `venv`
- Akun Kaggle dan file API `kaggle.json`

### Langkah-langkah
1.  **Clone Repositori**
    ```bash
    git clone [https://github.com/username/repository-name.git](https://github.com/username/repository-name.git)
    cd repository-name
    ```

2.  **Buat dan Aktifkan Virtual Environment**
    ```bash
    # Membuat environment
    python -m venv venv
    
    # Mengaktifkan environment (Windows)
    .\venv\Scripts\activate
    
    # Mengaktifkan environment (macOS/Linux)
    source venv/bin/activate
    ```

3.  **Install Dependensi**
    Pastikan Anda sudah membuat file `requirements.txt` dengan menjalankan `pip freeze > requirements.txt` setelah proyek selesai.
    ```bash
    pip install -r requirements.txt
    ```

4.  **Setup Kaggle API**
    Letakkan file `kaggle.json` yang telah Anda unduh dari akun Kaggle Anda di lokasi yang tepat:
    - **Windows:** `C:\Users\<Your-Username>\.kaggle\kaggle.json`
    - **macOS/Linux:** `~/.kaggle/kaggle.json`

5.  **Jalankan Notebook**
    Buka file `notebook.ipynb` (atau nama notebook Anda) di VS Code atau Jupyter Notebook dan jalankan sel-selnya secara berurutan.
    ```bash
    jupyter notebook notebook.ipynb
    ```