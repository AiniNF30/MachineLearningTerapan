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

Model machine learning yang digunakan pada sistem rekomendasi ini adalah model content-based filtering dengan simlarty measure yang digunakan adalah Cosine Similarity.

Model content-based filtering ini bekerja dengan mempelajari profil minat pengguna baru berdasarkan data dari objek yang telah dinilai pengguna. Metode ini bekerja dengan menyarankan item serupa yang pernah disukai sebelumnya atau sedang dilihat sekarang kepada pengguna berdasrakan kategori tertentu dari item yang dinilai oleh pengguna dengan menggunakan similarity tertentu.

Sedangkan cosine similarity adalah salah satu teknik mengukur kesamaan yang bekerja dengan mengukur kesamaan antara dua vektor dan menentukan apakah kedua vektor tersebut menunjuk ke arah yang sama dengan menghitung sudut cosinus antara dua vektor. Semakin kecil sudut cosinus, semakin besar nilai cosine similarity.

untuk memperoleh rekomendasi destinasi wisata , gunakan fungsi model.predict() dari library Keras dengan menerapkan kode berikut.
ini adalah 10 rekomendasi wisata 

<img width="1158" alt="Screenshot 2023-02-27 at 18 17 44" src="https://user-images.githubusercontent.com/90955264/221550217-1181e1e2-eeba-4319-bd21-74f14eb6ccc9.png">

Model machine learning yang digunakan pada sistem rekomendasi ini adalah model content-based filtering dengan similarity measure yang digunakan adalah Cosine Similarity.

#### collaborative filtering.
<img width="429" alt="Screenshot 2023-02-27 at 21 06 11" src="https://user-images.githubusercontent.com/90955264/221584699-4a94bd88-ead7-4709-8152-0863b5bcfa73.png">

Pertama-tama, data wisata dan data rating digabungkan menjadi satu data frame dengan menggunakan fungsi merge pada library pandas. Setelah itu, dilakukan proses pembuatan model content-based filtering dengan Cosine Similarity dengan menghitung similarity antara data wisata dengan data rating yang dimiliki oleh user.

<img width="746" alt="Screenshot 2023-02-27 at 18 08 59" src="https://user-images.githubusercontent.com/90955264/221548466-94823d54-3a34-4889-b111-ade89cd5f91b.png">


Pada proses di atas, dilakukan proses pembuatan user-item matrix yang akan digunakan sebagai acuan dalam proses rekomendasi. Kemudian, NaN values pada user-item matrix diubah menjadi 0. Selanjutnya, dilakukan perhitungan Cosine Similarity matrix antara data wisata dan data rating yang dimiliki oleh user.

Setelah mendapatkan Cosine Similarity matrix, langkah selanjutnya adalah membuat fungsi untuk melakukan proses rekomendasi berdasarkan input dari user. Pada sistem rekomendasi ini, fungsi rekomendasi yang dibuat akan menghasilkan 5 rekomendasi wisata yang paling sesuai dengan preferensi yang dimiliki oleh user.

<img width="1246" alt="Screenshot 2023-02-27 at 17 08 51" src="https://user-images.githubusercontent.com/90955264/221535037-7f77527e-c04e-47b1-998b-7c03b7120435.png">

Pada fungsi rekomendasi di atas, dilakukan proses pencarian similarity scores antara user yang sedang login dengan user lainnya pada Cosine Similarity matrix. Kemudian, similarity scores diurutkan dari yang terbesar hingga terkecil, dan diambil 5 user dengan similarity scores terbesar sel.

## Evaluation

Dalam proses evaluasi, akan disajikan informasi mengenai perbandingan mengenai model pertama dan kedua melalui dua metrik berikut:

Loss (Mean Squared Error Loss)
Mean Squared Erorr Loss berfungsi untuk menghitung rata-rata kuadrat kesalahan antara label dan prediksi. Dengan demikian semakin rendahnya nilai loss (mean squared error loss) maka semakin baik dan akurat model yang dibuat. Berikut adalah hasil perbandingan loss dan val_loss pada kedua model yang telah dibuat.

#### Precision Content Based Filtering
Metric yang digunakan pada sistem rekomendasi wisata dengan menggunakan accuracy precision. Precision adalah metrik yang membandingkan rasio prediksi benar atau positif dengan keseluruhan hasil yang diprediksi positif dengan rumus.

<img width="509" alt="Screenshot 2023-02-27 at 17 19 02" src="https://user-images.githubusercontent.com/90955264/221537298-0bba8751-d3dd-49ef-8387-f9a533a313d9.png">


<img width="821" alt="Screenshot 2023-02-27 at 20 58 22" src="https://user-images.githubusercontent.com/90955264/221583000-96c6adec-8baf-4e0e-9258-7d4a4c8b1e75.png">

Dari hasil rekomendasi di atas, diketahui bahwa Wisata Trans Studio bandung termasuk ke dalam kota Bandung. Dari 5 item yang direkomendasikan, 5 item memiliki kategori American (similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.

<img width="807" alt="Screenshot 2023-02-27 at 20 58 28" src="https://user-images.githubusercontent.com/90955264/221583030-a45e8b9b-a829-4264-9d4f-deb623029ae4.png">

Dari hasil rekomendasi di atas, diketahui bahwa Wisata Air Mancur Menari termasuk ke dalam kota Surabaya.  Dari 5 item yang direkomendasikan, 5 item memiliki kategori Surabaya(similar). Artinya, precision sistem kita sebesar 5/5 atau 100%.

