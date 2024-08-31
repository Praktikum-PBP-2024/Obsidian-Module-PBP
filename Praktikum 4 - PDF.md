# KONEKSI PHP DAN MYSQL

1. Tujuan Praktikum
Setelah mengikuti praktikum ini mahasiswa diharapkan dapat memahami cara untuk:
a. Melakukan koneksi ke basis data MySQL dan menampilkan hasil query select ke halaman web.
b. Membuat halaman untuk CRUD (create, read, update, delete) data dari/ ke basis data.
c. Membuat file untuk login dan logout serta menambahkan penanganan pada file yang hanya
dapat dibuka setelah login terlebih dahulu.
d. Menerapkan penggunaan client-state management (session) untuk membuat shopping cart.
2. Tools
Tools yang dibutuhkan adalah Apache web server, PHP, MySQL dan HTML/ PHP editor.
3. Langkah-Langkah Praktikum
Secara umum langkah-langkah untuk melakukan query ke database adalah:
1. Membuka koneksi ke basis data dan memilih database yang akan digunakan
3. Menyusun query
4. Mengeksekusi query
5. Menampilkan hasilnya
6. Menutup koneksi
Untuk melakukan koneksi ke MySQL dapat digunakan library mysqli. Library mysqli dapat digunakan
dengan pendekatan prosedural maupun pendekatan beorientasi objek. Contoh fungsi-fungsi dalam
library mysqli dapat dilihat pada Tabel 3.1.

Tabel 3.1 Fungsi-fungsi untuk melakukan query ke database dengan mysqli

Basis data yang digunakan yang digunakan adalah bookorama dengan struktur seperti berikut:

Sebelumnya buatlah file db_login.php yang digunakan untuk menyimpan data konfigurasi untuk
koneksi ke basis data.Pada file tersebut dapat pula dibuatkan langsung objek untuk koneksi dan
fungsi test_input() yang nantinya diperlukan untuk validasi masukan. File ini di-require pada file-file
lain yang membutuhkan koneksi ke basis data.

db_login.php.

3.1. Praktikum 1 : Membuat Halaman untuk Menampilkan Data Customer
Ikuti langkah-langkah berikut untuk membuat halaman yang menampilkan data customer:
1. Berikut ini adalah contoh file yang digunakan untuk menampilkan data customer.
Keterangan:
Link edit dan delete dibuat untuk setiap baris data, link tersebut menuju ke halaman untuk
mengubah (edit_customer.php) dan menghapus (confirm_delete_customer.php) data customer,
dengan melewatkan customerid (id=$row->customerid) melalui alamat url. customerid yang
dilewatkan selanjutnya dapat diakses oleh halaman yang dituju melalui $_GET[‘id’].

Tampilan dari file view_customer.php adalah sebagai berikut:

2. Ubahlah string query pada file view_customer.php menjadi:

4. Simpan dengan nama baru view_customer2.php.
5. Jalankan file view_customer2.php, apakah isi tabel customer dapat ditampilkan?
6. Ubahlah baris kode yang digunakan untuk menampilkan hasil eksekusi query seperti berikut:

6. Simpan dan jalankan kembali file view_customer2.php, apakah isi tabel customer dapat
ditampilkan dengan benar?
3.2. Praktikum 2 : Membuat Halaman Edit Customer
Halaman edit_customer.php menampilkan form untuk edit data customer dan form akan diproses
oleh file itu sendiri. Alur dari halaman edit ini adalah sebagai berikut:
1. Mengecek apakah user sudah melakukan submit form, jika belum maka akan ditampilkan form
untuk edit yang sudah terisi dengan data customer dengan customerid tertentu yang diambil dari
basis data.
1. Jika user sudah melakukan submit, maka dilakukan validasi isi form.
a. Jika validasi berhasil, user akan di-redirect ke halaman view_customer.php.
a. Jika validasi gagal, akan ditampilkan kembali halaman edit_customer.php dengan form yang
telah terisi sesuai nilai yang dimasukkan user sebelumnya beserta pesan kesalahan validasi.

Buatlah file dit_customer.php seperti berikut:

Selanjutnya, lakukan langkah-langkah sebagai berikut:
1. Panggil file edit_customer.php dan periksalah apakah validasi sudah dilakukan dengan benar dan
perubahan data dapat disimpan di basis data.
2. Panggil kembali file edit_customer.php, lalu pada alamat isikan: Queen’s Street. Selanjutnya,
submit dan periksalah apakah terdapat kesalahan dalam query?
3. Tambahkan baris kode berikut sebelum perintah query lalu simpan kembali.
4. Ulangi kembali langkah nomor 2, apakah update data berhasil dijalankan? Berikan penjelasan.
Tampilan dari file dit_customer.php untuk data customer tertentu adalah sebagai berikut:


1.2. Praktikum 3 : Membuat Halaman Login
Halaman login.php menampilkan form untuk login sebagai admin dan form akan diproses oleh file itu
sendiri. Alur dari halaman login ini adalah sebagai berikut:
1. Mengecek apakah user sudah melakukan submit form, jika sudah maka isi form akan divalidasi.
a. Jika validasi berhasil, akan dicek apakah email dan password yang dimasukkan cocok dengan
kombinasi email dan password yang ada di tabel admin.
- Jika cocok, maka akan dibuat S_SESSION[‘username’] dan user akan di-redirect ke
halaman admin.php.
- Jika tidak cocok, maka user akan ditampilkan pesan kesalahan bahwa email dan
password yang dimasukkan salah.

a. Jika validasi gagal, akan ditampilkan kembali halaman login.php dengan form yang telah terisi
sesuai nilai yang dimasukkan user sebelumnya beserta pesan kesalahan validasi.
1. Jika user belum melakukan submit, maka ditampilkan form login yang masih kosong.
Buatlah file login.php seperti berikut:


Buatlah file admin.php seperti berikut:

Buatlah file logout.php seperti berikut:


Jalankan file-file tersebut dengan cara sebagai berikut:
1. Panggil file admin.php, tanpa melakukan login terlebih dahulu. Cek apakah file dapat tersebut
dapat ditampilkan? Berikan penjelasan.
1. Panggil file login.php, isikan data yang salah, periksalah apakah validasi sudah dapat dijalankan
dengan benar.
1. Panggil file login.php, isikan kombinasi email dan password admin yang salah, periksalah apakah
validasi sudah dijalankan dengan benar.

1. Panggil file login.php, isikan kombinasi email dan password admin yang benar, periksalah apakah
halaman admin.php dapat ditampilkan.
1. Klik logout pada file admin.php, lalu panggil kembali file admin.php, setelah logout apakah file
admin.php dapat ditampilkan? Berikan penjelasan.
1.2. Praktikum 4 : Membuat Shopping Cart dengan Session
Pada bagian ini kita akan mencoba menggunakan session untuk menyimpan item-item yang dipilih
oleh customer ke dalam shopping cart.
1. Buatlah file view_books.php untuk menampilkan daftar buku beserta link untuk
menambahkannya ke shopping cart seperti tampilan berikut:

Link Add to Cart ditambahkan pada setiap record data buku, link tersebut menuju ke halaman
show_cart.php dengan melewatkan parameter id yang diisi dengan isbn buku tersebut, seperti
berikut:

2. Buatlah halaman show_cart.php menambahkan item ke shopping cart dan menampilkan isi
shopping cart.
● Shopping cart disimpan dalam variabel $\_SESSION['cart'] berupa array asosiatif dengan indeks
berupa id atau isbn buku dan value berupa quantity (qty) buku dengan isbn tersebut, contoh:
$\_SESSION['cart'][ '0-672-31697-8'] = 2
$\_SESSION['cart'][ '0-672-31509-2'] = 1
● Jika halaman show_cart.php dipanggil tanpa parameter di URL maka akan ditampilkan isi yang
ada di dalam session $\_SESSION['cart'].
● Jika halaman show_cart.php dipanggil dengan parameter di URL berupa id yang isinya isbn dari
sebuah buku maka akan ditambahkan ke $\_SESSION['cart'], misalnya
show_cart.php?id=0-672-31697-8.

Tampilan dari halaman show_cart.php adalah seperti berikut:

Link Continue Shopping menuju ke halaman view_books.php, sedangkan link Empty Cart menuju
ke halaman delete_cart.php.
3. Buatlah file delete_cart.php untuk mengosongkan isi $\_SESSION['cart'] lalu redirect ke halaman
view_books.php.

2. Tugas
1. Buatlah file untuk CRUD data berikut:
- view_customer.php, untuk menampilkan data pelanggan
- edit_customer.php, untuk edit data pelanggan
- add_customer.php, untuk menambah data customer baru
- delete_customer.php, untuk menghapus data customer tertentu.


2. Buatlah file untuk login seperti berikut:
- login.php seperti pada contoh di modul ini, jika berhasil redirect ke halaman view_customer.php.
- Tambahkan penanganan pada file view_customer.php sehingga file tersebut hanya dibuka oleh admin setelah berhasil login.
- Tambahkan link logout pada file view_customer.php untuk melakukan logout, lalu buatlah file logout.php seperti pada contoh di modul.
3. Buatlah file-file berikut untuk memproses shopping cart seperti yang dicontohkan di modul:
- view_books.php
- show_cart.php
- delete_cart.php
# TODO
- [ ] Content
- [ ] Second pass
- [ ] Proof read
- [ ] Appendix