# Laporan Proyek Machine Learning - Muhafidz Ahmad Halim
## Project Overview
*E-commerce* adalah salah satu inovasi di era modern ini yang memiliki fungsi untuk membantu konsumen membeli barang-barang yang mereka butuhkan dengan mudah melalui gawai mereka. Selain membantu konsumen, *e-commerce* juga membantu banyak penjual dalam menjual barangnya dengan lebih mudah. Dengan *e-commerce*, penjual dapat menjual barang tidak hanya terbatas kepada konsumen di daerahnya saja, tetapi penjual dapat menjual produknya ke konsumen di seluruh dunia.

Saat ini telah banyak sekali barang-barang yang dijual di *e-commerce*. Tak jarang barang-barang tersebut terdapat barang yang dijual oleh seorang penipu yang dapat merugikan konsumen. Oleh karena itu, pemilik *platform e-commerce* perlu memberikan rasa aman dan rasa nyaman kepada para konsumen dengan memfilter barang-barang yang direkomendasikan kepada user.

Selain itu, pemilik e-commerce juga perlu sebuah sistem rekomendasi yang dapat merekomendasikan barang yang sesuai dengan yang pembeli butuhkan atau pembeli inginkan. Hal ini bertujuan untuk memberikan kemudahan kepada pengguna, dan tentunya meningkatkan *trafic* dan transaksi di platform *e-commerce* tersebut.

Sistem rekomendasi di *ecommerce* telah beberapa kali dilakukan penelitian, terutama dengan yang berdasarkan big data [1]. Salah satu penelitian terbaru dalam pengembangan sistem rekomendasi ini adalah dengan menggunakan *AutoML* [2].

## Business Understanding
### Problem Statements
Banyaknya produk pilihan di *e-commerce* menjadi kelebihan sekaligus hambatan ketika belanja. Dengan banyaknya pilihan, tentu konsumen ingin mendapatkan pilihan produk yang tepat dan relevan dengan preferensi mereka. Namun konsumen mungkin saja tidak memiliki banyak waktu untuk menjelajah seluruh produk-produk yang ada di *platform e-commerce*. 

Tujuan dari proyek ini adalah mengembangkan sistem rekomendasi produk e-commerce. Masalah yang ingin diselesaikan adalah bagaimana memberikan rekomendasi produk yang relevan dan personal kepada konsumen, sehingga meningkatkan kepuasan konsumen dan memperoleh peningkatan penjualan.

### Goals
* Memberikan sistem rekomendasi produk yang relevan dengan preferensi pengguna.
* Mengoptimalkan pemanfaatan data pelanggan dan produk yang ada dalam platform e-commerce.

### Solution Approach
Untuk mencapai tujuan di atas, akan digunakan dua pendekatan dalam sistem rekomendasi kami, yaitu:
1. *Content-Based Filtering*, yang dapat memberikan rekomendasi produk yang memiliki kesamaan konden dengan produk yang disukai atau dicari oleh konsumen.
2. *Collaborative Filtering*, yang dapat memberikan rekomendasi berdasarkan preferensi konsumen atau pelanggan yang mirip.

## Data Understanding
Data yang akan digunakan untuk project ini adalah data dari Kaggle yang berisi merupakan data informasi *custumer*, produk, dan *review* dari salah satu platform *e-commerce* bernama *Olist*. Data dapat diunduh melalui [tautan berikut].(https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). Data ini telah diproses oleh *publisher* sehingga data ini tidak mengambil privasi konsumen maupun penjual dari *e-commerce* tersebut.

Dataset ini terdiri dari 9 skema dataset, diantaranya:

![image](https://github.com/muhafidz-ahmad/ecommerce-product-recommender-system/assets/115754250/426dec64-f6c4-4df4-8f1d-fd7f945f1e91)
Gambar 1. Skema dataset *e-commerce Olist*

1. olist_customers_dataset.csv
  * customer_id: id unik pelanggan
  * customer_unique_id: id unik pelanggan (anonim)
  * customer_zip_code_prefix: kode pos pelanggan
  * customer_city: kota pelanggan
  * customer_state: negara bagian pelanggan
2. olist_geolocation_dataset.csv
  * geolocation_zip_code_prefix: kode pos lokasi
  * geolocation_lat: latitude lokasi
  * geolocation_lng: longitude lokasi
  * geolocation_city: kota lokasi
  * geolocation_state: negara bagian lokasi
3. olist_order_items_dataset.csv
  * order_id: id unik pesanan
  * order_item_id: id unik item pesanan
  * product_id: id unik produk
  * seller_id: id unik penjual
  * shipping_limit_date: tanggal batas pengiriman
  * price: harga produk
  * freight_value: harga pengiriman
4. olist_order_payments_dataset.csv
  * order_id: id unik pesanan
  * payment_sequential: urutan pembayaran dalam satu pesanan
  * payment_type: jenis pembayaran (boleto atau kartu kredit)
  * payment_installments: jumlah cicilan pembayaran
  * payment_value: nilai pembayaran
5. olist_order_reviews_dataset.csv
  * review_id: id unik ulasan
  * order_id: id unik pesanan
  * review_score: skor ulasan dengan range dari 1 sampai 5
  * review_comment_title: judul ulasan dari customer dalam bahasa portugis
  * review_creation_date: tanggal dibuatnya ulasan
  * review_answer_timestamp: menunjukkan stempel waktu jawaban survei kepuasan
6. olist_orders_dataset.csv
  * order_id: id unik pesanan
  * customer_id: id unik pelanggan
  * order_status: status pesanan (dibayar, dikirim, selesai)
  * order_purchase_timestamp: waktu pembelian pesanan oleh pelanggan (UTC)
  * order_approved_at: waktu persetujuan pesanan oleh penjual (UTC)
  * order_delivered_carrier_date: waktu pengiriman oleh kurir (UTC)
  * order_delivered_customer_date: waktu pengiriman ke pelanggan (UTC)
  * order_estimated_delivery_date: waktu estimasi pengiriman ke pelanggan (UTC)
7. olist_products_dataset.csv
  * product_id: id unik produk
  * product_category_name: nama kategori produk dalam bahasa portugis
  * product_name_length: jumlah karakter yang diekstrak dari nama produk
  * product_description_length: jumlah karakter yang diekstrak dari deskripsi produk
  * product_photos_qty: jumlah foto produk yang dipublish
  * product_weight_g: berat produk dalam satuan gram
  * product_length_cm: ukuran panjang produk dalam satuan cm
  * product_height_cm: ukuran tinggi produk dalam satuan cm
  * product_width_cm: ukuran leabr produk dalam satuan cm
8. olist_sellers_dataset.csv:
  * seller_id: id unik penjual
  * seller_zip_code_prefix: kode pos penjual
  * seller_city: kota penjual
  * seller_state: negara bagian penjual
9. product_category_name.csv
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

### Exploratory Data Analysis
Pada dataset *olist_order_customers_dataset.csv* (selanjutnya akan ditulis dataset customer) memiliki kolom kode pos, kota, dan negara bagian dari konsumen. Namun pada proyek ini, hanya akan digunakan informasi kota konsumen saja. Sehingga datset customer ini tersisa 3 kolom, yaitu *customer_id*, *customer_unique_id*, dan *customer_city*. Masing-masing kolom tersebut memiliki jumlah nilai unik sebagai berikut:
* *customer_id* : 99441 nilai unik
* *customer_unique_id* : 96096 nilai unik
* *customer_city* : 4119 nilai unik

Kemudian pada dataset *olist_order_items_dataset.csv* (selanjutnya akan ditulis dataset order item) memiliki total 6 kolom, dengan jumlah nilai unik sebagai berikut:
* *order_id* : 98666 nilai unik
* *order_item_id* : 21 nilai unik
* *product_id* : 32951 nilai unik
* *seller_id* : 3095 nilai unik
* *price* : 5968 nilai unik
* *freight_value* : 6999 nilai unik
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
Skor review yang ada pada dataset ini adalah dalam rentang 1 sampai dengan 5.

Keempat, pada dataset *olist_orders_dataset.csv* (selanjutnya akan dituis dataset orders) memiliki 8 kolom dengan cukup banyak nilai yang hilang pada kolom *order_approved_at*, *order_delivered_carrier_date*, dan *order_delivered_customer_date* karena bisa saja kondisi ketika data ini diambil, terdapat status pembelian yang menyebabkan data pada kolom tersebut masih kosong. Namun untungmya, kolom tersebut tidak terpakai untuk membuat sistem rekomendasi, sehingga akan dihapus. Kemudian, untuk membuat sistem rekomendasi pada proyek ini juga hanya akan menggunakan data dengan status order sudah selesai atau *delivered*.

Kelima, dataset *olist_seller_dataset.csv* (selanjutnya akan ditulis dataset seller) kondisinya sudah sangat bersih. Sama seperti dataset customer, informasi seller juga hanya akan menggunakan informasi kota saja. Adapun nilai unik pada kolom dataset seller ini adalah:
* *seller_id* : 3095 nilai unik
* *seller_city* : 611 nilai unik

Terakhir, dataset *olist_products_dataset.csv* yang berisi data informasi produk dan *product_category_name_translation.csv* sebagai kamus nama kategori produk dari Bahasa Portugis ke Bahasa Inggris. Sayangnya, dataset produk ini tidak memiliki nama produk dan deskripsi produk yang eksplisit. Sehingga sistem rekomendasi yang akan dibuat akan digunakan *product_id* untuk menunjukan produk tertentu. Terdapat 73 kategori produk pada dataset ini.

## Data Preparation
Persiapan data akan dimulai dari data preprocessing, untuk mempermudah dalam pembuatan membaca nama produk dan seller karena nama produk dan seller tidak tersedia.
### Data Preprocessing

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

### Data Preparation
Dari hasil *preprocessing* di atas, diperoleh dataset *products* yang akan digunakan untuk membuat sistem rekomendasi. Dataset ini memiliki total 6 kolom sebagai berikut:
* product_id
* product_category_name
* price
* review_score
* sold
* seller_id

Terdapat nilai yang hilang pada *review_score*. Nilai yang kosong tersebut akan diganti dengan nilai 0 agar bisa dimasukan ke dalam perhitungan sistem rekomendasi.

## Model Development
Proyek ini menyajikan dua solusi rekomendasi dengan menggunakan algoritma yang berbeda, yaitu *Content-Based Filtering* dan *Collaborative Filtering*.

### Content-Based Filtering
Dalam pendekatan ini, digunakan metode TF-IDF dan Cosine Similarity untuk memperoleh rekomendasi yang relevan. Pertama, dilakukan pemrosesan teks pada kategori produk untuk menghasilkan matriks TF-IDF yang merupakan representasi numerik hubungan antara kategori produk dengan nama produk. Kemudian dihitung *cosine similarity* dari matriks TF-IDF dan menghasilkan *matrix similarity* yang merupakan representasi numerik kesamaan antar produk.

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

### Collaborative Filtering
Digunakan model RecommerderNet berbasis TensorFlow untuk mempelajari pola preferensi pelanggan dan interaksi mereka dengan produk. Model ini menggunakan embedding untuk merepresentasikan pelanggan dan produk. Dengan menggabungkan embedding tersebut, kami dapat memprediksi preferensi pelanggan terhadap produk tertentu.

Berbeda dengan pendekatan *Content-Based Filtering* yang hanya menggunakan data informasi tentang produk saja, pendekatan ini akan menggunakan data pelanggan juga.

Dataset yang digunakan dibagi menjadi data traning dan data testing dengan rasio 80%:20%.

Kelebihan dari pendekatan ini adalah kemampuannya dalam menemukan pola preferensi pelanggan yang kompleks dan merekomendasikan produk berdasarkan preferensi serupa dari pelanggan lain. Namun kekurangan dari pendekatan ini adalah adanya masalah *cold-start*, yaitu saat pelanggan baru atau produk baru tidak memiliki cukup interaksi untuk memberikan rekomendasi yang akurat.

Output dari pendekatan ini adalah daftar produk rekomendasi untuk setiap pelanggan. Misalnya, pelanggan B akan menerima rekomendasi berupa daftar produk yang banyak disukai oleh pelanggan lain dengan preferensi yang serupa.

Berikut ini adalah contoh top 10 rekomendasi dari salah satu pengguna.

1. product_9949 	: furniture_decor | seller_443
2. product_5630 	: fixed_telephony | seller_1043
3. product_31762 	: small_appliances | seller_2915
4. product_29040 	: stationery | seller_1787
5. product_11817 	: health_beauty | seller_1210
6. product_16087 	: stationery | seller_668
7. product_21496 	: fashion_bags_accessories | seller_1277
8. product_7408 	: housewares | seller_1815
9. product_8130 	: baby | seller_434
10. product_9125 	: stationery | seller_157

## Evaluation
Pada pendekatan Content-Based Filtering, akan dilihat hasil dari hasil rekomendasi pada contoh di subbab sebelumnya. Contoh di atas adalah mencari rekomendasi produk dengan keyword *"product_3248"*. Dimana product tersebut memiliki kategori *bed_bath_table*, penjual *seller_2174*, harga 24.9, skor review 3.9, dan jumlah terjual sebanyak 7 buah. Hasil rekomendasi dari *keyword* di atas diperoleh 5 rekomendasi dengan kategori produk yang sama. Sistem rekomendasi dengan Content-Based Filtering sudah berjalan dengan baik.

Pada pendekatan Collaborative Filtering, digunakan metrik evaluasi Root Mean Squared Error (RMSE). RMSE mengukur seberapa baik model Collaborative Filtering dalam memprediksi preferensi atau rating yang akan diberikan oleh pengguna pada item yang belum mereka sukai. RMSE mengukur perbedaan antara rating yang diprediksi oleh model dan rating yang sebenarnya oleh pengguna. Rumus untuk menghitung RMSE adalah sebagai berikut:

$$ RMSE = \sqrt{\sum_{i=1}^{n} {\hat{y}i - yi}}^{2} \over {n}} $$

Dengan proses training sebanyak 100 epochs, diperoleh nilai evaluasi sebagaim berikut:
* *root_mean_squared_error* : 0.0427
* *val_root_mean_squared_error* : 0.3353

## Conclusion


## Referensi
[1] [X. Zhao, "A Study on E-commerce Recommender System Based on Big Data," 2019 IEEE 4th International Conference on Cloud Computing and Big Data Analysis (ICCCBDA), Chengdu, China, 2019, pp. 222-226, doi: 10.1109/ICCCBDA.2019.8725694.](https://ieeexplore.ieee.org/abstract/document/8725694)

[2] [Ruiqi Zheng, Liang Qu, Bin Cui, Yuhui Shi, and Hongzhi Yin. 2023. AutoML for Deep Recommender Systems: A Survey. ACM Trans. Inf. Syst. 41, 4, Article 101 (October 2023), 38 pages. https://doi.org/10.1145/3579355](https://dl.acm.org/doi/abs/10.1145/3579355)
