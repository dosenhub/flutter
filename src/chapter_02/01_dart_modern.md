# Bab 2: Dasar Pemrograman Dart

Selamat datang di bab kedua! Pada bagian ini, kita akan menyelami dasar-dasar bahasa pemrograman Dart, yang merupakan fondasi dari Flutter. Dart adalah bahasa yang modern, fleksibel, dan dioptimalkan untuk membangun aplikasi di berbagai platform dari satu basis kode.

## Dart sebagai Bahasa Pemrograman Modern

Dart dikembangkan oleh Google dengan tujuan untuk menjadi bahasa yang mudah dipelajari, efisien, dan mampu menghasilkan aplikasi berkinerja tinggi. Beberapa fitur modern yang membuatnya menonjol adalah:

### 1. Type Inference (Penyimpulan Tipe)

Dalam banyak bahasa pemrograman, Anda harus secara eksplisit mendeklarasikan tipe data dari sebuah variabel (misalnya, `int age = 30;`). Dart juga mendukung ini, tetapi ia juga pintar dalam menyimpulkan tipe data secara otomatis. Ini membuat kode lebih ringkas dan mudah dibaca.

#### Menggunakan `var`

Kata kunci `var` digunakan untuk mendeklarasikan variabel yang nilainya dapat berubah (mutable). Dart akan secara otomatis menentukan tipe data saat pertama kali variabel diinisialisasi.

**Contoh:**
```dart
// Dart secara otomatis mengenali 'name' sebagai String
var name = 'John Doe';

// Anda tidak bisa mengubah tipe datanya nanti
// name = 123; // Ini akan menghasilkan error
```

#### Menggunakan `final`

Kata kunci `final` juga menggunakan *type inference*. `final` digunakan untuk mendeklarasikan variabel yang nilainya tidak akan pernah berubah setelah diinisialisasi (immutable).

**Contoh:**
```dart
final String greeting = 'Hello';
final year = 2023; // Tipe data int diinferensikan secara otomatis

// greeting = 'Hi'; // Ini akan menghasilkan error karena variabel final tidak bisa diubah
```

### 2. Mutability Control (Kontrol Perubahan Nilai)

Dart memberikan kontrol yang jelas atas apakah sebuah variabel dapat diubah nilainya atau tidak.

- **`final`**: Seperti yang telah disebutkan, `final` digunakan untuk variabel yang nilainya hanya akan diatur sekali. Ini sangat berguna untuk nilai yang Anda tahu tidak akan berubah, seperti konstanta atau data yang diterima dari sumber eksternal. Nilai `final` ditentukan saat runtime.

- **`const`**: Digunakan untuk nilai yang sudah diketahui pada saat kompilasi (*compile-time constant*). Ini lebih ketat daripada `final`. `const` tidak hanya membuat variabel itu sendiri tidak dapat diubah, tetapi juga memastikan bahwa nilainya adalah konstanta waktu kompilasi. Menggunakan `const` dapat meningkatkan performa aplikasi Anda.

**Contoh:**
```dart
// Benar: Nilai '10' sudah diketahui saat kompilasi
const int maxUsers = 10;

// Salah: DateTime.now() hanya bisa diketahui saat runtime
// const DateTime compileTimeError = DateTime.now();
```

### 3. Keamanan Null (Null Safety)

Salah satu fitur paling kuat di Dart adalah *null safety*. Fitur ini membantu Anda menghindari kesalahan yang disebabkan oleh nilai `null` (sering disebut "the billion-dollar mistake" dalam dunia pemrograman).

Secara default, semua tipe data di Dart tidak bisa bernilai `null`. Jika Anda ingin sebuah variabel bisa menampung nilai `null`, Anda harus secara eksplisit menyatakannya dengan menambahkan tanda tanya (`?`) setelah tipe data.

- **Tipe Non-Nullable (Default):**
  ```dart
  String name = "Alice";
  // name = null; // Ini akan menghasilkan error
  ```

- **Tipe Nullable:**
  ```dart
  String? middleName; // Bisa bernilai null
  middleName = 'Grace';
  middleName = null; // Ini valid
  ```

- **Operator `!` (Bang Operator):**
  Jika Anda 100% yakin bahwa sebuah variabel yang bisa bernilai `null` sebenarnya tidak `null` pada titik tertentu, Anda bisa menggunakan operator `!` untuk memberitahu Dart agar memperlakukannya sebagai non-nullable. Gunakan dengan hati-hati, karena jika ternyata nilainya `null`, aplikasi Anda akan mengalami *runtime error*.

  ```dart
  String? maybeName;
  // ... (logika yang memastikan maybeName tidak null)
  String name = maybeName!; // Memberi tahu Dart bahwa kita yakin maybeName tidak null
  ```

Dengan fitur-fitur ini, Dart membantu Anda menulis kode yang lebih aman, lebih bersih, dan lebih mudah dipelihara.
