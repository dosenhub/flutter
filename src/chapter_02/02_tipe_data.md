## Tipe Data Fundamental di Dart

Dart adalah bahasa yang diketik secara statis, yang berarti setiap variabel memiliki tipe yang ditentukan pada saat kompilasi. Berikut adalah beberapa tipe data dasar yang paling sering digunakan:

### 1. Numbers (`num`, `int`, `double`)

Dart memiliki dua jenis tipe data untuk angka:

-   **`int`**: Untuk bilangan bulat (integer).
    ```dart
    int quantity = 5;
    int hexValue = 0xFF; // Juga mendukung format heksadesimal
    ```

-   **`double`**: Untuk bilangan desimal (floating-point).
    ```dart
    double price = 19.99;
    double exponent = 1.2e3; // 1.2 x 10^3
    ```

-   **`num`**: Tipe ini bisa menampung `int` maupun `double`.

    ```dart
    num myNumber = 10; // Bisa berupa integer
    myNumber = 15.5;   // atau bisa juga berupa double
    ```

### 2. Strings (`String`)

Tipe `String` digunakan untuk menyimpan teks. Anda bisa menggunakan tanda kutip tunggal (`'`) atau ganda (`"`).

```dart
String singleQuote = 'Ini adalah string.';
String doubleQuote = "Ini juga string.";
```

Untuk menyisipkan nilai variabel ke dalam string, gunakan `$` (interpolasi string):

```dart
String name = 'Budi';
String greeting = 'Halo, $name!'; // Menghasilkan "Halo, Budi!"
```

### 3. Booleans (`bool`)

Tipe `bool` hanya memiliki dua nilai: `true` dan `false`.

```dart
bool isLoading = true;
bool isFinished = false;
```

### 4. Lists (atau Arrays)

`List` adalah kumpulan objek yang terurut. Ini mirip dengan array di bahasa lain.

```dart
// Membuat list string
List<String> fruits = ['Apel', 'Pisang', 'Jeruk'];

// Mengakses elemen berdasarkan indeks (dimulai dari 0)
String firstFruit = fruits[0]; // 'Apel'

// Menambah elemen baru
fruits.add('Mangga');

// Menghapus elemen
fruits.remove('Pisang');
```

### 5. Maps (atau Dictionaries)

`Map` adalah kumpulan pasangan kunci-nilai (*key-value pairs*). Setiap kunci harus unik.

```dart
// Membuat map dengan kunci String dan nilai dinamis
Map<String, dynamic> person = {
  'name': 'Andi',
  'age': 25,
  'isStudent': true
};

// Mengakses nilai berdasarkan kunci
String name = person['name']; // 'Andi'

// Menambahkan atau mengubah nilai
person['city'] = 'Jakarta';
person['age'] = 26;
```

Tipe-tipe data ini adalah fondasi untuk membangun struktur data yang lebih kompleks dalam aplikasi Flutter Anda.
