---
layout: post
title: Query Mysql 
toc: true
categories: [Tutorial Mysql Query]
tags: [Mysql, Query]
---
# Bab 1: Statemen SELECT

Statemen SELECT digunakan untuk mengambil data dari database. Statemen ini merupakan statemen utama dalam SQL karena sebagian besar query yang kita lakukan adalah pengambilan data, disamping itu statemen ini memiliki variasi paling banyak dibanding statemen lain seperti INSERT dan UPDATE. Pada BAB ini kita akan membahas syntax dasar statemen SELECT beserta variasinya, dengan memahami topik ini, Anda akan dapat dengan mudah memahami pembahasan pada bab berikutnya.

1.1. Syntax Statemen SELECT

Statemen SELECT memiliki struktur sebagai berikut:


```sql
SELECT ...
FROM ...
[WHERE ...]
[GROUP BY ...]
[ORDER BY ...]
[HAVING ...]
[LIMIT ...]
```

Penulisan klausa di atas harus urut mulai dari atas ke bawah. Keyword SELECT dan FROM wajib ada, sedangkan keyword lain (yang ada dalam tanda kurung siku \[\]) bersifat opsional.

Contoh penggunaan statemen SELECT: misal kita memiliki tabel "mhs" dengan data sebagai berikut:



```css
+------+---------+---------------+------------+
| nim  | nama    | jenis_kelamin | kd_jurusan |
+------+---------+---------------+------------+
| 001  | Alfa    | L             | J002       |
| 002  | Beta    | P             | J002       |
| 003  | Charlie | P             | J001       |
| 004  | Delta   | L             | J001       |
| 005  | Erdhi   | L             | J001       |
| 006  | Farah   | P             | J002       |
| 007  | Gisel   | P             | J002       |
| 008  | Haris   | L             | NULL       |
+------+---------+---------------+------------+
```

Untuk mengambil semua kolom, kita gunakan tanda asterik (\*) misal:


```sql
SELECT * FROM mhs;
```
Hasil:

sql

```sql
+------+---------+---------------+------------+
| nim  | nama    | jenis_kelamin | kd_jurusan |
+------+---------+---------------+------------+
| 001  | Alfa    | L             | J002       |
| 002  | Beta    | P             | J002       |
| 003  | Charlie | P             | J001       |
| 004  | Delta   | L             | J001       |
| 005  | Erdhi   | L             | J001       |
| 006  | Farah   | P             | J002       |
| 007  | Gisel   | P             | J002       |
| 008  | Haris   | L             | NULL       |
+------+---------+---------------+------------+

Untuk menampilkan kolom tertentu, kita tulis nama kolom tersebut pada klausa SELECT, misal:
```

SELECT nama, jenis\_kelamin FROM mhs;

makefile

```makefile
Hasil:
```

+---------+---------------+ | nama | jenis\_kelamin | +---------+---------------+ | Alfa | L | | Beta | P | | Charlie | P | | Delta | L | | Erdhi | L | | Farah | P | | Gisel | P | | Haris | L | +---------+---------------+

kotlin

```kotlin
Usahakan hanya mengambil kolom yang diperlukan, hindari penggunaan asterik. Hal ini merupakan "Best Practice" untuk meningkatkan efisiensi performa SQL.

WHERE
Klausa WHERE digunakan untuk memfilter data yang ingin diambil, misal kita akan mengambil data siswa dengan jenis kelamin laki-laki, query yang kita jalankan adalah sebagai berikut:
```

SELECT nama, jenis\_kelamin  
FROM mhs WHERE jenis\_kelamin = "L";

Hasil:

| nama | jenis\_kelamin | 
|-------|---------------|
 | Alfa | L | | Delta | L | 
 | Erdhi | L | | Haris | L | 
 
 
 Ketika menjalankan klausa WHERE, MySQL akan memeriksa baris pada tabel satu persatu sehingga pada tabel dengan jumlah baris banyak, proses ini akan memakan waktu cukup lama, untuk mengatasinya, gunakan teknik indexing (penggunaan index) - tidak di bahas pada buku ini-.

GROUP BY GROUP BY digunakan untuk mengelompokkan baris berdasarkan kolom tertentu. Penggunaan keyword ini selalu bersamaan dengan fungsi agregasi seperti COUNT, SUM, MIN, MAX, dan AVG. Contoh:

sql

```sql
SELECT kd_jurusan, COUNT(kd_jurusan)  
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan;
```

Pada contoh di atas, data dihitung (fungsi COUNT) dan dikelompokkan berdasarkan kolom kd\_jurusan. Jika Anda belum paham mengenai fungsi COUNT, tidak usah khawatir, kita akan membahasnya secara detail pada bab berikutnya. Penting diperhatikan bahwa sebelum menjalankan GROUP BY, terlebih dahulu MySQL akan mengurutkan data pada kolom yang ada pada klausa GROUP BY secara ascending, (hal ini penting untuk diingat).

Sebagai contoh, jika kita jalankan query di atas, maka hasil yang kita peroleh adalah:

sql

```sql
+------------+-------------------+
| kd_jurusan | COUNT(kd_jurusan) |
+------------+-------------------+
| NULL       |                 0 |
| J001       |                 2 |
| J002       |                 1 |
+------------+-------------------+
```

Pada tabel di atas terlihat bahwa data diurutkan berdasarkan kolom kd\_jurusan secara ascending.

ORDER BY Keyword ORDER BY digunakan untuk mengurutkan data baik secara ascending (dari kecil ke besar) maupun descending (dari besar ke kecil). Keyword ini akan dijalankan setelah MySQL menjalankan klausa GROUP BY (jika ada), yang artinya setelah data dikelompokkan, contoh:

sql

```sql
SELECT kd_jurusan, COUNT(kd_jurusan)  
FROM mhs 
WHERE jenis_kelamin = "L" 
GROUP BY kd_jurusan 
ORDER BY kd_jurusan DESC;
```

Hasil:

```sql
+------------+-------------------+
| kd_jurusan | COUNT(kd_jurusan) |
+------------+-------------------+
| J002       |                 1 |
| J001       |                 2 |
| NULL       |                 0 |
+------------+-------------------+
```

Pada contoh di atas, data diurutkan berdasarkan kolom kd\_jurusan secara descending (dari besar ke kecil). Jika ingin diurutkan secara ascending, hilangkan keyword DESC atau ganti dengan ASC.

Selain bersamaan dengan GROUP BY, keyword ORDER BY juga dapat digunakan tanpa GROUP BY, misal:



```sql
SELECT nama, jenis_kelamin 
FROM mhs 
ORDER BY nama;
```

Hasil:


```css
+---------+---------------+
| nama    | jenis_kelamin |
+---------+---------------+
| Alfa    | L             |
| Beta    | P             |
| Charlie | P             |
| Delta   | L             |
| Erdhi   | L             |
| Farah   | P             |
| Gisel   | P             |
| Haris   | L             |
+---------+---------------+
```

Pada contoh di atas, data diurutkan berdasarkan kolom nama secara ascending.

Dengan ORDER BY, kita dapat mengurutkan data dengan kriteria lebih dari satu kolom, misal:

```vbnet
SELECT nama, jenis_kelamin 
FROM mhs 
ORDER BY jenis_kelamin, nama;
```