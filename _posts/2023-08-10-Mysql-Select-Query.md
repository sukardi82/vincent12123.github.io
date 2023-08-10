---
layout: post
title: Materi Mysql 
toc: true
categories: [RPL XI]
tags: [Mysql, Query]
---

# BAB 1 Statemen SELECT

Statemen SELECT digunakan untuk mengambil data dari database. Statemen ini merupakan statemen utama SQL karena sebagian besar query yang kita lakukan adalah pengambilan data, disamping itu statemen ini memiliki variasi paling banyak dibanding statemen lain seperti INSERT dan UPDATE.
Pada BAB ini kita akan membahas syntax dasar statemen SELECT beserta variasinya, dengan memahami topik ini, Anda akan dapat dengan mudah memahami pembahasan pada bab bab berikutnya.

## 1.1. Syntax Statemen SELECT

Statemen `SELECT` memiliki struktur sebagai berikut:

```sql
SELECT ... 
FROM ... 
[WHERE ...] 
[GROUP BY ...] 
[ORDER BY ...] 
[HAVING ...] 
[LIMIT ...] 
```

Penulisan klausa diatas harus urut mulai dari atas ke bawah. Keyword SELECT dan FROM wajib ada, sedangkan keyword lain (yang ada didalam tanda kurung siku [] ) bersifat opsional.
Contoh penggunaan statemen SELECT: misal kita memiliki tabel mhs dengan data sebagai berikut:

| nim | nama    | jenis_kelamin | kd_jurusan |
| --- | ------- | ------------- | ---------- |
| 001 | Alfa    | L             | J002       |
| 002 | Beta    | P             | J002       |
| 003 | Charlie | P             | J001       |
| 004 | Delta   | L             | J001       |
| 005 | Erdhi   | L             | J001       |
| 006 | Farah   | P             | J002       |
| 007 | Gisel   | P             | J002       |
| 008 | Haris   | L             | NULL       |

Untuk mengambil semua kolom, kita gunakan tanda asterik (*) misal:

```sql
SELECT * FROM mhs 
```

Hasil:

| nim | nama    | jenis_kelamin | kd_jurusan |
| --- | ------- | ------------- | ---------- |
| 001 | Alfa    | L             | J002       |
| 002 | Beta    | P             | J002       |
| 003 | Charlie | P             | J001       |
| 004 | Delta   | L             | J001       |
| 005 | Erdhi   | L             | J001       |
| 006 | Farah   | P             | J002       |
| 007 | Gisel   | P             | J002       |
| 008 | Haris   | L             | NULL       |

Untuk menampilkan kolom tertentu, kita tulis nama kolom tersebut pada klausa `SELECT`, misal:

```sql
SELECT nama, jenis_kelamin FROM mhs; 
```

Hasil

| nama    | jenis_kelamin |
| ------- | ------------- |
| Alfa    | L             |
| Beta    | P             |
| Charlie | P             |
| Delta   | L             |
| Erdhi   | L             |
| Farah   | P             |
| Gisel   | P             |
| Haris   | L             |

Usahakan hanya mengambil kolom yang diperlukan, hindari penggunaan asterik. Hal ini merupakan "Best Practice" untuk meningkatkan efisiensi performa sql.

`WHERE`
Klausa `WHERE` digunakan untuk memfilter data yang ingin diambil, misal kita akan mengambil data siswa dengan jenis kelamin laki-laki, query yang kita jalankan adalah sebagai berikut:

```sql
SELECT nama, jenis_kelamin  
FROM mhs 
WHERE jenis_kelamin = "L" 
```

Hasil:

| nama  | jenis_kelamin |
| ----- | ------------- |
| Alfa  | L             |
| Delta | L             |
| Erdhi | L             |
| Haris | L             |

Ketika menjalankan klausa `WHERE`, MySQL akan memeriksa baris pada tabel satu persatu sehingga pada tabel dengan jumlah baris banyak, proses ini akan memakan waktu cukup lama, untuk mengatasinya, gunakan teknik indexing (penggunaan index) - tidak di bahas pada buku ini-.

`GROUP BY`
GROUP BY digunakan untuk mengelompokkan baris berdasarkan kolom tertentu.

Penggunaan keyword ini selalu bersamaan dengan fungsi agregsi seperti `COUNT, SUM, MIN, MAX, dan AVG`

Contoh:

```sql
SELECT kd_jurusan, COUNT(kd_jurusan)  
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan 
```

Pada contoh diatas, data dihitung (fungsi `COUNT`) dan dikelompokkan berdasarkan kolom kd_jurusan. Jika Anda belum paham mengenai fungsi `COUNT`, tidak usah khawatir, kita akan membahasnya secara detail pada bab berikutnya.

Penting diperhatikan bahwa sebelum menjalankan `GROUP BY`, terlebih dahulu MySQL akan mengurutkan data pada kolom yang ada pada klausa GROUP BY secara ascending, (hal ini penting untuk diingat)

Sebagai contoh, jika kita jalankan query diatas, maka hasil yang kita peroleh adalah:

| kd_jurusan | COUNT(kd_jurusan) |
| ---------- | ----------------- |
| NULL       | 0                 |
| J001       | 2                 |
| J002       | 1                 |

Pada tabel diatas terlihat bahwa data diurutkan berdasarkan kolom kd_jurusan secara ascending

`ORDER BY`
Keyword ORDER BY digunakan untuk mengurutkan data baik secara ascending (dari kecil ke besar) maupun descending (dari besar ke kecil)

Keyword ini akan dijalankan setelah MySQL menjalankan klausa GROUP BY (jika ada) yang artinya setelah data dikelompokkan, contoh:

```sql
SELECT kd_jurusan, COUNT(kd_jurusan)  
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan 
ORDER BY kd_jurusan DESC 
```

Hasil:

| kd_jurusan | COUNT(kd_jurusan) |
| ---------- | ----------------- |
| J002       | 1                 |
| J001       | 2                 |
| NULL       | 0                 |

Pada contoh diatas, data diurutkan berdasarkan kolom kd_jurusan secara descending (dari besar ke kecil). Jika ingin diurutkan secara ascending, hilangkan keyword DESC atau ganti dengan ASC
Selain bersama dengan **GROUP BY**, keyword ORDER BY juga dapat digunakan tanpa GROUP BY, misal:

```sql
SELECT nama, jenis_kelamin```
FROM mhs
ORDER BY nama
```

Hasil:

| nama    | jenis_kelamin |
| ------- | ------------- |
| Alfa    | L             |
| Beta    | P             |
| Charlie | P             |
| Delta   | L             |
| Erdhi   | L             |
| Farah   | P             |
| Gisel   | P             |
| Haris   | L             |

Pada contoh diatas, data diurutkan berdasarkan kolom nama secara ascending.
Dengan ORDER BY, kita dapat mengurutkan data dengan kriteria lebih dari satu kolom, misal:

```sql
SELECT nama, jenis_kelamin 
FROM mhs 
ORDER BY jenis_kelamin, nama
```

Hasil:

| nama    | jenis_kelamin |
| ------- | ------------- |
| Alfa    | L             |
| Delta   | L             |
| Erdhi   | L             |
| Haris   | L             |
| Beta    | P             |
| Charlie | P             |
| Farah   | P             |
| Gisel   | P             |

Pada contoh diatas, data diurutkan secara ascending berdasarkan kolom jenis_kelamin, selanjutnya pada jenis kelamin yang sama, data pada kolom nama diurutkan secara ascending.
Untuk mengubah menjadi descending, kita dapat menambahkan keyword DESC pada masing masing kolom, misal:

```sql
SELECT nama, jenis_kelamin 
FROM mhs 
ORDER BY jenis_kelamin DESC, nama DESC
```

Hasil:

| nama    | jenis_kelamin |
| ------- | ------------- |
| Gisel   | P             |
| Farah   | P             |
| Charlie | P             |
| Beta    | P             |
| Haris   | L             |
| Erdhi   | L             |
| Delta   | L             |
| Alfa    | L             |

`HAVING`
Keyword having sama seperti keyword WHERE, bedanya HAVING dapat dijalankan setelah klausa GROUP BY sedangkan WHERE tidak, contoh:

```sql
SELECT kd_jurusan, COUNT(kd_jurusan)  
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan 
HAVING kd_jurusan = "J002" 
```

Hasil:

| kd_jurusan | COUNT(kd_jurusan) |
| ---------- | ----------------- |
| J002       | 1                 |

Having dijalankan setelah tabel diolah sehingga kita dapat menggunakannya untuk memfilter data hasil olahan, misal:

```sql
SELECT kd_jurusan, COUNT(kd_jurusan) AS jml_mhs 
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan 
HAVING jml_mhs > 0 
 
```

Hasil:

| kd_jurusan | COUNT(kd_jurusan) |
| ---------- | ----------------- |
| J001       | 2                 |
| J002       | 1                 |

`LIMIT`
Keyword LIMIT digunakan untuk membatasi jumlah baris yang ingin ditampilkan, misal:

```sql
SELECT nama, jenis_kelamin  
FROM mhs 
LIMIT 5; 
```

Hasil:

| nama    | jenis_kelamin |
| ------- | ------------- |
| Alfa    | L             |
| Beta    | P             |
| Charlie | P             |
| Delta   | L             |
| Erdhi   | L             |

Pada contoh diatas, data diambil 5 teratas. Secara default LIMIT akan menghitung data mulai dari baris pertama, kita dapat menentukan mulai baris keberapa data diambil dengan menambahkan parameter offset, misal:

```sql
 SELECT nama, jenis_kelamin  
FROM mhs 
LIMIT 3, 5; 

```

Hasil:

| nama  | jenis_kelamin |
| ----- | ------------- |
| Delta | L             |
| Erdhi | L             |
| Farah | P             |
| Gisel | P             |
| Haris | L             |

Pada contoh query diatas, nilai offsetnya adalah 3. Penghitungan offset dimulai dari 0, sehingga, pada contoh diatas, karena kita mengambil sebanyak 5 data dan dimulai dari offset ke 3 (LIMIT 3, 5) maka data diambil mulai data ke-4, jika ingin mengambil mulai dari data pertama, gunakan offset 0 (LIMIT 0, 5) ataucukup ditulis LIMIT 5

## 1.2. Operator Aritmetika

Kolom pada klausa SELECT dapat diisi berbagai nilai termasuk ekspresi dengan operasi aritmetika seperti (x, /, + , dan - ), misal kita memiliki tabel penjualan_detail dengan data sebagai berikut:

| id  | id_trx | id_barang | qty | harga_satuan | diskon |
| --- | ------ | --------- | --- | ------------ | ------ |
| 1   | 1      | 9         | 1   | 46800        | 0      |
| 2   | 1      | 4         | 1   | 34800        | 0      |
| 3   | 1      | 6         | 2   | 33800        | 0.1    |
| 4   | 2      | 9         | 1   | 46800        | 0      |
| 5   | 2      | 10        | 2   | 39800        | 0      |

Selanjutnya kita tampilkan data id_barang, qty, dan harga_satuan selain itu kita tampilkan data sub_total dengan mengalikan nilai pada kolom qty dengan harga_satuan. Query yang kita jalankan:

```sql
 SELECT id, qty, harga_satuan, qty * harga_satuan AS sub_total  
FROM penjualan_detail 
```

Hasil yang kita peroleh:

| id  | qty | harga_satuan | sub_total |
| --- | --- | ------------ | --------- |
| 1   | 1   | 46800        | 46800     |
| 2   | 1   | 34800        | 34800     |
| 3   | 2   | 33800        | 67600     |
| 4   | 1   | 46800        | 46800     |
| 5   | 2   | 39800        | 79600     |

Pada query diatas, pada klausa SELECT terdapat keyword AS. Keyword ini digunakan untuk memberi nama alias pada kolom, yang pada contoh diatas, nama kolom menjadi sub_total. Jika tidak menggunakan kolom alias, maka nama kolom adalah qty * harga_satuan

Kolom alias dapat ditulis dengan atau tanpa keyword AS, jika tanpa keyword AS, pemberian nama kolom alias cukup diberi jarak spasi, misal: qty * harga_satuan sub_total. Saya sendiri lebih memilih menggunakan keyword AS karena mudah diidentifikasi terutama pada query yang kompleks.  

Selanjutnya kita tambahkan diskon untuk mendapatkan nilai sub_total dengan formula qty x harga_satuan – diskon. Query yang kita jalankan

```sql
 SELECT id, qty, harga_satuan 
 , qty * harga_satuan AS sub_total 
 , diskon 
 , qty * harga_satuan * diskon AS nilai_diskon 
 , qty * harga_satuan - ( qty * harga_satuan * diskon ) AS neto  
FROM penjualan_detail 
```

Hasil yang kita peroleh:

| id  | qty | harga_satuan | sub_total | diskon | nilai_diskon     | neto              |
| --- | --- | ------------ | --------- | ------ | ---------------- | ----------------- |
| 1   | 1   | 46800        | 46800     | 0      | 0                | 46800             |
| 2   | 1   | 34800        | 34800     | 0      | 0                | 34800             |
| 3   | 2   | 33800        | 67600     | 0.1    | 6760.00010073185 | 60839.99989926815 |
| 4   | 1   | 46800        | 46800     | 0      | 0                | 46800             |
| 5   | 2   | 39800        | 79600     | 0      | 0                | 79600             |

Pada contoh diatas, kolom nilai_diskon dan neto memiliki nilai desimal (nilai di belakang koma) yang cukup panjang, untuk itu kita perlu menyederhanakannya menggunakan fungsi ROUND, kita ubah query nya menjadi:

```sql
 SELECT id, qty, harga_satuan 
 , qty * harga_satuan AS sub_total 
 , diskon 
 , ROUND(qty * harga_satuan * diskon) AS nilai_diskon 
 , ROUND(qty * harga_satuan - ( qty * harga_satuan * diskon )) AS neto  
FROM penjualan_detail 
```

Hasil yang kita peroleh:

| id  | qty | harga_satuan | sub_total | diskon | nilai_diskon | neto  |
| --- | --- | ------------ | --------- | ------ | ------------ | ----- |
| 1   | 1   | 46800        | 46800     | 0      | 0            | 46800 |
| 2   | 1   | 34800        | 34800     | 0      | 0            | 34800 |
| 3   | 2   | 33800        | 67600     | 0.1    | 6760         | 60840 |
| 4   | 1   | 46800        | 46800     | 0      | 0            | 46800 |
| 5   | 2   | 39800        | 79600     | 0      | 0            | 79600 |

Ketika menggunakan operator aritmetika, jika diperlukan tambahkan tanda kurung, terutama jika melibatkan operator plus atau minus (+ -) dengan kali atau bagi (* /). Dengan tanda kurung, ekspresi yang ada di dalam tanda kurung akan di eksekusi terlebih dahulu.

## 1.3.  Operator Perbandingan

Operator perbandingan digunakan untuk membandingkan dua nilai atau ebih. Operator ini sering digunakan pada klausa WHERE.
Operator perbangingan yang sering digunakan adalah sama dengan ( = ) dan tidak sama dengan ( != ). Pada contoh sebelumnya kita telah menggunakan operator ini untuk mengambil data mahasiswa dengan jenis kelamin Laki Laki:

```sql
 SELECT nama, jenis_kelamin 
FROM mhs 
WHERE jenis_kelamin = "L" 
```

Selain sama dengan dan tidak sama dengan, kita juga dapat menggunakan operator > (lebih besar), < (lebih kecil), >= (lebih besar atau sama dengan), <= (lebih kecil atau sama dengan)

## 1.4.  Nilai NULL

Dalam database, terdapat nilai dengan perlakuan khusus yaitu NULL, nilai ini tidak sama dengan bilangan 0 maupun string kosong ''.  
Dalam dunia database, NULL diartikan sebagai ketiadaan data / data tidak terdefinisi, sehingga untuk mengujinya kita tidak dapat menggunakan operator apapun seperti: nama_kolom = NULL
Untuk menguji nilai NULL, kita hanya bisa menggunakan IS NULL dan IS NOT NULL, misal kita memiliki data tabel mahasiswa sebagai berikut:

| nim | nama    | jenis_kelamin | kd_jurusan |
| --- | ------- | ------------- | ---------- |
| 001 | Alfa    | L             | J002       |
| 002 | Beta    | P             | J002       |
| 003 | Charlie | P             | J001       |
| 004 | Delta   | L             | J001       |
| 005 | Erdhi   | L             | J001       |
| 006 | Farah   | P             | J002       |
| 007 | Gisel   | P             | J002       |
| 008 | Haris   | L             | NULL       |

Selanjutnya kita ambil data mahasiswa dengan kd_jurusan NULL

```sql
 SELECT *  
FROM mhs 
WHERE kd_jurusan IS NULL 
```

Hasil:

| nim | nama  | jenis_kelamin | kd_jurusan |
| --- | ----- | ------------- | ---------- |
| 008 | Haris | L             | NULL       |

Sebaliknya, jika ingin mengambil data mahasiswa yang telah memilih jurusan, yang artinya kolom kd_jurusan tidak bernilai NULL, maka tinggal kita ubah klausa WHERE menjadi WHERE kd_jurusan IS NOT NULL
Contoh lainnya ketika kita menggunakan keyword HAVING, misal melanjutnya pembahasan pada klausa GROUP BY

```sql
SELECT kd_jurusan, COUNT(kd_jurusan) AS jml_mahasiswa 
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan 
```

Hasil:

| kd_jurusan | jml_mahasiswa |
| ---------- | ------------- ||
| NULL       | 0             |
| J001       | 2             |
| J002       | 1             |

Selanjutnya kita ingin menampilkan kd_jurusan yang tidak memiliki nilai NULL

```sql
 SELECT kd_jurusan, COUNT(kd_jurusan) AS jml_mahasiswa 
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan 
HAVING kd_jurusan IS NOT NULL 
```

Hasil:

| kd_jurusan | jml_mahasiswa |
| ---------- | ------------- |
| J001       | 2             |
| J002       | 1             |

Jika kita ingin menampilkan hanya kd_jurusan yang memiliki nilai NULL, maka kita tinggal ubah klausa HAVING menjadi HAVING kd_jurusan IS NULL
1.5. Operator OR dan AND
Ketika mengevaluasi nilai pada tabel menggunakan klausa WHERE atau HAVING, maka kita dapat menggunakan operator logika (AND dan OR)
Pada operator OR, kondisi bernilai benar (true) jika salah satu kondisi bernilai true, misal:

```sql
 SELECT kd_jurusan, nama, jenis_kelamin 
FROM mhs 
WHERE kd_jurusan = "J001" OR kd_jurusan IS NULL 
```

Hasil:

| kd_jurusan | nama    | jenis_kelamin |
| ---------- | ------- | ------------- |
| J001       | Charlie | P             |
| J001       | Delta   | L             |
| J001       | Erdhi   | L             |
| NULL       | Haris   | L             |

Pada contoh diatas, mahasiswa yang memiliki kd_jurusan 001 atau kd_jurusan bernilai NULL akan ditampilkan (salah satu bernilai true baik kd_jurusan bernilai 001 atau kd_jurusan bernilai  NULL). Agar lebih jelas, perhatikan ilustrasi berikut:

Gambar 1.1 Ilustrasi Operator Logika OR
Ingat kembali bahwa ketika menjalankan klausa WHERE, maka baris pada tabel akan di evaluasi satu per satu, seperti pada gambar diatas.  
Pada operator AND, kondisi bernilai true, jika keduanya bernilai true, contoh:

```sql
 SELECT kd_jurusan, nama, jenis_kelamin 
FROM mhs 
WHERE kd_jurusan = "J001" AND jenis_kelamin = "L" 
```

Hasil:

| kd_jurusan | nama | jenis_kelamin |
| ---------- | ---- | ------------- ||
| J001       | Delta | L             |
| J001       | Erdhi | L             |

Pada contoh diatas, hanya mahasiswa yang memiliki kd_jurusan J001 dan jenis_kelamin L yang akan ditampilkan, (keduanya bernilai true) untuk alur logikanya mirip dengan ilustrasi
gambar I.1
Prioritas
Ketika orator OR dan AND digunakan secara bersama sama, maka operator AND memiliki prioritas lebih tinggi sehingga akan dievaluasi terlebih dahulu, sehingga jika tidak hati hati, bisa jadi hasil yang kita peroleh  tidak sesuai yang kita harapkan.
Misal kita akan menampilkan semua data siswa wanita dengan kd_jurusan NULL atau kd_jurusan J001
Bagaimana klausa WHERE nya?
Umumnya kita akan menulis begini:

```sql
 SELECT kd_jurusan, nama, jenis_kelamin 
FROM mhs 
WHERE kd_jurusan IS NULL OR kd_jurusan = "J001" AND jenis_kelamin = "P" 
```

Hasil yang kita peroleh:

| kd_jurusan | nama    | jenis_kelamin |
| ---------- | ------- | ------------- |
| J001       | Charlie | P             |
| NULL       | Haris   | L             |

Apakah sudah benar?
Yup, ternyata mahasiswa dengan jenis kelamin L tetap ditampilkan, padahal kita ingin menampilkan hanya mahasiswa perempuan (P), kenapa bisa seperti itu?

Hal ini karena **operator AND akan dievaluasi terlebih dahulu, sehingga pertama tama MySQL akan mencari data dengan kd_jurusan 001 dan jenis_kelamin P (  kd_jurusan = "J001" AND jenis_kelamin = "P" ) yang menghasilkan baris pertama, kemudian mencari semua mahasiswa yang memiliki kd_jurusan NULL (kd_jurusan IS NULL) yang menghasilkan baris ke dua.**

Bagaimana mengatasinya?

Untuk mengatasinya, **gunakan tanda kurung pada operator yang ingin didahulukan, yang dalam hal ini adalah operator OR, ingat prinsip bahwa semua yang ada didalam tanda kurung akan di evaluasi terlebih dahulu.**
Kita ubah querynya menjadi:

```sql
SELECT kd_jurusan, nama, jenis_kelamin 
FROM mhs 
WHERE (kd_jurusan IS NULL OR kd_jurusan = "J001") AND jenis_kelamin = "P" 
```

Hasil:

| kd_jurusan | nama    | jenis_kelamin |
| ---------- | ------- | ------------- |
| J001       | Charlie | P             |

Semua yang ada di dalam tanda kurung akan di eksekusi terlebih dahulu, baik operator, fungsi, ekspresi dll.

Selalu gunakan tanda kurung ketika menggunakan operator OR dan AND secara bersama sama.

# BAB 2  Kunci Menguasai SELECT

Seperti telah disampaikan pada awal bab ini, statemen SELECT merupakan statemen yang paling rumit dan kompleks karena variasinya sangat banyak sekali.
Namun demikian, seberapapun rumitnya kasus yang Anda hadapi, Anda akan mampu memecahkannya jika Anda menguasai konsep bagaimana statemen SELECT dieksekusi.
Dalam internal database, eksekusi statemen SELECT membutuhkan proses yang rumit, banyak yang akan dipertimbangkan, terutama jika query yang dieksekusi bentuknya kompleks  
Pada BAB ini akan kita membahas konsep eksekusi ini. Konsep ini tidak mencerminkan 100% cara MySQL menangani statemen SELECT namun akan dapat memudahkan Anda memecahkan berbagai masalah pengambilan data.
N.B. konsep yang disampaikan disini merupakan hasil penelitian saya pribadi sehingga mungkin berbeda dengan yang ada di referensi lain.

## 2.1 Memahami Urutan Eksekusi

Hal terpenting yang pertama harus dipahami adalah memahami urutan eksekusi statemen SELECT.

Hal ini sangat penting karena akan memudahkan kita untuk mendapatkan gambaran umum urutan / langkah yang akan kita ambil dalam menyusun query.

So, bagaimana urutannya?

Pertama…
Ketika MySQL mengeksekusi statemen SELECT, maka pertama tama MySQL akan mengeksekusi klausa FROM dan WHERE (jika ada) sehingga menghasilkan intermediate table atau tabel antara.
Tabel ini bisa berupa tabel riil (Jika klausa FROM menunjuk tabel  pada database) atau tabel sementara (temporary table) – jika tabel hasil klausa FROM tidak ada pada database, seperti penggunaan JOIN atau subquery.  
Klausa WHERE (jika ada) akan dieksekusi setelah tabel hasil klausa FROM terbentuk, gunanya untuk membatasi jumlah data yang diambil.

Kenapa klausa FROM dulu?
Logikanya begini…

Jika klausa SELECT yang dijalankan terlebih dahulu, maka MySQL akan mencari kolom yang pada klausa SELECT ke semua tabel yang ada pada database.

Hal ini tentu saja sangat tidak efisien. Dengan memilih atau membentuk tabel terlebih dahulu maka akan jauh lebih efektif ketika memilih kolom mana yang akan diambil.

Bagian pertama ini sangat vital yang akan menentukan langkah selanjutnya, so… pahami dengan baik

Tabel hasil klausa FROM ini harus berupa satu tabel bagaimanapun kompleksnya data yang digunakan, sehingga jika sumber data terdiri dari beberapa tabel maka tabel tersebut harus kita gabungkan terlebih dahulu menjadi satu menggunakan JOIN atau UNION

Kedua…
Selanjutnya MySQL mengeksekusi klausa SELECT, eksekusi ini bertujuan:

1. Untuk membuat kolom baru jika kolom tersebut belum ada pada tabel hasil klausa FROM, misal kolom hasil perkalian atau kolom hasil fungsi agregasi.

1. Untuk mengambil kolom yang akan ditampilkan pada tabel output. Penting diperhatikan bahwa pengambilan kolom ini dilakukan terakhir setelah semua klausa selesai dieksekusi.

Ketiga…

Setelah selesai  pada klausa  SELECT, MySQL akan mengeksekusi klausa opsional lain urut mulai dari GROUP BY, dst.. hingga LIMIT

Terakhir…

Setelah semua dieksekusi, MySQL akan menghasilkan tabel output dengan kolom sesuai yang didefinisikan pada klausa SELECT
Ilustrasinya adalah sebagai berikut:

Gambar 2.1 Ilustrasi eksekusi statemen SELECT
Gunakan konsep alur diatas untuk menyelesaikan setiap kasus query yang kita hadapi, dijamin akan jauh lebih cepat dan mudah.

Untuk lebih memahami alur diatas, mari kita langsung praktek. Misal kita memiiki tabel penjualan sebagai berikut:

| id_trx | id_pelanggan | tgl_trx    | total_trx |
| ------ | ------------ | ---------- | --------- |
| 1      | 1            | 2017-03-02 | 192000    |
| 2      | 1            | 2017-03-10 | 186000    |
| 3      | 0            | 2017-04-10 | 259000    |
| 4      | 2            | 2017-04-05 | 110000    |
| 5      | 2            | 2016-11-10 | 256000    |

Selanjutnya kita tampilkan data 3 penjualan terbesar di tahun 2017, dengan menampilkan kolom id_pelanggan, tgl_trx, dan total_trx sehingga terbentuk tabel output sebagai berikut:

| id_pelanggan | tgl_trx    | total_trx |
| ------------ | ---------- | --------- |
| 0            | 2017-04-10 | 259000    |
| 1            | 2017-03-02 | 192000    |
| 1            | 2017-03-10 | 186000    |

Bagaimana querynya?
Mari kita bahas…

Pertama…  

Ingat alur query, pertama identifikasi tabel pada klausa FROM, jika perlu batasi data dengan klausa WHERE.

Pada kasus diatas kita akan menampilkan data penjualan tahun 2017, maka kita ambil tabel penjualan dan dengan klausa WHERE kita batasi hanya data tahun 2017 yang diambil, mari kita tes dengan menggunakan klausa SELECT *

```sql
SELECT *  
FROM penjualan  
WHERE YEAR(tgl_trx) = 2017; 
```

Hasilnya:

| id_trx | id_pelanggan | tgl_trx    | total_trx |
| ------ | ------------ | ---------- | --------- |
| 1      | 1            | 2017-03-02 | 192000    |
| 2      | 1            | 2017-03-10 | 186000    |
| 3      | 0            | 2017-04-10 | 259000    |
| 4      | 2            | 2017-04-05 | 110000    |

Pada query diatas, fungsi YEAR digunakan untuk mengambil  data tahun, kita akan membahas lebih jauh tentang fungsi ini pada BAB VI Menguasai Fungsi Scalar.
Hasil diatas sudah sesuai dengan yang kita harapkan, mari kita lanjutkan…

Kedua…

Selanjutnya kita menuju ke klausa SELECT, kita pilih kolom yang ingin kita tampilkan, yaitu kolom id_pelanggan, tgl_trx, dan total_trx, sehingga klausa SELECT nya menjadi:

```sql
SELECT id_pelanggan, tgl_trx, total_trx 
FROM penjualan 
WHERE YEAR(tgl_trx) = 2017 
```

Ketiga…

Terakhir, karena kita akan mengurutkan data berdasarkan penjualan terbesar, maka kita gunakan klausa ORDER BY yang kita terapkan pada pada kolom total_trx sebagai berikut:

```sql
SELECT id_pelanggan, tgl_trx, total_trx 
FROM penjualan 
WHERE YEAR(tgl_trx) = 2017 
ORDER BY total_trx DESC 
```

Query diatas akan menghasilkan tabel dengan data yang diurutkan berdasarkan jumlah pembayaran (kolom total_byr) mulai dari yang terbesar
Selanjutnya kita hanya akan mengambil tiga terbesar, sehingga kita tambahkan klausa LIMIT sebagai berikut:

```sql
SELECT id_pelanggan, tgl_trx, total_trx 
FROM penjualan 
WHERE YEAR(tgl_trx) = 2017 
ORDER BY total_trx DESC 
LIMIT 3 
```

Hasil yang kita peroleh:

| id_pelanggan | tgl_trx    | total_trx |
| ------------ | ---------- | --------- |
| 0            | 2017-04-10 | 259000    |
| 1            | 2017-03-02 | 192000    |
| 1            | 2017-03-10 | 186000    |

Nah, hasilnya sudah pas dengan yang kita inginkan.
Untuk lebih jelasnya, perhatikan ilustrasi berikut:
Gambar 2.2 Ilustrasi Proses Pengambilan Data

Exception 1: Fungsi Agregasi

Pada eksekusi statemen SELECT, terdapat beberapa hal atau pengecualian (exception) yang menyebabkan urutan proses eksekusi berubah.  

Apa penyebabnya? penyebabnya adalah adanya fungsi agregasi pada klausa SELECT.

>Note: Kita akan membahas lebih jauh mengenai fungsi agregasi ini pada bab V. Menguasai Fungsi Agregasi

Jika pada klausa SELECT terdapat fungsi agregasi –-dan pastinya kita akan sering menggunakan fungsi ini-- maka fungsi ini akan dijalankan belakangan bersama-sama dengan klausa GROUP BY  
Sebagai contoh: pada query sebelumnya kita tambahkan fungsi SUM pada klausa SELECT untuk menjumlahkan nilai total transaksi, selain itu juga kita batasi jumlah baris yang ditampilkan sebanyak 2 baris, query nya adalah sebagai berikut:

```sql
SELECT id_pelanggan, tgl_trx, SUM(total_trx) 
FROM penjualan 
WHERE YEAR(tgl_trx) = 2017 
GROUP BY id_pelanggan 
ORDER BY SUM(total_trx) DESC 
LIMIT 2 
```

Hasil yang kita peroleh:

| id_pelanggan | tgl_trx    | SUM(total_trx) |
| ------------ | ---------- | -------------- |
| 1            | 2017-03-02 | 378000         |
| 0            | 2017-04-10 | 259000         |

Urutan eksekusi query diatas sama seperti yang telah kita pelajari, namun ada sedikit perubahan, urutannya adalah sebagai berikut:  

1. Klausa FROM dan WHERE

2. Klausa SELECT (untuk membuat kolom baru – jika ada). Fungsi SUM tidak dieksekusi.  

3. Klausa GROUP BY bersama dengan fungsi SUM

4. Klausa ORDER BY, dan  

5. Klausa LIMIT.

Pada urutan diatas, terlihat bahwa fungsi agregasi SUM di jalankan bersama dengan klausa GROUP BY lebih tepatnya setelah data diurutkan.

Kenapa demikian?  

Hal ini untuk memudahkan pengelompokan data (ketika menjalankan fungsi agregasi -  SUM), karena data sudah diurutkan secara ascending (ingat kembali bahwa ketika menjalankan klausa GROUP BY, data akan diurutkan terlebih dahulu)
Untuk lebih jelasnya, perhatikan ilustrasi berikut:

Gambar 2.3 Ilustrasi Eksekusi Statemen SELECT Yang Mengandung

Fungsi Agregasi SUM

Pada ilustrasi diatas terlihat bahwa pada bagian GROUP BY id_pelanggan + SUM(total_trx) data diurutkan berdasarkan kolom

id_pelanggan baru kemudian di kelompokkan (GROUP BY) dan di jumlahkan (SUM), sehingga data menjadi urut berdasarkan id_pelanggan, betul kan? Baru kemudian diurutkan berdasarkan kolom SUM(total_trx)

Nah setelah Anda memahami contoh diatas, mari kita sedikit kembangkan query nya, mari kita tambahkan fungsi COUNT pada klausa SELECT, sehingga querynya menjadi:

```sql
SELECT id_pelanggan, COUNT(id_trx), SUM(total_trx) 
FROM penjualan 
WHERE YEAR(tgl_trx) = 2017 
GROUP BY id_pelanggan 
ORDER BY total_trx DESC 
LIMIT 2 
```

Jika kita jalankan query diatas akan menghasilkan output:

| id_pelanggan | COUNT(id_trx) | SUM(total_trx) |
| ------------ | ------------- | -------------- |
| 0            | 1             | 259000         |
| 1            | 2             | 378000         |

Fungsi COUNT diatas digunakan untuk menghitung banyaknya baris pada kolom id_trx yang tidak mengandung nilai NULL.  
Kita hitung banyaknya baris untuk menghitung banyaknya transaksi karena banyaknya transaksi tercermin dari banyaknya baris yang ada.

Lebih jauh tentang fungsi agregasi kita pelajari pada BAB V Menguasai Fungsi Agregasi

Selanjutnya, bagaimana alur querynya?

Alurnya sama persis dengan gambar II. 3 Bedanya ada tambahan kolom COUNT(id_trx)

## 2.2. Konsekuensi Urutan Eksekusi

Setelah memahami urutan eksekusi statmen SELECT, maka kita perlu memahami konsekuensi konsekuensi yang terjadi ketika masing-masing klausa dieksekusi.

Apa saja konsekuensinya?

Dari masing masing tahapan eksekusi, jika diperlukan, MySQL akan membuat temporary tabel. Ketika temporary tabel ini sudah terbentuk, konsekusensinya kita dapat menggunakan nama kolom dari tabel tersebut.

Bingung?  

Baiklah, ambil contoh seperti ini, kita memiliki tabel penjualan_detail sebagai berikut:

| id  | id_trx | kd_barang | qty | harga_satuan | diskon |
| --- | ------ | --------- | --- | ------------ | ------ |
| 1   | 1      | 1         | 1   | 76000        | 0      |
| 2   | 1      | 3         | 1   | 35000        | 0      |
| 3   | 1      | 5         | 2   | 45000        | 0.1    |
| 4   | 2      | 1         | 1   | 70000        | 0      |
| 5   | 2      | 2         | 2   | 55000        | 0      |

Selanjutnya kita akan urutkan data berdasarkan total harga (qty x harga_satuan) mulai dari yang tersbesar. Query yang kita jalankan adalah sebagai berikut:

```sql
SELECT id, qty, harga_satuan, qty * harga_satuan AS total 
FROM penjualan_detail 
ORDER BY total DESC 
```

Hasil yang kita peroleh:

| id  | qty | harga_satuan | total  |
| --- | --- | ------------ | ------ |
| 5   | 2   | 55000        | 110000 |
| 3   | 2   | 45000        | 90000  |
| 1   | 1   | 76000        | 76000  |
| 4   | 1   | 70000        | 70000  |
| 2   | 1   | 35000        | 35000  |

Pada query diatas, kita menggunakan keyword AS. Seperti yang telah kita pelajari, keyword ini digunakan untuk memberi nama alias pada kolom.

Seperti yang kita pelajari, maka urutan query diatas adalah:

Pertama…

MySQL akan mengeksekusi klausa FROM, pada kasus ini, MySQL akan menggunakan tabel riil karena tabel penjualan_detail sudah ada di database

Kedua…

Selanjutnya MySQL akan mengeksekusi klausa SELECT,  untuk membuat kolom baru (jika ada). Pada contoh diatas terdapat kolom baru yaitu kolom total.  

Pada tahap ini, MySQL akan membat temporary tabel yang isinya kolom pada tabel penjualan_detai dan kolom total sebagai berikut:

| id  | id_trx | kd_barang | qty | harga_satuan | diskon | total  |
| --- | ------ | --------- | --- | ------------ | ------ | ------ |
| 1   | 1      | 1         | 1   | 76000        | 0      | 76000  |
| 2   | 1      | 3         | 1   | 35000        | 0      | 35000  |
| 3   | 1      | 5         | 2   | 45000        | 0.1    | 90000  |
| 4   | 2      | 1         | 1   | 70000        | 0      | 70000  |
| 5   | 2      | 2         | 2   | 55000        | 0      | 110000 |

Selanjutnya temporary tabel ini akan digunakan untuk menjalankan proses pada tahap berikutnya.

Ketiga…

Selanjutnya, MySQL akan mengeksekusi klausa opsional yang ada, yang yang dalam contoh kali ini klausa ORDER BY.

Klausa tersebut menggunakan kolom total untuk mengurutkan data secara descending (ORDER BY total DESC), dan karena kolom total ini sudah terbentuk pada proses sebelumnya maka kita dapat menggunakannya.

>`Catatan:`Kolom alias baru tersedia mulai klausa GROUP BY dst… tidak bisa digunakan pada proses (tahapan) sebelumnya yaitu SELECT Kenapa? Karena kolom tersebut baru terbentuk setelah klausa SELECT selesai dieksekusi

Sebagai contoh, jalankan query berikut:

```sql
SELECT id, qty, harga_satuan, qty * harga_satuan AS total, 
total * 0.1 AS diskon, 
FROM penjualan_detail_copy, 
ORDER BY total DESC; 
```

Maka kita akan mendapati error:
ERROR 1054 (42S22): Unknown column 'total' in 'field list'

Error tersebut terjadi karena kolom total belum terbentuk.

Contoh lain: penggunaan kolom alias  

```sql
SELECT id, qty, harga_satuan, qty * harga_satuan AS total, 
FROM penjualan_detail_copy, 
GROUP BY total DESC; 
```

Hasil:

| id  | qty | harga_satuan | total  |
| --- | --- | ------------ | ------ |
| 5   | 2   | 55000        | 110000 |
| 3   | 2   | 45000        | 90000  |
| 1   | 1   | 76000        | 76000  |
| 4   | 1   | 70000        | 70000  |
| 2   | 1   | 35000        | 35000  |

Pada contoh diatas, karena klausa GROUP BY dieksekusi setelah klausa SELECT, maka kita dapat menggunakan kolom alias

**Pendalaman materi**

Untuk lebih memahami proses ini, misal dari contoh diatas, kita akan mengambil data dengan total harga lebih dari 50.000

Mari kita jalankan query berikut:

```sql
SELECT id, qty, harga_satuan, qty * harga_satuan AS total 
FROM penjualan_detail 
WHERE total > 50000 
ORDER BY total DESC 
```

Maka pasti kita akan mendapati error:
ERROR 1054 (42S22): Unknown column 'total' in 'where clause'

Sudah tahu kan kenapa muncul  error seperti itu?
Karena klausa FROM dan WHERE akan di eksekusi pertama kali dan pada tahap itu, hanya tersedia kolom tabel penjualan_detail dan tidak ada kolom total

Solusinya bagaimana?

Mau tidak mau kita harus menggunakan kolom yang ada yaitu kolom qty dan harga_satuan
Jalankan query berikut:

```sql
SELECT id, qty, harga_satuan, qty * harga_satuan AS total 
FROM penjualan_detail 
WHERE qty * harga_satuan > 50000 
ORDER BY total DESC 
```

Hasilnya adalah sebagai berikut:

| id  | qty | harga_satuan | total  |
| --- | --- | ------------ | ------ |
| 5   | 2   | 55000        | 110000 |
| 3   | 2   | 45000        | 90000  |
| 1   | 1   | 76000        | 76000  |
| 4   | 1   | 70000        | 70000  |
+----+------+--------------+--------+

Mungkin anda bertanya…., bagaimana data bisa diambil hanya yang total nya diatas 50.000?  

Lihat kembali BAB I, ketika MySQL mengeksekusi klausa WHERE, maka setiap baris pada tabel akan dievaluasi satu per satu dan hanya diambil baris yang memenuhi kriteria pada klausa WHERE

Pada query diatas, MySQL akan mengalikan qty dengan harga_satuan di setiap baris pada tabel penjualan_detail dan hanya diambil baris yang hasil perkalian nya diatas 50.000
Catatan 2: Fungsi Agregasi

Lagi lagi terdapat hal di luar “pakem” dan lagi lagi terkait fungsi agregasi, yaitu jika kolom alias tersebut terbentuk dari fungsi

agregasi, maka kolom tersebut baru terbentuk setelah klausa GROUP BY selesai dieksekusi.

Kenapa?

Karena fungsi agregasi dieksekusi bersama dengan klausa GROUP BY (seperti yang telah kita bahas pada bagian sebelumnya) sehingga kolom tersebut baru terbentuk setelah klausa GROUP BY selesai dieksekusi.

Dengan demikian, kita tidak dapat menggunakannya pada klausa GROUP BY, melainkan mulai klausa ORDER BY dan seterusnya, contoh:

```sql
SELECT id_trx, id_pelanggan, SUM(total_trx) AS total 
FROM penjualan 
GROUP BY total 
```

Jika query tersebut dijalankan maka kita akan mendapatki pesan error:
SQL Error (1056): Can't group on 'total'

Pada contoh diatas, karena kolom total merupakan kolom alias dan baru terbentuk setelah klausa GROUP BY selesai dieksekusi, maka tidak dapat digunakan pada klausa GROUP BY

Kasus seperti ini jarang sekali terjadi, sehingga tidak perlu difikirkan terlalu menadalam cukup dijadikan pengetahuan saja.

## 2.3. Identifikasikan Bentuk Tabel

Pada bagian ini kita akan membahas lebih dalam bagaimana mengidentifikasi bentuk tabel hasil eksekusi klausa FROM

Bentuk tabel ini sangat penting karena akan menentukan tabel awal yang akan digunakan pada tahap berikutnya, untuk itu kita perlu meng identifikasikan bentuk tabel ini dengan benar

Pada bagian sebelumnya telah sedikit dibahas bagaimana bentuk tabel hasil klausa FROM ini, pada pembahasan tersebut bentuk tabel berupa tabel riil yaitu tabel penjualan_detail (FROM penjualan_detail)

Pada banyak kasus, kita perlu menggunakan dua atau lebih tabel, dan karena hasil tabel pada klausa FROM ini harus berupa satu tabel, maka kita harus menggabungkan tabel tabel tersebut menjadi satu.

Terkait penggabungan ini, terdapat dua bentuk yang dapat digunakan yaitu menggunakan JOIN dan UNION, keduanya akan kita bahas pada BAB tersendiri.

Pertanyaan selanjutnya, kapan menggunakan JOIN dan kapan menggunakan UNION?
Untuk memutuskan apakah menggunakan JOIN atau UNION, perhatikan kondisi berikut:

1. JOIN. Gunakan JOIN jika kolom pada tabel hasil klausa FROM terdapat kolom dari tabel yang digabungkan, atau bisa juga jika kedua tabel saling berhubungan (ada key antar tabel - foreign key)  

2. UNION. Gunakan UNION jika tabel hasil klausa FROM memiliki kolom yang sama dengan tabel yang digabungkan atau jika kita

perlu data pada kedua tabel namun keduanya tidak saling berhubungan (tidak ada key antar tabel).

Praktik di lapangan kita akan sering menggunakan JOIN dan jarang (hampir tidak pernah) menggunakan UNION.

Selanjutnya mari kita belajar dari contoh…

Kali ini kita akan menggunakan JOIN

> Note: Jika Anda belum memahami join, tidak masalah, cukup ikuti saja dulu pembahasannya.  

Misal kita memiliki dua buah tabel, yaitu tabel penjualan dan pelanggan sebagai berikut:

penjualan

| id_trx | id_pelanggan | tgl_trx    | total_trx |
| ------ | ------------ | ---------- | --------- |
| 1      | 1            | 2017-03-02 | 192000    |
| 2      | 1            | 2017-03-10 | 186000    |
| 3      | 0            | 2017-04-10 | 259000    |
| 4      | 2            | 2017-04-05 | 110000    |
| 5      | 2            | 2016-11-10 | 256000    |

pelanggan

| id_pelanggan | nama    | alamat    | id_staf |
| ------------ | ------- | --------- | ------- |
| 1            | Alfa    | Jakarta   | 1       |
| 2            | Beta    | Semarang  | 1       |
| 3            | Charlie | Surabaya  | 2       |
| 4            | Delta   | Surakarta | 3       |

Selanjutnya kita ingin menampilkan data penjualan beserta nama pelanggannya  dengan output sebagai berikut:

| nama | tgl_trx    | total_trx |
| ---- | ---------- | --------- |
| Alfa | 2017-03-02 | 192000    |
| Alfa | 2017-03-10 | 186000    |
| Beta | 2017-04-05 | 110000    |
| Beta | 2016-11-10 | 256000    |
| NULL | 2017-04-10 | 259000    |

Bagaimana querynya?

Sesuai dengan prinsip yang telah kita bahas, maka pertama kita buat gabungan tabel melalui klausa FROM, selanjutnya kita ambil kolom melalui klausa SELECT.  

Pertama…

Karena kita menggunakan lebih dari satu tabel, maka kita perlu identifikase tabel output

Pada tabel output terdapat kolom nama yang berasal dari tabel pelanggan, dan kolom tgl_trx dan total_trx yang berasal dari tabel penjualan.

Nah karena kolom pada tabel output ada pada kedua tabel, maka kita harus menggabungkan kedua tabel tersebut.

Selanjutnya menggunakan JOIN atau UNION?  

Jika kita perhatikan, kolom yang akan kita tampilkan adalah kolom nama, tgl_trx, dan total_trx ketiga kolom tersebut ada pada gabungan kedua tabel, maka tabel hasil klausa FROM harus memuat ketiga kolom tersebut, selain itu, kedua tabel juga saling berhubungan pada kolom id_pelanggan, oleh karena itu kita gunakan JOIN  
Mari kita gabungkan kedua tabel menggunakan JOIN, jalankan query berikut:

```sql
 SELECT *  
FROM penjualan  
LEFT JOIN pelanggan USING(id_pelanggan); 
```

Hasilnya adalah:

| id_pelanggan | id_trx | tgl_trx    | total_trx | nama | alamat   | id_staf |
| ------------ | ------ | ---------- | --------- | ---- | -------- | ------- |
| 1            | 1      | 2017-03-02 | 192000    | Alfa | Jakarta  | 1       |
| 1            | 2      | 2017-03-10 | 186000    | Alfa | Jakarta  | 1       |
| 2            | 4      | 2017-04-05 | 110000    | Beta | Semarang | 1       |
| 2            | 5      | 2016-11-10 | 256000    | Beta | Semarang | 1       |
| 0            | 3      | 2017-04-10 | 259000    | NULL | NULL     | NULL    |

Kedua…

Selanjutnya kita definisikan kolom pada klausa SELECT, sehingga querynya menjadi:

```sql
SELECT nama, tgl_trx, total_trx  
FROM penjualan  
LEFT JOIN pelanggan USING(id_pelanggan); 
```

Hasil:

| nama | tgl_trx    | total_trx |
| ---- | ---------- | --------- |
| Alfa | 2017-03-02 | 192000    |
| Alfa | 2017-03-10 | 186000    |
| Beta | 2017-04-05 | 110000    |
| Beta | 2016-11-10 | 256000    |
| NULL | 2017-04-10 | 259000    |

Bagaimana alur eksekusi querynya?

Alurnya Sama persis dengan yang telah kita bahas bada bagian sebelumnya. Langsung saja, perhatikan ilustrasi berikut:

Gambar 2. 4 Ilustrasi alur eksekusi statemen SELECT yang terdapat klausa JOIN

Pada ilustrasi diatas, terlihat bahwa MySQL membuat temporary tabel yang berisi gabungan tabel penjualan dan pelanggan, temporary tabel ini perlu dibuat karena tabel hasil klausa FROM merupakan hasil dari penggabungan tabel, sehingga tidak mungkin ada di database.

## 2.4. Pendefinisian Kolom Baru

Setelah kita memahami bagaimana statemen SELECT dieksekusi dan bagaimana mendefinisikan tabel pada klausa FROM, selanjutnya kita
harus dapat mengidentifikasi kolom pada tabel output yang akan kita tampilkan.
Pendefinisian kolom ini sangat bervariasi tergantung kondisi dilapangan, kolom bisa berupa existing column (kolom yang sudah ada - kolom yang berasal dari tabel hasil klausa FROM), maupun kolom baru yang berasal dari nilai skalar, string, fungsi, ekspresi, dll.

Yang terpenting adalah bagaimanapun rumitnya penghitungan yang dilaukan, semua kolom pada tabel output harus ada pada klausa SELECT, perhatikan ilustrasi berikut:

Gambar 2.5. Ilustrasi Jenis Kolom Pada Klausa SELECT

Pada ilustrasi diatas terlihat bahwa setiap yang kita tulis pada statemen select (dengan pemisah tanda koma) akan selalu menghasilkan kolom, baik nilai skalar (nilai 1) ekspresi berupa operasi aritmatika, maupun nama kolom tabel hasil klausa FROM.
Berdasarkan hal tersebut diatas, dapat disimpulkan bahwa jika kita ingin menambahkan kolom yang tidak ada pada

tabel hasil klausa FROM, maka kita harus mendefinisikannya pada klausa SELECT

## 2.5. Eksekusi Baris

Selanjutnya, perlu dipahami juga bahwa setiap baris pada tabel yang terbentuk oleh kalusa FROM akan dieksekusi sesuai dengan apa yang di definisikan pada klausa SELECT.
Hal ini sesuai dengan prinsip yang telah kita pelajari bahwa ketika mengeksekusi klausa SELECT, maka jika diperlukan, MySQL akan membuat kolom baru, nah isi dari kolom baru ini merupakan hasil eksekusi dari setiap baris yang ada pada tabel hasil klausa FROM  

Perhatikan ilustrasi berikut:

Gambar 2.6. Ilustrasi Eksekusi Klausa SELECT

Pada gambar diatas terlihat bahwa untuk menghasilkan nilai pada kolom output (kolom baru), setiap baris yang ada pada tabel penjualan_detail akan diseksekusi sesuai dengan yang ada pada klausa SELECT.

## 2.6. Pembatas Tampilan Data  

Konsep terakhir adalah mengetahui hal-hal yang menyebabkan data tidak ditampilkan semua.  

Maksudnya apa?  

Secara default, ketika mengeksekusi statemen  SELECT, maka  semua baris pada tabel hasil akan ditampilkan, kecuali jika terdapat klausa:

1. WHERE;

2. GROUP BY;

3. LIMIT; dan  

4. Fungsi agregasi pada klausa SELECT.

Sebenarnya tidak ada konsep baru disini, karena dengan mengetahui arti dari klausa diatas (telah dibahas pada BAB I) otomatis akan tahu bahwa ada pembatasan data yang ditampikan.

Namun demikian, hal ini perlu ditekankan lagi, karena pada kasus yang rumit, kita bingung dan ragu apa yang harus dilakukan.

## 2.7. Poin Penting

Dari berbagai pembahasan diatas, dapat disimpulkan bahwa terdapat beberapa hal penting yang perlu dipahami yaitu:

1. Memahami urutan eksekusi query. Urutannya adalah: FROM, WHERE, SELECT, GROUP BY, ORDER BY, HAVING, dan LIMIT

2. Ketika menyusun query, pertama tama kita perlu mendefinisikan tabel yang akan terbentuk pada eksekusi klausa FROM, jika data melibatkan lebih dari satu tabel, gabungkan tabel tersebut menjadi satu menggunakan JOIN atau UNION.

3. Jika ada kolom baru yang tidak ada pada tabel hasil eksekusi klausa FROM, definisikan kolom tersebut pada klausa SELECT.

4. Kolom baru tersebut terbentuk setelah klausa SELECT selesai dieksekusi, sehingga baru  dapat digunakan pada klausa GROUP BY, dst…  Khusus untuk kolom hasil fungsi Agregasi, seperti SUM(), dan COUNT(), maka kolom ini baru terbentuk setelah klausa GROUP BY selesai dieksekusi, sehingga baru dapat digunakan mulai klausa ORDER BY, dst…

5. Ketika mengeksekusi klausa SELECT dan WHERE maka setiap baris pada tabel hasil eksekusi klausa FROM akan dieksekusi.
