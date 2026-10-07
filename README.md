# Feature Engineering

## Identitas
Kelas 2025C

Program Studi S1 Sains Data

Universitas Negeri Surabaya

Nama Anggota:

Namira Rachmi Andini (25031554153)

Syahira Nanda Raihanna (25031554199)
## Deskripsi

Repository ini berisi implementasi **Feature Engineering pada data teks** yang bertujuan mengubah teks menjadi bentuk numerik agar dapat diproses dan dianalisis menggunakan metode machine learning maupun teknik analisis teks.

Dataset yang digunakan adalah dataset film `combined.csv` yang berisi informasi mengenai film, termasuk judul, genre, tahun, distribusi, deskripsi, URL, dan gambar sampul. Pada proses ini, kolom **description** digunakan sebagai sumber utama data teks.

Feature Engineering dilakukan dengan mengubah teks menjadi representasi numerik menggunakan **TF-IDF** dan **Binary Count Vectorizer**. Kedua metode tersebut menghasilkan bentuk representasi yang berbeda dan dapat digunakan sebagai dasar untuk proses analisis kemiripan antar dokumen.

## Langkah-Langkah

### 1. Mempersiapkan Dataset

Dataset `combined.csv` dibaca menggunakan Pandas. Data kemudian diperiksa untuk mengetahui jumlah baris dan struktur kolom yang tersedia.

Kolom `description` digunakan sebagai teks utama karena berisi deskripsi atau sinopsis film yang dapat dianalisis.

### 2. Menyiapkan Teks

Data pada kolom `description` digunakan sebagai corpus. Nilai yang kosong ditangani dengan menggantinya menjadi teks kosong agar tidak menyebabkan error pada proses berikutnya.

### 3. Mengubah Teks Menjadi Lowercase

Seluruh teks diubah menjadi huruf kecil menggunakan proses `lower()`.

Langkah ini dilakukan agar kata yang sama tetapi memiliki perbedaan kapitalisasi, seperti `Movie` dan `movie`, dapat dianggap sebagai kata yang sama.

### 4. Menghapus Stopwords

Stopwords bahasa Inggris dihapus menggunakan daftar stopwords dari NLTK.

Contohnya seperti kata umum `the`, `is`, `and`, dan kata lainnya yang dianggap kurang memberikan informasi penting dalam proses analisis teks.

### 5. Melakukan Stemming

Setelah stopwords dihapus, setiap kata diproses menggunakan **Porter Stemmer**.

Stemming bertujuan mengubah kata ke bentuk dasarnya. Dengan demikian, kata yang memiliki bentuk berbeda tetapi berasal dari kata dasar yang sama dapat direpresentasikan secara lebih seragam.

### 6. Membentuk Corpus

Hasil preprocessing setiap deskripsi kemudian digabungkan kembali menjadi teks dan disimpan dalam variabel `corpus`.

Corpus inilah yang digunakan sebagai input untuk proses Feature Engineering.

### 7. Feature Engineering Menggunakan TF-IDF

Metode pertama yang digunakan adalah **TF-IDF (Term Frequency-Inverse Document Frequency)**.

TF-IDF memberikan bobot pada setiap kata berdasarkan tingkat kepentingannya dalam suatu dokumen dibandingkan dengan keseluruhan dokumen.

Pada implementasi ini digunakan `TfidfVectorizer` dengan:

* `sublinear_tf=True`
* `max_features=5000`

Hasilnya berupa representasi numerik yang dapat digunakan untuk membandingkan dokumen berdasarkan kandungan kata di dalamnya.

### 8. Feature Engineering Menggunakan Binary Count Vectorizer

Metode kedua menggunakan **CountVectorizer** dengan parameter `binary=True`.

Pada representasi binary, setiap kata hanya menunjukkan apakah kata tersebut muncul atau tidak dalam suatu dokumen.

Nilai fitur akan berupa:

* `1` → kata terdapat dalam dokumen
* `0` → kata tidak terdapat dalam dokumen

Jumlah fitur dibatasi hingga maksimal 5000 fitur menggunakan `max_features=5000`.

### 9. Menampilkan Fitur yang Dihasilkan

Setelah proses Feature Engineering selesai, fitur yang terbentuk ditampilkan menggunakan `get_feature_names_out()`.

Fitur tersebut menunjukkan kumpulan kata yang digunakan sebagai representasi numerik dari seluruh dokumen.

## Hasil

Feature Engineering menghasilkan dua bentuk representasi teks, yaitu:

1. **TF-IDF**, yang memberikan bobot berdasarkan tingkat kepentingan kata dalam dokumen.
2. **Binary Vector**, yang menunjukkan keberadaan atau ketidakberadaan kata dalam dokumen.

Hasil representasi tersebut selanjutnya dapat digunakan untuk proses **Text Similarity**, seperti Cosine Similarity dan Jaccard Similarity.

