# Bab 8: Mengkonsumsi API (Consume API)

Di dunia nyata, aplikasi yang berguna seringkali adalah aplikasi yang mampu "berbicara" dengan layanan lain — mengambil daftar, mengirim perubahan, atau memperbarui antarmuka berdasarkan data jarak jauh. Bab ini dimaksudkan untuk membawa Anda melewati perjalanan tersebut: bukan hanya sebagai kumpulan perintah, melainkan sebagai latihan merancang alur data yang masuk dan keluar sambil menjaga pengalaman pengguna tetap mulus ketika koneksi tidak sempurna. Contoh dan studi kasus yang disertakan akan membantu Anda memahami pola pikir yang diperlukan agar aplikasi tetap responsif, mudah diuji, dan mudah dirawat.

Bab ini membahas bagaimana aplikasi Flutter/Dart berkomunikasi dengan service backend melalui HTTP: dari konsep dasar, request/response, parsing JSON, sampai implementasi aplikasi nyata.

Di akhir bab ini Anda akan bisa:
- Memahami arsitektur request HTTP dan format data umum (JSON)
- Menggunakan paket `http` (atau alternatif seperti Dio) untuk melakukan GET/POST/PUT/DELETE
- Membuat model data (Dart class) dari JSON dan sebaliknya
- Menangani error, timeouts (otentikasi akan dibahas di bab terpisah)
- Mengimplementasikan studi kasus aplikasi yang mengambil data dari API publik dan melakukan operasi CRUD sederhana

Struktur bab:
- [Konsep: Apa itu API dan bagaimana aplikasi mengkonsumsinya](./chapter_08/01_konsep_consume_api.md)
- [HTTP di Dart: async, Future, dan paket `http`](./chapter_08/02_http_request_dart.md)
- [Parsing JSON ke Model Dart](./chapter_08/03_parsing_json.md)
- [Penanganan Error](./chapter_08/04_error_handling.md)
- [Studi Kasus: Aplikasi Sederhana Konsumsi API (Posts)](./chapter_08/05_implementasi_studi_kasus.md)

Saran: ikuti studi kasus langkah demi langkah sambil mengetik dan menjalankan contoh. Gunakan emulator atau perangkat fisik untuk melihat hasilnya.
