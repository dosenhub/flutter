## 1.4 Membuat Proyek Flutter Pertama

Setelah berhasil menginstal Flutter, saatnya untuk membuat proyek pertama Anda.

### Membuat Proyek Baru

Untuk membuat proyek Flutter baru, jalankan perintah berikut di terminal:

```bash
flutter create my_app
```

Perintah ini akan membuat direktori baru bernama `my_app` yang berisi proyek Flutter sederhana.

### Struktur Direktori

Berikut adalah beberapa direktori dan file penting dalam proyek Flutter:

- **`lib/`**: Direktori utama tempat Anda akan menulis kode aplikasi Dart. File `main.dart` adalah titik masuk utama aplikasi Anda.
- **`pubspec.yaml`**: File konfigurasi proyek yang berisi metadata seperti nama proyek, deskripsi, dan dependensi (paket eksternal).
- **`android/` dan `ios/`**: Direktori yang berisi proyek Android dan iOS. Anda akan jarang menyentuh direktori ini secara langsung.
- **`test/`**: Direktori untuk menulis tes unit dan widget.

### Menjalankan Aplikasi

Untuk menjalankan aplikasi, pastikan Anda memiliki emulator yang berjalan atau perangkat fisik yang terhubung. Kemudian, jalankan perintah berikut dari direktori proyek Anda:

```bash
cd my_app
flutter run
```

Flutter akan membangun dan menjalankan aplikasi di emulator atau perangkat Anda.

### Hot Reload

Salah satu fitur terbaik Flutter adalah *hot reload*. Coba buka file `lib/main.dart`, ubah teks `You have pushed the button this many times:` menjadi `Anda telah menekan tombol ini sebanyak:`, dan simpan file tersebut. Anda akan melihat perubahan di aplikasi secara instan tanpa perlu me-restart aplikasi.