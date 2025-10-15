# Studi Kasus dan Praktek

Teori tanpa praktek akan terasa kurang lengkap. Di bagian ini, kita akan mengaplikasikan semua konsep widget dan layout yang telah kita pelajari untuk membangun beberapa komponen UI sederhana.

## Praktek 1: Membuat Kartu Nama Digital

Mari kita buat sebuah kartu nama digital sederhana yang menampilkan foto, nama, jabatan, dan informasi kontak.

**Tujuan:**
- Mengkombinasikan `Container`, `Column`, `Row`, `CircleAvatar`, `Text`, dan `Icon`.
- Menggunakan `SizedBox` untuk memberikan spasi.
- Menerapkan `mainAxisAlignment` dan `crossAxisAlignment`.

**Kode Lengkap:**
```dart
import 'package:flutter/material.dart';

class DigitalBusinessCard extends StatelessWidget {
  const DigitalBusinessCard({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      backgroundColor: Colors.teal,
      body: SafeArea(
        child: Center(
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: <Widget>[
              CircleAvatar(
                radius: 50.0,
                backgroundImage: NetworkImage('https://i.pravatar.cc/150?img=3'),
              ),
              Text(
                'Jane Doe',
                style: TextStyle(
                  fontFamily: 'Pacifico',
                  fontSize: 40.0,
                  color: Colors.white,
                  fontWeight: FontWeight.bold,
                ),
              ),
              Text(
                'FLUTTER DEVELOPER',
                style: TextStyle(
                  fontFamily: 'Source Sans Pro',
                  color: Colors.teal.shade100,
                  fontSize: 20.0,
                  letterSpacing: 2.5,
                  fontWeight: FontWeight.bold,
                ),
              ),
              SizedBox(
                height: 20.0,
                width: 150.0,
                child: Divider(
                  color: Colors.teal.shade100,
                ),
              ),
              Card(
                margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                child: ListTile(
                  leading: Icon(
                    Icons.phone,
                    color: Colors.teal,
                  ),
                  title: Text(
                    '+62 123 4567 890',
                    style: TextStyle(
                      color: Colors.teal.shade900,
                      fontFamily: 'Source Sans Pro',
                      fontSize: 20.0,
                    ),
                  ),
                ),
              ),
              Card(
                margin: EdgeInsets.symmetric(vertical: 10.0, horizontal: 25.0),
                child: ListTile(
                  leading: Icon(
                    Icons.email,
                    color: Colors.teal,
                  ),
                  title: Text(
                    'jane.doe@example.com',
                    style: TextStyle(
                      fontSize: 20.0,
                      color: Colors.teal.shade900,
                      fontFamily: 'Source Sans Pro',
                    ),
                  ),
                ),
              )
            ],
          ),
        ),
      ),
    );
  }
}
```
*Catatan: Untuk font `Pacifico` dan `Source Sans Pro`, Anda perlu menambahkannya ke `pubspec.yaml` dan folder assets terlebih dahulu.*

## Praktek 2: Membuat Layout Galeri Gambar Sederhana

Sekarang, kita akan membuat sebuah galeri gambar sederhana menggunakan `GridView`.

**Tujuan:**
- Menggunakan `GridView.count` untuk membuat layout grid.
- Menempatkan `Image` di dalam `Container` yang diberi `BoxShadow`.

**Kode Lengkap:**
```dart
import 'package:flutter/material.dart';

class SimpleImageGallery extends StatelessWidget {
  const SimpleImageGallery({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Image Gallery'),
      ),
      body: GridView.count(
        crossAxisCount: 2, // 2 kolom
        mainAxisSpacing: 8, // Spasi vertikal
        crossAxisSpacing: 8, // Spasi horizontal
        padding: EdgeInsets.all(8),
        children: List.generate(10, (index) {
          return Container(
            decoration: BoxDecoration(
              color: Colors.white,
              borderRadius: BorderRadius.circular(12),
              boxShadow: [
                BoxShadow(
                  color: Colors.black.withOpacity(0.1),
                  blurRadius: 5,
                  spreadRadius: 1,
                )
              ],
            ),
            child: ClipRRect(
              borderRadius: BorderRadius.circular(12),
              child: Image.network(
                'https://picsum.photos/200/200?random=$index',
                fit: BoxFit.cover,
              ),
            ),
          );
        }),
      ),
    );
  }
}
```

## Praktek 3: Layout Responsif Sederhana

Terakhir, mari kita coba membuat layout yang sedikit beradaptasi dengan ukuran layar. Kita akan membuat sebuah `Container` yang warnanya berubah jika layarnya lebih lebar dari 600 pixel.

**Tujuan:**
- Menggunakan `LayoutBuilder` untuk mendapatkan informasi batasan (constraints) dari parent widget.
- Membuat kondisi sederhana berdasarkan `maxWidth`.

**Kode Lengkap:**
```dart
import 'package:flutter/material.dart';

class ResponsiveLayout extends StatelessWidget {
  const ResponsiveLayout({Key? key}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Responsive Layout'),
      ),
      body: Center(
        child: LayoutBuilder(
          builder: (BuildContext context, BoxConstraints constraints) {
            // constraints.maxWidth akan berisi lebar maksimal yang tersedia
            if (constraints.maxWidth > 600) {
              // Jika layar lebar (misal: tablet, desktop)
              return Container(
                width: 400,
                height: 200,
                color: Colors.green,
                child: Center(
                  child: Text(
                    'Wide Layout (width: ${constraints.maxWidth.toStringAsFixed(0)})',
                    style: TextStyle(color: Colors.white, fontSize: 24),
                  ),
                ),
              );
            } else {
              // Jika layar sempit (misal: handphone)
              return Container(
                width: 200,
                height: 200,
                color: Colors.blue,
                child: Center(
                  child: Text(
                    'Narrow Layout (width: ${constraints.maxWidth.toStringAsFixed(0)})',
                    style: TextStyle(color: Colors.white, fontSize: 18),
                  ),
                ),
              );
            }
          },
        ),
      ),
    );
  }
}
```

Dengan menyelesaikan praktek-praktek ini, Anda telah mengambil langkah besar dalam memahami bagaimana menyusun dan membangun antarmuka pengguna yang nyata dengan Flutter.
