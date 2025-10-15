# Bab 2: Dasar Pemrograman Dart

## Rencana Implementasi

### Bagian 1: Teori

-   [x] **Dart sebagai Bahasa Pemrograman Modern:**
    -   [x] Jelaskan konsep *Type Inference* dengan `var` dan `final`.
    -   [x] Jelaskan konsep *Mutability Control* dengan `final` dan `const`.
    -   [x] Jelaskan konsep *Null Safety* dengan `?` dan `!`.
-   [x] **Tipe Data Fundamental di Dart:**
    -   [x] Jelaskan tipe data `String` untuk teks.
    -   [x] Jelaskan tipe data `num` (`int` dan `double`) untuk angka.
    -   [x] Jelaskan tipe data `bool` untuk nilai *true/false*.
    -   [x] Jelaskan tipe data `List` untuk koleksi data.
    -   [x] Jelaskan tipe data `Map` untuk koleksi data *key-value*.

### Bagian 2: Praktek (Studi Kasus)

-   [x] **Studi Kasus: Membuat Program Pengelolaan Data Kontak Sederhana**
    -   [x] **Langkah 1: Mendefinisikan Data Kontak**
        -   [x] Gunakan `var` dan `final` untuk membuat variabel nama, umur, dan nomor telepon (*Type Inference* & *Mutability*).
        -   [x] Gunakan tipe data `String` dan `int`.
        -   [x] Buat variabel untuk hobi menggunakan `List<String>`.
    -   [x] **Langkah 2: Menangani Data yang Mungkin Kosong (Null)**
        -   [x] Buat variabel `String?` untuk alamat email yang boleh kosong (*Null Safety*).
        -   [x] Tulis fungsi untuk menampilkan email, dengan penanganan jika email tersebut `null`.
    -   [x] **Langkah 3: Mengelompokkan Data dengan `Map`**
        -   [x] Gabungkan semua informasi kontak (nama, umur, telepon, hobi, email) ke dalam sebuah `Map<String, dynamic>`.
        -   [x] Gunakan `const` untuk membuat `Map` yang tidak dapat diubah.
    -   [x] **Langkah 4: Menampilkan Data Kontak**
        -   [x] Buat fungsi yang menerima `Map` data kontak dan menampilkannya dalam format yang rapi menggunakan interpolasi `String`.
        -   [x] Tunjukkan cara mengakses data dari `List` dan `Map`.
