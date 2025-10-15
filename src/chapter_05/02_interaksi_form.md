# Interaksi dengan Form

Setelah memahami konsep dasar `Form` dan `TextFormField`, langkah selanjutnya adalah mempelajari cara berinteraksi dengannya: bagaimana cara mengambil nilai yang dimasukkan pengguna, bagaimana cara memvalidasinya, dan bagaimana cara merespons event yang terjadi.

## 1. Pengambilan Nilai dari Form

Ada dua cara utama untuk mendapatkan data dari `TextFormField`.

### Menggunakan `TextEditingController`
Ini adalah pendekatan yang paling umum, terutama jika Anda memerlukan akses ke nilai field secara *real-time* atau di luar proses `save` dari `Form`.

**Langkah-langkah:**
1.  Buat sebuah `TextEditingController` untuk setiap `TextFormField`.
    ```dart
    final _emailController = TextEditingController();
    ```
2.  Hubungkan controller tersebut ke properti `controller` pada `TextFormField`.
    ```dart
    TextFormField(
      controller: _emailController,
      // ...
    )
    ```
3.  Akses nilainya kapan pun Anda butuhkan melalui properti `.text`.
    ```dart
    print('Current email value: ${_emailController.text}');
    ```
4.  **Penting:** Jangan lupa untuk membuang (`dispose`) controller ketika widget tidak lagi digunakan untuk mencegah kebocoran memori.
    ```dart
    @override
    void dispose() {
      _emailController.dispose();
      super.dispose();
    }
    ```

### Menggunakan `onSaved`
Pendekatan ini sangat cocok jika Anda hanya perlu mengumpulkan semua data dari form pada saat proses submit.

**Langkah-langkah:**
1.  Buat variabel untuk menampung nilai yang akan disimpan.
    ```dart
    String _userEmail = '';
    ```
2.  Implementasikan callback `onSaved` pada `TextFormField`. Callback ini akan memberikan nilai akhir dari field tersebut.
    ```dart
    TextFormField(
      // ...
      onSaved: (value) {
        _userEmail = value ?? '';
      },
    )
    ```
3.  Panggil `_formKey.currentState!.save()` untuk memicu semua callback `onSaved` di dalam `Form`.
    ```dart
    ElevatedButton(
      onPressed: () {
        if (_formKey.currentState!.validate()) {
          // Panggil save() setelah validasi berhasil
          _formKey.currentState!.save();
          print('Saved email: $_userEmail');
        }
      },
      child: Text('Submit'),
    )
    ```

## 2. Form Validation (Validasi Form)

Validasi memastikan bahwa data yang dimasukkan pengguna sesuai dengan format yang kita harapkan.

### Properti `validator`
Setiap `TextFormField` memiliki properti `validator`, yaitu sebuah fungsi yang menerima nilai input saat ini (`String?`) dan harus mengembalikan:
-   `null` jika inputnya **valid**.
-   Sebuah `String` yang berisi pesan error jika inputnya **tidak valid**. Pesan error ini akan otomatis ditampilkan di bawah field.

**Contoh Validasi:**
```dart
TextFormField(
  decoration: InputDecoration(labelText: 'Password'),
  obscureText: true,
  validator: (value) {
    if (value == null || value.isEmpty) {
      return 'Password tidak boleh kosong';
    }
    if (value.length < 6) {
      return 'Password harus lebih dari 6 karakter';
    }
    return null; // Valid
  },
)
```

### Memicu Validasi
Validasi tidak terjadi secara otomatis. Anda harus memicunya secara manual dengan memanggil `_formKey.currentState!.validate()`.

Method `validate()` akan menjalankan semua fungsi `validator` di dalam `Form` dan mengembalikan:
-   `true` jika semua field valid.
-   `false` jika setidaknya ada satu field yang tidak valid.

Ini memungkinkan Anda untuk membuat alur seperti ini:
```dart
// Di dalam onPressed sebuah tombol
if (_formKey.currentState!.validate()) {
  // Jika form valid, lanjutkan proses (misalnya, kirim data ke server)
  ScaffoldMessenger.of(context).showSnackBar(
    SnackBar(content: Text('Processing Data')),
  );
} else {
  // Jika form tidak valid, error akan otomatis ditampilkan
}
```

## 3. Form Events

Selain `onSaved`, ada beberapa event lain yang berguna.

-   **`onChanged`**: Dipicu **setiap kali** ada perubahan pada input (setiap karakter yang diketik atau dihapus). Ini berguna untuk logika yang berjalan secara *real-time*, seperti memfilter daftar atau menampilkan kekuatan password.
    ```dart
    TextFormField(
      onChanged: (value) {
        print('Current value: $value');
      },
    )
    ```
-   **`onFieldSubmitted`**: Dipicu ketika pengguna menekan tombol "submit" (seperti "enter" atau "done") pada keyboard. Ini berguna untuk memindahkan fokus ke field berikutnya atau langsung men-submit form.
    ```dart
    TextFormField(
      textInputAction: TextInputAction.next, // Tampilkan tombol 'next' di keyboard
      onFieldSubmitted: (value) {
        // Pindahkan fokus ke field berikutnya
        FocusScope.of(context).nextFocus();
      },
    )
    ```
