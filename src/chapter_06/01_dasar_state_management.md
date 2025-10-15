# Dasar State Management

Dalam aplikasi Flutter, "state" adalah data yang dapat berubah selama aplikasi berjalan dan memengaruhi tampilan antarmuka pengguna (UI). Mengelola state ini secara efektif adalah kunci untuk membangun aplikasi yang responsif, efisien, dan mudah dipelihara.

## 1. Apa itu State?

Secara sederhana, **state** adalah segala data yang dapat dibaca oleh widget pada saat widget tersebut dibangun, dan yang dapat berubah seiring waktu. Ketika state sebuah widget berubah, Flutter akan membangun ulang (rebuild) widget tersebut untuk mencerminkan perubahan data.

Ada dua jenis state utama yang perlu Anda pahami:

### a. Ephemeral State (Local State)
-   **Definisi:** State yang hanya relevan untuk satu widget tertentu dan tidak perlu dibagikan dengan widget lain di pohon widget.
-   **Contoh:**
    -   Apakah sebuah `Checkbox` dicentang atau tidak.
    -   Posisi saat ini dari sebuah `PageView`.
    -   Nilai input dalam sebuah `TextFormField` sebelum disubmit.
-   **Pengelolaan:** Biasanya dikelola di dalam `StatefulWidget` itu sendiri menggunakan method `setState()`.

### b. App State (Global State)
-   **Definisi:** State yang perlu dibagikan di banyak bagian aplikasi, diakses oleh banyak widget, dan mungkin bertahan selama siklus hidup aplikasi.
-   **Contoh:**
    -   Status autentikasi pengguna (sudah login atau belum).
    -   Keranjang belanja dalam aplikasi e-commerce.
    -   Preferensi pengguna (misalnya, tema gelap/terang).
    -   Data yang diambil dari server.
-   **Pengelolaan:** Membutuhkan solusi state management yang lebih canggih (seperti Provider, BLoC, Riverpod, GetX, dll.) untuk menyediakannya ke seluruh aplikasi.

## 2. Mengapa State Management Penting?

Tanpa strategi state management yang baik, aplikasi Anda dapat menghadapi beberapa masalah:

-   **Prop Drilling:** Anda harus meneruskan data dari widget induk yang jauh ke widget anak yang dalam melalui banyak konstruktor perantara, meskipun widget perantara tersebut tidak menggunakan data tersebut. Ini membuat kode menjadi berantakan dan sulit diubah.
-   **Rebuild yang Tidak Perlu:** Jika state tidak dikelola dengan baik, perubahan kecil pada data dapat memicu rebuild seluruh pohon widget, yang dapat memengaruhi performa aplikasi.
-   **Kode yang Sulit Dipelihara:** Logika bisnis dan UI menjadi bercampur aduk, membuat kode sulit dibaca, diuji, dan diperbaiki.
-   **Skalabilitas:** Aplikasi akan sulit untuk diperluas dan dikembangkan lebih lanjut.

State management membantu memisahkan logika bisnis dari UI, membuat kode lebih modular, mudah diuji, dan lebih mudah dipelihara.

## 3. Pendekatan State Management Sederhana (tanpa package eksternal)

Flutter menyediakan beberapa mekanisme bawaan untuk mengelola state, terutama untuk *Ephemeral State*.

### a. `setState()`
Ini adalah cara paling dasar dan paling sering digunakan untuk mengelola state di dalam `StatefulWidget`. Ketika Anda memanggil `setState()`, Flutter akan menandai widget tersebut sebagai "kotor" dan akan membangun ulang method `build()` dari widget tersebut (dan semua widget anaknya) pada frame berikutnya.

```dart
class MyCounter extends StatefulWidget {
  @override
  _MyCounterState createState() => _MyCounterState();
}

class _MyCounterState extends State<MyCounter> {
  int _count = 0; // State yang akan berubah

  void _incrementCounter() {
    setState(() { // Panggil setState untuk memberitahu Flutter bahwa state telah berubah
      _count++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Column(
      children: [
        Text('Count: $_count'), // UI akan diperbarui saat _count berubah
        ElevatedButton(
          onPressed: _incrementCounter,
          child: Text('Increment'),
        ),
      ],
    );
  }
}
```

### b. `InheritedWidget` (Konsep Dasar)
`InheritedWidget` adalah mekanisme bawaan Flutter yang memungkinkan data untuk diwariskan ke bawah pohon widget secara efisien. Widget anak dapat mengakses data dari `InheritedWidget` terdekat di atasnya tanpa perlu meneruskan data melalui setiap konstruktor.

Meskipun sangat kuat, `InheritedWidget` seringkali digunakan sebagai dasar untuk membangun solusi state management yang lebih tinggi (seperti `Provider`), dan jarang digunakan secara langsung untuk aplikasi sehari-hari karena implementasinya yang sedikit lebih kompleks.

### c. `ChangeNotifier` dan `Provider` (Konsep Dasar)
-   **`ChangeNotifier`:** Ini adalah kelas sederhana dari Flutter SDK (`foundation` library) yang dapat Anda *extend* untuk membuat objek yang dapat memberi tahu "pendengar" (listeners) ketika ada perubahan.
-   **`Provider`:** Ini adalah package populer yang dibangun di atas `InheritedWidget` dan `ChangeNotifier`. `Provider` menyederhanakan proses penyediaan `ChangeNotifier` (atau objek lain) ke pohon widget dan memungkinkan widget untuk "mendengarkan" perubahan pada objek tersebut.

Meskipun kita tidak akan mengimplementasikan `Provider` secara detail di bab ini, penting untuk mengetahui bahwa `setState()` adalah langkah awal yang baik, dan `Provider` adalah langkah berikutnya yang logis untuk mengelola *App State* yang lebih kompleks.
