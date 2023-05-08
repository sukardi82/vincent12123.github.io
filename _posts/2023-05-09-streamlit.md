---
layout: post
title: "Streamlit Student Task"
toc: true
date: 2023-05-09 10:00:00 +0700
categories: [tutorial]
tags: [Streamlit, Tutorial] 
---

Langkah 1: Persiapan Pastikan Python sudah terinstal di komputer Anda. Selanjutnya, instal library Streamlit dengan menggunakan perintah berikut di terminal atau command prompt:

`pip install streamlit`

Langkah 2: Buat file Python Buat file baru dengan ekstensi `.py`, misalnya `app.py`, dan buka dengan editor teks favorit Anda.

Langkah 3: Impor library yang diperlukan Tambahkan baris berikut di awal file `app.py`:



```python
import streamlit as st
```

Langkah 4: Tambahkan konten ke aplikasi `Streamlit` Tambahkan kode berikut di bawah baris kode yang telah ditambahkan pada langkah sebelumnya:



```python
def main():
    st.title("Aplikasi Tugas Siswa")
    
    # Input nama siswa
    nama_siswa = st.text_input("Masukkan Nama Siswa:")
    
    # Pilihan tugas
    pilihan_tugas = st.selectbox("Pilih Tugas:", ["Tugas 1", "Tugas 2", "Tugas 3"])
    
    # Input nilai
    nilai = st.number_input("Masukkan Nilai:", min_value=0.0, max_value=100.0, step=0.1)
    
    # Tombol submit
    submit_button = st.button("Submit")
    
    # Tampilkan hasil
    if submit_button:
        st.write("Nama Siswa:", nama_siswa)
        st.write("Tugas:", pilihan_tugas)
        st.write("Nilai:", nilai)

if __name__ == '__main__':
    main()
```

Langkah 5: Menjalankan aplikasi Streamlit Simpan file `app.py` dan jalankan perintah berikut di terminal atau command prompt:



```python
streamlit run app.py
```

Setelah itu, aplikasi Streamlit akan berjalan dan URL lokal akan ditampilkan di terminal atau command prompt. Anda dapat mengakses aplikasi melalui URL tersebut di web browser Anda.

Langkah 6: Menggunakan aplikasi Streamlit Anda akan melihat judul "Aplikasi Tugas Siswa" di halaman aplikasi. Masukkan nama siswa, pilih tugas, dan masukkan nilai. Setelah itu, klik tombol "Submit". Hasilnya akan ditampilkan di bawah tombol tersebut.

Anda dapat mengubah nama siswa, tugas, dan nilai, kemudian klik tombol "Submit" lagi untuk melihat hasil yang berbeda.

# Buat file baru dengan nama app1.py

```python
import streamlit as st

def main():
    st.title("Aplikasi Tugas Siswa")
    
    # Input nama siswa
    nama_siswa = st.text_input("Masukkan Nama Siswa:")
    
    # Pilihan tugas
    pilihan_tugas = st.selectbox("Pilih Tugas:", ["Tugas 1", "Tugas 2", "Tugas 3"])
    
    # Input nilai
    nilai = st.number_input("Masukkan Nilai:", min_value=0.0, max_value=100.0, step=0.1)
    
    # Tombol submit
    submit_button = st.button("Submit")
    
    # Tampilkan hasil
    if submit_button:
        st.write("Nama Siswa:", nama_siswa)
        st.write("Tugas:", pilihan_tugas)
        st.write("Nilai:", nilai)
        
        # Hitung rata-rata
        nilai_list = st.session_state.get('nilai_list', [])
        nilai_list.append(nilai)
        rata_rata = sum(nilai_list) / len(nilai_list)
        st.write("Rata-rata Nilai:", round(rata_rata, 2))
        
        # Simpan nilai ke session
        st.session_state['nilai_list'] = nilai_list

if __name__ == '__main__':
    main()
```

Pada versi ini, kami menggunakan `st.session_state` untuk menyimpan data nilai siswa. Setiap kali tombol "Submit" diklik, nilai akan ditambahkan ke dalam daftar `nilai_list` dan rata-rata akan dihitung ulang. Hasil rata-rata nilai akan ditampilkan di bawah nilai yang dimasukkan.

Anda dapat menjalankan aplikasi ini dengan perintah `streamlit run app1.py` seperti sebelumnya. Setiap kali Anda mengirimkan nilai baru, aplikasi akan menghitung ulang rata-rata nilai berdasarkan semua nilai yang telah dimasukkan sebelumnya.

# Buat File baru dengan nama app2.py

```python
import streamlit as st

def main():
    st.title("Aplikasi Tugas Siswa")
    
    # Input nama siswa
    nama_siswa = st.text_input("Masukkan Nama Siswa:")
    
    # Pilihan tugas
    pilihan_tugas = st.selectbox("Pilih Tugas:", ["Tugas 1", "Tugas 2", "Tugas 3"])
    
    # Input nilai
    nilai = st.number_input("Masukkan Nilai:", min_value=0.0, max_value=100.0, step=0.1)
    
    # Tombol submit
    submit_button = st.button("Submit")
    
    # Tampilkan hasil
    if submit_button:
        st.write("Nama Siswa:", nama_siswa)
        st.write("Tugas:", pilihan_tugas)
        st.write("Nilai:", nilai)
        
        # Hitung rata-rata
        nilai_list = st.session_state.get('nilai_list', [])
        nilai_list.append(nilai)
        rata_rata = sum(nilai_list) / len(nilai_list)
        st.write("Rata-rata Nilai:", round(rata_rata, 2))
        
        # Tentukan Grade
        if rata_rata >= 90:
            grade = "A"
        elif rata_rata >= 80:
            grade = "B"
        elif rata_rata >= 70:
            grade = "C"
        elif rata_rata >= 60:
            grade = "D"
        else:
            grade = "E"
        
        st.write("Grade:", grade)
        
        # Simpan nilai ke session
        st.session_state['nilai_list'] = nilai_list

if __name__ == '__main__':
    main()
```

Pada kode di atas, kami menambahkan perhitungan grade berdasarkan rata-rata nilai. Sesuai dengan skala standar, kami menggunakan batas nilai tertentu untuk menentukan grade siswa. Setelah rata-rata nilai dihitung, grade akan ditentukan berdasarkan batas-batas tersebut dan ditampilkan di aplikasi.

Anda dapat menjalankan aplikasi ini dengan perintah `streamlit run app2.py` seperti sebelumnya. Setiap kali Anda mengirimkan nilai baru, aplikasi akan menghitung ulang rata-rata nilai dan menampilkan grade yang sesuai.