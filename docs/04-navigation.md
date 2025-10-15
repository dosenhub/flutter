# Chapter 04: Navigation

## Rencana Materi

### 1. Konsep Navigation di Flutter
-   **Stack of Pages:** Menjelaskan bagaimana Flutter mengelola layar (disebut `Route`) dalam sebuah tumpukan (Stack). Layar baru ditumpuk di atas, dan tombol kembali akan melepas layar teratas.
-   **Navigator Widget:** Pengenalan `Navigator`, widget yang mengelola tumpukan `Route`.
-   **Route:** Apa itu `Route`? (Contoh: `MaterialPageRoute`).

### 2. Metode Navigasi dalam Flutter
-   **Navigasi Dasar (Anonymous Routes):**
    -   `Navigator.push()`: Mendorong `Route` baru ke tumpukan. Ini digunakan untuk pindah ke layar baru.
    -   `Navigator.pop()`: Melepas `Route` teratas dari tumpukan. Ini digunakan untuk kembali ke layar sebelumnya.
    -   Mengirim data ke layar baru (melalui konstruktor `Widget`).
    -   Mengembalikan data dari layar (menggunakan `await` pada `Navigator.push()` dan `Navigator.pop(result)`).

-   **Navigasi Bernama (Named Routes):**
    -   **Keuntungan:** Memisahkan definisi rute dari logika navigasi, menghindari duplikasi kode, dan membuat navigasi lebih bersih.
    -   Mendefinisikan `routes` di `MaterialApp`.
    -   `Navigator.pushNamed()`: Pindah ke layar baru menggunakan nama rutenya.
    -   `Navigator.pushReplacementNamed()`: Pindah ke layar baru dan menghapus layar saat ini dari tumpukan (berguna untuk skenario seperti login).
    -   `Navigator.popAndPushNamed()`: Kembali satu langkah, lalu langsung mendorong rute baru.
    -   Mengirim argumen dengan `pushNamed` (menggunakan `arguments` parameter).

### 3. Implementasi Navigasi ke dalam Studi Kasus
-   **Studi Kasus: Aplikasi Multi-Layar Sederhana**
    -   **Layar 1 (HomeScreen):** Berisi daftar item (misalnya, daftar produk). Terdapat tombol untuk pindah ke layar detail.
    -   **Layar 2 (DetailScreen):** Menampilkan detail dari item yang dipilih di `HomeScreen`. Menerima data (misalnya, ID produk) dari `HomeScreen`. Terdapat tombol kembali.
    -   **Layar 3 (SettingsScreen):** Layar pengaturan yang dapat diakses dari `HomeScreen`.
    -   **Implementasi:**
        1.  Membuat proyek baru.
        2.  Membuat file terpisah untuk setiap layar (`home_screen.dart`, `detail_screen.dart`, `settings_screen.dart`).
        3.  Menggunakan **Named Routes** untuk mendefinisikan rute (`/`, `/detail`, `/settings`).
        4.  Mengimplementasikan `Navigator.pushNamed` dari `HomeScreen` ke `DetailScreen` sambil mengirim ID item.
        5.  Membaca argumen di `DetailScreen` untuk menampilkan data yang benar.
        6.  Menggunakan `Navigator.pop` di `DetailScreen` untuk kembali.
        7.  Menambahkan tombol di `HomeScreen` untuk navigasi ke `SettingsScreen`.
