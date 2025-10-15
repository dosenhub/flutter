# Studi Kasus: Aplikasi Multi-Layar

Saatnya mempraktikkan semua yang telah kita pelajari. Kita akan membangun sebuah aplikasi sederhana dengan tiga layar menggunakan **Named Routes**.

**Skenario Aplikasi:**
1.  **HomeScreen:** Menampilkan daftar produk. Setiap item produk dapat diklik untuk melihat detailnya. Ada juga tombol untuk membuka halaman Pengaturan.
2.  **DetailScreen:** Menampilkan detail produk yang dipilih.
3.  **SettingsScreen:** Halaman pengaturan sederhana.

## Langkah 1: Struktur Proyek

Pertama, buat tiga file baru di dalam folder `lib` Anda untuk setiap layar:
- `lib/home_screen.dart`
- `lib/detail_screen.dart`
- `lib/settings_screen.dart`

## Langkah 2: Mendefinisikan Rute di `main.dart`

Kita akan mendaftarkan semua rute kita di file `main.dart` di dalam `MaterialApp`.

**`lib/main.dart`**
```dart
import 'package:flutter/material.dart';
import 'package:navigation_example/home_screen.dart';
import 'package:navigation_example/detail_screen.dart';
import 'package:navigation_example/settings_screen.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Named Routes Example',
      // 1. Definisikan initialRoute
      initialRoute: '/',
      // 2. Definisikan semua rute yang tersedia
      routes: {
        '/': (context) => HomeScreen(),
        // Kita akan menangani rute '/detail' secara khusus nanti
        // untuk bisa membaca argumen.
        '/settings': (context) => SettingsScreen(),
      },
      // 3. Gunakan onGenerateRoute untuk rute yang butuh logika tambahan
      onGenerateRoute: (settings) {
        if (settings.name == DetailScreen.routeName) {
          // Ekstrak argumen yang dikirim
          final args = settings.arguments as String;

          // Buat MaterialPageRoute
          return MaterialPageRoute(
            builder: (context) {
              return DetailScreen(productId: args);
            },
          );
        }
        // Jika rute tidak ditemukan, bisa tampilkan halaman error
        assert(false, 'Need to implement ${settings.name}');
        return null;
      },
    );
  }
}
```
*Catatan: Menggunakan `onGenerateRoute` adalah cara yang lebih fleksibel untuk menangani rute, terutama saat Anda perlu meneruskan argumen yang kompleks.*

## Langkah 3: Membuat `HomeScreen`

Layar ini akan menampilkan daftar dan tombol navigasi.

**`lib/home_screen.dart`**
```dart
import 'package:flutter/material.dart';
import 'package:navigation_example/detail_screen.dart';

class HomeScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home Screen'),
        actions: [
          IconButton(
            icon: Icon(Icons.settings),
            onPressed: () {
              // Navigasi ke halaman settings
              Navigator.pushNamed(context, '/settings');
            },
          ),
        ],
      ),
      body: ListView.builder(
        itemCount: 5,
        itemBuilder: (context, index) {
          final productId = 'Product ${index + 1}';
          return ListTile(
            title: Text(productId),
            onTap: () {
              // Navigasi ke halaman detail dengan mengirim argumen
              Navigator.pushNamed(
                context,
                DetailScreen.routeName,
                arguments: productId,
              );
            },
          );
        },
      ),
    );
  }
}
```

## Langkah 4: Membuat `DetailScreen`

Layar ini akan menerima dan menampilkan `productId`.

**`lib/detail_screen.dart`**
```dart
import 'package:flutter/material.dart';

class DetailScreen extends StatelessWidget {
  // Definisikan nama rute sebagai konstanta statis
  static const routeName = '/detail';

  final String productId;

  const DetailScreen({Key? key, required this.productId}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Detail for $productId'),
      ),
      body: Center(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.center,
          children: [
            Text(
              'Showing details for $productId',
              style: TextStyle(fontSize: 20),
            ),
            SizedBox(height: 20),
            ElevatedButton(
              onPressed: () {
                // Kembali ke layar sebelumnya
                Navigator.pop(context);
              },
              child: Text('Go Back'),
            ),
          ],
        ),
      ),
    );
  }
}
```

## Langkah 5: Membuat `SettingsScreen`

Ini adalah layar sederhana dengan tombol kembali.

**`lib/settings_screen.dart`**
```dart
import 'package:flutter/material.dart';

class SettingsScreen extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Settings'),
      ),
      body: Center(
        child: Text('This is the settings page.'),
      ),
    );
  }
}
```

Dengan mengikuti langkah-langkah ini, Anda telah berhasil mengimplementasikan alur navigasi multi-layar yang bersih dan terkelola dengan baik menggunakan *named routes* di Flutter.
