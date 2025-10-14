# Bab 1.4: Membuat Proyek Flutter Pertama

Setelah memahami persyaratan sistem dan cara mengatasi masalah umum, saatnya untuk masuk ke bagian praktik, yaitu membuat dan menjalankan proyek Flutter pertama Anda. Namun, sebelum itu, penting untuk memahami struktur direktori yang akan Anda temui.

## Struktur Proyek Flutter

Saat Anda membuat proyek baru menggunakan perintah `flutter create`, Flutter akan menghasilkan serangkaian file dan folder dengan struktur yang terorganisir. Memahami struktur ini adalah kunci untuk menavigasi dan mengembangkan aplikasi Anda secara efisien.

Berikut adalah penjelasan mengenai direktori dan file utama dalam sebuah proyek Flutter:

- **`lib/`**
  Ini adalah direktori terpenting dalam proyek Anda. Sebagian besar kode Dart yang akan Anda tulis akan berada di sini.
  - **`main.dart`**: Ini adalah titik masuk (*entry point*) utama dari aplikasi Anda. Eksekusi kode dimulai dari file ini.

- **`android/` dan `ios/`**
  Direktori ini berisi proyek *native* untuk masing-masing platform.
  - **`android/`**: Berisi semua file yang diperlukan untuk membangun aplikasi Android, termasuk file Gradle dan `AndroidManifest.xml`.
  - **`ios/`**: Berisi semua file yang diperlukan untuk membangun aplikasi iOS, termasuk konfigurasi Xcode dan `Info.plist`.
  Anda biasanya tidak perlu sering mengubah file di dalam direktori ini, kecuali saat melakukan konfigurasi spesifik untuk platform tertentu (misalnya, menambahkan izin atau mengintegrasikan pustaka *native*).

- **`web/`, `windows/`, `macos/`, `linux/`**
  Sama seperti `android/` dan `ios/`, direktori ini berisi file konfigurasi untuk membangun aplikasi Anda di platform web, desktop Windows, macOS, dan Linux.

- **`test/`**
  Direktori ini adalah tempat untuk menyimpan semua file pengujian (*testing*) Anda. Flutter mendukung berbagai jenis pengujian, seperti *unit test*, *widget test*, dan *integration test*.

- **`pubspec.yaml`**
  Ini adalah file konfigurasi utama untuk proyek Flutter Anda. Di sinilah Anda akan:
  - Mendeklarasikan dependensi atau *package* eksternal yang digunakan dalam proyek.
  - Menambahkan aset seperti gambar, *font*, atau file JSON.
  - Mengatur informasi metadata proyek seperti nama, deskripsi, dan versi aplikasi.

- **`build/`**
  Direktori ini dibuat secara otomatis saat Anda membangun atau menjalankan aplikasi. Isinya adalah hasil kompilasi dari kode Anda untuk platform target. Anda tidak perlu mengubah isi direktori ini secara manual.

- **`.gitignore`**
  File ini berisi daftar file dan direktori yang akan diabaikan oleh sistem kontrol versi Git, seperti direktori `build/`, `.dart_tool/`, dan file konfigurasi lokal lainnya.

Dengan memahami struktur dasar ini, Anda akan lebih mudah mengelola file dan mengembangkan aplikasi yang lebih kompleks di kemudian hari.

## Membuat dan Menjalankan Proyek

Sekarang, mari kita praktikkan cara membuat, menjalankan, dan memodifikasi proyek Flutter pertama Anda.

### Langkah 1: Membuat Proyek Baru

1.  Buka terminal atau Command Prompt.
2.  Navigasikan ke direktori tempat Anda ingin menyimpan proyek (misalnya, `~/development` atau `C:\Users\Anda\Documents`).
3.  Jalankan perintah `flutter create` diikuti dengan nama proyek Anda. Nama proyek harus menggunakan format `snake_case` (huruf kecil dan garis bawah sebagai pemisah).

    ```bash
    flutter create proyek_pertama_saya
    ```
    Perintah ini akan membuat sebuah direktori baru bernama `proyek_pertama_saya` yang berisi aplikasi Flutter demo sederhana.

4.  Masuk ke direktori proyek yang baru dibuat:
    ```bash
    cd proyek_pertama_saya
    ```

### Langkah 2: Menjalankan Aplikasi

Sebelum menjalankan aplikasi, pastikan Anda memiliki perangkat target yang aktif, baik itu emulator, simulator, atau perangkat fisik yang terhubung.

1.  **Pilih Perangkat Target:**
    -   **Emulator/Simulator:** Buka Android Studio atau Xcode untuk meluncurkan emulator Android atau simulator iOS.
    -   **Perangkat Fisik:** Hubungkan perangkat Android atau iOS Anda ke komputer melalui USB dan pastikan mode *developer* serta *USB debugging* telah diaktifkan.
    -   **Web:** Anda juga dapat menjalankan aplikasi di browser Chrome.

2.  **Jalankan Aplikasi:**
    Di dalam direktori proyek, jalankan perintah berikut:
    ```bash
    flutter run
    ```
    Flutter akan membangun aplikasi dan menginstalnya di perangkat target yang aktif. Proses ini mungkin memakan waktu beberapa saat saat pertama kali dijalankan. Setelah selesai, aplikasi demo akan terbuka di perangkat Anda.

### Langkah 3: Mengenal Hot Reload

Salah satu fitur paling kuat dari Flutter adalah *Hot Reload*. Fitur ini memungkinkan Anda untuk melihat perubahan pada kode secara instan tanpa harus memulai ulang aplikasi.

Mari kita coba:

1.  Buka file `lib/main.dart` di editor kode Anda (misalnya, Visual Studio Code atau Android Studio).
2.  Cari baris kode yang berisi teks `'Flutter Demo Home Page'`.
3.  Ubah teks tersebut menjadi sesuatu yang lain, misalnya `'Proyek Pertamaku'`.
    ```dart
    // Ganti ini:
    title: 'Flutter Demo Home Page',

    // Menjadi ini:
    title: 'Proyek Pertamaku',
    ```
4.  Simpan perubahan pada file tersebut (`Ctrl + S` atau `Cmd + S`).
5.  Perhatikan aplikasi Anda di perangkat. Judul aplikasi akan langsung berubah tanpa aplikasi dimulai ulang.

Itulah keajaiban *Hot Reload*! Fitur ini sangat mempercepat proses pengembangan, terutama saat Anda sedang membangun antarmuka pengguna (UI) dan ingin mencoba berbagai perubahan dengan cepat.

**Kapan menggunakan Hot Reload vs. Hot Restart?**
-   **Hot Reload (tekan `r` di terminal):** Digunakan untuk perubahan UI dan logika minor. State aplikasi tetap terjaga.
-   **Hot Restart (tekan `Shift + R` di terminal):** Digunakan untuk perubahan yang lebih besar, seperti mengubah `main()` atau `initState()`. State aplikasi akan di-reset.