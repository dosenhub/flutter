# Data Persistence dengan Shared Preferences

Setelah pengguna menutup aplikasi, semua state di dalam memori akan hilang. **Data Persistence** adalah proses menyimpan data secara permanen di penyimpanan lokal perangkat, sehingga data tersebut dapat diakses kembali saat aplikasi dibuka lagi.

## 1. Dasar Data Persistence

Flutter menawarkan beberapa cara untuk menyimpan data secara lokal, masing-masing dengan kegunaannya sendiri.

-   **Shared Preferences:**
    -   **Kegunaan:** Untuk menyimpan data sederhana dalam format *key-value pair*. Sangat cocok untuk menyimpan preferensi pengguna (misalnya, mode gelap), status login, atau skor tertinggi dalam game.
    -   **Karakteristik:** Cepat dan mudah digunakan, tetapi tidak cocok untuk data yang besar atau terstruktur secara kompleks.
    -   **Inilah fokus kita di bab ini.**

-   **Database Lokal (misalnya, SQLite):**
    -   **Kegunaan:** Untuk menyimpan data yang besar, kompleks, dan terstruktur. Misalnya, daftar kontak, riwayat transaksi, atau data aplikasi yang bisa diakses offline.
    -   **Karakteristik:** Sangat kuat dan fleksibel, mendukung query yang kompleks, tetapi membutuhkan lebih banyak setup awal. Package populer untuk ini adalah `sqflite`.

-   **Penyimpanan File (File Storage):**
    -   **Kegunaan:** Untuk membaca dan menulis file mentah langsung ke perangkat, seperti gambar, dokumen, log, atau data JSON.
    -   **Karakteristik:** Memberikan kontrol penuh atas data, tetapi Anda bertanggung jawab untuk proses serialisasi dan deserialisasi data (mengubah objek menjadi string/byte dan sebaliknya).

## 2. Implementasi `shared_preferences`

Mari kita fokus pada cara termudah untuk memulai persistensi data: `shared_preferences`.

### Langkah 1: Tambahkan Dependensi
Buka file `pubspec.yaml` Anda dan tambahkan `shared_preferences` di bawah `dependencies`.

```yaml
dependencies:
  flutter:
    sdk: flutter
  shared_preferences: ^2.0.15 # Gunakan versi terbaru
```
Setelah itu, jalankan `flutter pub get` di terminal Anda.

### Langkah 2: Dapatkan Instance SharedPreferences
Untuk bisa membaca atau menulis data, Anda perlu mendapatkan instance dari `SharedPreferences`. Karena proses ini bersifat *asynchronous* (asinkron), kita menggunakan `async/await`.

```dart
import 'package:shared_preferences/shared_preferences.dart';

void main() async {
  // ...
  final prefs = await SharedPreferences.getInstance();
  // ...
}
```

### Langkah 3: Menyimpan Data (Write)
`SharedPreferences` menyediakan method `set` untuk tipe data primitif: `setBool`, `setInt`, `setDouble`, dan `setString`.

```dart
// Mendapatkan instance
final prefs = await SharedPreferences.getInstance();

// Menyimpan data
await prefs.setBool('isLoggedIn', true);
await prefs.setInt('userLevel', 10);
await prefs.setString('username', 'john_doe');
```
Setiap method `set` mengembalikan `Future<bool>`, yang akan bernilai `true` jika penyimpanan berhasil.

### Langkah 4: Membaca Data (Read)
Sama seperti `set`, ada method `get` untuk setiap tipe data: `getBool`, `getInt`, `getDouble`, dan `getString`.

Penting untuk diingat bahwa method `get` bisa mengembalikan `null` jika *key* yang Anda cari tidak ada. Oleh karena itu, Anda harus selalu menangani kasus `null` ini, biasanya dengan menyediakan nilai default menggunakan operator `??`.

```dart
// Mendapatkan instance
final prefs = await SharedPreferences.getInstance();

// Membaca data dengan nilai default jika null
final bool isLoggedIn = prefs.getBool('isLoggedIn') ?? false;
final int userLevel = prefs.getInt('userLevel') ?? 1;
final String username = prefs.getString('username') ?? 'Guest';

print('Is Logged In: $isLoggedIn');
print('User Level: $userLevel');
print('Username: $username');
```

### Langkah 5: Menghapus Data
Untuk menghapus *key-value pair* tertentu, gunakan method `remove()`.

```dart
// Mendapatkan instance
final prefs = await SharedPreferences.getInstance();

// Menghapus satu key
await prefs.remove('userLevel');
```

Jika Anda ingin menghapus **semua** data di `SharedPreferences` (berguna untuk fungsi "logout" atau "reset aplikasi"), gunakan `clear()`.

```dart
// Menghapus semua data
await prefs.clear();
```

Dengan `shared_preferences`, Anda dapat dengan mudah menambahkan kemampuan persistensi data sederhana ke aplikasi Anda, membuatnya lebih cerdas dan personal bagi pengguna.
