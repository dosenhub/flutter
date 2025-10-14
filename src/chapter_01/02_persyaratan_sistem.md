## 1.2 Persyaratan Sistem dan Instalasi

Sebelum memulai pengembangan dengan Flutter, langkah pertama adalah memastikan bahwa lingkungan pengembangan Anda memenuhi persyaratan sistem yang dibutuhkan. Setiap sistem operasi memiliki beberapa kebutuhan spesifik yang harus dipenuhi.

### Persyaratan Sistem

Berikut adalah rincian persyaratan sistem untuk pengembangan Flutter pada Windows, macOS, dan Linux.

#### Windows

| Kategori      | Persyaratan Minimum                                       |
|---------------|-----------------------------------------------------------|
| **Sistem Operasi** | Windows 10 atau yang lebih baru (64-bit).                 |
| **Ruang Disk**  | 1.64 GB (tidak termasuk IDE dan *tools* lainnya).          |
| **Peralatan**   | - **Windows PowerShell 5.0** atau lebih baru.             |
|               | - **Git for Windows** 2.x atau lebih baru.                |

#### macOS

| Kategori      | Persyaratan Minimum                                       |
|---------------|-----------------------------------------------------------|
| **Sistem Operasi** | macOS, versi 10.15 (Catalina) atau yang lebih baru.       |
| **Ruang Disk**  | 2.8 GB (tidak termasuk IDE dan *tools* lainnya).          |
| **Peralatan**   | - **Git** 2.x atau lebih baru.                            |
|               | - **Xcode** untuk pengembangan aplikasi iOS.              |

#### Linux

| Kategori      | Persyaratan Minimum                                       |
|---------------|-----------------------------------------------------------|
| **Sistem Operasi** | Distribusi Linux 64-bit (contoh: Debian, Ubuntu, Fedora). |
| **Ruang Disk**  | 600 MB (tidak termasuk IDE dan *tools* lainnya).          |
| **Peralatan**   | - `bash`, `curl`, `file`, `git 2.x`, `mkdir`, `rm`, `unzip`, `which`, `xz-utils`, `zip` |
|               | - `libGLU.so.1` (biasanya tersedia melalui paket `mesa`).   |

**Catatan Penting:**
- **IDE (Integrated Development Environment):** Meskipun tidak wajib, sangat disarankan untuk menggunakan IDE seperti **Visual Studio Code** atau **Android Studio** dengan *plugin* Flutter dan Dart untuk pengalaman pengembangan yang lebih baik.
- **Ruang Disk Tambahan:** Persyaratan ruang disk di atas hanya untuk Flutter SDK. Anda akan memerlukan ruang tambahan yang signifikan untuk Android SDK, Xcode, dan *tools* lainnya, yang bisa mencapai 10 GB atau lebih.

### Panduan Instalasi Flutter SDK

Berikut adalah panduan langkah demi langkah untuk menginstal Flutter SDK di berbagai sistem operasi.

#### Langkah 1: Unduh Flutter SDK

1.  Buka situs resmi Flutter di [flutter.dev](https://flutter.dev).
2.  Navigasi ke halaman instalasi dan unduh versi stabil terbaru dari Flutter SDK yang sesuai dengan sistem operasi Anda (Windows, macOS, atau Linux).

#### Langkah 2: Ekstrak File SDK

-   **Windows:** Ekstrak file `.zip` yang telah diunduh ke lokasi yang tidak memerlukan hak akses administrator, misalnya `C:\src\flutter`. Hindari menginstalnya di `C:\Program Files\`.
-   **macOS/Linux:** Ekstrak file `tar.xz` ke direktori pilihan Anda, misalnya `~/development/` atau `~/flutter_sdk/`.

#### Langkah 3: Konfigurasi `PATH`

Langkah ini penting agar perintah `flutter` dapat diakses dari terminal mana pun.

-   **Windows:**
    1.  Cari "Environment Variables" di Start Menu dan pilih "Edit the system environment variables".
    2.  Klik tombol "Environment Variables...".
    3.  Di bawah "User variables", pilih variabel `Path` dan klik "Edit".
    4.  Klik "New" dan tambahkan path lengkap ke direktori `bin` di dalam folder Flutter Anda (contoh: `C:\src\flutter\bin`).
    5.  Klik "OK" untuk menyimpan perubahan.

-   **macOS/Linux:**
    1.  Buka file konfigurasi *shell* Anda (misalnya, `~/.zshrc`, `~/.bashrc`, atau `~/.bash_profile`) dengan editor teks. Contoh untuk Zsh: `nano ~/.zshrc`.
    2.  Tambahkan baris berikut di akhir file, sesuaikan dengan path tempat Anda mengekstrak Flutter:
        ```bash
        export PATH="$PATH:[PATH_KE_FLUTTER_ANDA]/bin"
        ```
        Contoh: `export PATH="$PATH:~/development/flutter/bin"
    3.  Simpan file dan muat ulang konfigurasi *shell* dengan menjalankan `source ~/.zshrc` (atau file yang sesuai) atau dengan memulai ulang terminal.

#### Langkah 4: Jalankan `flutter doctor`

`flutter doctor` adalah perintah untuk memeriksa lingkungan pengembangan Anda dan melaporkan status instalasi Flutter.

1.  Buka terminal atau Command Prompt **baru**.
2.  Jalankan perintah berikut:
    ```bash
    flutter doctor
    ```
3.  Perhatikan outputnya. `flutter doctor` akan memberikan laporan tentang:
    -   Versi Flutter SDK.
    -   Status Android toolchain (termasuk Android Studio dan SDK).
    -   Status Xcode (di macOS).
    -   Perangkat yang terhubung.
    -   Plugin IDE yang terinstal.

Jika `flutter doctor` menemukan masalah (ditandai dengan `[!]` atau `[X]`), ikuti instruksi yang disarankan untuk memperbaikinya.