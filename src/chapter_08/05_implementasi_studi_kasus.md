# 8.5 Studi Kasus: Aplikasi Sederhana Konsumsi API (Posts)

Di studi kasus ini kita akan membuat aplikasi Flutter sederhana yang:
- Mengambil daftar post dari `https://jsonplaceholder.typicode.com/posts`
- Menampilkan daftar di `ListView`
- Menampilkan detail saat item dipilih
- Menambahkan post baru (POST)

Struktur file contoh singkat:

- lib/
  - models/post.dart
  - services/api_service.dart
  - screens/home_screen.dart
  - screens/detail_screen.dart

Contoh `models/post.dart`:

```dart
class Post {
  final int userId;
  final int id;
  final String title;
  final String body;

  Post({required this.userId, required this.id, required this.title, required this.body});

  factory Post.fromJson(Map<String, dynamic> json) => Post(
    userId: json['userId'],
    id: json['id'],
    title: json['title'],
    body: json['body'],
  );
}
```

Contoh `services/api_service.dart`:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;
import '../models/post.dart';

class ApiService {
  final base = 'https://jsonplaceholder.typicode.com';

  Future<List<Post>> fetchPosts() async {
    final res = await http.get(Uri.parse('
      '$base/posts'
    ));
    if (res.statusCode == 200) {
      final List json = jsonDecode(res.body);
      return json.map((e) => Post.fromJson(e)).toList();
    }
    throw Exception('Gagal fetch posts');
  }

  Future<Post> createPost(Post p) async {
    final res = await http.post(Uri.parse('$base/posts'), headers: {
      'Content-Type': 'application/json'
    }, body: jsonEncode({'title': p.title, 'body': p.body, 'userId': p.userId}));

    if (res.statusCode == 201) return Post.fromJson(jsonDecode(res.body));
    throw Exception('Gagal membuat post');
  }
}
```

Saran: implementasikan UI dengan `FutureBuilder` untuk fetch awal, dan `Navigator.push` ke detail screen.

Langkah verifikasi:
1. Tambahkan `http` ke `pubspec.yaml`
2. Jalankan `flutter pub get`
3. Run aplikasi di emulator dan pastikan daftar posts muncul