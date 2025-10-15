# Konsep Fundamental Navigasi

Sebelum kita masuk ke kode, penting untuk memahami tiga konsep inti yang menjadi dasar sistem navigasi di Flutter: **Stack of Pages (Routes)**, **Navigator Widget**, dan **Route**.

## 1. Stack of Pages (Tumpukan Halaman)

Bayangkan layar-layar dalam aplikasi Anda sebagai setumpuk kartu. Ketika Anda pindah ke layar baru, Anda meletakkan kartu baru di atas tumpukan. Ketika Anda menekan tombol "kembali", Anda mengambil kartu teratas dari tumpukan, sehingga kartu di bawahnya kembali terlihat.

Inilah cara kerja navigasi di Flutter. Tumpukan ini dikelola oleh `Navigator` dan setiap "kartu" atau "halaman" dalam tumpukan ini disebut **Route**.

- **Push:** Operasi "mendorong" `Route` baru ke atas tumpukan. Ini akan menampilkan layar baru kepada pengguna.
- **Pop:** Operasi "melepas" `Route` teratas dari tumpukan. Ini akan menutup layar saat ini dan kembali ke layar sebelumnya.

Layar pertama yang dibuka aplikasi Anda adalah dasar dari tumpukan tersebut.

## 2. Navigator Widget

`Navigator` adalah widget khusus yang mengelola tumpukan `Route`. Anda tidak sering berinteraksi langsung dengan widget `Navigator` itu sendiri, tetapi Anda akan sering menggunakan method statisnya, seperti `Navigator.of(context)` atau `Navigator.push()` dan `Navigator.pop()`.

Secara default, `MaterialApp` atau `CupertinoApp` sudah secara otomatis membuatkan sebuah `Navigator` untuk Anda. `Navigator` inilah yang menjadi "otak" di balik semua perpindahan layar dalam aplikasi Anda.

Setiap `Navigator` mengelola tumpukan riwayatnya sendiri. Ini memungkinkan skenario navigasi yang kompleks, seperti memiliki alur navigasi terpisah di dalam sebuah tab.

## 3. Route

Sebuah **Route** adalah representasi dari sebuah layar atau halaman dalam tumpukan `Navigator`. Ini bukan hanya `Widget` itu sendiri, melainkan sebuah objek yang membungkus `Widget` Anda dan menangani hal-hal seperti transisi animasi saat layar muncul atau hilang.

Ada beberapa jenis `Route`, tetapi yang paling umum Anda gunakan adalah `MaterialPageRoute`.

### `MaterialPageRoute`
`MaterialPageRoute` adalah `Route` yang mengimplementasikan transisi halaman standar sesuai dengan pedoman Material Design. Di Android, halaman baru akan meluncur dari bawah ke atas. Di iOS, halaman baru akan meluncur dari kanan ke kiri.

Untuk membuat `MaterialPageRoute`, Anda perlu menyediakan sebuah `builder`. `builder` ini adalah sebuah fungsi yang menerima `BuildContext` dan mengembalikan widget yang ingin Anda tampilkan untuk rute tersebut.

```dart
// Contoh membuat sebuah MaterialPageRoute
MaterialPageRoute(
  builder: (BuildContext context) {
    return SecondScreen(); // Widget untuk layar kedua
  },
)
```

Secara ringkas, alurnya adalah: Anda meminta `Navigator` untuk `push` sebuah `Route` (misalnya, `MaterialPageRoute`), dan `Route` tersebut akan `build` (membangun) widget layar Anda untuk ditampilkan kepada pengguna.
