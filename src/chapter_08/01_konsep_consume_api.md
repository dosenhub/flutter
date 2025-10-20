# 8.1 Konsep: Apa itu API dan bagaimana aplikasi mengkonsumsinya

API (Application Programming Interface) adalah sekumpulan aturan yang memungkinkan satu aplikasi berkomunikasi dengan aplikasi lain. Di konteks aplikasi mobile/web, API biasanya merujuk ke layanan backend yang menyediakan data melalui protokol HTTP dan format data seperti JSON.

Konsep penting:
- Endpoint: URL yang mewakili resource (contoh: `https://api.example.com/posts`)
- Method HTTP: GET (ambil data), POST (kirim data baru), PUT/PATCH (ubah data), DELETE (hapus)
- Status Code: angka yang menunjukkan hasil (200 OK, 201 Created, 400 Bad Request, 401 Unauthorized, 404 Not Found, 500 Server Error)
- Payload/Body: data yang dikirim atau diterima, umumnya dalam format JSON
- Headers: meta-data request seperti `Content-Type`, `Authorization` (untuk token)

Alur konsumsi API di aplikasi Flutter:
1. Aplikasi membuat request HTTP ke endpoint
2. Server memproses dan mengirim response (status + body)
3. Aplikasi menerima response, melakukan parsing JSON ke model data
4. UI di-refresh untuk menampilkan data

Pertimbangan desain:
- Asinkron: operasi jaringan memakan waktu — gunakan `Future`, `async/await`, atau stream
- Error handling: network errors, parsing errors, dan error server harus ditangani
- Caching & offline: simpan data lokal (SharedPreferences / Hive / SQLite) untuk pengalaman offline
- Keamanan: jangan simpan token sensitif secara terbuka; gunakan secure storage bila perlu

