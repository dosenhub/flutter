# Pengenalan Flutter dan Widget

## Apa itu Widget?

Dalam Flutter, **Widget** adalah blok bangunan dasar untuk membuat antarmuka pengguna (UI). Anggap saja widget seperti potongan-potongan LEGO yang dapat Anda susun untuk membangun aplikasi Anda. Setiap widget adalah representasi dari bagian tertentu dari UI, seperti teks, tombol, gambar, atau bahkan tata letak yang tidak terlihat.

Widget di Flutter bersifat *immutable* (tidak dapat diubah). Ini berarti bahwa setiap kali framework perlu memperbarui tampilan, ia akan membuat instance widget baru, bukan memodifikasi yang lama. Proses ini sangat efisien dan membantu Flutter mencapai performa rendering yang tinggi.

## Filosofi "Everything is a Widget"

Salah satu konsep paling kuat di Flutter adalah "segalanya adalah widget". Ini berarti bahwa hampir semua yang Anda buat di Flutter, dari hal paling sederhana hingga paling kompleks, adalah sebuah widget.

- Sebuah `Text` adalah widget.
- Sebuah `Image` adalah widget.
- `Padding` (untuk memberi ruang) adalah widget.
- `Center` (untuk memposisikan di tengah) adalah widget.
- `Row` dan `Column` (untuk tata letak) adalah widget.
- Bahkan aplikasi Anda secara keseluruhan (`MaterialApp` atau `CupertinoApp`) adalah sebuah widget.

Filosofi ini memberikan konsistensi dan kemudahan dalam menyusun UI. Anda tidak perlu belajar konsep yang berbeda untuk layout, styling, atau logika bisnis. Anda hanya perlu berpikir tentang bagaimana cara menyusun widget.

## Hierarki Widget (Widget Tree)

Aplikasi Flutter dibangun dengan menyusun widget dalam sebuah hierarki yang disebut **Widget Tree**. Ada widget induk (parent) dan widget anak (child/children). Widget induk dapat berisi satu atau lebih widget anak, membentuk struktur seperti pohon.

Misalnya, untuk membuat sebuah halaman sederhana, Anda mungkin memiliki struktur seperti ini:

```
Scaffold
└── Center
    └── Column
        ├── Text
        ├── Button
        └── Image
```

- `Scaffold` adalah widget dasar untuk layout halaman Material Design.
- `Center` adalah widget yang memposisikan anaknya di tengah.
- `Column` adalah widget yang menyusun anak-anaknya secara vertikal.
- `Text`, `Button`, dan `Image` adalah widget-widget yang menampilkan konten.

Flutter akan "berjalan" melalui pohon widget ini untuk merender UI ke layar. Memahami bagaimana widget tree bekerja adalah kunci untuk membangun layout yang kompleks dan efisien di Flutter.
