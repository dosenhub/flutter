# 8.3 Parsing JSON ke Model Dart

Untuk memudahkan kerja dengan data, sebaiknya buat kelas model yang merepresentasikan struktur JSON.

Contoh JSON dari endpoint `posts`:

```json
{
  "userId": 1,
  "id": 1,
  "title": "sunt aut facere repellat provident occaecati excepturi optio reprehenderit",
  "body": "quia et suscipit..."
}
```

Model Dart sederhana:

```dart
class Post {
  final int userId;
  final int id;
  final String title;
  final String body;

  Post({required this.userId, required this.id, required this.title, required this.body});

  factory Post.fromJson(Map<String, dynamic> json) {
    return Post(
      userId: json['userId'] as int,
      id: json['id'] as int,
      title: json['title'] as String,
      body: json['body'] as String,
    );
  }

  Map<String, dynamic> toJson() {
    return {
      'userId': userId,
      'id': id,
      'title': title,
      'body': body,
    };
  }
}
```

Tips:
- Untuk proyek besar, gunakan generator seperti `json_serializable` untuk mengurangi boilerplate.
- Validasi tipe dan nilai null safety penting: gunakan `as Type?` dan fallback bila perlu.
