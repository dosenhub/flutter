# Jenis-jenis Widget

Secara garis besar, widget di Flutter dapat dikategorikan menjadi beberapa jenis berdasarkan fungsi dan karakteristiknya. Dua kategorisasi yang paling penting untuk dipahami adalah **Stateless vs Stateful Widget** dan **UI vs Layout Widget**.

## 1. StatelessWidget vs StatefulWidget

Ini adalah klasifikasi mendasar yang berkaitan dengan bagaimana sebuah widget menangani *state* atau data dinamis.

### StatelessWidget
`StatelessWidget` adalah widget yang tidak memiliki *state* internal. Artinya, setelah widget ini dibuat, tampilannya tidak dapat berubah. Properti atau konfigurasinya diterima dari widget induknya dan bersifat *immutable* (tidak bisa diubah).

**Kapan menggunakan `StatelessWidget`?**
Gunakan `StatelessWidget` ketika bagian dari UI yang Anda bangun tidak bergantung pada data yang bisa berubah di dalam widget itu sendiri. Contohnya:
- Ikon (`Icon`)
- Teks statis (`Text`)
- Tombol tanpa logika internal yang kompleks (`ElevatedButton`)

**Contoh Kode:**
```dart
class MyStaticCard extends StatelessWidget {
  final String title;
  final String description;

  const MyStaticCard({Key? key, required this.title, required this.description}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return Card(
      child: Column(
        children: [
          Text(title, style: TextStyle(fontWeight: FontWeight.bold)),
          Text(description),
        ],
      ),
    );
  }
}
```

### StatefulWidget
`StatefulWidget` adalah widget yang memiliki *state* internal yang dapat berubah selama *lifecycle* (siklus hidup) widget tersebut. Ketika *state* berubah, widget ini akan memberi tahu Flutter untuk membangun ulang (rebuild) tampilannya dengan data yang baru.

`StatefulWidget` sebenarnya terdiri dari dua kelas:
1.  `StatefulWidget`: Kelas yang bersifat *immutable* dan menyimpan instance dari kelas `State`.
2.  `State`: Kelas di mana *state* (data yang bisa berubah) disimpan dan di mana method `build()` berada. Perubahan *state* harus dilakukan di dalam `setState()` agar UI diperbarui.

**Kapan menggunakan `StatefulWidget`?**
Gunakan `StatefulWidget` ketika UI perlu diperbarui secara dinamis sebagai respons terhadap interaksi pengguna atau perubahan data. Contohnya:
- Checkbox yang bisa dicentang dan tidak dicentang.
- Slider yang nilainya bisa digeser.
- Form input di mana pengguna mengetikkan teks.
- Tampilan yang datanya diambil dari internet dan bisa berubah.

**Contoh Kode:**
```dart
class Counter extends StatefulWidget {
  const Counter({Key? key}) : super(key: key);

  @override
  _CounterState createState() => _CounterState();
}

class _CounterState extends State<Counter> {
  int _count = 0;

  void _increment() {
    setState(() {
      _count++;
    });
  }

  @override
  Widget build(BuildContext context) {
    return Row(
      children: [
        ElevatedButton(onPressed: _increment, child: Text('Increment')),
        SizedBox(width: 16),
        Text('Count: $_count'),
      ],
    );
  }
}
```

## 2. UI Widget vs Layout Widget

Klasifikasi ini didasarkan pada fungsi utama widget: apakah untuk menampilkan sesuatu ke pengguna atau untuk mengatur tata letak widget lain.

### UI Widget (Widget Antarmuka)
Ini adalah widget yang dilihat dan berinteraksi langsung dengan pengguna. Mereka adalah "daging" dari aplikasi Anda.
- **Contoh:**
  - `Text`: Menampilkan string teks.
  - `Image`: Menampilkan gambar.
  - `Icon`: Menampilkan ikon grafis.
  - `ElevatedButton`, `TextButton`: Tombol yang bisa ditekan.
  - `TextField`: Input field untuk teks.
  - `Scaffold`: Struktur dasar halaman Material Design.

### Layout Widget (Widget Tata Letak)
Widget ini biasanya tidak terlihat secara langsung, tetapi perannya sangat krusial: mengatur posisi, ukuran, dan susunan dari widget-widget lain (anak-anaknya).
- **Contoh:**
  - `Container`: Kotak serbaguna yang bisa di-styling dengan padding, margin, border, warna, dll.
  - `Row`: Menyusun widget anaknya secara horizontal.
  - `Column`: Menyusun widget anaknya secara vertikal.
  - `Stack`: Menumpuk widget anaknya dari belakang ke depan.
  - `Center`: Memposisikan anaknya di tengah.
  - `Padding`: Memberi ruang kosong di sekitar anaknya.

Dalam praktiknya, Anda akan selalu mengkombinasikan kedua jenis widget ini. Anda akan menggunakan *layout widget* untuk membangun struktur halaman, dan di dalamnya Anda akan menempatkan *UI widget* untuk menampilkan konten yang sebenarnya.
