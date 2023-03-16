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
``` mysql
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