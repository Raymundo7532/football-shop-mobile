Nama: Raymundo Rafaelito Maryos Von Woloblo
Kelas: PBP B

# Tugas 8
##### 1. Perbedaan `Navigator.push()` dan `Navigator.pushReplacement()` serta kasus terbaik untuk digunakan pada apliksi ini

Untuk setiap tumpukan (stack) route,
- `Navigator.push()` menambahkan route baru pada bagian atas stack. Kasus terbaiknya adalah ketika pengguna ingin pergi ke route yang lain, tetapi tetap ingin menyimpan route sebelumnya, sedangkan
- `Navigator.pushReplacement()` mengganti route paling atas pada stack dengan route yang diinginkan. Kasus terbaiknya adalah ketika pengguna ingin pergi ke route baru tanpa menyimpan route sebelumnya

##### 2. Cara memanfaatkan hierarchy widget seperti Scaffold, AppBar, dan Drawer untuk membangun struktur halaman yang konsisten di seluruh aplikasi

Widget seperti Scaffold, AppBar, dan Drawer berperan penting dalam membangun struktur halaman yang konsisten di seluruh aplikasi Flutter. 
Biasanya, ketiganya digunakan dalam satu hierarki seperti ini:

``` dart
Scaffold(
  appBar: AppBar(title: Text("Football Shop")),
  drawer: Drawer(...),
  body: ...,
)
```

Penjelasan perannya:
- 🧱 Scaffold: jadi “kerangka utama” halaman yang menyediakan area untuk AppBar, Drawer, FloatingActionButton, dan body.
- 📑 AppBar: menampilkan judul halaman, ikon navigasi, atau tombol aksi yang seragam di setiap halaman.
- 📂 Drawer: berfungsi sebagai menu navigasi samping (sidebar) agar user bisa berpindah antar-halaman dengan mudah.

> Keuntungannya:
> Dengan memanfaatkan struktur ini, setiap halaman punya tampilan dan navigasi yang konsisten, sehingga pengalaman pengguna terasa lebih stabil dan profesional.

##### 3. Kelebihan menggunakan layout widget seperti `Padding`, `SingleChildScrollView`, dan `ListView` saat menampilkan elemen-elemen form (dala, konteks desain antarmuka pegguna) beserta contoh penggunaannya dari aplikasi ini

Dalam desain antarmuka, widget seperti Padding, SingleChildScrollView, dan ListView sangat membantu menjaga kenyamanan tampilan dan interaksi form.

| Widget                  | Fungsi                                               | Kelebihan                                                                               |
| ----------------------- | ---------------------------------------------------- | --------------------------------------------------------------------------------------- |
| `Padding`               | Memberikan jarak di sekitar elemen form.             | Membuat tampilan lebih rapi, tidak menempel di tepi layar.                              |
| `SingleChildScrollView` | Membuat halaman bisa di-scroll jika isinya panjang.  | Mencegah overflow saat keyboard muncul atau layar kecil.                                |
| `ListView`              | Menampilkan elemen dalam daftar yang bisa di-scroll. | Cocok untuk form dengan banyak input, karena efisien dalam manajemen layout dan scroll. |

> Kesimpulan:
> Kombinasi widget ini bikin layout form jadi lebih responsif, rapi, dan mudah diakses di berbagai ukuran layar.

Sampai saat tulisan ini dibuat:
- `Padding` digunakan pada semua file .dart, kecuali main.dart,
- `SingleChildScrollView` digunakan pada productlist_form.dart, dan
- `ListView` digunakan pada left_drawer.dart

##### 4. Cara menyesuaikan warna tema agar aplikasi Football Shop memiliki identitas visual yang konsisten dengan brand toko

Dengan cara menentukan primary dan secondary color pada ColorScheme pada root widget di main.dart

# Tugas 7
##### 1. Widget Tree dan Hubungan Parent-Child

Widget tree adalah struktur hierarki dari semua widget yang membentuk tampilan aplikasi Flutter. Setiap widget bisa memiliki widget lain di dalamnya (child), sedangkan widget pembungkusnya disebut parent. Parent mengatur tata letak dan perilaku anaknya. Contoh: `Scaffold` (parent) → `Column` (child) → `Text` (grandchild).

##### 2. Daftar Widget yang Digunakan dan Fungsinya

| Widget           | Fungsi                                                          |
| :--------------- | :-------------------------------------------------------------- |
| `MaterialApp`    | Root aplikasi; mengatur tema, title, dan halaman awal (`home`). |
| `ThemeData`      | Menentukan tema warna dan gaya global aplikasi.                 |
| `Scaffold`       | Struktur dasar halaman (memiliki `AppBar`, `body`, dll).        |
| `AppBar`         | Bagian atas halaman yang menampilkan judul aplikasi.            |
| `Text`           | Menampilkan teks seperti nama, NPM, kelas, dan sambutan.        |
| `Padding`        | Memberikan jarak di sekitar widget.                             |
| `Column`         | Menyusun widget secara vertikal.                                |
| `Row`            | Menyusun widget secara horizontal.                              |
| `SizedBox`       | Menambahkan jarak antar elemen.                                 |
| `Center`         | Menempatkan child di tengah.                                    |
| `GridView.count` | Menampilkan grid item dalam jumlah kolom tertentu.              |
| `Card`           | Membuat tampilan kotak dengan bayangan.                         |
| `Material`       | Memberi efek visual Material Design.                            |
| `InkWell`        | Menangani interaksi sentuhan (tap).                             |
| `Icon`           | Menampilkan ikon pada item.                                     |
| `SnackBar`       | Menampilkan pesan singkat di bawah layar.                       |
| `Container`      | Widget serbaguna untuk layout dan styling.                      |
| `MediaQuery`     | Mendapatkan ukuran layar agar tampilan responsif.               |

##### 3. Fungsi Widget `MaterialApp`

`MaterialApp` adalah widget utama yang membungkus seluruh aplikasi dan menyediakan konfigurasi global seperti tema, title, dan halaman awal. Widget ini menjadi root karena menyediakan context dan resource Material Design yang dibutuhkan widget lain seperti `Scaffold`, `AppBar`, dan `SnackBar`.

##### 4. Perbedaan `StatelessWidget` dan `StatefulWidget`

- `StatelessWidget`: Tidak memiliki state; tampilannya tidak berubah selama aplikasi berjalan. Contoh: InfoCard, ItemCard.
- `StatefulWidget`: Memiliki state yang dapat berubah saat user berinteraksi atau data diperbarui.

Pemilihan:
Gunakan `StatelessWidget` untuk tampilan statis, dan `StatefulWidget` untuk tampilan yang berubah-ubah.

##### 5. Pengertian dan Fungsi `BuildContext`

`BuildContext` adalah objek yang merepresentasikan posisi suatu widget dalam widget tree. Digunakan untuk mengakses data atau widget lain yang berada di atasnya, seperti:
```dart
Theme.of(context)
ScaffoldMessenger.of(context)
```
Dalam metode `build`, `BuildContext` penting untuk mengambil tema, ukuran layar, dan navigasi antar halaman.

##### 6. Konsep `Hot Reload` dan `Hot Restart`

- `Hot Reload`: Memperbarui kode tanpa mengulang seluruh aplikasi. State tidak hilang, cocok untuk menguji perubahan UI cepat.
- `Hot Restart`: Memulai ulang aplikasi dari awal. State di-reset ke kondisi awal.

Perbedaan utama:
`Hot Reload` = update tampilan tanpa kehilangan state.
`Hot Restart` = menjalankan ulang aplikasi dari nol.