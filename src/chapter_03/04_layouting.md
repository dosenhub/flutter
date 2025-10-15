# Layouting di Flutter

Membangun layout adalah salah satu tugas fundamental dalam pengembangan UI. Flutter menyediakan serangkaian widget layout yang sangat kaya dan fleksibel. Di bagian ini, kita akan membahas widget-widget layout yang paling umum digunakan, yang terbagi menjadi dua kategori utama: *single-child* dan *multi-child* layout widgets.

## 1. Single-Child Layout Widgets

Widget ini hanya dapat memiliki satu widget anak (`child`). Fungsinya adalah untuk memberikan styling, batasan, atau alignment tertentu pada satu widget tersebut.

### `Container`
`Container` adalah widget layout yang paling serbaguna. Anggap saja ini seperti sebuah kotak kosong yang bisa Anda hias sesuka hati.

- **Properti Utama:**
  - `child`: Widget yang akan berada di dalam `Container`.
  - `width`, `height`: Ukuran container.
  - `color`: Warna latar belakang. **Penting:** Jangan gunakan `color` jika Anda sudah menggunakan `decoration`.
  - `decoration`: Untuk styling yang lebih kompleks seperti gradien, border, atau bayangan (`BoxDecoration`).
  - `padding`: Jarak dari batas `Container` ke `child`-nya.
  - `margin`: Jarak dari batas `Container` ke widget lain di luarnya.
  - `alignment`: Posisi `child` di dalam `Container`.

- **Contoh:**
  ```dart
  Container(
    width: 200,
    height: 100,
    padding: EdgeInsets.all(10),
    margin: EdgeInsets.all(20),
    decoration: BoxDecoration(
      color: Colors.blue,
      borderRadius: BorderRadius.circular(8),
      boxShadow: [
        BoxShadow(
          color: Colors.black.withOpacity(0.2),
          spreadRadius: 2,
          blurRadius: 5,
          offset: Offset(0, 3),
        ),
      ],
    ),
    child: Text('Styled Box', style: TextStyle(color: Colors.white)),
  )
  ```

### `Center`
Sesuai namanya, `Center` adalah widget sederhana yang fungsinya hanya untuk memposisikan `child`-nya di tengah-tengah ruang yang tersedia.

```dart
Center(
  child: Text('Hello, Center!'),
)
```

### `Padding`
Widget ini lebih spesifik daripada `padding` di `Container`. Tujuannya hanya satu: memberikan ruang kosong (padding) di sekeliling `child`-nya.

```dart
Padding(
  padding: EdgeInsets.symmetric(horizontal: 20, vertical: 10),
  child: ElevatedButton(
    onPressed: () {},
    child: Text('Padded Button'),
  ),
)
```

### `SizedBox`
`SizedBox` adalah kotak dengan ukuran yang spesifik. Widget ini sangat berguna untuk:
1.  Memberi ukuran pasti pada sebuah widget anak.
2.  Menciptakan ruang kosong (spasi) di antara widget lain (misalnya di dalam `Row` atau `Column`).

```dart
Column(
  children: [
    Text('Item 1'),
    SizedBox(height: 20), // Spasi vertikal 20 pixel
    Text('Item 2'),
  ],
)
```

### `AspectRatio`
Widget ini memaksa `child`-nya untuk memiliki rasio aspek tertentu (perbandingan lebar dan tinggi).

```dart
AspectRatio(
  aspectRatio: 16 / 9, // Rasio video widescreen
  child: Container(color: Colors.green),
)
```

## 2. Multi-Child Layout Widgets

Widget ini dapat memiliki banyak widget anak dalam sebuah list (`children`). Fungsinya adalah untuk menyusun widget-widget tersebut dalam pola tertentu.

### `Row` dan `Column`
Ini adalah dua widget layout multi-child yang paling fundamental.
- `Row`: Menyusun `children`-nya secara **horizontal**.
- `Column`: Menyusun `children`-nya secara **vertikal**.

- **Properti Utama:**
  - `children`: List widget yang akan disusun.
  - `mainAxisAlignment`: Mengatur alignment `children` di sumbu utama (`horizontal` untuk `Row`, `vertical` untuk `Column`).
    - `MainAxisAlignment.start` (default)
    - `MainAxisAlignment.center`
    - `MainAxisAlignment.end`
    - `MainAxisAlignment.spaceBetween`
    - `MainAxisAlignment.spaceAround`
    - `MainAxisAlignment.spaceEvenly`
  - `crossAxisAlignment`: Mengatur alignment `children` di sumbu silang (`vertical` untuk `Row`, `horizontal` untuk `Column`).
    - `CrossAxisAlignment.start`
    - `CrossAxisAlignment.center` (default)
    - `CrossAxisAlignment.end`
    - `CrossAxisAlignment.stretch`

- **Contoh `Row`:**
  ```dart
  Row(
    mainAxisAlignment: MainAxisAlignment.spaceEvenly,
    children: [
      Icon(Icons.star),
      Icon(Icons.star),
      Icon(Icons.star),
    ],
  )
  ```

### `Stack`
`Stack` memungkinkan Anda untuk menumpuk widget di atas satu sama lain, seperti tumpukan kartu. Widget pertama dalam list `children` akan berada di paling bawah, dan widget terakhir akan berada di paling atas.

- **Contoh:**
  ```dart
  Stack(
    alignment: Alignment.center,
    children: [
      Container(width: 200, height: 200, color: Colors.red),
      Container(width: 150, height: 150, color: Colors.green),
      Text('On Top'),
    ],
  )
  ```

### `ListView`
`ListView` adalah widget yang menyusun `children`-nya dalam daftar yang dapat di-scroll. Ini sangat efisien untuk menampilkan daftar item yang panjang.

```dart
ListView(
  children: [
    ListTile(leading: Icon(Icons.map), title: Text('Map')),
    ListTile(leading: Icon(Icons.photo_album), title: Text('Album')),
    ListTile(leading: Icon(Icons.phone), title: Text('Phone')),
  ],
)
```

### `GridView`
`GridView` menyusun `children`-nya dalam format grid (kisi-kisi) 2D yang dapat di-scroll.

```dart
GridView.count(
  crossAxisCount: 2, // Jumlah kolom
  children: List.generate(10, (index) {
    return Center(
      child: Text(
        'Item $index',
        style: Theme.of(context).textTheme.headline5,
      ),
    );
  }),
)
```

Menguasai widget-widget layout ini adalah langkah penting untuk dapat membangun hampir semua jenis tampilan yang bisa Anda bayangkan di Flutter.
