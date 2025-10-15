# Konsep Named Parameter pada Widget

Salah satu fitur bahasa Dart yang membuat kode Flutter sangat mudah dibaca dan deklaratif adalah penggunaan **Named Parameter** (parameter bernama). Saat Anda membuat instance sebuah widget, Anda hampir selalu menggunakan *named parameter* untuk mengonfigurasinya.

## Apa itu Named Parameter?

Di Dart, fungsi atau konstruktor dapat memiliki dua jenis parameter: *positional* dan *named*.

- **Positional Parameter:** Parameter yang nilainya ditentukan oleh posisinya dalam pemanggilan fungsi. Ini adalah jenis parameter standar di banyak bahasa pemrograman.
- **Named Parameter:** Parameter yang diidentifikasi oleh namanya, bukan posisinya. Mereka bersifat opsional secara default dan ditandai dengan kurung kurawal `{}` dalam definisi fungsi/konstruktor.

**Contoh Sederhana di Dart:**
```dart
// Definisi fungsi dengan named parameter
void printUserDetails({String name, int age}) {
  print('Name: $name, Age: $age');
}

// Pemanggilan fungsi
printUserDetails(name: 'Alice', age: 30);
printUserDetails(age: 25, name: 'Bob'); // Urutan tidak penting
```

## Named Parameter pada Widget Flutter

Konstruktor widget di Flutter secara ekstensif menggunakan *named parameter*. Ini adalah pilihan desain yang disengaja karena beberapa alasan kuat:

1.  **Keterbacaan (Readability):** Dengan puluhan properti yang mungkin dimiliki sebuah widget, *named parameter* membuat kode menjadi jauh lebih jelas. Anda tahu persis properti apa yang sedang Anda atur tanpa harus menghafal urutan parameter.

    *Kurang Jelas (Tanpa Named Parameter):*
    ```dart
    // Ini BUKAN kode Flutter, hanya ilustrasi
    // new Container(300.0, 200.0, Colors.blue, new Text("Hello"), 16.0);
    ```

    *Sangat Jelas (Dengan Named Parameter):*
    ```dart
    Container(
      width: 300.0,
      height: 200.0,
      color: Colors.blue,
      padding: EdgeInsets.all(16.0),
      child: Text("Hello"),
    );
    ```

2.  **Fleksibilitas dan Opsionalitas:** Sebagian besar properti widget bersifat opsional. Anda hanya perlu menentukan properti yang ingin Anda ubah dari nilai defaultnya. *Named parameter* sangat cocok untuk skenario ini.

3.  **Kemudahan Penggunaan (Discoverability):** Saat menggunakan IDE seperti VS Code atau Android Studio, IDE dapat secara otomatis menampilkan daftar *named parameter* yang tersedia untuk sebuah widget, membuatnya lebih mudah untuk "menemukan" properti apa saja yang bisa Anda konfigurasi.

## Contoh Penggunaan pada Widget Umum

Mari kita lihat bagaimana *named parameter* digunakan pada beberapa widget yang sering kita temui.

### `Text` Widget
Widget `Text` memiliki satu parameter *positional* wajib (yaitu data teks itu sendiri) dan banyak *named parameter* opsional untuk styling.

```dart
Text(
  'Ini adalah teks utama', // Positional parameter
  style: TextStyle(         // Named parameter
    color: Colors.red,
    fontSize: 24.0,
    fontWeight: FontWeight.bold,
  ),
  textAlign: TextAlign.center, // Named parameter
)
```

### `Container` Widget
Widget `Container` adalah contoh utama dari kekuatan *named parameter*. Hampir semua konfigurasinya dilakukan melalui parameter ini.

```dart
Container(
  // Properti untuk ukuran dan batasan
  width: 150,
  height: 100,

  // Properti untuk dekorasi (tidak bisa dipakai bersamaan dengan `color`)
  decoration: BoxDecoration(
    color: Colors.amber,
    borderRadius: BorderRadius.circular(12),
  ),

  // Properti untuk tata letak internal
  padding: EdgeInsets.symmetric(horizontal: 20, vertical: 10),
  alignment: Alignment.center,

  // Widget anak
  child: Text('Hello World'),
)
```

Dengan menggunakan *named parameter*, Flutter memungkinkan kita untuk membuat UI yang kompleks dengan cara yang sangat deklaratif dan mudah dipelihara. Anda "mendeskripsikan" seperti apa tampilan UI yang Anda inginkan, dan Flutter yang akan mengurus sisanya.
