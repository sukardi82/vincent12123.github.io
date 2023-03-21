---
layout: post
title: "Streamlit Phyton"
toc: true
date: 2023-03-21 10:00:00 +0700
categories: [tutorial]
tags: [Streamlit, Tutorial] 
---

kerangka tutorial streamlit untuk pemula:

1.  Pendahuluan

*   Apa itu Streamlit
*   Manfaat menggunakan Streamlit

2.  Persiapan

*   Instalasi Streamlit
*   Struktur folder project

3.  Memulai

*   Import library Streamlit
*   Menampilkan teks pada web app

4.  Menampilkan data

*   Membaca data dari file
*   Menampilkan data dalam bentuk tabel

5.  Visualisasi data

*   Membuat grafik dengan Streamlit

6.  Interaksi

*   Membuat widget sederhana (checkbox, slider, dsb.)
*   Mereaktifkan tampilan berdasarkan input widget

7.  Deploy aplikasi

*   Hosting aplikasi dengan Heroku

8.  Kesimpulan

*   Ringkasan pembelajaran
*   Saran untuk meningkatkan aplikasi

## Pendahuluan
Streamlit adalah sebuah framework open source yang digunakan untuk membangun aplikasi web interaktif dengan mudah menggunakan bahasa Python. Dibandingkan dengan framework web lainnya, Streamlit dirancang dengan fokus pada data science dan machine learning, sehingga memungkinkan pengguna untuk membuat prototipe dan visualisasi data dengan cepat.

Manfaat menggunakan Streamlit adalah:

*   Mempermudah proses pengembangan aplikasi web, terutama untuk data science dan machine learning.
*   Tidak perlu menguasai bahasa pemrograman web seperti HTML, CSS, atau JavaScript, karena Streamlit sudah menyediakan fungsi-fungsi yang cukup untuk membuat tampilan dan interaksi pada aplikasi web.
*   Memiliki tampilan yang minimalis dan mudah dipahami, sehingga mempermudah pengguna untuk memfokuskan pada pengembangan aplikasi, bukan pada tampilannya.

Dalam tutorial ini, kita akan mempelajari cara menggunakan Streamlit dari awal hingga akhir, mulai dari instalasi, membuat tampilan, menampilkan data, hingga membuat interaksi pada aplikasi web.

## Persiapan
Sebelum kita memulai mengembangkan aplikasi web dengan Streamlit, ada beberapa persiapan yang harus dilakukan.

### 2.1 Instalasi Streamlit

Untuk menginstal Streamlit, kita dapat menggunakan pip dengan menjalankan perintah berikut pada terminal:

`pip install streamlit`

Pastikan bahwa kita menggunakan versi Python yang sudah terinstal pada komputer. Streamlit dapat berjalan pada Python versi 3.6 hingga 3.9.

### 2.2 Struktur folder project

Setelah menginstal Streamlit, kita perlu membuat struktur folder project yang akan digunakan. Struktur folder ini dapat disesuaikan dengan kebutuhan pengembangan aplikasi web yang akan dibangun. Berikut adalah struktur folder yang sederhana:

kotlin

```kotlin
- project_folder/
  - app.py
  - data/
    - data.csv
```

*   `app.py` adalah file Python yang berisi kode untuk mengembangkan aplikasi web dengan Streamlit.
*   `data/` adalah folder yang berisi data yang akan digunakan pada aplikasi web.

Setelah kita membuat struktur folder project, kita siap memulai membuat aplikasi web dengan Streamlit.

## Memulai 

Baik, berikut adalah contoh kode untuk memulai aplikasi web menggunakan Streamlit dan menampilkan teks pada web app:

```python
Copy code
import streamlit as st

st.write("Hello World!")
```

Pada contoh kode di atas, pertama-tama kita mengimpor library Streamlit menggunakan import streamlit as st. Selanjutnya, kita menampilkan teks "Hello World!" pada web app menggunakan fungsi st.write().

Setelah menjalankan kode di atas, Anda akan melihat halaman web app kosong dengan hanya teks "Hello World!" pada layar. Namun, dari sini, Anda dapat membangun aplikasi web Anda dengan menambahkan komponen lain seperti input, tombol, dan visualisasi.

## Menampilkan Data
Setelah mempersiapkan struktur folder project, langkah selanjutnya adalah menampilkan data pada aplikasi web. Untuk menampilkan data, kita perlu membaca data dari file terlebih dahulu.

### 4.1 Membaca data dari file

Berikut adalah contoh data dalam format CSV yang dapat digunakan untuk latihan atau ujicoba aplikasi web menggunakan Streamlit:
```
name,age,gender
John,25,Male
Sarah,30,Female
Tom,35,Male
Lisa,28,Female
Chris,22,Male
Emily,29,Female
Mike,40,Male
```
File tersebut terdiri dari tiga kolom yaitu "name", "age", dan "gender". Kolom "name" berisi nama orang, kolom "age" berisi usia orang dalam tahun, dan kolom "gender" berisi jenis kelamin orang (Male/Female). File ini hanya merupakan contoh, dan Anda dapat mengganti data dalam file tersebut dengan data Anda sendiri.

Kita dapat membaca data dari file CSV menggunakan library Pandas. Berikut adalah contoh kode untuk membaca file CSV dan menyimpannya ke dalam sebuah DataFrame:

python

```python
import pandas as pd

data = pd.read_csv('data/data.csv')
```

Pastikan bahwa path file CSV sesuai dengan lokasi file pada struktur folder project yang sudah kita buat sebelumnya.

### 4.2 Menampilkan data dalam bentuk tabel

Setelah membaca data, kita dapat menampilkan data dalam bentuk tabel dengan menggunakan fungsi `st.table()` dari Streamlit. Berikut adalah contoh kode untuk menampilkan data dalam bentuk tabel:

python

```python
import streamlit as st
import pandas as pd

data = pd.read_csv('data/data.csv')

st.table(data)
```

Dalam contoh kode di atas, kita mengimport Streamlit dan Pandas, membaca data dari file CSV, dan menampilkan data dalam bentuk tabel dengan fungsi `st.table()`.

Kita dapat menyesuaikan tampilan tabel dengan menambahkan argumen pada fungsi `st.table()`. Beberapa argumen yang dapat digunakan antara lain:

*   `use_container_width`: mengatur lebar tabel agar sesuai dengan lebar container aplikasi web.
*   `height`: mengatur tinggi tabel dalam satuan piksel.
*   `width`: mengatur lebar tabel dalam satuan piksel.

Berikut adalah contoh kode untuk menampilkan data dalam bentuk tabel dengan lebar tabel yang sesuai dengan lebar container aplikasi web:

python

```python
import streamlit as st
import pandas as pd

data = pd.read_csv('data/data.csv')

st.table(data, use_container_width=True)
```

Dengan mengikuti langkah-langkah di atas, kita sudah berhasil menampilkan data dalam bentuk tabel pada aplikasi web yang kita buat menggunakan Streamlit.

## Visualisasi Data
Setelah menampilkan data pada aplikasi web, langkah selanjutnya adalah membuat visualisasi data. Visualisasi data dapat membantu kita untuk memahami data dengan lebih baik dan cepat.

### 5.1 Membuat plot dengan Matplotlib

Untuk membuat plot, kita dapat menggunakan library Matplotlib. Berikut adalah contoh kode untuk membuat plot histogram pada data:

python

```python
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv('data/data.csv')

fig, ax = plt.subplots()
ax.hist(data['age'])
ax.set_xlabel('Age')
ax.set_ylabel('Count')

st.pyplot(fig)
```

Dalam contoh kode di atas, kita mengimport Streamlit, Pandas, dan Matplotlib, membaca data dari file CSV, membuat plot histogram dengan fungsi `ax.hist()`, dan menampilkan plot pada aplikasi web dengan fungsi `st.pyplot()`.

Kita dapat menyesuaikan tampilan plot dengan menambahkan argumen pada fungsi `st.pyplot()`. Beberapa argumen yang dapat digunakan antara lain:

*   `width`: mengatur lebar plot dalam satuan piksel.
*   `height`: mengatur tinggi plot dalam satuan piksel.
*   `dpi`: mengatur resolusi plot dalam dot per inch.
*   `bbox_inches`: mengatur ukuran bounding box plot dalam satuan piksel.

Berikut adalah contoh kode untuk menampilkan plot dengan lebar 700 piksel dan tinggi 400 piksel:

python

```python
import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

data = pd.read_csv('data/data.csv')

fig, ax = plt.subplots()
ax.hist(data['age'])
ax.set_xlabel('Age')
ax.set_ylabel('Count')

st.pyplot(fig, width=700, height=400)
```

### 5.2 Membuat plot dengan Seaborn

Selain Matplotlib, kita juga dapat menggunakan library Seaborn untuk membuat plot pada aplikasi web. Seaborn dapat mempermudah kita dalam membuat plot dengan tampilan yang lebih estetis dan interaktif.

Berikut adalah contoh kode untuk membuat plot histogram dengan Seaborn:

python

```python
import streamlit as st
import pandas as pd
import seaborn as sns

data = pd.read_csv('data/data.csv')

fig = sns.histplot(data=data, x='age', bins=10, kde=True)

st.pyplot(fig)
```

Dalam contoh kode di atas, kita mengimport Streamlit, Pandas, dan Seaborn, membaca data dari file CSV, membuat plot histogram dengan Seaborn, dan menampilkan plot pada aplikasi web dengan fungsi `st.pyplot()`.

Kita dapat menyesuaikan tampilan plot dengan menggunakan fungsi-fungsi dari Seaborn seperti `sns.set_style()`, `sns.set_palette()`, atau `sns.despine()`. Selain itu, Seaborn juga menyediakan banyak jenis plot seperti scatter plot, line plot, dan heat map yang dapat kita gunakan untuk membuat visualisasi data yang lebih kompleks.

Dengan mengikuti langkah-langkah di atas, kita sudah berhasil membuat visualisasi data pada aplikasi web yang kita buat menggunakan Streamlit.

## Interaksi dengan Pengguna
Streamlit memungkinkan kita untuk membuat interaksi dengan pengguna pada aplikasi web yang kita buat. Interaksi tersebut dapat berupa input data, memilih opsi, atau mengeklik tombol.

### 6.1 Membuat Input Text

Untuk membuat input text, kita dapat menggunakan fungsi `st.text_input()`. Berikut adalah contoh kode untuk membuat input text pada aplikasi web:

python

```python
import streamlit as st

name = st.text_input('Enter your name:')
st.write('Hello, ' + name)
```

Dalam contoh kode di atas, kita membuat input text dengan label "Enter your name:" dan menyimpan hasil input dalam variabel `name`. Selanjutnya, kita menampilkan pesan "Hello, \[nama\]" dengan fungsi `st.write()`.

### 6.2 Membuat Dropdown

Untuk membuat dropdown, kita dapat menggunakan fungsi `st.selectbox()`. Berikut adalah contoh kode untuk membuat dropdown pada aplikasi web:

python

```python
import streamlit as st

gender = st.selectbox('Select your gender:', ['Male', 'Female'])
st.write('You selected', gender)
```

Dalam contoh kode di atas, kita membuat dropdown dengan label "Select your gender:" dan opsi "Male" dan "Female". Selanjutnya, kita menampilkan pesan "You selected \[gender\]" dengan fungsi `st.write()`.

### 6.3 Membuat Checkbox

Untuk membuat checkbox, kita dapat menggunakan fungsi `st.checkbox()`. Berikut adalah contoh kode untuk membuat checkbox pada aplikasi web:

python

```python
import streamlit as st

show_image = st.checkbox('Show image')
if show_image:
    st.image('image.png')
```

Dalam contoh kode di atas, kita membuat checkbox dengan label "Show image". Jika checkbox dicentang, maka gambar "image.png" akan ditampilkan dengan fungsi `st.image()`.

### 6.4 Membuat Button

Untuk membuat tombol, kita dapat menggunakan fungsi `st.button()`. Berikut adalah contoh kode untuk membuat tombol pada aplikasi web:

python

```python
import streamlit as st

if st.button('Click me'):
    st.write('You clicked the button!')
```

Dalam contoh kode di atas, kita membuat tombol dengan label "Click me". Jika tombol diklik, maka pesan "You clicked the button!" akan ditampilkan dengan fungsi `st.write()`.

### 6.5 Menggunakan Sidebar

Sidebar pada Streamlit memungkinkan kita untuk menampilkan opsi atau input pada sisi kanan halaman aplikasi web. Berikut adalah contoh kode untuk menggunakan sidebar pada aplikasi web:

python

```python
import streamlit as st

name = st.sidebar.text_input('Enter your name:')
gender = st.sidebar.selectbox('Select your gender:', ['Male', 'Female'])

if st.sidebar.button('Click me'):
    st.write('Hello, ' + name + ' (' + gender + ')')
```

Dalam contoh kode di atas, kita menggunakan fungsi `st.sidebar.text_input()` untuk membuat input text pada sidebar, `st.sidebar.selectbox()` untuk membuat dropdown pada sidebar, dan `st.sidebar.button()` untuk membuat tombol pada sidebar. Jika tombol pada sidebar diklik, maka pesan "Hello, \[nama\] (\[gender\])" akan ditampilkan dengan fungsi `st.write()`.

> buatkan lagi untuk mengunakan sidebar dan lanjutkan apabila belum selesai

### 6.6 Menggunakan Date Input

Untuk membuat input tanggal, kita dapat menggunakan fungsi `st.date_input()`. Berikut adalah contoh kode untuk membuat input tanggal pada aplikasi web:

python

```python
import streamlit as st

birthday = st.date_input('Enter your birthday:')
st.write('Your birthday is:', birthday)
```

Dalam contoh kode di atas, kita membuat input tanggal dengan label "Enter your birthday:". Selanjutnya, kita menampilkan pesan "Your birthday is: \[tanggal\]" dengan fungsi `st.write()`.

### 6.7 Menggunakan Slider

Untuk membuat slider, kita dapat menggunakan fungsi `st.slider()`. Berikut adalah contoh kode untuk membuat slider pada aplikasi web:

python

```python
import streamlit as st

age = st.slider('Enter your age:', 0, 100, 25)
st.write('Your age is:', age)
```

Dalam contoh kode di atas, kita membuat slider dengan label "Enter your age:", nilai minimum 0, nilai maksimum 100, dan nilai awal 25. Selanjutnya, kita menampilkan pesan "Your age is: \[umur\]" dengan fungsi `st.write()`.

### 6.8 Menampilkan Progress Bar

Untuk menampilkan progress bar, kita dapat menggunakan fungsi `st.progress()`. Berikut adalah contoh kode untuk menampilkan progress bar pada aplikasi web:

python

```python
import streamlit as st
import time

progress = st.progress(0)
for i in range(100):
    progress.progress(i+1)
    time.sleep(0.1)
st.write('Progress completed!')
```

Dalam contoh kode di atas, kita membuat progress bar dengan fungsi `st.progress()` dan inisialisasi nilai awal 0. Selanjutnya, kita mengupdate nilai progress bar dalam loop dan menunggu 0.1 detik setiap iterasi menggunakan fungsi `time.sleep()`. Setelah progress bar selesai, kita menampilkan pesan "Progress completed!" dengan fungsi `st.write()`.

Dalam beberapa kasus, kita mungkin ingin menghubungkan interaksi pengguna dengan data atau visualisasi yang kompleks. Dalam kasus ini, kita dapat menggunakan perpustakaan Python seperti Pandas atau Matplotlib untuk memproses data dan menghasilkan visualisasi.

Ketika kita memiliki kode yang kompleks atau membutuhkan waktu lama untuk dieksekusi, kita dapat menggunakan fitur caching Streamlit untuk mempercepat waktu loading. Caching pada Streamlit memungkinkan kita untuk menyimpan hasil perhitungan pada cache dan menggunakannya kembali saat aplikasi web dimuat kembali oleh pengguna.

