# Laporan Proyek Machine Learning - Azel Fabian Azmi

Proyek ini bertujuan untuk membangun sistem rekomendasi laptop berbasis konten (content-based filtering) dengan memanfaatkan data spesifikasi seperti prosesor, RAM, harga, dan penyimpanan Sistem ini diharapkan mampu memberikan rekomendasi laptop yang sesuai dengan kebutuhan pengguna berdasarkan kemiripan spesifikasi.

---

## Project Domain

Konsumen dihadapkan dengan banyak pilihan saat ingin membeli laptop. Permasalahan muncul ketika calon pembeli tidak mengetahui model apa yang cocok berdasarkan kebutuhan spesifikasinya, seperti kecepatan prosesor, kapasitas RAM, atau rentang harga. Terlebih lagi, deskripsi produk di pasar online sering kali tidak konsisten dan membingungkan.

Dengan menerapkan pendekatan machine learning berbasis content-based filtering, sistem rekomendasi ini mengukur kemiripan antar laptop berdasarkan fitur-fitur teknis yang relevan. Sistem ini diharapkan dapat membantu pengguna menemukan alternatif produk yang setara atau lebih baik berdasarkan pilihan laptop yang mereka pertimbangkan.

### Bagaimana Masalah tersebut Diselesaikan?

Masalah diselesaikan dengan pendekatan bertahap sebagai berikut:

#### 1. Data Understanding 
Data dieksplorasi untuk mengetahui struktur, tipe fitur, nilai ekstrem, serta distribusi data. Tahap ini juga dilakukan visualisasi univariat dan bivariat untuk memahami pola dan korelasi antar variabel.

#### 2. Pembersihan dan Persiapan Data (Data Preparation)
Tahapan ini mencakup:
- Pembersihan data dilakukan dengan mendeteksi duplikasi dan nilai null, serta menormalkan penulisan entri seperti prosesor dan RAM.
- Fitur seperti merek, prosesor, RAM, dan penyimpanan diubah menjadi representasi numerik agar bisa dihitung kemiripannya.
- Encoding fitur kategorikal agar dapat diterima oleh model
- Normalisasi dan transformasi fitur jika diperlukan

#### 3. Modeling
- Pendekatan content-based filtering digunakan dengan menghitung cosine similarity antar laptop berdasarkan vektor fiturnya.

#### 4. Evaluasi
- Evaluasi dilakukan dengan menghitung rata-rata persentase kemiripan antar hasil rekomendasi serta membuat visualisasi persebaran harga dan fitur utama lainnya.
- Sistem diuji terhadap sampel laptop secara acak dan diperiksa apakah hasil rekomendasinya relevan secara spesifikasi.


### State Of The Art Penelitian Sebelumnya

Beberapa penelitian sebelumnya telah mengaplikasikan **content-based filtering (CBF)** sering dikombinasikan dengan metode lain—dalam sistem rekomendasi yang relevan dengan topik laptop atau produk elektronik:

- Oktavian & Amin mengembangkan sistem rekomendasi laptop untuk *Els Computer Shop Semarang* menggunakan pendekatan CBF dan *ordinal encoding*, yang menghasilkan rekomendasi tiga laptop paling relevan berdasarkan cosine similarity spesifikasi teknis [1].
- Rojabi dkk. (2024) merancang sistem rekomendasi laptop berbasis CBF dan K-Nearest Neighbors (KNN), dengan penggunaan TF-IDF pada metadata teknis. Hasil penelitian menunjukkan CBF+KNN efektif untuk mengelompokkan produk laptop secara akurat [2].
- Wijaya & Alfian (2018) membandingkan CBF dan Collaborative Filtering dalam sistem rekomendasi laptop. Mereka menemukan bahwa CBF lebih cepat dalam eksekusi saat menggunakan TF-IDF, meskipun hybrid model memberikan hasil yang lebih seimbang [3].

**Kontribusi Proyek Ini**  
Proyek ini mengambil pendekatan CBF dengan beberapa penyempurnaan:
- Normalisasi input harga ke IDR untuk konteks lokal.
- Penerapan *manual encoding* (tanpa library berat seperti `sklearn`), sehingga lebih fleksibel dan transparan.
- Penambahan opsi pembobotan fitur seperti `RAM` dan `Prosesor`, memungkinkan tuning sesuai kebutuhan pengguna.

---

## Business Understanding

Kebutuhan akan perangkat komputasi yang andal seperti laptop semakin meningkat, baik untuk keperluan pendidikan, pekerjaan, maupun hiburan. Banyaknya pilihan laptop yang beredar di pasaran dengan berbagai merek, spesifikasi, dan harga, seringkali membuat calon pembeli mengalami kesulitan dalam menentukan produk yang paling sesuai dengan kebutuhannya. Konsumen tidak hanya mempertimbangkan faktor harga, tetapi juga spesifikasi teknis seperti jenis prosesor, kapasitas RAM, tipe penyimpanan, ukuran layar, dan sistem operasi. 

Oleh karena itu, dibutuhkan sebuah sistem cerdas yang mampu memberikan rekomendasi laptop secara otomatis berdasarkan preferensi pengguna. Salah satu pendekatan yang dapat digunakan untuk menjawab permasalahan ini adalah content-based filtering, yaitu metode sistem rekomendasi yang menganalisis kesamaan antar item berdasarkan karakteristik atau fitur yang dimiliki masing-masing produk. Dengan memanfaatkan data spesifikasi laptop dari berbagai brand yang telah tersedia dalam bentuk dataset, sistem ini dapat mengolah informasi tersebut dan menyarankan produk-produk serupa berdasarkan item yang diminati pengguna. Pengembangan sistem rekomendasi ini diharapkan mampu memberikan solusi efisien dalam proses pengambilan keputusan pembelian laptop, serta menjadi dasar untuk pengembangan layanan e-commerce yang lebih personal dan adaptif di masa mendatang.

### Problem Statements
- Bagaimana cara membantu pengguna menemukan laptop dengan spesifikasi yang sesuai kebutuhannya tanpa harus memahami detail teknis yang kompleks?
- Bagaimana sistem dapat merekomendasikan laptop lain dengan spesifikasi serupa secara otomatis?

### Goals
- Membangun sistem rekomendasi laptop yang dapat menyarankan produk alternatif dengan spesifikasi serupa secara otomatis.

### Solution Statements
- Dengan menggunakan pendekatan Content-Based Filtering
    Menggunakan kemiripan antar fitur laptop seperti RAM, Prosesor, dan Harga (yang telah di-normalisasi dan dikonversi ke IDR), sistem akan menghitung skor cosine similarity antar produk. Pengguna akan diberikan rekomendasi laptop serupa dengan yang dipilih berdasarkan kemiripan fitur-fitur tersebut.

---

## Data Understanding
### EDA - Deskripsi Variabel
**Informasi Datasets**


| Jenis | Keterangan |
| ------ | ------ |
| Title | _Laptop League: A Comprehensive Dataset for Laptops_ |
| Source | [Kaggle](https://www.kaggle.com/datasets/shrutiambekar/laptop-league-a-comprehensive-dataset-for-laptops/data) |
| Maintainer | [Shruti Ambekar](https://www.kaggle.com/shrutiambekar) |
| License | [CC0: Public Domain](https://creativecommons.org/publicdomain/zero/1.0/) |
| Visibility | Publik |
| Tags | _Data Analytics, Data Visualization, Exploratory Data Analysis, Data Cleaning, Recommender Systems_ |
| View | 4300 |


Tabel 1. Informasi Dataset

![data info](https://github.com/user-attachments/assets/ca3ed720-e0d1-45ed-8904-fca54aafc579)

Dilihat dari _Tabel 1. Informasi Dataset_ dataset ini berisi informasi sebagai berikut ini : 
- Dataset berupa CSV (Comma-Seperated Values).
- Dataset memiliki 984 entri dengan 13 fitur.

### Variable - variable pada dataset
- Unnamed: 0 (numeric): Kolom indeks otomatis dari file CSV saat ekspor. Tidak memiliki makna analitis dan dapat diabaikan atau dihapus saat proses pra-pemrosesan.
- Company (categorical): Merek atau brand dari laptop.
- Rating (numeric): Nilai rating rata-rata dari pengguna terhadap laptop, dalam skala 0 sampai 5.
- No_of_ratings (numeric): Jumlah total pengguna yang memberikan rating terhadap laptop tersebut.
- Review (numeric): Jumlah ulasan atau review teks yang diberikan pengguna (tidak dijelaskan isi review-nya).
- Size (numeric): Ukuran layar laptop dalam satuan inci.
- Processor (categorical): Informasi detail mengenai prosesor yang digunakan, mencakup jenis, seri, dan generasi.
- RAM (numeric): Kapasitas RAM laptop dalam satuan gigabyte (GB).
- Memory (categorical): Informasi penyimpanan laptop, biasanya terdiri dari kapasitas dan jenis penyimpanan (HDD atau SSD).
- OpSys (categorical): Sistem operasi yang digunakan pada laptop.
- Price (numeric): Harga jual laptop saat ini di pasaran atau e-commerce (dalam Rupee).
- MRP (numeric): Harga eceran maksimum (harga asli sebelum diskon).
- ImgURL (categorical): Tautan URL ke gambar produk laptop, biasanya berasal dari situs e-commerce.

### Pengecekan Data Duplikat dan Missing Value
-	Data Duplikat

![data duplikat](https://github.com/user-attachments/assets/4b14d8e2-73de-4028-980f-ea76257fc5de)

Gambar 1. Data Duplikat.

Pada gambar 1 tersebut, menjelaskan bahwa pada dataset tidak memiliki data duplikat.

-	Missing Value
  
![missing value](https://github.com/user-attachments/assets/cdee5cae-aec7-4528-b43a-4420f7046602)

Gambar 2. Missing Value

Pada gambar tersebut, menjelaskan bahwa pada dataset tidak memiliki data missing value.

### Pengecekan Value Unik yang Ada Pada Dataset

![value unik](https://github.com/user-attachments/assets/56baf833-7138-4c0e-8d93-0dedf6196ee4)

Gambar 3. Value Unik

Berdasarkan gambar di atas, berikut adalah deskripsi singkat mengenai banyaknya nilai unik dari masing-masing fitur dalam dataset:

- **Unnamed: 0** (984 unique values)  
Merupakan indeks baris dari dataset yang bersifat unik untuk setiap entri. Karena ini hanya penomoran, fitur ini tidak memiliki pengaruh analitis dan biasanya dihapus dalam tahap pra-pemrosesan.
- **ImgURL** (532 unique values)  
Berisi tautan gambar laptop. Banyaknya nilai unik menunjukkan bahwa sebagian besar laptop memiliki gambar masing-masing, namun fitur ini jarang digunakan dalam analisis model kecuali pada pemrosesan berbasis visual.
- **MRP** (487 unique values)  
Menunjukkan harga asli atau harga maksimum ritel dari laptop. Variasi yang cukup tinggi menunjukkan bahwa harga awal sebelum diskon sangat beragam di pasaran.
- **Price** (393 unique values)  
Merupakan harga akhir atau harga diskon dari laptop. Meski sedikit lebih rendah variasinya dibanding MRP, nilai ini tetap cukup beragam dan relevan untuk fitur target atau filter harga.
- **No_of_ratings** (248 unique values)  
Mencerminkan jumlah orang yang memberikan rating terhadap laptop. Nilai ini sangat bervariasi dan bisa menjadi indikator popularitas suatu produk.
- **Review** (136 unique values)  
Jumlah review teks untuk setiap produk. Meski tidak menjelaskan isi review, variasinya bisa mengindikasikan tingkat ketertarikan pengguna.
- **Processor** (87 unique values)  
Menunjukkan tipe dan varian prosesor. Jumlah nilai unik yang tinggi mencerminkan keragaman performa dan teknologi pada laptop.
- **OpSys** (40 unique values)  
Berisi informasi sistem operasi. Adanya 40 jenis berbeda mengindikasikan banyaknya kombinasi versi OS dan arsitektur yang digunakan.
- **Memory** (37 unique values)  
Deskripsi penyimpanan yang mencakup ukuran dan tipe (SSD/HDD). Nilai unik yang tinggi menandakan variasi besar pada konfigurasi penyimpanan.
- **Company** (19 unique values)  
Merek produsen laptop. Terdiri dari 19 brand berbeda yang menunjukkan keberagaman produsen di pasar.
- **Rating** (19 unique values)  
Nilai rating laptop dalam skala 1–5. Jumlah nilai unik yang kecil menunjukkan rating dibulatkan, biasanya satu atau dua digit desimal.
- **Size** (16 unique values)  
Ukuran layar dalam inci. Variasi ini mencerminkan preferensi layar yang berbeda, dari laptop kecil hingga besar.
- **RAM** (4 unique values)  
Kapasitas RAM dalam GB. Hanya memiliki 4 nilai unik, biasanya 4GB, 8GB, 16GB, dan 32GB, yang umum ditemukan pada laptop modern.

> Insight: Beberapa kolom seperti `Processor`, `Memory`, dan `OpSys` memiliki jumlah nilai unik yang tinggi, sehingga dapat memerlukan preprocessing lebih lanjut (seperti pengelompokan atau encoding). Sebaliknya, fitur seperti `RAM`, `Company`, dan `Rating` cenderung lebih terstruktur dan mudah ditangani saat modeling.

### EDA - Univariate Analysis

![EDA Describe Data](https://github.com/user-attachments/assets/1ddce1e0-df3b-45f1-a524-9f1ad4829a0c)

Gambar 4. Penjelasan Dataset

Gambar 4 merupakan penjelasan mengenai dataset yang digunakan
- **Kolom `Rating`** mencatat skor rata-rata yang diberikan pengguna terhadap laptop, dengan nilai rata-rata sebesar 4.25 dalam rentang antara 1.7 hingga 5.0, yang menunjukkan bahwa sebagian besar laptop dalam dataset ini dinilai cukup baik oleh konsumen.
- **Kolom `No_of_ratings`** mencerminkan jumlah pengguna yang memberikan rating pada setiap laptop, dengan rata-rata sebanyak 1.372 rating, dan distribusinya sangat bervariasi mulai dari hanya 1 hingga mencapai 13.376, menandakan perbedaan signifikan dalam popularitas produk.
- **Kolom `Review`** menunjukkan jumlah ulasan teks dari pengguna, dengan rata-rata sebanyak 127 ulasan per produk dan nilai maksimum hingga 1.904 ulasan, sementara terdapat juga laptop yang tidak mendapatkan ulasan sama sekali, mengindikasikan tingkat interaksi pengguna yang tidak merata.
- **Kolom `Size`** merepresentasikan ukuran layar laptop dalam inci, dengan rata-rata sebesar 40.82 inci dan rentang nilai dari 29 hingga 103 inci, namun nilai maksimum tersebut tampak tidak realistis dan kemungkinan merupakan anomali atau kesalahan input data.
- **Kolom `RAM`** menunjukkan kapasitas memori utama laptop dalam GB, dengan nilai rata-rata sebesar 11.9 GB dan rentang dari 4 GB hingga 32 GB, mencerminkan variasi dari perangkat entry-level hingga high-end.
- **Kolom `Price`** mencatat harga jual saat ini dari laptop, dengan nilai rata-rata sebesar 82.145 dan kisaran harga dari 16.990 hingga 399.990, menunjukkan adanya produk dari berbagai segmen harga mulai dari murah hingga premium.
- **Kolom `MRP`** atau harga eceran maksimum menunjukkan harga sebelum diskon atau promosi, dengan rata-rata sebesar 100.740 dan nilai maksimum mencapai 467.990, yang memperlihatkan adanya perbedaan harga signifikan dan kemungkinan strategi pemasaran berupa diskon besar.

![num hist](https://github.com/user-attachments/assets/9a6fe8c1-add5-40fc-a4ff-278fb616108b)

Gambar 5. Histogram Kolom Numerik

Pada gambar 5, terilhat grafik histogram masing-masing kolom numerik.
- **`Rating`**: Distribusinya cenderung condong ke kanan dengan mayoritas laptop memiliki rating antara 4.0 hingga 4.5.
- **`No_of_ratings`** dan **`Review`**: Sangat tidak merata; sebagian besar laptop hanya memiliki sedikit rating atau review, namun ada beberapa outlier dengan jumlah yang sangat tinggi.
- **`Size`**: Terlihat mayoritas ukuran layar laptop berkisar antara 36 hingga 40 inci, sementara nilai ekstrem di atas 100 kemungkinan adalah anomali.
- **`RAM`**: Distribusi bimodal yang jelas—terutama pada RAM 8GB dan 16GB—menunjukkan dua kelompok besar segmentasi pasar.
- **`Price`** dan **`MRP`**: Menunjukkan distribusi miring ke kanan (_right-skewed_), dengan sebagian besar laptop memiliki harga di bawah 150.000, namun terdapat sejumlah produk premium dengan harga sangat tinggi sebagai outlier.

![cat hist](https://github.com/user-attachments/assets/316471f7-0ac3-4966-a621-fd347b46f849)

Gambar 6. Histogram Kolom Kategorikal

Pada gambar 6, terilhat grafik histogram masing-masing kolom kategorikal.
- **`Company`**: Merek yang paling dominan adalah Lenovo, ASUS, dan HP, yang mencerminkan dominasi pasar oleh brand-brand besar, sementara brand lain seperti GIGABYTE, ALIENWARE, dan RedmiBook jumlahnya sangat kecil.
- **`Processor`**: Mayoritas laptop menggunakan prosesor Intel, khususnya seri Core i3 dan i5 generasi ke-11 dan ke-12, disusul oleh AMD Ryzen 5 dan Ryzen 7; ini menunjukkan fokus pasar pada prosesor mid-range yang populer untuk penggunaan harian dan produktivitas.
- **`Memory`**: Penyimpanan paling umum adalah 512 GB SSD, jauh mengungguli kombinasi HDD dan SSD lainnya; namun terdapat beberapa entri yang tampak seperti noise atau deskripsi produk yang salah masuk kolom, sehingga perlu dibersihkan lebih lanjut.
- **`OpSys`**: Sistem operasi paling umum adalah 64 bit Windows 11, diikuti oleh Windows 10 dan varian lainnya, namun ada entri seperti deskripsi fitur yang keliru masuk kolom ini (misalnya "Graphics & Keyboard" atau "Stylish Thin and Light Laptop") yang menunjukkan perlunya preprocessing untuk normalisasi data.

### EDA - Multivariate Analysis

![heatmap corr](https://github.com/user-attachments/assets/2684ffc3-16c5-4be6-a7e9-0626e06073cd)

Gambar 7. Heatmap Korelasi

Heatmap pada gambar 7 ini menggambarkan korelasi antar fitur. Temuan utama:
- Terdapat korelasi yang cukup kuat antara `Price` dan `MRP` (nilai korelasi mendekati 1), yang masuk akal karena keduanya merepresentasikan harga, meskipun `MRP` adalah harga sebelum diskon.
- `No_of_ratings` dan `Review` juga memiliki korelasi yang cukup tinggi, menandakan bahwa semakin banyak pengguna yang memberikan rating, maka kemungkinan besar review teks juga meningkat.
- Variabel seperti `RAM`, `Size`, dan `Rating` memiliki korelasi yang rendah terhadap harga (Price), yang artinya spesifikasi ini tidak secara langsung menentukan harga laptop dalam dataset ini, atau ada variabel lain yang lebih dominan (seperti merek atau fitur tambahan).

![Price - RAM](https://github.com/user-attachments/assets/047359cd-feed-4ae9-a378-7b3f54f2b683)

Gambar 8. Scatter Plot antara RAM dan Price (Harga)

Gambar 8 menunjukkan distribusi harga kendaraan berdasarkan RAM (`RAM`) dan harga (`Price`). Hasil pengamatan menunjukkan:
- Secara umum, terlihat bahwa semakin besar kapasitas RAM, cenderung harga laptop juga meningkat, meskipun hubungan ini tidak linear sempurna.
- Terjadi tumpukan harga yang cukup tinggi pada RAM 8GB dan 16GB, yang memang merupakan konfigurasi paling umum di pasar.
- Beberapa laptop dengan RAM tinggi (32GB) berada di kisaran harga premium, namun masih ada juga laptop dengan RAM besar namun harga relatif lebih terjangkau, kemungkinan karena spesifikasi lain yang lebih rendah (seperti prosesor atau storage).

![rat - price](https://github.com/user-attachments/assets/37267f78-6b03-4177-9f99-501bfabec42a)

Gambar 9. Scatter Plot antara Rating dan Price

Gambar 9 menunjukkan hubungan antara `Rating` (skor rating) dan `price` (harga). Dari grafik terlihat bahwa:
- Tidak terdapat pola hubungan yang jelas antara rating dan harga laptop.
- Laptop dengan harga tinggi tidak selalu memiliki rating yang tinggi, begitu juga sebaliknya. Beberapa laptop dengan harga relatif rendah justru mendapat rating tinggi dari pengguna.
- Distribusi rating sangat padat di kisaran 4.0 hingga 4.5, mencerminkan bahwa mayoritas laptop dinilai cukup baik oleh pengguna terlepas dari harganya.

![price - comp](https://github.com/user-attachments/assets/5cebe99b-cf9e-4937-9a71-603b2b7f0309)

Gambar 10. Boxplot distribusi harga (Price) laptop berdasarkan Company

Gambar 10 menunjukkan hubungan antara `Price` (harga) dan `Company` (merek laptop). Dari grafik terlihat bahwa:
- **Apple** dan **Microsoft** tampak memiliki harga median yang paling tinggi, menunjukkan bahwa produk mereka lebih condong ke segmen premium.
- Brand seperti **Infinix**, **Avita**, dan **RedmiBook** menunjukkan harga median yang lebih rendah, sesuai dengan positioning mereka sebagai brand entry-level atau value-for-money.
- Sebagian besar brand seperti **HP**, **Lenovo**, **ASUS**, dan **DELL** menunjukkan variasi harga yang cukup lebar, mencerminkan banyaknya varian produk dari low hingga high-end.
- Terdapat beberapa outlier harga sangat tinggi, kemungkinan berasal dari seri gaming atau laptop profesional dengan spesifikasi sangat tinggi.

---

## Data Preparation

Tahap ini dilakukan untuk mempersiapkan data mentah menjadi bentuk yang siap digunakan untuk proses modeling. Adapun tahapan-tahapan yang dilakukan meliputi:

### 1. Pembersihan Kolom yang Tidak Dibutuhkan
Kolom `Unnamed: 0` dihapus karena merupakan hasil auto-index dari file CSV dan `ImgURL` karena merupakan link gambar. Keduanya tidak memberikan informasi analitis yang berguna.

### 2. Handling Outlier
- Pada kolom `Size`, mayoritas laptop memiliki ukuran layar antara 36 hingga 40 inci. Namun, terdapat nilai maksimum sebesar 103 inci, yang sangat tidak realistis untuk ukuran layar laptop dan kemungkinan besar adalah outlier atau kesalahan input. Maka, buang entri dengan ukuran layar di atas 50 inci sebagai outlier (karena laptop umumnya tidak lebih dari 20 inci).

### 3. Normalisasi dan Transformasi Fitur
Beberapa kolom diubah atau diproses lebih lanjut:
- **Processor** diparsing menjadi kolom baru `Processor_Short` untuk menyederhanakan jenis prosesor (contoh: “Intel Core i5”, “AMD Ryzen 7”).
- **Memory** dipisahkan menjadi dua fitur baru: `Storage_Size` dan `Storage_Type`.
- **OpSys** disederhanakan menjadi `OS_Simplified` agar lebih konsisten, misalnya “Windows 11”, “DOS”, "Windows 10", dll.
- Menghapus baris yang memiliki nilai **Other** dalam fitur `Memory`, `Storage_Type`, dan `OS_Simplified` karena tidak terlalu membantu dalam pemilihan spesifikasi laptop.

### 4. Konversi Harga dari Rupee ke IDR
Karena data harga (`Price`, `MRP`) masih dalam satuan Rupee (₹), dilakukan konversi ke Rupiah (Rp) menggunakan kurs tetap:
- **Kurs konversi**: ₹1 = Rp189

### 5. Encoding Fitur Kategori
Agar bisa digunakan dalam perhitungan kesamaan antar item, fitur kategori seperti `Company`, `Processor_Short`, `OS_Simplified`, dan `Storage_Type` diencoding menjadi bentuk numerik menggunakan teknik Label Encoding manual (tanpa library sklearn).

---

## Modelling

Sistem rekomendasi yang dikembangkan menggunakan pendekatan Content-Based Filtering, yaitu merekomendasikan produk (laptop) yang memiliki kemiripan atribut dengan produk yang sudah dipilih pengguna sebelumnya. Setiap laptop direpresentasikan sebagai vektor berdasarkan fitur-fitur seperti merek, prosesor, RAM, jenis penyimpanan, sistem operasi, dan rentang harga.

Untuk mengukur kemiripan antar produk, digunakan metrik Cosine Similarity, di mana semakin tinggi nilai similarity, maka semakin mirip laptop tersebut dengan preferensi pengguna.

### Fitur yang Digunakan
Fitur yang digunakan dalam pemodelan adalah:
- `Company`
- `Processor_Short`
- `RAM`
- `Storage_Type`
- `OS_Simplified`
- `Price` (harga yang telah dikonversi dari rupee ke rupiah)

Setiap fitur dikonversi ke bentuk numerik menggunakan teknik One-Hot Encoding untuk fitur kategorikal, dan disatukan ke dalam matriks fitur.

### Sistem Rekomendasi
Pengguna dapat memasukkan preferensi seperti:
- Merek laptop
- Jenis prosesor
- Kapasitas RAM
- Jenis penyimpanan (SSD/HDD)
- Sistem operasi
- Rentang harga

Sistem akan mencocokkan preferensi ini terhadap dataset dan mencari 5 laptop teratas yang paling mirip berdasarkan nilai cosine similarity.

![function rec](https://github.com/user-attachments/assets/fad8eae2-ed0a-4b9f-898e-2e3e26b5ca49)


Gambar 11. Fungsi Sistem Rekomendasi

Output dari sistem ini akan menampilkan 5 rekomendasi laptop paling relevan berdasarkan parameter tersebut, lengkap dengan skor similarity-nya.

### Hasil Rekomendasi 
Berikut adalah hasil rekomendasi ketika pengguna mencari laptop ASUS, Intel Core i7, RAM 16GB, SSD, Windows 11, dan harga antara 10 juta hingga 20 juta rupiah:

| Index | Company | Processor                     | RAM | Memory       | OS_Simplified | Price     | Similarity |
|-------|---------|-------------------------------|-----|--------------|----------------|-----------|------------|
| 32    | ASUS    | AMD Ryzen 5 Hexa Core Processor | 16  | 512 GB SSD   | Windows 11     | 10,771,110 | 1.0        |
| 328   | ASUS    | AMD Ryzen 5 Hexa Core Processor | 16  | 512 GB SSD   | Windows 11     | 10,393,110 | 1.0        |
| 576   | ASUS    | AMD Ryzen 5 Hexa Core Processor | 16  | 512 GB SSD   | Windows 11     | 10,393,110 | 1.0        |
| 525   | ASUS    | AMD Ryzen 5 Hexa Core Processor | 16  | 512 GB SSD   | Windows 11     | 10,393,110 | 1.0        |
| 376   | ASUS    | AMD Ryzen 5 Hexa Core Processor | 16  | 512 GB SSD   | Windows 11     | 10,393,110 | 1.0        |

Tabel 2. Hasil Rekomendasi

---

## Evaluation
Untuk mengevaluasi sistem rekomendasi laptop yang dibangun, digunakan pendekatan berbasis similarity score yang dihitung menggunakan cosine similarity. Evaluasi ini berfokus pada seberapa relevan hasil rekomendasi terhadap input pengguna berdasarkan fitur-fitur seperti merk, processor, RAM, jenis storage, sistem operasi, dan rentang harga.

### Metrik Evaluasi
Metrik yang digunakan dalam sistem ini adalah cosine similarity, yang mengukur kesamaan antara dua vektor fitur. Nilai cosine similarity berkisar antara 0 hingga 1, di mana nilai mendekati 1 menunjukkan tingkat kemiripan yang sangat tinggi.

![rumus consine](https://github.com/user-attachments/assets/9d622a1f-264d-4a02-aa11-27f2e6ba73c2)

Gambar 12. Rumus Cosine Similarity

Dalam sistem ini, semakin tinggi skor similarity, maka semakin relevan hasil rekomendasi terhadap preferensi pengguna.

### Hasil Evaluasi
Berikut adalah hasil rekomendasi berdasarkan query dengan kriteria:
- Brand: ASUS
- Processor: AMD Ryzen 5 Hexa Core Processor
- RAM: 16 GB
- Storage: SSD
- OS: Windows 11
- Price range: IDR 10.000.000 – IDR 20.000.000

Hasil menunjukkan bahwa semua rekomendasi memiliki similarity score sebesar 1.0, yang menandakan bahwa sistem berhasil menemukan laptop yang sangat mirip dengan preferensi pengguna.

### Visualisasi
Untuk memberikan gambaran lebih lanjut tentang performa sistem, berikut visualisasi nilai similarity untuk 5 rekomendasi teratas:

![vis eval](https://github.com/user-attachments/assets/82c36486-d52b-4681-94e5-40e88c269848)

Gambar 13. Visualisasi Cosine Similarity terhadap Rekomendasi

---

## Kesimpulan

Model **content-based filtering** menggunakan cosine similarity terbukti sangat efektif untuk memberikan rekomendasi laptop yang sesuai dengan kebutuhan pengguna. Seluruh hasil rekomendasi memiliki similarity score sebesar **1.0**, yang berarti sangat relevan dan identik dengan kriteria pencarian. Sistem ini dapat digunakan untuk meningkatkan pengalaman pengguna dalam memilih laptop, khususnya di platform e-commerce yang menawarkan ribuan pilihan produk. Efektivitasnya terlihat dari kemampuannya menyaring produk sesuai kebutuhan, sehingga mempermudah proses pengambilan keputusan.

### Kesimpulan Dampak Model Terhadap Business Understanding

Sistem rekomendasi ini memberikan kontribusi signifikan terhadap peningkatan pengalaman pengguna dalam mencari laptop sesuai kebutuhan tanpa harus memahami aspek teknis secara mendalam. Dengan penyajian rekomendasi produk yang relevan, pengguna dapat membuat keputusan lebih cepat dan akurat, yang pada akhirnya berkontribusi pada peningkatan konversi penjualan di platform e-commerce. Selain itu, pendekatan berbasis fitur ini memungkinkan fleksibilitas integrasi ke berbagai platform digital serta dapat diskalakan untuk berbagai jenis produk lainnya. Dengan sistem ini, pemilik bisnis dapat mengurangi beban pengguna dalam proses pencarian dan meningkatkan loyalitas melalui pengalaman pencarian yang efisien dan personal.

---

## Daftar Pustaka

1. R. Oktavian and F. Amin, "Perancangan Sistem Rekomendasi Laptop dengan Model Prototyping dan Penerapan Content‑Based Filtering Approach pada ELS Computer Shop Semarang," *G‑Tech: Jurnal Teknologi Terapan*, vol. 8, no. 1, pp. 66–80, Jan. 2024. DOI: 10.33379/gtech.v8i1.3490.

2. I. Rojabi, I. Saifudin, and G. Wijaya, "Sistem Rekomendasi Pemilihan Laptop Menggunakan Metode Content Based Filtering Dan K‑Nearest Neighbor," *Jurnal Mahasiswa Teknik Informatika (JATI)*, vol. 6, no. 2, 2024.

3. A. E. Wijaya and D. Alfian, "Sistem Rekomendasi Laptop Menggunakan Collaborative Filtering Dan Content‑Based Filtering," *Jurnal Computech & Bisnis*, vol. 12, no. 1, pp. 11–27, 2018.
