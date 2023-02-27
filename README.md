# Machine Learning Terapan - Aini Nurpadilah

## Domain Proyek

![wisata](https://user-images.githubusercontent.com/90955264/221451450-1fa788f7-e846-4d6a-9be9-7188153083e2.png)

informasi tentang kunjungan wisatawan ke beberapa destinasi wisata utama di Indonesia. Dataset ini dikumpulkan oleh Kementerian Pariwisata dan Ekonomi Kreatif Indonesia, dan kemudian dibagikan di platform Kaggle untuk digunakan oleh para pengembang data dan ilmuwan.

Latar belakang dari proyek ini adalah untuk memberikan informasi tentang tren kunjungan wisatawan ke Indonesia, khususnya ke beberapa destinasi wisata utama di negara ini. Data ini meliputi jumlah kunjungan wisatawan ke berbagai destinasi wisata di Indonesia, asal negara pengunjung, jenis wisata yang dilakukan, serta jumlah pengeluaran wisatawan selama berkunjung di Indonesia. Informasi ini dapat membantu pengembang pariwisata dan pemerintah dalam merencanakan pengembangan pariwisata di Indonesia serta meningkatkan pelayanan bagi para wisatawan.


## Business Understanding

### Problem Statements
* Destinasi wisata mana yang paling banyak dikunjungi oleh wisatawan di Indonesia?
* Apa jenis wisata yang paling diminati oleh wisatawan di Indonesia?
* Bagaimana tren kunjungan wisatawan ke Indonesia dalam beberapa tahun terakhir?

### Goals
Tujuan utamanya adalah :
* Menganalisis tren kunjungan wisatawan ke Indonesia dan meningkatkan pengembangan pariwisata di Indonesia.

### Solution Statement.
Beberapa langkah yang dapat dilakukan dalam proses analisis data adalah:

  1. Melakukan eksplorasi data dan cleaning data untuk memastikan kualitas dan  integritas data.
  2. Melakukan analisis deskriptif untuk mengetahui distribusi data dan     karakteristik setiap variabel dalam dataset.
  3. Melakukan analisis korelasi untuk mengetahui hubungan antara variabel-variabel dalam dataset.
  4. Melakukan analisis sentimen terhadap data rating pengunjung terhadap tempat wisata.
  5. Membuat model rekomendasi tempat wisata berdasarkan data user dan rating pengunjung.


## Data Undestanding
Dataset yang digunakan adalah [Indonesia Tourism Destination](https://www.kaggle.com/datasets/aprabowo/indonesia-tourism-destination)
Dataset ini merupakan dataset yang memuat beberapa tempat wisata di 5 kota besar di Indonesia yaitu Jakarta, Yogyakarta, Semarang, Bandung, Surabaya. 
Dataset Kaggle "Indonesia Tourism Destination" terdiri dari tiga file data, yaitu:

#### tourism__with__id.csv

  - Place_Id: id unik untuk setiap tempat wisata
  - Place_Name: nama tempat wisata
  - Description: deskripsi singkat tentang tempat wisata
  - Category: kategori tempat wisata (misalnya wisata alam, wisata sejarah,    wisata budaya)
  - City: kota tempat wisata tersebut berada
  - Price: harga tiket masuk ke tempat wisata dalam rupiah
  - Rating: rating tempat wisata dalam skala 1-5
  - Time_Minutes: waktu yang diperlukan untuk mengunjungi tempat wisata dalam menit
  - Coordinate: koordinat tempat wisata dalam format latitude dan longitude
  - Lat: nilai latitude tempat wisata
  
#### user.csv

File ini berisi data dummy pengguna yang akan digunakan untuk membuat fitur rekomendasi berdasarkan pengguna. Terdapat 3 variabel dalam file ini, yaitu:

  - User_Id: id unik untuk setiap pengguna
  - Location: kota asal pengguna
  - Age: usia pengguna
  - tourism_rating.csv

File ini berisi informasi tentang rating yang diberikan oleh pengguna pada setiap tempat wisata yang dikunjungi. Terdapat 3 variabel dalam file ini, yaitu:

  - User_Id: id unik untuk setiap pengguna
  - Place_Id: id unik untuk setiap tempat wisata
  - Place_Ratings: rating yang diberikan oleh pengguna pada tempat wisata tersebut dalam skala 1-5


## Data Preparation
Teknik yang digunakan pada tahapan Data Preparation adalah vektorisasi fungsi CountVectorizer dari library scikit-learn. CountVectorizer digunakan untuk mengubah teks yang diberikan menjadi vektor berdasarkan frekuensi (jumlah) setiap kata yang muncul di seluruh teks.

CountVectorizer membuat matriks di mana setiap kata unik diwakili oleh kolom matriks, dan setiap sampel teks dari dokumen adalah baris dalam matriks. Nilai setiap sel tidak lain adalah jumlah kata dalam sampel teks tertentu.

Pada proses vektorisasi ini, digunakan metode sebagai berikut.

    1. fit metode berfungsi untuk melakukan perhitungan idf pada data
    2. get_feature berfungsi untuk melakukan mapping array dari fitur index integer ke fitur nama
    3. fit_transform berfungsi untuk mempelajari kosa kata dan Inverse Document Frequency (IDF) dengan memberikan nilai return berupa document-term matrix
    4. todense berfungsi untuk mengubah vektor tf-idf dalam bentuk matriks
    
## Modeling

#### content-based filtering

Model machine learning yang digunakan pada sistem rekomendasi ini adalah model content-based filtering dengan similarty measure yang digunakan adalah Cosine Similarity.

<img width="635" alt="Screenshot 2023-02-27 at 22 22 25" src="https://user-images.githubusercontent.com/90955264/221604668-0afc5047-9e90-4fc7-9f03-95449c5fdeca.png">

cosine similarity adalah salah satu teknik mengukur kesamaan yang bekerja dengan mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity.


untuk memperoleh rekomendasi destinasi wisata , gunakan fungsi model.predict() dari library Keras dengan menerapkan kode berikut.
ini adalah 10 rekomendasi wisata 

<img width="589" alt="Screenshot 2023-02-27 at 22 15 29" src="https://user-images.githubusercontent.com/90955264/221602747-9119b736-6f3e-4aa0-a049-aa86177c20f7.png">
 
#### Collaborative Based Filtering
Model ini memilki konsep merekomendasikan wisata berdasarkan rating yang diberikan pengunjung lain. Sebelum membuat model ini, data harus melalui proses Training terlebih dahulu. Sebelum malakukan training, data harus di bagi terlebih dahulu menjadi data training dan data validation, dengan skala perbandingan data adalah 80:20, dan menggunakan activation sigmoid. Namun sebelumnya, perlu memetakan (mapping) data user dan game menjadi satu value terlebih dahulu, kemudian membuat rating dalam skala 0 sampai 1 agar mudah dalam melakukan proses training. Setelah melakukan semua proses itu maka selanjutnya melakukan uji coba pada model

<img width="338" alt="Screenshot 2023-02-27 at 22 25 58" src="https://user-images.githubusercontent.com/90955264/221605617-dc9de48a-685e-493d-b940-38b23a08f699.png">


## Evaluation

#### Content based Filtering
Metric yang digunakan pada sistem rekomendasi wisata dengan menggunakan accuracy precision. Precision adalah metrik yang membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif dengan rumus.

<img width="821" alt="Screenshot 2023-02-27 at 20 58 22" src="https://user-images.githubusercontent.com/90955264/221583000-96c6adec-8baf-4e0e-9258-7d4a4c8b1e75.png">

Dari hasil rekomendasi di atas, diketahui bahwa Wisata Trans Studio bandung termasuk ke dalam kota Bandung. Dari 5 item yang direkomendasikan, 5 item memiliki kategori American (similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.

<img width="807" alt="Screenshot 2023-02-27 at 20 58 28" src="https://user-images.githubusercontent.com/90955264/221583030-a45e8b9b-a829-4264-9d4f-deb623029ae4.png">

Dari hasil rekomendasi di atas, diketahui bahwa Wisata Air Mancur Menari termasuk ke dalam kota Surabaya.  Dari 5 item yang direkomendasikan, 5 item memiliki kategori Surabaya(similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.

#### collaborative based Filtering

Pada Collaborative Based Filtering, saya memakai metrik evaluasi RMSE untuk mengevaluasi model saya. Mean Squared Erorr Loss berfungsi untuk menghitung rata-rata kuadrat kesalahan antara label dan prediksi. Dengan demikian semakin rendahnya nilai loss (mean squared error loss) maka semakin baik dan akurat model yang dibuat. Berikut adalah hasil perbandingan loss dan val_loss pada kedua model yang telah dibuat.

<img width="509" alt="Screenshot 2023-02-27 at 17 19 02" src="https://user-images.githubusercontent.com/90955264/221537298-0bba8751-d3dd-49ef-8387-f9a533a313d9.png">

Perhatikanlah, proses training model cukup smooth dan model konvergen pada epochs sekitar 100. Dari proses ini, kita memperoleh nilai error akhir sebesar sekitar 0.32 dan error pada data validasi sebesar 0.37. 

