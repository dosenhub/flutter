# Chapter 05: Form Handling dan Data Persistence

## Rencana Materi

### 1. Konsep Form di Flutter
-   **Pentingnya Form:** Untuk mengumpulkan input dari pengguna (login, pendaftaran, feedback, dll.).
-   **Widget `Form`:** Widget yang berfungsi sebagai kontainer untuk mengelompokkan, memvalidasi, dan menyimpan beberapa `FormField`.
-   **`GlobalKey<FormState>`:** Kunci unik yang digunakan untuk mengidentifikasi `Form` dan memungkinkan kita untuk berinteraksi dengannya (misalnya, untuk memvalidasi atau menyimpan form).
-   **Widget `TextFormField`:** Kombinasi dari `TextField` dengan kemampuan untuk berpartisipasi dalam sebuah `Form` (validasi, penyimpanan, dll.).

### 2. Pengambilan Nilai dari Form
-   **Menggunakan `TextEditingController`:**
    -   Cara paling umum untuk mendapatkan nilai dari sebuah `TextField` atau `TextFormField` secara *real-time*.
    -   Membuat instance `TextEditingController`.
    -   Menghubungkannya ke properti `controller` di `TextFormField`.
    -   Mengakses nilai melalui `_controller.text`.
    -   Pentingnya memanggil `dispose()` pada controller.
-   **Menggunakan `onSaved` dari `Form`:**
    -   Cara untuk mendapatkan semua nilai dari `FormField` di dalam `Form` sekaligus.
    -   Mendefinisikan callback `onSaved` pada setiap `TextFormField`.
    -   Memanggil `_formKey.currentState.save()` untuk mentrigger semua callback `onSaved`.

### 3. Form Validation
-   **Pentingnya Validasi:** Memastikan pengguna memasukkan data yang valid dan sesuai format sebelum diproses.
-   **Menggunakan Properti `validator`:**
    -   Setiap `FormField` memiliki properti `validator`.
    -   `validator` adalah sebuah fungsi yang menerima `String?` (nilai input) dan harus mengembalikan `null` jika valid, atau `String` (pesan error) jika tidak valid.
    -   Contoh validasi: tidak boleh kosong, format email, panjang minimal password.
-   **Memicu Validasi:**
    -   Memanggil `_formKey.currentState.validate()` akan menjalankan semua fungsi `validator` di dalam `Form`.
    -   Method ini mengembalikan `true` jika semua field valid, dan `false` jika ada yang tidak valid.

### 4. Form Event
-   **`onChanged`:** Event yang dipicu setiap kali nilai dalam `TextFormField` berubah. Berguna untuk logika *real-time* (misalnya, search filter).
-   **`onFieldSubmitted`:** Event yang dipicu ketika pengguna menekan tombol "submit" atau "next" pada keyboard. Berguna untuk memindahkan fokus ke field berikutnya atau men-submit form.

### 5. Dasar Data Persistence
-   **Apa itu Data Persistence?** Proses menyimpan data sehingga data tersebut tidak hilang ketika aplikasi ditutup.
-   **Jenis-jenis Penyimpanan Lokal di Flutter:**
    -   **Shared Preferences:** Untuk data sederhana (key-value pairs) seperti pengaturan, status login, tema. (Fokus bab ini).
    -   **Local Database (SQLite/sqflite):** Untuk data terstruktur yang kompleks dan besar.
    -   **File Storage:** Untuk menyimpan file mentah (gambar, dokumen, JSON).

### 6. Implementasi Data Persistence dengan `shared_preferences`
-   **Menambahkan Dependensi:** Menambahkan `shared_preferences` ke `pubspec.yaml`.
-   **Mendapatkan Instance:** `SharedPreferences.getInstance()`.
-   **Menyimpan Data (Write):**
    -   `prefs.setString(key, value)`
    -   `prefs.setInt(key, value)`
    -   `prefs.setBool(key, value)`
    -   `prefs.setDouble(key, value)`
-   **Membaca Data (Read):**
    -   `prefs.getString(key)`
    -   `prefs.getInt(key)`
    -   `prefs.getBool(key)`
    -   `prefs.getDouble(key)`
    -   Menangani nilai `null` jika key tidak ditemukan.
-   **Menghapus Data:** `prefs.remove(key)`.

### Studi Kasus: Halaman Login Sederhana
-   Membuat halaman login dengan field "Email" dan "Password".
-   Menerapkan validasi untuk kedua field.
-   Jika login berhasil (validasi lolos), simpan status "sudah login" ke `shared_preferences`.
-   Saat aplikasi dibuka kembali, periksa `shared_preferences`. Jika status "sudah login" ada, langsung arahkan ke halaman utama (HomeScreen), lewati halaman login.
-   Menambahkan tombol "Logout" di HomeScreen yang akan menghapus status login dari `shared_preferences`.
