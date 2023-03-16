---
layout: post
title: "Belajar Flask di Jekyll"
date: 2022-03-15 10:00:00 +0700
categories: tutorial
tags: jekyll flask python
---

Flask adalah sebuah web framework yang dibuat dengan bahasa pemrograman Python. Dalam postingan ini, saya akan memberikan tutorial tentang cara memulai belajar Flask di Jekyll.

## Persiapan

Sebelum memulai belajar Flask, pastikan Anda sudah memiliki lingkungan pengembangan Python yang sudah siap. Anda bisa menggunakan IDE seperti PyCharm atau Visual Studio Code, atau bisa juga menggunakan editor teks seperti Sublime Text atau Atom.

Selain itu, pastikan Anda sudah menginstal Flask di lingkungan pengembangan Anda. Anda bisa menginstal Flask menggunakan perintah pip seperti berikut:

~~~
pip install Flask
~~~

## Membuat Aplikasi Flask

Setelah persiapan selesai, Anda bisa mulai membuat aplikasi Flask dengan membuat file Python baru. Berikut adalah contoh kode untuk membuat aplikasi Flask sederhana:

~~~ python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello():
    return 'Hello, World!'

    if __name__ == '__main__':
        app.run(debug=True)
~~~
Kode di atas akan membuat sebuah aplikasi Flask yang berjalan di port 5000 dan akan mengembalikan teks "Hello, World!" saat URL utama diakses.

## Menjalankan Aplikasi Flask

Untuk menjalankan aplikasi Flask, cukup jalankan file Python tersebut. Anda bisa menjalankannya menggunakan perintah berikut:
~~~ python
python nama_file.py
~~~

Setelah itu, buka browser dan akses http://localhost:5000 untuk melihat hasil dari aplikasi Flask yang telah dibuat.

## Kesimpulan
Itulah tutorial singkat tentang cara belajar Flask di Jekyll. Semoga tutorial ini bisa membantu Anda memulai belajar Flask. Jika Anda ingin belajar lebih lanjut tentang Flask, Anda bisa membaca dokumentasi resminya di https://flask.palletsprojects.com/.