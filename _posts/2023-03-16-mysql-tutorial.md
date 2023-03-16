---
layout: post
title: Belajar Query Mysql 
categories: [Tutorial Mysql Query]
tags: [Mysql, Query]
---
## Query Mysql
Query MySQL adalah perintah atau instruksi yang digunakan untuk berinteraksi dengan database MySQL. Query dapat digunakan untuk mengambil, memasukkan, menghapus, atau memperbarui data dalam database MySQL. Query MySQL ditulis dalam bahasa SQL (Structured Query Language) yang merupakan bahasa standar untuk manajemen database relasional
Dalam MySQL, query digunakan untuk memanipulasi data dalam tabel. Beberapa contoh query MySQL yang umum digunakan adalah SELECT, INSERT, UPDATE, DELETE, JOIN, dan lain sebagainya. Setiap query terdiri dari perintah kunci (command key) dan klausa (clause) yang digunakan untuk memodifikasi, memanipulasi, dan mengambil data dari tabel.
contoh query mysql
``` mysql
SELECT * FROM customers WHERE city='Jakarta';
```
Query di atas digunakan untuk mengambil data dari tabel customers dengan syarat bahwa nilai kolom city sama dengan 'Jakarta'
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

- id : kolom id sebagai primary key yang secara otomatis di-generate oleh MySQL setiap kali data baru dimasukkan ke dalam tabel.
- tanggal : kolom tanggal dengan tipe data DATE untuk mencatat tanggal penjualan dilakukan.
- produk : kolom produk dengan tipe data VARCHAR(50) untuk mencatat nama produk yang terjual.
- jumlah : kolom jumlah dengan tipe data INT untuk mencatat jumlah produk yang terjual.
- harga : kolom harga dengan tipe data DECIMAL(10,2) untuk mencatat harga satuan produk.
- total : kolom total dengan tipe data DECIMAL(10,2) untuk mencatat total harga penjualan.

Contoh data yang dimasukkan ke dalam tabel ini mencatat beberapa penjualan produk pada tanggal-tanggal tertentu. Dalam contoh ini, kolom total dihitung otomatis berdasarkan nilai jumlah dan harga.
Setelah tabel penjualan dibuat, ada beberapa query MySQL yang dapat Anda gunakan untuk mengambil data dari tabel ini, antara lain:
1. SELECT - untuk mengambil data dari tabel
``` sql
SELECT * FROM penjualan;
```
Query di atas akan menampilkan semua data dari tabel penjualan.

2. WHERE - untuk mengambil data dengan kondisi tertentu
``` sql
SELECT * FROM penjualan WHERE tanggal BETWEEN '2022-01-01' AND '2022-01-03';
```
