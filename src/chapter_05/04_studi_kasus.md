# Studi Kasus: Form Login dengan Persistence

Sekarang kita akan menggabungkan semua yang telah kita pelajari di bab ini: membuat form, memvalidasi input, dan menyimpan status login menggunakan `shared_preferences`.

**Skenario Aplikasi:**
1.  Saat aplikasi pertama kali dibuka, tampilkan halaman `LoginPage`.
2.  `LoginPage` memiliki form untuk email dan password.
3.  Validasi input: email harus valid dan password tidak boleh kosong.
4.  Jika login berhasil, simpan `bool` `isLoggedIn = true` ke `shared_preferences` dan arahkan pengguna ke `HomePage`.
5.  Saat aplikasi dibuka kembali, periksa nilai `isLoggedIn`. Jika `true`, langsung tampilkan `HomePage` dan lewati `LoginPage`.
6.  `HomePage` memiliki tombol "Logout" yang akan menghapus `isLoggedIn` dari `shared_preferences` dan mengembalikan pengguna ke `LoginPage`.

## Langkah 1: Struktur Proyek dan Dependensi
Pastikan Anda sudah menambahkan `shared_preferences` di `pubspec.yaml`.

Buat 3 file di folder `lib`:
- `lib/main.dart`
- `lib/login_page.dart`
- `lib/home_page.dart`

## Langkah 2: `main.dart` (Entry Point)
File ini akan menjadi titik awal yang memeriksa status login.

**`lib/main.dart`**
```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';
import 'package:form_persistence_example/home_page.dart';
import 'package:form_persistence_example/login_page.dart';

void main() async {
  // Pastikan Flutter binding sudah diinisialisasi
  WidgetsFlutterBinding.ensureInitialized();

  // Dapatkan instance SharedPreferences
  final prefs = await SharedPreferences.getInstance();
  // Baca status login, default-nya false jika tidak ada
  final bool isLoggedIn = prefs.getBool('isLoggedIn') ?? false;

  runApp(MyApp(isLoggedIn: isLoggedIn));
}

class MyApp extends StatelessWidget {
  final bool isLoggedIn;

  const MyApp({Key? key, required this.isLoggedIn}) : super(key: key);

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Form & Persistence',
      // Tentukan halaman awal berdasarkan status login
      home: isLoggedIn ? HomePage() : LoginPage(),
      // Definisikan rute untuk navigasi
      routes: {
        '/login': (context) => LoginPage(),
        '/home': (context) => HomePage(),
      },
    );
  }
}
```

## Langkah 3: `login_page.dart`
Ini adalah halaman yang berisi form login.

**`lib/login_page.dart`**
```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

class LoginPage extends StatefulWidget {
  @override
  _LoginPageState createState() => _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final _formKey = GlobalKey<FormState>();
  final _emailController = TextEditingController();
  final _passwordController = TextEditingController();

  @override
  void dispose() {
    _emailController.dispose();
    _passwordController.dispose();
    super.dispose();
  }

  void _login() async {
    // Validasi form
    if (_formKey.currentState!.validate()) {
      // Simpan status login ke SharedPreferences
      final prefs = await SharedPreferences.getInstance();
      await prefs.setBool('isLoggedIn', true);

      // Navigasi ke HomePage dan hapus semua rute sebelumnya
      Navigator.of(context).pushReplacementNamed('/home');
    }
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text('Login')),
      body: Padding(
        padding: const EdgeInsets.all(16.0),
        child: Form(
          key: _formKey,
          child: Column(
            mainAxisAlignment: MainAxisAlignment.center,
            children: [
              TextFormField(
                controller: _emailController,
                decoration: InputDecoration(labelText: 'Email'),
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Email tidak boleh kosong';
                  }
                  // Validasi format email sederhana
                  if (!value.contains('@')) {
                    return 'Format email tidak valid';
                  }
                  return null;
                },
              ),
              SizedBox(height: 16),
              TextFormField(
                controller: _passwordController,
                decoration: InputDecoration(labelText: 'Password'),
                obscureText: true,
                validator: (value) {
                  if (value == null || value.isEmpty) {
                    return 'Password tidak boleh kosong';
                  }
                  return null;
                },
              ),
              SizedBox(height: 32),
              ElevatedButton(
                onPressed: _login,
                child: Text('Login'),
              ),
            ],
          ),
        ),
      ),
    );
  }
}
```

## Langkah 4: `home_page.dart`
Halaman utama yang ditampilkan setelah login berhasil.

**`lib/home_page.dart`**
```dart
import 'package:flutter/material.dart';
import 'package:shared_preferences/shared_preferences.dart';

class HomePage extends StatelessWidget {
  void _logout(BuildContext context) async {
    // Hapus status login dari SharedPreferences
    final prefs = await SharedPreferences.getInstance();
    await prefs.remove('isLoggedIn');

    // Navigasi ke LoginPage dan hapus semua rute sebelumnya
    Navigator.of(context).pushReplacementNamed('/login');
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Home Page'),
        actions: [
          IconButton(
            icon: Icon(Icons.logout),
            onPressed: () => _logout(context),
          ),
        ],
      ),
      body: Center(
        child: Text('Selamat Datang! Anda berhasil login.'),
      ),
    );
  }
}
```

Dengan studi kasus ini, Anda telah berhasil mengintegrasikan dua konsep penting: menangani input pengguna dengan `Form` dan menjaga state aplikasi tetap ada dengan `shared_preferences`. Ini adalah pola yang sangat umum dan berguna di banyak aplikasi nyata.
