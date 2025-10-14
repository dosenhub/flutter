## 1.3 Troubleshooting Instalasi

Proses instalasi Flutter dan konfigurasinya terkadang dapat menimbulkan beberapa masalah umum. Bab ini akan membahas masalah-masalah tersebut beserta solusinya untuk membantu Anda memulai pengembangan dengan lancar.

### Masalah Umum dan Solusi

Berikut adalah beberapa masalah yang sering ditemui saat instalasi Flutter.

#### 1. Perintah `flutter` Tidak Dikenali

- **Masalah:** Setelah instalasi, terminal atau *Command Prompt* menampilkan pesan seperti `flutter: command not found` atau `'flutter' is not recognized as an internal or external command`.
- **Penyebab:** Lokasi direktori `bin` di dalam folder instalasi Flutter SDK belum ditambahkan ke *environment variable* `PATH` sistem Anda.
- **Solusi:**
    1.  Temukan lokasi folder `flutter` di sistem Anda.
    2.  Salin path lengkap menuju direktori `bin` di dalamnya (contoh: `C:\src\flutter\bin` di Windows atau `~/development/flutter/bin` di macOS/Linux).
    3.  Tambahkan path tersebut ke *environment variable* `PATH` Anda.
    4.  Tutup dan buka kembali jendela terminal atau IDE Anda agar perubahan dapat diterapkan.

#### 2. `flutter doctor` Menemukan Masalah

- **Masalah:** Perintah `flutter doctor` menampilkan satu atau lebih tanda seru `[!
]` atau tanda silang `[X]` yang menandakan adanya masalah.
- **Penyebab:** Ada komponen atau dependensi yang belum terinstal atau terkonfigurasi dengan benar.
- **Solusi:** `flutter doctor` adalah alat diagnostik yang sangat membantu. Perhatikan output yang dihasilkannya dan ikuti instruksi yang disarankan. Beberapa contoh umum:
    - **`Android toolchain - develop for Android devices`:** Masalah ini biasanya terkait dengan instalasi Android Studio, Android SDK, atau `cmdline-tools`. Buka Android Studio, pergi ke **SDK Manager**, dan pastikan komponen yang dibutuhkan sudah terinstal.
    - **`Xcode - develop for iOS and macOS`:** (Khusus macOS) Pastikan Xcode sudah terinstal dari App Store dan *command-line tools*-nya sudah diatur dengan menjalankan `sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer`.
    - **`Android license status unknown`:** Jalankan perintah `flutter doctor --android-licenses` dan setujui semua lisensi dengan mengetik `y`.

#### 3. Masalah Terkait Lisensi Android

- **Masalah:** `flutter doctor` mengindikasikan bahwa lisensi Android belum disetujui.
- **Penyebab:** Anda belum menyetujui perjanjian lisensi dari Android SDK.
- **Solusi:** Jalankan perintah `flutter doctor --android-licenses` di terminal. Tekan `y` dan `Enter` untuk setiap lisensi yang ditampilkan hingga semua lisensi disetujui.

#### 4. Emulator atau Simulator Gagal Berjalan

- **Masalah:** Android Emulator atau iOS Simulator tidak dapat dimulai atau langsung tertutup.
- **Penyebab:** Bisa disebabkan oleh berbagai hal, mulai dari kurangnya sumber daya sistem, masalah konfigurasi, hingga *driver* grafis yang usang.
- **Solusi:**
    - **Android Emulator:**
        - Pastikan fitur virtualisasi (seperti Intel HAXM atau AMD-V) sudah diaktifkan di BIOS/UEFI komputer Anda.
        - Di Android Studio, buka **AVD Manager** dan coba hapus (*Wipe Data*) *virtual device* yang bermasalah, atau buat yang baru.
        - Pastikan Anda memiliki ruang disk yang cukup.
    - **iOS Simulator:** (Khusus macOS)
        - Coba reset simulator dengan memilih **Device > Erase All Content and Settings...** dari menu simulator.
        - Pastikan versi Xcode Anda kompatibel dengan versi macOS Anda.

### Tips Tambahan

- **Jalankan `flutter upgrade`:** Jika Anda mengalami masalah yang tidak terduga, coba perbarui Flutter SDK ke versi terbaru dengan menjalankan `flutter upgrade`.
- **Gunakan Perintah `flutter clean`:** Terkadang, *file build* yang lama dapat menyebabkan konflik. Jalankan `flutter clean` di direktori proyek Anda untuk membersihkannya.
- **Cari Bantuan Komunitas:** Jika masalah berlanjut, jangan ragu untuk mencari solusi di platform seperti **Stack Overflow** (dengan tag `flutter`), **GitHub Issues** repositori Flutter, atau forum komunitas Flutter lainnya. Saat bertanya, sertakan output lengkap dari `flutter doctor -v` untuk membantu orang lain memahami masalah Anda.
