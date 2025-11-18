Nama: Raymundo Rafaelito Maryos Von Woloblo
Kelas: PBP B

# Tugas 9
##### 1. Alasan Perlunya Membuat Model Dart Saat Mengambil/Mengirim Data JSON

Membuat model Dart itu penting karena data dari backend selalu datang dalam bentuk JSON yang strukturnya bisa berubah-ubah. Dengan model, kita bisa memastikan setiap field punya tipe data yang jelas dan aman secara null-safety. Kalau kita langsung pakai Map<String, dynamic>, kita bakal repot validasi sendiri, rawan salah akses key, dan susah ngelacak error kalau backend berubah sedikit saja. Model juga bikin kode lebih rapi dan maintainable karena semua aturan struktur data terpusat di satu tempat. Akhirnya, development jangka panjang jadi lebih stabil dan mudah di-debug.

Tanpa model, aplikasi bisa gampang crash kalau tipe datanya tidak sesuai ekspektasi atau ada nilai null yang tidak ditangani. Selain itu, kode yang pakai map mentah cenderung berantakan dan sulit dikembangkan karena tidak ada jaminan tipe data sama di seluruh aplikasi. Intinya: model bukan cuma soal “nyaman,” tapi soal menjaga keamanan data, konsistensi, dan maintainability aplikasi.

##### 2. Fungsi Package http dan CookieRequest serta Perbedaan Perannya

Dalam tugas ini, package http dipakai untuk melakukan request standar seperti GET atau POST tanpa perlu mengurus sesi atau cookie. Ini cocok dipakai untuk endpoint publik atau request yang tidak butuh autentikasi. Sementara CookieRequest dipakai untuk semua request yang perlu session login Django, karena dia otomatis menyimpan dan mengirim cookie supaya backend mengenali user yang sedang login.

Singkatnya, http adalah alat request umum, sedangkan CookieRequest adalah alat request “berbasis sesi” yang nge-handle autentikasi. Jadi kalau butuh akses data user yang login, atau perlu menjaga session tetap aktif, maka CookieRequest adalah pilihan yang tepat.

##### 3. Alasan Instance CookieRequest Perlu Dibagikan ke Semua Komponen

Karena autentikasi di Django menggunakan sesi (session cookie), instance CookieRequest harus dibagikan ke seluruh komponen Flutter supaya setiap request yang butuh login bisa tetap mengirim cookie yang sama. Kalau setiap halaman membuat instance baru, cookie tidak akan terbawa, dan backend bakal menganggap user belum login. Akibatnya, fitur seperti mengambil data milik user atau membuat produk baru tidak akan bekerja.

Dengan membagikan satu instance ke seluruh widget tree (biasanya lewat Provider), aplikasi punya satu sumber kebenaran untuk status login, cookie, dan informasi user. Ini bikin state autentikasi lebih konsisten, tidak mudah hilang, dan lebih mudah dikelola di seluruh bagian aplikasi.

##### 4. Konfigurasi Konektivitas Flutter ↔ Django dan Konsekuensi Jika Salah Konfigurasi

Agar Flutter bisa berkomunikasi dengan Django, ada beberapa konfigurasi penting yang harus dibereskan. Penambahan 10.0.2.2 pada ALLOWED_HOSTS memungkinkan emulator Android mengakses server Django yang berjalan di localhost. CORS perlu diaktifkan supaya Flutter diizinkan untuk melakukan request lintas domain. Selain itu, konfigurasi cookie seperti SameSite dan Secure harus disesuaikan agar session cookie bisa dikirim dan diterima dengan benar oleh Flutter.

Jika izin akses internet di Android tidak ditambahkan, aplikasi tidak akan bisa melakukan request sama sekali. Jika ALLOWED_HOSTS salah, request akan ditolak dengan error 400. Jika CORS atau cookie tidak dikonfigurasi, autentikasi gagal karena cookie tidak pernah sampai ke Django atau tidak diterima kembali oleh Flutter. Intinya: salah satu konfigurasi saja rusak, komunikasi Flutter↔Django bisa langsung gagal total.

##### 5. Mekanisme Pengiriman Data dari Input Hingga Ditampilkan di Flutter

Prosesnya dimulai ketika user mengisi form di Flutter dan data tersebut dikumpulkan dari input widget. Data yang sudah dirangkum kemudian dikirim ke backend Django melalui POST request (pakai http atau CookieRequest tergantung kebutuhan). Django lalu memproses data tersebut, menyimpannya ke database, dan mengembalikan respons JSON berisi hasil atau statusnya.

Setelah JSON diterima Flutter, data tersebut di-decode lalu dipetakan ke model Dart. Model inilah yang kemudian digunakan untuk menampilkan data di UI, misalnya ditaruh dalam ListView atau Card. Alur ini bikin data terasa “mengalir” secara natural dari input user → server → database → balik lagi ke UI.

##### 6. Mekanisme Autentikasi Login, Register, dan Logout

Untuk login dan register, Flutter mengirim data akun (username, password, dll.) ke Django lewat CookieRequest. Django akan memvalidasi data tersebut menggunakan mekanisme autentikasi bawaannya. Jika login berhasil, Django mengembalikan session cookie, yang langsung disimpan oleh CookieRequest. Cookie ini akan dikirim pada setiap request berikutnya supaya backend tahu siapa user yang sedang aktif.

Setelah sukses login atau register, Flutter biasanya akan menampilkan halaman menu utama karena status login sudah disimpan di instance CookieRequest. Untuk logout, Flutter memanggil endpoint Django yang menghapus session di server, lalu CookieRequest juga menghapus cookie lokal. Hasilnya, user otomatis dianggap keluar dan kembali ke halaman login. Mekanisme ini memastikan seluruh interaksi yang butuh autentikasi berjalan aman dan konsisten.

##### 7. Cara ku mengimplementasikan checklist di tugas 9 secara step-by-step:
- Memastikan deployment proyek tugas Django ku telah berjalan dengan baik.
- Mengimplementasikan fitur registrasi akun pada proyek tugas Flutter.
- Membuat halaman login pada proyek tugas Flutter.
- Mengintegrasikan sistem autentikasi Django dengan proyek tugas Flutter.
- Membuat model kustom sesuai dengan proyek aplikasi Django.
- Membuat halaman yang berisi daftar semua item yang terdapat pada endpoint JSON di Django yang telah ku deploy.
  - Tampilkan name, price, description, thumbnail, category, dan is_featured dari masing-masing item pada halaman ini (Dapat disesuaikan dengan field yang kalian buat sebelumnya).
- Membuat halaman detail untuk setiap item yang terdapat pada halaman daftar Item.
  - Halaman ini dapat diakses dengan menekan salah satu card item pada halaman daftar Item.
  - Tampilkan seluruh atribut pada model item ku pada halaman ini.
  - Tambahkan tombol untuk kembali ke halaman daftar item.
- Melakukan filter pada halaman daftar item dengan hanya menampilkan item yang terasosiasi dengan pengguna yang login.

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