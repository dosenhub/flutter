# Chapter 07: Flutter Permissions

## Rencana Materi

### 1. Dasar Flutter Permissions
-   **Apa itu Permissions?**
    -   Definisi izin (permissions) dalam konteks aplikasi mobile (akses ke kamera, lokasi, penyimpanan, dll.).
    -   Mengapa aplikasi membutuhkan izin (keamanan, privasi pengguna).
-   **Jenis-jenis Permissions:**
    -   **Install-time Permissions (Normal Permissions):** Izin yang diberikan secara otomatis saat aplikasi diinstal (misalnya, akses internet). Tidak memerlukan konfirmasi pengguna secara eksplisit saat runtime.
    -   **Runtime Permissions (Dangerous Permissions):** Izin yang memerlukan konfirmasi eksplisit dari pengguna saat aplikasi berjalan (misalnya, akses kamera, lokasi, kontak). Pengguna dapat mencabut izin ini kapan saja.
-   **Alur Permintaan Izin (Request Permission Flow):**
    -   Periksa status izin saat ini.
    -   Jika belum diberikan, minta izin kepada pengguna.
    -   Tangani respons pengguna (diberikan, ditolak, ditolak permanen).
-   **Platform-Specific Permissions:**
    -   **Android:** Menambahkan izin ke `AndroidManifest.xml`.
    -   **iOS:** Menambahkan deskripsi penggunaan izin ke `Info.plist`.

### 2. Implementasi Flutter Permissions
-   **Menggunakan Package `permission_handler`:**
    -   **Mengapa `permission_handler`?** Package ini adalah solusi cross-platform yang populer dan andal untuk mengelola izin di Flutter. Ini menyederhanakan interaksi dengan API izin native.
    -   **Menambahkan Dependensi:** Menambahkan `permission_handler` ke `pubspec.yaml`.
-   **Konfigurasi Platform-Specific:**
    -   **Android:** Menambahkan izin ke `AndroidManifest.xml` (misalnya, `CAMERA`, `ACCESS_FINE_LOCATION`).
    -   **iOS:** Menambahkan deskripsi penggunaan izin ke `Info.plist` (misalnya, `NSCameraUsageDescription`, `NSLocationWhenInUseUsageDescription`).
-   **Langkah-langkah Implementasi dengan `permission_handler`:**
    1.  **Import:** `import 'package:permission_handler/permission_handler.dart';`
    2.  **Periksa Status Izin:** `Permission.camera.status` atau `await Permission.location.status`.
        -   `PermissionStatus.granted`: Izin sudah diberikan.
        -   `PermissionStatus.denied`: Izin ditolak, bisa diminta lagi.
        -   `PermissionStatus.permanentlyDenied`: Izin ditolak permanen, pengguna harus mengaktifkan dari pengaturan aplikasi.
        -   `PermissionStatus.restricted`: Izin dibatasi oleh sistem (misalnya, kontrol orang tua).
    3.  **Minta Izin:** `await Permission.camera.request()`. Ini akan menampilkan dialog permintaan izin kepada pengguna.
    4.  **Tangani Hasil:** Berdasarkan `PermissionStatus` yang dikembalikan setelah permintaan.
    5.  **Buka Pengaturan Aplikasi:** `openAppSettings()` untuk mengarahkan pengguna ke pengaturan aplikasi jika izin ditolak permanen.

### Studi Kasus: Aplikasi Kamera Sederhana
-   **Fitur:**
    -   Meminta izin kamera.
    -   Jika izin diberikan, tampilkan pesan "Kamera siap digunakan".
    -   Jika izin ditolak, tampilkan pesan "Izin kamera ditolak".
    -   Jika izin ditolak permanen, berikan opsi untuk membuka pengaturan aplikasi.
-   **Implementasi:**
    1.  Membuat `StatefulWidget` utama.
    2.  Menggunakan `permission_handler` untuk memeriksa dan meminta izin kamera.
    3.  Memperbarui UI berdasarkan status izin.
    4.  Menambahkan tombol untuk membuka pengaturan aplikasi jika diperlukan.
