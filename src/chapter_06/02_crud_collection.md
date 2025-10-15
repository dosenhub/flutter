# Implementasi CRUD dengan Collection

Setelah memahami dasar-dasar state management, sekarang kita akan menerapkan konsep tersebut untuk membangun aplikasi sederhana yang dapat melakukan operasi **CRUD (Create, Read, Update, Delete)** pada sebuah koleksi data di memori. Kita akan menggunakan `List<String>` sebagai "database" in-memory dan `setState()` untuk mengelola state.

## 1. Konsep CRUD

-   **Create (Membuat):** Menambahkan item baru ke dalam koleksi.
-   **Read (Membaca):** Menampilkan semua item yang ada dalam koleksi.
-   **Update (Memperbarui):** Mengubah item yang sudah ada dalam koleksi.
-   **Delete (Menghapus):** Menghilangkan item dari koleksi.

## 2. Studi Kasus: Aplikasi Daftar Belanja Sederhana (To-Do List)

Kita akan membuat aplikasi daftar belanja sederhana di mana pengguna dapat menambah, melihat, mengedit, dan menghapus item.

### Langkah 1: Struktur Proyek
Buat file `lib/main.dart` sebagai entry point aplikasi.

### Langkah 2: `main.dart` (Entry Point dan Aplikasi)

```dart
import 'package:flutter/material.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Simple To-Do List',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TodoListScreen(),
    );
  }
}

class TodoListScreen extends StatefulWidget {
  @override
  _TodoListScreenState createState() => _TodoListScreenState();
}

class _TodoListScreenState extends State<TodoListScreen> {
  final List<String> _todos = []; // Koleksi data kita
  final TextEditingController _textFieldController = TextEditingController();

  // Fungsi untuk menambahkan item
  void _addTodoItem(String title) {
    setState(() {
      _todos.add(title);
    });
    _textFieldController.clear(); // Bersihkan input setelah ditambahkan
  }

  // Fungsi untuk mengedit item
  void _editTodoItem(int index, String newTitle) {
    setState(() {
      _todos[index] = newTitle;
    });
  }

  // Fungsi untuk menghapus item
  void _deleteTodoItem(int index) {
    setState(() {
      _todos.removeAt(index);
    });
  }

  // Dialog untuk menambahkan/mengedit item
  Future<void> _displayTextInputDialog(BuildContext context, {int? index, String? currentTitle}) async {
    _textFieldController.text = currentTitle ?? ''; // Isi dengan judul saat ini jika mengedit

    return showDialog(
      context: context,
      builder: (context) {
        return AlertDialog(
          title: Text(index == null ? 'Add New To-Do' : 'Edit To-Do'),
          content: TextField(
            controller: _textFieldController,
            decoration: InputDecoration(hintText: 'Enter your to-do item'),
            autofocus: true,
          ),
          actions: <Widget>[
            TextButton(
              child: Text('Cancel'),
              onPressed: () {
                Navigator.pop(context);
                _textFieldController.clear();
              },
            ),
            ElevatedButton(
              child: Text(index == null ? 'Add' : 'Save'),
              onPressed: () {
                if (_textFieldController.text.isNotEmpty) {
                  if (index == null) {
                    _addTodoItem(_textFieldController.text);
                  } else {
                    _editTodoItem(index, _textFieldController.text);
                  }
                  Navigator.pop(context);
                }
              },
            ),
          ],
        );
      },
    );
  }

  @override
  void dispose() {
    _textFieldController.dispose();
    super.dispose();
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('To-Do List'),
      ),
      body: _todos.isEmpty
          ? Center(child: Text('No to-do items yet! Add some below.'))
          : ListView.builder(
              itemCount: _todos.length,
              itemBuilder: (context, index) {
                return Card(
                  margin: EdgeInsets.symmetric(vertical: 4, horizontal: 8),
                  child: ListTile(
                    title: Text(_todos[index]),
                    trailing: Row(
                      mainAxisSize: MainAxisSize.min,
                      children: [
                        IconButton(
                          icon: Icon(Icons.edit),
                          onPressed: () => _displayTextInputDialog(
                            context,
                            index: index,
                            currentTitle: _todos[index],
                          ),
                        ),
                        IconButton(
                          icon: Icon(Icons.delete),
                          onPressed: () => _deleteTodoItem(index),
                        ),
                      ],
                    ),
                  ),
                );
              },
            ),
      floatingActionButton: FloatingActionButton(
        onPressed: () => _displayTextInputDialog(context),
        child: Icon(Icons.add),
      ),
    );
  }
}
```

### Penjelasan Kode:

-   **`_TodoListScreenState`:** Ini adalah `State` dari `TodoListScreen` yang menampung `_todos` (daftar item) dan `_textFieldController`.
-   **`_todos`:** Sebuah `List<String>` yang berfungsi sebagai koleksi data kita. Setiap perubahan pada list ini akan memicu `setState()`.
-   **`_addTodoItem`, `_editTodoItem`, `_deleteTodoItem`:** Fungsi-fungsi ini memodifikasi `_todos` dan kemudian memanggil `setState()` untuk memberitahu Flutter agar membangun ulang UI.
-   **`_displayTextInputDialog`:** Fungsi ini menampilkan `AlertDialog` yang berisi `TextField` untuk input. Ini digunakan baik untuk menambahkan item baru maupun mengedit item yang sudah ada.
-   **`ListView.builder`:** Digunakan untuk menampilkan daftar item secara efisien. Setiap `ListTile` menampilkan satu item to-do.
-   **`IconButton` (Edit & Delete):** Tombol-tombol ini memicu fungsi `_editTodoItem` dan `_deleteTodoItem` masing-masing.
-   **`FloatingActionButton`:** Tombol ini memicu dialog untuk menambahkan item baru.

Dengan studi kasus ini, Anda telah berhasil mengimplementasikan operasi CRUD dasar pada koleksi data in-memory menggunakan `setState()` untuk state management. Ini adalah fondasi yang kuat untuk membangun aplikasi yang lebih kompleks dengan data dinamis.
