# Chapter 03: Widget dan Layout Flutter

## Rencana Materi

### 1. Pengenalan Flutter dan Widget
- Apa itu Widget?
- Filosofi "Everything is a Widget"
- Hierarki Widget (Widget Tree)

### 2. Jenis-jenis Widget
- **Stateless vs Stateful Widget**
  - Perbedaan konsep, siklus hidup (lifecycle), dan penggunaan.
  - Kapan menggunakan `StatelessWidget`?
  - Kapan menggunakan `StatefulWidget`?
- **UI Widget vs Layout Widget**
  - Widget untuk menampilkan UI (Text, Image, Icon, Button).
  - Widget untuk mengatur tata letak (Container, Row, Column, Stack).

### 3. Konsep Named Parameter pada Widget
- Penjelasan tentang *named parameter* di Dart.
- Bagaimana *named parameter* membuat konfigurasi widget menjadi lebih mudah dibaca dan deklaratif.
- Contoh penggunaan pada widget seperti `Container` atau `Text`.

### 4. Layouting
- **Single-child layout widgets:**
  - `Container`: Properti `child`, `padding`, `margin`, `color`, `decoration`.
  - `Center`: Memposisikan widget anak di tengah.
  - `Padding`: Memberi ruang di sekitar widget.
  - `SizedBox`: Membuat kotak dengan ukuran tertentu.
  - `AspectRatio`: Mengatur rasio aspek widget.
- **Multi-child layout widgets:**
  - `Row`: Menyusun widget secara horizontal. Properti `mainAxisAlignment` dan `crossAxisAlignment`.
  - `Column`: Menyusun widget secara vertikal. Properti `mainAxisAlignment` dan `crossAxisAlignment`.
  - `Stack`: Menumpuk widget di atas satu sama lain.
  - `ListView`: Menampilkan daftar widget yang dapat di-scroll.
  - `GridView`: Menampilkan widget dalam format grid.

### 5. Contoh-contoh Widget dan Layout Flutter
- **Praktek 1: Membuat Kartu Nama Digital (Digital Business Card)**
  - Menggunakan `Container`, `Row`, `Column`, `Icon`, `Text`, dan `Image`.
- **Praktek 2: Membuat Layout Galeri Gambar Sederhana**
  - Menggunakan `GridView` dan `Container`.
- **Praktek 3: Layout Responsif Sederhana**
  - Menggunakan `MediaQuery` untuk mendapatkan ukuran layar.
  - Menggunakan `LayoutBuilder` untuk membuat layout yang beradaptasi.
