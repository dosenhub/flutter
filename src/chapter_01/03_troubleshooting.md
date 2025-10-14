## 1.3 Troubleshooting Instalasi dan Masalah Umum

Meskipun proses instalasi Flutter umumnya berjalan lancar, terkadang Anda mungkin mengalami beberapa masalah. Bagian ini akan membahas beberapa masalah umum dan cara mengatasinya.

### Masalah Umum

- **`flutter` command not found:** Masalah ini biasanya terjadi karena direktori `flutter/bin` tidak ditambahkan dengan benar ke `PATH` environment variable. Pastikan Anda telah mengikuti langkah-langkah untuk mengupdate `PATH` dengan benar.
- **Android toolchain - develop for Android devices:** Pesan ini muncul jika ada masalah dengan instalasi Android Studio atau Android SDK. Pastikan Anda telah menginstal Android Studio dan Android SDK, dan `ANDROID_HOME` environment variable telah diatur dengan benar.
- **Xcode - develop for iOS and macOS:** Pesan ini khusus untuk pengguna macOS dan menunjukkan bahwa Xcode tidak terinstal atau belum dikonfigurasi. Instal Xcode dari Mac App Store dan jalankan perintah `sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer` dan `sudo xcodebuild -runFirstLaunch` untuk mengkonfigurasinya.
- **Unable to find bundled Java version:** Masalah ini dapat terjadi jika instalasi Android Studio Anda rusak atau tidak lengkap. Coba instal ulang Android Studio atau atur `JAVA_HOME` environment variable secara manual ke direktori instalasi Java Anda.

### Mencari Bantuan

Jika Anda mengalami masalah yang tidak tercantum di sini, sumber daya terbaik untuk mencari bantuan adalah:

- **Dokumentasi Resmi Flutter:** [https://flutter.dev/docs](https://flutter.dev/docs)
- **Stack Overflow:** [https://stackoverflow.com/questions/tagged/flutter](https://stackoverflow.com/questions/tagged/flutter)
- **Komunitas Flutter di Discord:** [https://discord.gg/flutter](https://discord.gg/flutter)