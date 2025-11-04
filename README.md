Nama: Raymundo Rafaelito Maryos Von Woloblo
Kelas: PBP B

## Tugas 7
1. Widget Tree dan Hubungan Parent-Child

Widget tree adalah struktur hierarki dari semua widget yang membentuk tampilan aplikasi Flutter. Setiap widget bisa memiliki widget lain di dalamnya (child), sedangkan widget pembungkusnya disebut parent. Parent mengatur tata letak dan perilaku anaknya. Contoh: `Scaffold` (parent) → `Column` (child) → `Text` (grandchild).

2. Daftar Widget yang Digunakan dan Fungsinya

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

3. Fungsi Widget `MaterialApp`

`MaterialApp` adalah widget utama yang membungkus seluruh aplikasi dan menyediakan konfigurasi global seperti tema, title, dan halaman awal. Widget ini menjadi root karena menyediakan context dan resource Material Design yang dibutuhkan widget lain seperti `Scaffold`, `AppBar`, dan `SnackBar`.

4. Perbedaan `StatelessWidget` dan `StatefulWidget`

- `StatelessWidget`: Tidak memiliki state; tampilannya tidak berubah selama aplikasi berjalan. Contoh: InfoCard, ItemCard.
- `StatefulWidget`: Memiliki state yang dapat berubah saat user berinteraksi atau data diperbarui.
Pemilihan:
Gunakan `StatelessWidget` untuk tampilan statis, dan `StatefulWidget` untuk tampilan yang berubah-ubah.

5. Pengertian dan Fungsi `BuildContext`

`BuildContext` adalah objek yang merepresentasikan posisi suatu widget dalam widget tree. Digunakan untuk mengakses data atau widget lain yang berada di atasnya, seperti:
```sh
Theme.of(context)
ScaffoldMessenger.of(context)
```
Dalam metode `build`, `BuildContext` penting untuk mengambil tema, ukuran layar, dan navigasi antar halaman.

6. Konsep `Hot Reload` dan `Hot Restart`

- `Hot Reload`: Memperbarui kode tanpa mengulang seluruh aplikasi. State tidak hilang, cocok untuk menguji perubahan UI cepat.
- `Hot Restart`: Memulai ulang aplikasi dari awal. State di-reset ke kondisi awal.
Perbedaan utama:
`Hot Reload` = update tampilan tanpa kehilangan state.
`Hot Restart` = menjalankan ulang aplikasi dari nol.