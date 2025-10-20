# 8.4 Penanganan Error

Network code rentan terhadap berbagai kegagalan. Berikut beberapa pola penanganan error:

- Timeouts: gunakan `.timeout(Duration(...))` dan tangani `TimeoutException`.
- Network errors: `SocketException` jika tidak ada koneksi.
- Response error: periksa `statusCode` dan parsing message dari body.
- Retries: untuk operasi idempotent, gunakan retry dengan exponential backoff.

Contoh penanganan sederhana:

```dart
import 'dart:async';
import 'dart:io';
import 'package:http/http.dart' as http;

Future<String> safeGet(Uri url) async {
  try {
    final response = await http.get(url).timeout(Duration(seconds: 10));
    if (response.statusCode == 200) return response.body;
    throw HttpException('Server returned ${response.statusCode}');
  } on TimeoutException {
    throw Exception('Request timed out');
  } on SocketException {
    throw Exception('No internet connection');
  }
}
```

Catatan: otentikasi (token, OAuth, dsb.) tidak dibahas di bab ini. Kita akan membahas otentikasi di bab terpisah.
