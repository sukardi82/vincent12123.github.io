---
layout: post
title: Belajar Query Mysql 
toc: true
categories: [Tutorial Mysql Query]
tags: [Mysql, Query]
---
## Query Mysql
Query MySQL adalah perintah atau instruksi yang digunakan untuk berinteraksi dengan database MySQL. Query dapat digunakan untuk mengambil, memasukkan, menghapus, atau memperbarui data dalam database MySQL. Query MySQL ditulis dalam bahasa SQL (Structured Query Language) yang merupakan bahasa standar untuk manajemen database relasional
Dalam MySQL, query digunakan untuk memanipulasi data dalam tabel. Beberapa contoh query MySQL yang umum digunakan adalah `SELECT, INSERT, UPDATE, DELETE, JOIN,` dan lain sebagainya. Setiap query terdiri dari perintah kunci (command key) dan klausa (clause) yang digunakan untuk memodifikasi, memanipulasi, dan mengambil data dari tabel.
contoh query mysql
``` sql
SELECT * FROM customers WHERE city='Jakarta';
```
Query di atas digunakan untuk mengambil data dari tabel customers dengan syarat bahwa nilai `kolom city sama dengan 'Jakarta'`
Query MySQL adalah alat yang sangat penting dalam pengelolaan database MySQL. Dengan menggunakan query, pengguna dapat mengambil, memasukkan, memperbarui, atau menghapus data dalam database dengan cepat dan efisien. Namun, penting bagi pengguna untuk memahami bagaimana query MySQL bekerja dan bagaimana menggunakan query dengan benar untuk menghindari kesalahan dan kerusakan data

> Query MySQL adalah kekuatan penuh untuk mengakses dan memanipulasi data dalam database relasional. Dengan memahami cara menggunakan query dengan benar, Anda dapat mengambil keuntungan penuh dari potensi database Anda dan memungkinkan aplikasi Anda untuk menjadi lebih efektif dan efisien.

## Tutorial Mysql
berikut adalah contoh tabel penjualan dengan beberapa data contoh:
``` sql
CREATE TABLE penjualan (
  id INT PRIMARY KEY AUTO_INCREMENT,
  tanggal DATE,
  produk VARCHAR(50),
  jumlah INT,
  harga DECIMAL(10,2),
  total DECIMAL(10,2)
);

INSERT INTO penjualan (tanggal, produk, jumlah, harga, total) VALUES
('2022-01-01', 'Buku Tulis', 10, 5000, 50000),
('2022-01-02', 'Pensil', 20, 2000, 40000),
('2022-01-03', 'Bolpoin', 15, 2500, 37500),
('2022-01-04', 'Stabilo', 5, 10000, 50000),
('2022-01-05', 'Penghapus', 8, 1500, 12000);
```
Tabel penjualan terdiri dari 6 kolom yaitu:

- `id :` kolom id sebagai primary key yang secara otomatis di-generate oleh MySQL setiap kali data baru dimasukkan ke dalam tabel.
- `tanggal :` kolom tanggal dengan tipe data DATE untuk mencatat tanggal penjualan dilakukan.
- `produk :` kolom produk dengan tipe data VARCHAR(50) untuk mencatat nama produk yang terjual.
- `jumlah :` kolom jumlah dengan tipe data INT untuk mencatat jumlah produk yang terjual.
- `harga :` kolom harga dengan tipe data DECIMAL(10,2) untuk mencatat harga satuan produk.
- `total :` kolom total dengan tipe data DECIMAL(10,2) untuk mencatat total harga penjualan.

Contoh data yang dimasukkan ke dalam tabel ini mencatat beberapa penjualan produk pada tanggal-tanggal tertentu. Dalam contoh ini, kolom total dihitung otomatis berdasarkan nilai jumlah dan harga.
Setelah tabel penjualan dibuat, ada beberapa query MySQL yang dapat Anda gunakan untuk mengambil data dari tabel ini, antara lain:
1. `SELECT` - untuk mengambil data dari tabel
``` sql
SELECT * FROM penjualan;
```
Query di atas akan menampilkan semua data dari tabel penjualan.

2. `WHERE` - untuk mengambil data dengan kondisi tertentu
``` sql
SELECT * FROM penjualan WHERE tanggal BETWEEN '2022-01-01' AND '2022-01-03';
```
Query di atas akan menampilkan data penjualan yang dilakukan antara tanggal 1 Januari 2022 hingga 3 Januari 2022.

3. `ORDER BY` - untuk mengurutkan data
``` sql
SELECT * FROM penjualan ORDER BY tanggal DESC;
```
Query di atas akan menampilkan semua data penjualan yang telah diurutkan secara descending berdasarkan kolom tanggal.

4. `GROUP BY` - untuk mengelompokkan data berdasarkan kolom tertentu
``` sql
SELECT produk, SUM(jumlah) AS total_jumlah FROM penjualan GROUP BY produk;
```
Query di atas akan menampilkan jumlah produk yang terjual untuk setiap produk, dengan data diurutkan berdasarkan nama produk.

5. `JOIN` - untuk menggabungkan dua tabel atau lebih berikut adalah contoh tabel supplier dengan beberapa data contoh:

``` sql
CREATE TABLE supplier (
  id INT PRIMARY KEY AUTO_INCREMENT,
  nama VARCHAR(50),
  produk VARCHAR(50),
  alamat VARCHAR(100),
  kota VARCHAR(50)
);

INSERT INTO supplier (nama, produk, alamat, kota) VALUES
('Supplier A', 'Buku Tulis', 'Jl. Merdeka No. 10', 'Jakarta'),
('Supplier B', 'Pensil', 'Jl. Sudirman No. 25', 'Bandung'),
('Supplier C', 'Bolpoin', 'Jl. Imam Bonjol No. 15', 'Surabaya'),
('Supplier D', 'Stabilo', 'Jl. Asia Afrika No. 20', 'Bandung'),
('Supplier E', 'Penghapus', 'Jl. Gatot Subroto No. 30', 'Jakarta');

```
`Tabel supplier terdiri dari 5 kolom` yaitu:

- `id :` kolom id sebagai primary key yang secara otomatis di-generate oleh MySQL setiap kali data baru dimasukkan ke dalam tabel.
- `nama :` kolom nama dengan tipe data VARCHAR(50) untuk mencatat nama supplier.
- `produk :` kolom produk dengan tipe data VARCHAR(50) untuk mencatat produk yang dijual oleh supplier.
- `alamat :` kolom alamat dengan tipe data VARCHAR(100) untuk mencatat alamat supplier.
- `kota :` kolom kota dengan tipe data VARCHAR(50) untuk mencatat kota tempat supplier berada.

Contoh data yang dimasukkan ke dalam tabel ini mencatat beberapa supplier yang menyediakan produk tertentu. Query yang bisa dilakukan:

``` sql
SELECT penjualan.tanggal, penjualan.produk, penjualan.jumlah, supplier.nama AS nama_supplier 
FROM penjualan 
JOIN supplier ON penjualan.produk = supplier.produk;
```
Query di atas akan `menggabungkan tabel penjualan dengan tabel supplier dan menampilkan tanggal, produk, jumlah produk yang terjual, dan nama supplier untuk setiap produk yang terjual`.


