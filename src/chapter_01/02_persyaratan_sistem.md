## 1.2 Persyaratan Sistem dan Instalasi Flutter

Bagian ini akan menjelaskan persyaratan sistem yang dibutuhkan untuk pengembangan aplikasi dengan Flutter dan memberikan panduan instalasi langkah demi langkah.

### Persyaratan Sistem

Untuk dapat mengembangkan aplikasi dengan Flutter, pastikan sistem Anda memenuhi persyaratan minimum berikut:

- **Windows:**
    - Windows 7 SP1 atau yang lebih baru (64-bit).
    - Ruang disk kosong minimal 1.64 GB (tidak termasuk IDE/tools).
    - Windows PowerShell 5.0 atau yang lebih baru.
    - Git for Windows.

- **macOS:**
    - macOS (64-bit).
    - Ruang disk kosong minimal 2.8 GB (tidak termasuk IDE/tools).
    - Git.

- **Linux:**
    - Linux (64-bit).
    - Ruang disk kosong minimal 600 MB (tidak termasuk IDE/tools).
    - `bash`, `mkdir`, `rm`, `git`, `curl`, `unzip`, `which`.

### Panduan Instalasi

Berikut adalah langkah-langkah untuk menginstal Flutter SDK:

1.  **Unduh Flutter SDK:** Kunjungi situs resmi Flutter di [https://flutter.dev/docs/get-started/install](https://flutter.dev/docs/get-started/install) dan unduh versi stabil terbaru yang sesuai dengan sistem operasi Anda.

2.  **Ekstrak File:** Ekstrak file zip yang telah diunduh ke lokasi yang Anda inginkan (misalnya, `C:\src\flutter` di Windows atau `~/development` di macOS/Linux).

3.  **Update Path:** Tambahkan direktori `flutter/bin` ke dalam *environment variable* `PATH` Anda.
    - **Windows:** Cari "Edit the system environment variables" -> "Environment Variables..." -> di bawah "User variables", pilih "Path" -> "Edit..." -> "New" -> tambahkan path ke `flutter\bin`.
    - **macOS/Linux:** Buka file `~/.zshrc` atau `~/.bashrc` dan tambahkan baris berikut: `export PATH="$PATH:[PATH_TO_FLUTTER_GIT_DIRECTORY]/flutter/bin"`.

4.  **Verifikasi Instalasi:** Jalankan perintah `flutter doctor` di terminal atau *command prompt*. Perintah ini akan memeriksa *environment* Anda dan menampilkan laporan tentang status instalasi Flutter.