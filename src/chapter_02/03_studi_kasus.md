## Studi Kasus: Membuat Program Pengelolaan Data Kontak Sederhana

Mari kita terapkan konsep-konsep yang telah kita pelajari dalam sebuah studi kasus kecil. Kita akan membuat program sederhana untuk mengelola data kontak.

### Langkah 1: Mendefinisikan Data Kontak

Pertama, kita akan mendefinisikan data untuk satu kontak. Kita akan menggunakan `final` untuk nilai yang tidak akan berubah dan `var` untuk nilai yang mungkin akan kita ubah nanti.

```dart
void main() {
  // Menggunakan 'final' karena nama dan tanggal lahir tidak akan berubah
  final String name = 'Budi Santoso';
  final int birthYear = 1995;

  // Menggunakan 'var' karena nomor telepon bisa saja diubah
  var phoneNumber = '081234567890';

  // Menggunakan List untuk menyimpan beberapa hobi
  List<String> hobbies = ['Membaca', 'Berenang', 'Menulis'];

  // Menghitung umur
  var currentYear = DateTime.now().year;
  var age = currentYear - birthYear;

  print('Nama: $name');
  print('Umur: $age tahun');
  print('Nomor Telepon: $phoneNumber');
  print('Hobi: $hobbies');
}
```

### Langkah 2: Menangani Data yang Mungkin Kosong (Null Safety)

Tidak semua kontak memiliki alamat email. Kita bisa menggunakan tipe data nullable (`String?`) untuk menangani ini.

```dart
void main() {
  // ... (kode dari Langkah 1)

  // Alamat email bisa jadi null
  String? email;

  // Fungsi untuk menampilkan email jika ada
  void printEmail(String? emailAddress) {
    if (emailAddress != null) {
      print('Email: $emailAddress');
    } else {
      print('Email: (tidak ada)');
    }
  }

  printEmail(email); // Output: Email: (tidak ada)

  // Sekarang kita tambahkan email
  email = 'budi.santoso@example.com';
  printEmail(email); // Output: Email: budi.santoso@example.com
}
```

### Langkah 3: Mengelompokkan Data dengan Map

Menggunakan variabel terpisah bisa menjadi tidak praktis. Mari kita kelompokkan semua informasi kontak ke dalam sebuah `Map`.

```dart
void main() {
  // ... (kode dari Langkah 1 & 2)

  // Membuat Map untuk menyimpan data kontak
  final Map<String, dynamic> contact = {
    'name': 'Budi Santoso',
    'age': 28,
    'phone': '081234567890',
    'hobbies': ['Membaca', 'Berenang', 'Menulis'],
    'email': 'budi.santoso@example.com',
    'is_active': true
  };

  // Mengakses data dari Map
  print('Nama dari Map: ${contact['name']}');
  print('Hobi pertama: ${contact['hobbies'][0]}');
}
```

### Langkah 4: Menampilkan Data Kontak dengan Rapi

Sekarang, mari kita buat fungsi yang dapat menampilkan detail kontak dari `Map` yang sudah kita buat.

```dart
void displayContact(Map<String, dynamic> contact) {
  print('--- Detail Kontak ---');
  print('Nama: ${contact['name']}');
  print('Umur: ${contact['age']} tahun');
  print('Telepon: ${contact['phone']}');
  
  // Menampilkan hobi
  List<String> hobbies = contact['hobbies'];
  print('Hobi:');
  for (var hobby in hobbies) {
    print('- $hobby');
  }

  // Menampilkan email dengan pengecekan null
  String? email = contact['email'];
  if (email != null) {
    print('Email: $email');
  } else {
    print('Email: Tidak tersedia');
  }
  
  print('Status Aktif: ${contact['is_active'] ? 'Ya' : 'Tidak'}');
  print('---------------------');
}

void main() {
  final Map<String, dynamic> contact = {
    'name': 'Budi Santoso',
    'age': 28,
    'phone': '081234567890',
    'hobbies': ['Membaca', 'Berenang', 'Menulis'],
    'email': 'budi.santoso@example.com',
    'is_active': true
  };

  displayContact(contact);
}
```

Dengan studi kasus ini, kita telah menerapkan konsep-konsep dasar Dart seperti variabel, tipe data, null safety, dan struktur data seperti List dan Map dalam konteks yang praktis.
