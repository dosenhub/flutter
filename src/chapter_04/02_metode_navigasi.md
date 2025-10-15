# Metode Navigasi dalam Flutter

Flutter menyediakan dua pendekatan utama untuk navigasi: **Navigasi Dasar (Anonymous Routes)** dan **Navigasi Bernama (Named Routes)**. Keduanya menggunakan `Navigator` di belakang layar, tetapi menawarkan cara kerja yang berbeda.

## 1. Navigasi Dasar (Anonymous Routes)

Ini adalah cara paling langsung untuk berpindah layar. Anda membuat `Route` (misalnya, `MaterialPageRoute`) secara *on-the-fly* (langsung di tempat) dan "mendorong"-nya ke `Navigator`.

### `Navigator.push()`
Method ini digunakan untuk pindah ke layar baru. Anda perlu memberikan `context` dan sebuah `Route`.

**Contoh:**
Misalkan kita punya dua widget layar: `FirstScreen` dan `SecondScreen`.

```dart
// Di dalam widget FirstScreen
ElevatedButton(
  child: Text('Go to Second Screen'),
  onPressed: () {
    Navigator.push(
      context,
      MaterialPageRoute(builder: (context) => SecondScreen()),
    );
  },
)
```
Ketika tombol ditekan, `MaterialPageRoute` baru dibuat, yang kemudian membangun `SecondScreen`, dan `Navigator` menampilkannya di atas `FirstScreen`.

### `Navigator.pop()`
Method ini digunakan untuk kembali ke layar sebelumnya dengan "melepas" `Route` saat ini dari tumpukan `Navigator`.

```dart
// Di dalam widget SecondScreen
ElevatedButton(
  child: Text('Go Back'),
  onPressed: () {
    Navigator.pop(context);
  },
)
```
Flutter secara otomatis menambahkan tombol "kembali" di `AppBar` yang juga akan memanggil `Navigator.pop(context)`.

### Mengirim Data ke Layar Baru
Cara paling umum untuk mengirim data adalah melalui konstruktor widget layar tujuan.

```dart
// Di FirstScreen, saat memanggil push
Navigator.push(
  context,
  MaterialPageRoute(
    builder: (context) => DetailScreen(productId: '123'), // Kirim data via konstruktor
  ),
);

// Di DetailScreen, terima data di konstruktor
class DetailScreen extends StatelessWidget {
  final String productId;

  const DetailScreen({Key? key, required this.productId}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Product ID: $productId')),
      // ...
    );
  }
}
```

### Mengembalikan Data dari Layar
Terkadang, layar kedua perlu mengembalikan data ke layar pertama (misalnya, layar pengaturan yang mengembalikan pilihan pengguna).

1.  Gunakan `await` saat memanggil `Navigator.push()`.
2.  Gunakan `Navigator.pop(result)` untuk mengirim data kembali.

```dart
// Di FirstScreen
void _navigateToSelectionScreen() async {
  // Tunggu hasil dari SelectionScreen
  final result = await Navigator.push(
    context,
    MaterialPageRoute(builder: (context) => SelectionScreen()),
  );

  // Tampilkan hasil yang dikembalikan
  ScaffoldMessenger.of(context)
    ..removeCurrentSnackBar()
    ..showSnackBar(SnackBar(content: Text('$result')));
}

// Di SelectionScreen
ElevatedButton(
  onPressed: () {
    // Kembalikan data 'Yep!' ke layar sebelumnya
    Navigator.pop(context, 'Yep!');
  },
  child: Text('Yep!'),
)
```

## 2. Navigasi Bernama (Named Routes)

Pendekatan ini memungkinkan Anda untuk mendefinisikan semua rute navigasi di satu tempat, lalu memanggilnya menggunakan nama string yang unik. Ini sangat direkomendasikan untuk aplikasi berukuran sedang hingga besar.

**Keuntungan:**
- **Kode Lebih Bersih:** Tidak perlu membuat `MaterialPageRoute` setiap kali. Cukup panggil `Navigator.pushNamed(context, '/routeName')`.
- **Tersentralisasi:** Semua rute didefinisikan di satu tempat (`MaterialApp`), sehingga mudah dikelola.
- **Mengurangi Duplikasi:** Menghindari kesalahan pengetikan dan duplikasi kode.

### Langkah 1: Definisikan Rute
Di dalam `MaterialApp`, gunakan properti `routes` untuk mendaftarkan nama rute dan widget yang sesuai.

```dart
MaterialApp(
  title: 'Named Routes Demo',
  initialRoute: '/', // Rute awal saat aplikasi dibuka
  routes: {
    '/': (context) => HomeScreen(),
    '/details': (context) => DetailsScreen(),
    '/settings': (context) => SettingsScreen(),
  },
)
```

### Langkah 2: Navigasi Menggunakan Nama
Gunakan `Navigator.pushNamed()` untuk berpindah layar.

```dart
// Dari HomeScreen ke DetailsScreen
ElevatedButton(
  child: Text('View Details'),
  onPressed: () {
    Navigator.pushNamed(context, '/details');
  },
)
```

### Mengirim Argumen dengan `pushNamed`
Bagaimana jika kita perlu mengirim data seperti ID produk? Gunakan parameter `arguments`.

```dart
// Mengirim argumen
Navigator.pushNamed(
  context,
  '/details',
  arguments: 'product-id-456',
);

// Menerima argumen di layar tujuan
class DetailsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    // Ekstrak argumen
    final String productId = ModalRoute.of(context)!.settings.arguments as String;

    return Scaffold(
      appBar: AppBar(
        title: Text('Details for $productId'),
      ),
      // ...
    );
  }
}
```

### Method Navigasi Bernama Lainnya
- `Navigator.pushReplacementNamed()`: Pindah ke rute baru dan buang rute saat ini. Berguna untuk halaman login (setelah login berhasil, pengguna tidak bisa kembali ke halaman login).
- `Navigator.popAndPushNamed()`: Pop rute saat ini, lalu push rute baru. Berguna untuk berpindah antar item di menu samping (drawer).
