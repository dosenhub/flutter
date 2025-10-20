# 8.2 HTTP di Dart: async, Future, dan paket `http`

Paket yang paling sederhana untuk HTTP di Dart/Flutter adalah `package:http`. Untuk proyek yang lebih besar dan fitur lebih lengkap dapat digunakan `dio`.

Contoh dependensi pada `pubspec.yaml`:

```yaml
dependencies:
  http: ^0.13.0
```

Contoh membuat GET request sederhana:

```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<void> fetchPosts() async {
  final url = Uri.parse('https://jsonplaceholder.typicode.com/posts');
  final response = await http.get(url);

  if (response.statusCode == 200) {
    final List data = jsonDecode(response.body);
    print('Diterima ${data.length} item');
  } else {
    throw Exception('Gagal fetch: ${response.statusCode}');
  }
}
```

Catatan:
- Gunakan `Uri.parse` untuk membangun URL; ini membantu query parameters dan encoding.
- Jangan memanggil fungsi jaringan di `build()` — gunakan `initState`, `FutureBuilder`, Provider, Riverpod atau state management lain.
- Tambahkan timeout jika perlu: `await http.get(url).timeout(Duration(seconds: 10))`

Contoh POST request:

```dart
Future<void> createPost(Map<String, dynamic> payload) async {
  final url = Uri.parse('https://jsonplaceholder.typicode.com/posts');
  final response = await http.post(url,
    headers: {'Content-Type': 'application/json'},
    body: jsonEncode(payload),
  );

  if (response.statusCode == 201) {
    print('Berhasil membuat post');
  } else {
    throw Exception('Gagal membuat post: ${response.statusCode}');
  }
}
```