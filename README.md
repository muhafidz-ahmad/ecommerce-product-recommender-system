# E-commerce Product Recommender System
## 1. Project Overview
*E-commerce* adalah salah satu inovasi di era modern ini yang memiliki fungsi untuk membantu konsumen membeli barang-barang yang mereka butuhkan dengan mudah melalui gawai mereka. Selain membantu konsumen, *e-commerce* juga membantu banyak penjual dalam menjual barangnya dengan lebih mudah. Dengan *e-commerce*, penjual dapat menjual barang tidak hanya terbatas kepada konsumen di daerahnya saja, tetapi penjual dapat menjual produknya ke konsumen di seluruh dunia.

Saat ini telah banyak sekali barang-barang yang dijual di *e-commerce*. Tak jarang barang-barang tersebut terdapat barang yang dijual oleh seorang penipu yang dapat merugikan konsumen. Oleh karena itu, pemilik *platform e-commerce* perlu memberikan rasa aman dan rasa nyaman kepada para konsumen dengan memfilter barang-barang yang direkomendasikan kepada user.

Selain itu, pemilik e-commerce juga perlu sebuah sistem rekomendasi yang dapat merekomendasikan barang yang sesuai dengan yang pembeli butuhkan atau pembeli inginkan. Hal ini bertujuan untuk memberikan kemudahan kepada pengguna, dan tentunya meningkatkan *trafic* dan transaksi di platform *e-commerce* tersebut. Sebagai pembeli, sistem rekomendasi dapat memberikan kemudahan bagi pembeli untuk menemukan produk yang sesuai dengan yang kita inginkan. Sebagai penjual, bisa dibilang sistem rekomendasi ini dapat mengiklankan produknya secara tepat kepada orang-orang yang benar-benar membutuhkan atau menginginkan produk tersebut.

Terdapat dua pendekatan yang umum digunakan untuk membuat sistem rekomendasi, yaitu *content-based filtering* dan *collaborative filtering*. *Content-based filtering* sangat berguna untuk diterapkan pada fitur _search engine e-commerce_. Karena *content-based filtering* ini mengandalkan _keyword_ untuk bisa memperoleh rekomendasi produk yang relevan. *Collaborative filtering* sangat berguna untuk diterapkan kepada setiap pengguna sehingga pengguna bisa dengan cepat menemukan produk yang mungkin relevan dan sedang diinginkan oleh pembeli tanpa perlu menggunakan fitur _search engine_.

Sistem rekomendasi di *ecommerce* telah beberapa kali dilakukan penelitian, terutama dengan yang berdasarkan big data [1]. Salah satu penelitian terbaru dalam pengembangan sistem rekomendasi ini adalah dengan menggunakan *AutoML* [2].

## 2. Business Understanding
### 2.1. Problem Statements
Dari kondisi yang telah dijelaskan di atas, akan dibuat sebuah sistem rekomendasi untuk menjawab permasalahan berikut:
* Bagaimana cara memberikan rekomendasi produk yang relevan kepada pengguna berdasarkan preferensi dan perilaku mereka?
* Bagaimana sistem rekomendasi dapat membantu meningkatkan pengalaman belanja pengguna dan mendorong penjualan?
* Bagaimana kita dapat memanfaatkan informasi dari pengguna, produk, dan riwayat pembelian untuk menghasilkan rekomendasi yang personal dan akurat?

### 2.2. Goals
* Membuat sistem rekomendasi yang bisa memberikan rekomendasi produk yang relevan dengan preferensi pengguna.
* Mengetahui kemampuan sistem rekomendasi dalam memberikan rekomendasi produk kepada pengguna.
* Mengoptimalkan pemanfaatan data pelanggan dan produk yang ada dalam platform *e-commerce* untuk membuat sistem rekomendasi lebih akurat dan presisi.

### 2.3. Solution Approach
Untuk mencapai tujuan di atas, akan digunakan dua pendekatan dalam sistem rekomendasi kami, yaitu:
1. *Content-Based Filtering*, yang dapat memberikan rekomendasi produk yang memiliki kesamaan konden dengan produk yang disukai atau dicari oleh konsumen.
2. *Collaborative Filtering*, yang dapat memberikan rekomendasi berdasarkan preferensi konsumen atau pelanggan yang mirip.

## 3. Data Understanding
Data yang akan digunakan untuk project ini adalah data dari Kaggle yang berisi merupakan data informasi *custumer*, produk, dan *review* dari salah satu platform *e-commerce* bernama *Olist*. Data dapat diunduh melalui [tautan berikut](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). Data ini telah diproses oleh *publisher* sehingga data ini tidak mengambil privasi konsumen maupun penjual dari *e-commerce* tersebut.

Dataset ini terdiri dari 9 skema dataset, diantaranya:

![image](https://github.com/muhafidz-ahmad/ecommerce-product-recommender-system/assets/115754250/426dec64-f6c4-4df4-8f1d-fd7f945f1e91)

Gambar 1. Skema dataset *e-commerce Olist*

1. olist_customers_dataset.csv --> berisi data-data pelanggan secara detail. Terdiri dari 99.441 baris dan 5 kolom. Berikut adalah deskripsi tiap kolomnya:
  * customer_id: id unik pelanggan
  * customer_unique_id: id unik pelanggan (anonim)
  * customer_zip_code_prefix: kode pos pelanggan
  * customer_city: kota pelanggan
  * customer_state: negara bagian pelanggan
2. olist_geolocation_dataset.csv --> berisi data-data lokasi geografis kode pos.
  * geolocation_zip_code_prefix: kode pos lokasi
  * geolocation_lat: latitude lokasi
  * geolocation_lng: longitude lokasi
  * geolocation_city: kota lokasi
  * geolocation_state: negara bagian lokasi
3. olist_order_items_dataset.csv --> berisi data-data pesanan produk. Terdiri dari 112.650 baris dan 7 kolom. Berikut adalah deskripsi tiap kolomnya:
  * order_id: id unik pesanan
  * order_item_id: id unik item pesanan
  * product_id: id unik produk
  * seller_id: id unik penjual
  * shipping_limit_date: tanggal batas pengiriman
  * price: harga produk
  * freight_value: harga pengiriman
4. olist_order_payments_dataset.csv --> berisi data-data metode pembayaran yang dipakai untuk melakukan pesanan yang sudah dilakukan.
  * order_id: id unik pesanan
  * payment_sequential: urutan pembayaran dalam satu pesanan
  * payment_type: jenis pembayaran (boleto atau kartu kredit)
  * payment_installments: jumlah cicilan pembayaran
  * payment_value: nilai pembayaran
5. olist_order_reviews_dataset.csv --> berisi data-data *review* dari pesanan yang telah selesai. Terdiri dari 99.224 baris dan 7 kolom. Berikut adalah deskripsi tiap kolomnya:
  * review_id: id unik ulasan
  * order_id: id unik pesanan
  * review_score: skor ulasan dengan range dari 1 sampai 5
  * review_comment_title: judul ulasan dari customer dalam bahasa portugis
  * review_creation_date: tanggal dibuatnya ulasan
  * review_answer_timestamp: menunjukkan stempel waktu jawaban survei kepuasan
6. olist_orders_dataset.csv --> berisi data-data lengkap pesanan yang telah dilakukan. Terdiri dari 99.441 baris dan 8 kolom. Berikut adalah deskripsi tiap kolomnya:
  * order_id: id unik pesanan
  * customer_id: id unik pelanggan
  * order_status: status pesanan (dibayar, dikirim, selesai)
  * order_purchase_timestamp: waktu pembelian pesanan oleh pelanggan (UTC)
  * order_approved_at: waktu persetujuan pesanan oleh penjual (UTC)
  * order_delivered_carrier_date: waktu pengiriman oleh kurir (UTC)
  * order_delivered_customer_date: waktu pengiriman ke pelanggan (UTC)
  * order_estimated_delivery_date: waktu estimasi pengiriman ke pelanggan (UTC)
7. olist_products_dataset.csv --> berisi data-data detail produk yang dijual di ecommerce. Terdiri dari 32.951 baris dan 9 kolom. Berikut adalah deskripsi tiap kolomnya:
  * product_id: id unik produk
  * product_category_name: nama kategori produk dalam bahasa portugis
  * product_name_length: jumlah karakter yang diekstrak dari nama produk
  * product_description_length: jumlah karakter yang diekstrak dari deskripsi produk
  * product_photos_qty: jumlah foto produk yang dipublish
  * product_weight_g: berat produk dalam satuan gram
  * product_length_cm: ukuran panjang produk dalam satuan cm
  * product_height_cm: ukuran tinggi produk dalam satuan cm
  * product_width_cm: ukuran leabr produk dalam satuan cm
8. olist_sellers_dataset.csv --> berisi data-data detail penjual. Terdiri dari 2.095 baris dan 4 kolom. Berikut adalah deskripsi tiap kolomnya:
  * seller_id: id unik penjual
  * seller_zip_code_prefix: kode pos penjual
  * seller_city: kota penjual
  * seller_state: negara bagian penjual
9. product_category_name.csv --> kamus penerjemah nama kategori produk dari Bahasa Portugis dan Bahasa Inggris. Terdiri dari 71 baris dan 2 kolom. Berikut adalah deskripsi tiap kolomnya:
  * product_category_name: nama kategori produk dalam bahasa portugis
  * product_category_name_english: nama kategori produk dalam bahasa Inggris

Namun pada proyek ini, hanya akan digunakan 7 skema dataset, yaitu:
1. olist_order_customers_dataset.csv
2. olist_order_items_dataset.csv
3. olist_order_reviews_dataset.csv
4. olist_orders_dataset.csv
5. olist_seller_dataset.csv
6. olist_products_dataset.csv
7. product_category_name_translation.csv

Secara umum, kondisi data sudah bersih dari data duplikat, walau jika dieksplorasi lebih dalam, terdapat beberapa skema dataset yang memiliki data yang hilang karena kondisi tertentu.

**Exploratory Data Analysis**

Pada dataset *olist_order_customers_dataset.csv* (selanjutnya akan ditulis dataset customer) memiliki kolom kode pos, kota, dan negara bagian dari konsumen. Namun pada proyek ini, hanya akan digunakan informasi kota konsumen saja. Sehingga datset customer ini tersisa 3 kolom, yaitu *customer_id*, *customer_unique_id*, dan *customer_city*. Terdapat 96096 pelanggan unik yang tersebar di 4119 kota.

![image](https://github.com/muhafidz-ahmad/ecommerce-product-recommender-system/assets/115754250/0f667060-5439-412a-862c-a2a05d02cbd0)

Gambar 2. Top 10 kota dengan pembeli terbanyak

Kemudian pada dataset *olist_order_items_dataset.csv* (selanjutnya akan ditulis dataset order item) memiliki total 6 kolom, dengan jumlah nilai unik sebagai berikut:
* *order_id* : 98666 nilai unik
* *order_item_id* : 21 nilai unik
* *product_id* : 32951 nilai unik
* *seller_id* : 3095 nilai unik
* *price* : 5968 nilai unik
* *freight_value* : 6999 nilai unik
Terdapat 32.951 produk terjual beberapa kali dari 3095 penjual.

Pada dataset order item ini terdapat kolom harga dengan statistik sebagai berikut:

Tabel 1. Statistik harga order

|         | price       |
|-------- |------------ |
| mean    | 120.653739  |
| std     | 183.633928  |
| min     | 0.850000	   |
| 25%     | 39.900000	  |
| 50%     | 74.990000   |
| 75%     | 134.900000  |
| max     | 6735.000000	|

Selanjutnya pada dataset *olist_order_reviews_dataset.csv* (selanjutnya akan ditulis dataset order review) memiliki 7 kolom, dua di antaranya adalah *review_comment_title* dan *review_comment_message* yang memiliki banyak nilai yang hilang. Ini karena memang terkadang pembeli ketika memberi review tidak memiliki waktu untuk menulis ulasan yang detail, sehingga hanya memberi skor saja. Oleh karena itu, kedua kolom tersebut dihapus saja. 
Skor review yang ada pada dataset ini adalah dalam rentang 1 sampai dengan 5 dan rata-rata skor review sebesar 4.09 dari total 99224 review.

Keempat, pada dataset *olist_orders_dataset.csv* (selanjutnya akan dituis dataset orders) memiliki 8 kolom dengan cukup banyak nilai yang hilang pada kolom *order_approved_at*, *order_delivered_carrier_date*, dan *order_delivered_customer_date* karena bisa saja kondisi ketika data ini diambil, terdapat status pembelian yang menyebabkan data pada kolom tersebut masih kosong. Namun untungmya, kolom tersebut tidak terpakai untuk membuat sistem rekomendasi, sehingga akan dihapus. Kemudian, untuk membuat sistem rekomendasi pada proyek ini juga hanya akan menggunakan data dengan status order sudah selesai atau *delivered*.

![image](https://github.com/muhafidz-ahmad/ecommerce-product-recommender-system/assets/115754250/c33dc43f-93d8-403d-9835-cccb972db8f7)

Gambar 3. Jumlah status pesanan

Kelima, dataset *olist_seller_dataset.csv* (selanjutnya akan ditulis dataset seller) kondisinya sudah sangat bersih. Sama seperti dataset customer, informasi seller juga hanya akan menggunakan informasi kota saja. Terdapat total 3095 penjual yang tersebar di 611 kota.

![image](https://github.com/muhafidz-ahmad/ecommerce-product-recommender-system/assets/115754250/15737acf-b07e-4316-98fe-bf427d56c6dc)

Gambar 4. Top 10 kota dengan penjual terbanyak

Terakhir, dataset *olist_products_dataset.csv* yang berisi data informasi produk dan *product_category_name_translation.csv* sebagai kamus nama kategori produk dari Bahasa Portugis ke Bahasa Inggris. Sayangnya, dataset produk ini tidak memiliki nama produk dan deskripsi produk yang eksplisit. Sehingga sistem rekomendasi yang akan dibuat akan digunakan *product_id* untuk menunjukan produk tertentu. Terdapat 73 kategori produk pada dataset ini.

![image](https://github.com/muhafidz-ahmad/ecommerce-product-recommender-system/assets/115754250/a4a0da60-3ae4-44a7-a214-bfbd1165dcfe)

Gambar 5. Top 10 kategori produk

## 4. Data Preparation
### 4.1. Content-Based Filtering
Persiapan data akan dimulai dari data preprocessing, untuk mempermudah dalam pembuatan membaca nama produk dan seller karena nama produk dan seller tidak tersedia.
#### 4.1.1. Data Preprocessing

**Membuat Nama Produk dan Seller Buatan**
* Nama produk dan *seller* akan dibuat dengan format *product_(number)* untuk nama produk, dan format *seller_(number)* untuk nama *seller*. 

**Harga Produk**
* Karena harga produk terkadang berubah karena ada diskon, maka akan diambil harga rata-rata dari dataset order item untuk menentukan harga produk. Kemudian data harga produk ini dimasukan ke dataset *products*.

**Review dan Jumlah Produk Terjual**
* Digabungkan data review produk ke dalam dataset *products*.
* Dibuat juga kolom baru berisi informasi jumlah barang terjual yang kemudian dimasukan juga ke dalam dataset *products*.

**Nama Seller ke Products**
* Tentunya, dimasukan juga nama seller ke dalam dataset *products*.

**Respons Time Order**
* Ditambahkanj juga kolom baru yang berisi informasi kecepatan *seller* dalam merespon sebuah pesanan.

#### 4.1.2. Data Preparation
Dari hasil *preprocessing* di atas, diperoleh dataset *products* yang akan digunakan untuk membuat sistem rekomendasi. Dataset ini memiliki total 6 kolom sebagai berikut:
* product_id : id produk unik (string)
* product_category_name : nama kategori produk (string)
* price : harga produk (int)
* review_score : skor review produk (float)
* sold : jumlah produk terjual (int)
* seller_id : id penjuan (string)

Terdapat nilai yang hilang pada *review_score*. Nilai yang kosong tersebut akan diganti dengan nilai 0 agar bisa dimasukan ke dalam perhitungan sistem rekomendasi.

### 4.2. Collaborative Filtering
Data yang digunakan untuk membuat sistem rekomendasi menggunakan *collaborative filtering* merupakan gabungan dari beberapa skema data yang diperlukan dan menyisakan kolom-kolom berikut:
* *product_id*
* *seller_id*
* *price*
* *review_score*
* *respons_time_order*
* *customer_unique_id*
* *customer_city*
* *product_category_name*
* *seller_city*
* *sold*

Setelah itu data ini dibersihkan dari data-data yang kosong dan diperoleh:
* 91479 jumlah pelanggan unik
* 31485 jumlah produk unik

Kemudian, fitur-fitur yang akan digunakan untuk sistem rekomendasi akan di-encode ke dalam bentuk numerik. Adapun fitur-fitur yang digunakan untuk sistem rekomendasi pada proyek ini adalah *customer_unique_id* yang disimpan dalam kolom baru bernama *customer*, *product_id* yang disimpan dalam kolom baru bernama *product*, dan *review_score*.

Terakhir data dipecah menjadi data *training* dan data *testing* dengan rasio 80%:20%. Fitur prediktor yang digunakan adalah *customer* dan *product*. Fitur targetnya adalah *review_score*.

## 5. Model Development
Proyek ini menyajikan dua solusi rekomendasi dengan menggunakan algoritma yang berbeda, yaitu *Content-Based Filtering* dan *Collaborative Filtering*.

### 5.1. Content-Based Filtering
Dalam pendekatan ini, digunakan metode TF-IDF dan Cosine Similarity untuk memperoleh rekomendasi yang relevan.

Pertama, membangun matriks TF-IDF dari kategori produk. Matriks ini akan merepresentasikan setiap produk dalam dataset sebagai vektor numerik berdasarkan frekuensi kata dalam kategori produk tersebut. TF-IDF mengukur seberapa penting suatu kata dalam sebuah dokumen atau konteks. Nilai TF-IDF tinggi menunjukkan kata yang spesifik dan relevan untuk dokumen tersebut. Langkah pertama dalam pembangunan matriks TF-IDF adalah menghitung Term Frequency (TF), yaitu frekuensi kata dalam deskripsi produk. Selanjutnya, perlu dihitung Inverse Document Frequency (IDF), yaitu kebalikan dari frekuensi kata di seluruh dokumen. Ini mengurangi bobot kata-kata yang umum dan meningkatkan bobot kata-kata yang jarang muncul. Akhirnya, matriks TF-IDF terbentuk dengan mengalikan nilai TF dengan nilai IDF. Matriks ini akan menjadi representasi numerik dari kategori produk dalam dataset.

Setelah matriks TF-IDF terbentuk, langkah berikutnya adalah menghitung cosine similarity antara setiap pasangan produk. Cosine similarity mengukur kesamaan antara dua vektor dengan mengukur sudut antara vektor-vektor tersebut. Semakin kecil sudut antara vektor-vektor, semakin mirip produk-produk tersebut. Untuk menghitung cosine similarity, dapat digunakan formula cosine similarity:

$$ cosine similarity = {{A . B} \over {||A|| ||B||}} $$

Dengan menghitung cosine similarity antara semua pasangan produk, kita dapat memperoleh matriks similarity antara produk-produk dalam dataset. Nilai cosine similarity ini dapat digunakan untuk menemukan produk-produk yang paling mirip satu sama lain. Semakin tinggi nilai cosine similarity antara dua produk, semakin mirip kedua produk tersebut.

Dengan menggunakan metode TF-IDF dan Cosine Similarity dalam content-based filtering, kita dapat memperoleh rekomendasi produk yang memiliki kategori yang mirip dengan produk yang sedang ditinjau oleh pengguna. Hal ini memungkinkan sistem rekomendasi untuk mengidentifikasi dan merekomendasikan produk yang memiliki kesamaan konten dengan produk yang disukai oleh pengguna.

Kelebihan dari pendekatan ini adalah kemampuannya dalam memberikan rekomendasi yang relevan berdasarkan konten produk, bahkan bisa menjangkau produk yang baru muncul. Namun kekurangannya adalah kurangnya kemampuan untuk menemukan preferensi pelanggan lain, dan baru bisa memberikan rekomendasi produk jika memang pengguna sedang melakukan pencarian dengan keyword.

Output dari pendekatan Content-Based Filtering ini adalah daftar produk rekomendasi berdasarkan keyword yang dimasukan. Misalnya, pengguna aplikasi melakukan pencarian dengan keyword "bola", maka akan ditampilkan beberapa rekomendasi produk yang relevan dengan keyword "bola".

Namun karena data yang digunakan pada proyek ini tidak memiliki nama produk, maka akan diberikan contoh dengan keyword "product_3248". Diperoleh top 5 rekomendasi produk berdasarkan keyword tersebut:

Tabel 2. Top 5 rekomendasi dengan Content-Based Filtering

| product_id    | product_category_name | seller_id   | price   | review_score | sold |
| ----------    | --------------------- | ---------   | -----   | ------------ | ---- |
| product_2147  | bed_bath_table        | seller_319  | 107.50  | 5.0 | 1 |
| product_2348  | bed_bath_table        | seller_2250 | 34.99   | 4.0 | 1 |
| product_27122 | bed_bath_table        | seller_35   | 146.99  | 5.0 | 1 |
| product_19127 | bed_bath_table        | seller_1630 | 34.90   | 4.0 | 2 |
| product_29998 | bed_bath_table        | seller_2340 | 52.99   | 4.0 | 1 |

### 5.2. Collaborative Filtering
Digunakan model RecommerderNet berbasis TensorFlow untuk mempelajari pola preferensi pelanggan dan interaksi mereka dengan produk. Model ini menggunakan embedding untuk merepresentasikan pelanggan dan produk. Dengan menggabungkan embedding tersebut, kami dapat memprediksi preferensi pelanggan terhadap produk tertentu.

Berbeda dengan pendekatan *Content-Based Filtering* yang hanya menggunakan data informasi tentang produk saja, pendekatan ini akan menggunakan data pelanggan juga.

Dataset yang digunakan dibagi menjadi data traning dan data testing dengan rasio 80%:20%.

Kelebihan dari pendekatan ini adalah kemampuannya dalam menemukan pola preferensi pelanggan yang kompleks dan merekomendasikan produk berdasarkan preferensi serupa dari pelanggan lain. Namun kekurangan dari pendekatan ini adalah adanya masalah *cold-start*, yaitu saat pelanggan baru atau produk baru tidak memiliki cukup interaksi untuk memberikan rekomendasi yang akurat.

Output dari pendekatan ini adalah daftar produk rekomendasi untuk setiap pelanggan. Misalnya, pelanggan B akan menerima rekomendasi berupa daftar produk yang banyak disukai oleh pelanggan lain dengan preferensi yang serupa.

Tabel 3. Top 10 rekomendasi dari salah satu pengguna.

| product       | product_category_name    | seller_id     |
| -----------   | -----------------  | ---------   |
| product_9949  | furniture_decor    | seller_443  |
| product_5630 	| fixed_telephony    | seller_1043 |
| product_31762 | small_appliances   | seller_2915 |
| product_29040 | stationery         | seller_1787 |
| product_11817 | health_beauty      | seller_1210 |
| product_16087 | stationery         | seller_668  |
| product_21496 | fashion_bags_accessories | seller_1277 |
| product_7408 	| housewares         | seller_1815 |
| product_8130 	| baby               | seller_434  |
| product_9125 	| stationery         | seller_157  |

## 6. Evaluation
Setelah model berhasil dibuat, akan dilakukan evaluasi dengan menggunakan metrik evaluasi untuk memvalidasi performa model. 

### 6.1. Content-Based Filtering
Pada pendekatan Content-Based Filtering, akan digunakan metrik evaluasi *precision*.

*Precision* adalah metrik evaluasi yang digunakan untuk mengukur sejauh mana sistem rekomendasi mampu memberikan rekomendasi yang relevan dan tepat kepada pengguna. Precision menggambarkan persentase item rekomendasi yang relevan dari keseluruhan item yang direkomendasikan. Presisi dapat dihitung menggunakan rumus berikut:

$$ precision = {TP \over TP + FP} $$

dimana:
* TP (*True Positive*) : jumlah item rekomendasi yang relevan yang benar-benar dipilih oleh pengguna
* FP (*False Positive*) : jumlah item rekomendasi yang tidak relevan yang dipilih oleh pengguna.

Digunakan 3 pencarian produk secara acak, yaitu:
1. *"product_3248"*. Dari 20 rekomendasi yang diberikan semuanya relevan. Sehingga nilai presisinya 100%.
2. *"product_453"*. Dari 20 rekomendasi yang diberikan semuanya relevan. Sehingga nilai presisinya 100%.
3. *"product_31234"*. Dari 20 rekomendasi yang diberikan semuanya relevan. Sehingga nilai presisinya 100%.

Dari hasil pencarian produk di atas, diperoleh nilai akurasi 100% yang berarti semua hasil pencarian memperoleh rekomendasi yang relevan.

### 6.2. Collaborative Filtering
Pada pendekatan Collaborative Filtering, digunakan metrik evaluasi Root Mean Squared Error (RMSE). RMSE mengukur seberapa baik model Collaborative Filtering dalam memprediksi preferensi atau rating yang akan diberikan oleh pengguna pada item yang belum mereka sukai. RMSE mengukur perbedaan antara rating yang diprediksi oleh model dan rating yang sebenarnya oleh pengguna. Rumus untuk menghitung RMSE adalah sebagai berikut:

$$ RMSE = \sqrt{\sum ({\hat{y}i - yi})^{2} \over {n}} $$

dimana:
* y topi = rating prediksi
* y = rating sebenarnya
* n = jumlah data

Dengan proses training sebanyak 100 epochs, diperoleh nilai evaluasi sebagai berikut:
* *root_mean_squared_error* : 0.0427
* *val_root_mean_squared_error* : 0.3353

### 6.3. Analisis Hasil
Dari nilai metrik evaluasi terlihat model memiliki kemampuan rekomendasi yang baik. Terlebih pada pendekatan *content-based filtering* yang presisinya bisa mencapai 100% yang artinya produk yang direkomendasikan sangat relevan dengan produk yang sedang dicari. Ini juga menjadi kelebihan pendekatan *content-based filtering* yang bisa secara tepat memberikan rekomendasi barang yang spesifik. Namun kelemahannya adalah produk yang ditampilkan tidak luas, dengan kata lain, kita tidak akan menemukan produk lainnya yang tidak sesuai dengan *keyword* yang kita cari.

Namun untuk pendekatan *collaborative filtering*, memang terlihat bahwa produk yang direkomendasikan cukup campur-campur. Karena tujuan dari pendekatan ini tidak hanya mencari produk dengan kategori yang sama, tetapi juga kategori lainnya yang kemungkinan disukai oleh pengguna. Ini menjadi kelebihan pendekatan *collaborative filtering* yang bisa menemukan produk lain yang mungkin sebelumnya kita belum ketahui, tetapi mungkin kita akan menyukainya. Kelemahannya adalah rekomendasi yang diberikan bisa jadi sedikit *random* karena produk yang direkomendasikan adalah berdasarkan tren yang sedang disukai pengguna lain.

## 7. Conclusion
Sistem rekomendasi memberikan performa yang baik dengan pendekatan Content-Based Filtering maupun Collaborative Filtering.

Pada Content-Based Filtering, sistem berhasil memberikan nilai evaluasi precision hingga 100% pada contoh 3 pencarian produk yang diuji.

Pada Collaborative Filtering, diperoleh evaluasi RMSE pada data validasi sebesar 0.3353 dan ketika diuji kepada pengguna, produk yang direkomendasikan beragam berdasarkan tren dari pengguna lain yang memiliki historis minat yang sama.

## 8. Suggestion
Untuk membuat sistem rekomendasi ini lebih baik, dapat digunakan fitur-fitur yang lebih kompleks untuk membuat prediksi rekomendasi. Selain itu, dapat digunakan pula metode sistem rekomendasi yang lebih modern yang dapat membaca berbagai jenis fitur, seperti teks, gambar, hingga video.

## Referensi
[1] [X. Zhao, "A Study on E-commerce Recommender System Based on Big Data," 2019 IEEE 4th International Conference on Cloud Computing and Big Data Analysis (ICCCBDA), Chengdu, China, 2019, pp. 222-226, doi: 10.1109/ICCCBDA.2019.8725694.](https://ieeexplore.ieee.org/abstract/document/8725694)

[2] [Ruiqi Zheng, Liang Qu, Bin Cui, Yuhui Shi, and Hongzhi Yin. 2023. AutoML for Deep Recommender Systems: A Survey. ACM Trans. Inf. Syst. 41, 4, Article 101 (October 2023), 38 pages. https://doi.org/10.1145/3579355](https://dl.acm.org/doi/abs/10.1145/3579355)
