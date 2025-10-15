# Chapter 06: State Management dan Implementasi CRUD dengan Collection

## Rencana Materi

### 1. Dasar State Management
-   **Apa itu State?**
    -   Definisi "state" dalam konteks aplikasi Flutter (data yang dapat berubah dan memengaruhi UI).
    -   Perbedaan antara *Ephemeral State* (Local State) dan *App State* (Global State).
-   **Mengapa State Management Penting?**
    -   Masalah yang muncul tanpa state management yang baik (prop drilling, rebuild yang tidak perlu, kode yang sulit dipelihara).
    -   Kebutuhan untuk memisahkan logika bisnis dari UI.
-   **Pendekatan State Management Sederhana (tanpa package eksternal):**
    -   **`setState()`:** Untuk mengelola *Ephemeral State* di dalam `StatefulWidget`.
    -   **`InheritedWidget` (Konsep Dasar):** Menjelaskan bagaimana data dapat diwariskan ke bawah pohon widget tanpa harus meneruskannya secara manual melalui setiap konstruktor. (Tidak akan diimplementasikan secara detail, hanya konsep).
    -   **`ChangeNotifier` dan `Provider` (Konsep Dasar):** Pengenalan singkat tentang bagaimana `ChangeNotifier` dapat memberi tahu pendengar tentang perubahan, dan `Provider` sebagai cara sederhana untuk menyediakan `ChangeNotifier` ke pohon widget. (Tidak akan diimplementasikan secara detail, hanya konsep).

### 2. Implementasi State Management untuk CRUD dengan Collection
-   **Konsep CRUD:**
    -   **C**reate (Membuat): Menambahkan data baru.
    -   **R**ead (Membaca): Menampilkan data yang ada.
    -   **U**pdate (Memperbarui): Mengubah data yang sudah ada.
    -   **D**elete (Menghapus): Menghilangkan data.
-   **Menggunakan `List` sebagai Collection:**
    -   Kita akan menggunakan `List<String>` atau `List<Map<String, dynamic>>` sederhana sebagai "database" in-memory.
-   **Pendekatan State Management yang Digunakan:**
    -   Kita akan menggunakan kombinasi `StatefulWidget` dengan `setState()` untuk mengelola daftar item. Ini adalah cara paling dasar dan mudah dipahami untuk memulai CRUD in-memory.
    -   (Opsional, jika waktu/kompleksitas memungkinkan): Pengenalan singkat tentang bagaimana `Provider` bisa menyederhanakan ini.
-   **Studi Kasus: Aplikasi Daftar Belanja Sederhana (To-Do List)**
    -   **Fitur:**
        -   Menampilkan daftar item belanja.
        -   Menambahkan item baru ke daftar.
        -   Mengedit nama item yang sudah ada.
        -   Menghapus item dari daftar.
    -   **Implementasi:**
        1.  Membuat `StatefulWidget` utama yang akan menampung daftar item.
        2.  Menggunakan `TextEditingController` untuk input item baru dan editing.
        3.  Mengimplementasikan fungsi `addItem()`, `editItem()`, dan `deleteItem()` yang memanggil `setState()` untuk memperbarui UI.
        4.  Menggunakan `ListView.builder` untuk menampilkan daftar item secara efisien.
        5.  Menambahkan `AlertDialog` untuk konfirmasi penghapusan atau input editing.
