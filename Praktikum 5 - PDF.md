# PHP dan AJAX

# 1. Tujuan Praktikum
Setelah mengikuti praktikum ini mahasiswa diharapkan dapat memahami cara untuk:

1. Membuat objek file XMLHttpRequest sebagai core Ajax
2. Melakukan request ke server melalui AJAX menggunakan method GET
3. Melakukan request ke server melalui AJAX menggunakan method POST

# 2. Tools

Tools yang dibutuhkan untuk melakukan praktikum ini adalah Apache web server, PHP interpreter, DBMS MySQL dan text editor.

# 3. Langkah-Langkah Praktikum
## 3.1. Membuat objek XMLHttpRequest
Fungsi berikut digunakan untuk membuat objek XMLHttpRequest sebagai core Ajax. Buatlah fungsi tersebut dalam sebuah file dan simpan dengan nama ajax.js.

`ajax.js`
## 3.2. Contoh AJAX sederhana
Berikut ini merupakan contoh sederhana penggunaan Ajax untuk melakukan request ke server untuk
menampilkan waktu server.
1. File `show_server_time.php` berisi tombol 'Show Server Time'. Jika tombol tersebut diklik, maka akan memanggil fungsi javascript `get_server_time()` yang melakukan request ke file `get_server_time.php` melalui Ajax dan menampilkan responnya di elemen dengan `id="show_time"`.

Tampilan dari file `show_server_time.php` adalah sebagai berikut:

2. Isi dari fungsi javascript `get_server_time()`. Tambahkan fungsi javascript tersebut pada file `ajax.js`

lalu, include file `ajax.js` pada file `show_server_time.php`. Lokasi file `get_server_time.php` yang di-request relatif terhadap file `show_server_time.php`.

`ajax.js`

3. Isi dari file `get_server_time.php` yang di-request adalah sebagai berikut:

`get_server_time.php`

4. Panggil file `show_server_time.php` di browser,lalu klik tombol "Show Server Time", perhatikan bahwa waktu server akan ditampilkan pada halaman tersebut tanpa melakukan load keseluruhan isi halaman.

## 3.3. Contoh AJAX dengan method GET
Berikut ini adalah contoh request ke server melalui Ajax menggunakan method GET untuk menyimpan data ke basis data.

1. File add_customer.php berisi form data customer yang terdiri atas name, address, dan city. Tombol submit diganti dengan `<button type="button" ...>` yang jika diklik akan memanggil fungsi javascript `add_customer_get()`. Fungsi tersebut selanjutnya me-request file `add_customer_get.php` melalui Ajax dengan method GET dan menampilkan responnya pada elemen dengan `id="add_response"`.

`add_customer.php`

Tampilan dari file `add_customer.php` adalah sebagai berikut:


2. Isi dari fungsi javascript `add_customer_get()` adalah sebagai berikut. Tambahkan fungsi javascript tersebut pada file `ajax.js` lalu, include file `ajax.js` pada file `add_customer.php`. Lokasi file `add_customer_post.php` yang di-request relatif terhadap file `add_customer.php`. Perhatikan bahwa saat menggunakan method GET, data yang dikirimkan (isi form add customer) dilewatkan melalui URL.

`ajax.js`

3. Isi dari file `add_customer_get.php` yang di-request adalah sebagai berikut. File tersebut menyimpan masukan isi form ke basis data, lalu menampilkan respon berupa konfirmasi berdasarkan hasil eksekusi query. Saat menggunakan method GET, data yang dikirimkan diakses melalui array superglobal `$_GET[]`.

`add_customer_get.php`

4. Panggil file `add_customer.php` di browser,lalu isi form dan klik tombol **Add**, perhatikan bahwa isi form akan disimpan ke basis data dan konfirmasi akan ditampilkan pada halaman tersebut tanpa melakukan load keseluruhan isi halaman.Tampilan file `add_customer.php` setelah pengisian form adalah sebagai berikut:

## 3.4. Contoh AJAX dengan method POST

Berikut ini adalah contoh request ke server melalui Ajax menggunakan method POST untuk menyimpan data ke basis data.

1. Ubah isi pada file `add_customer.php`, yaitu pada `<button type="button" ...>` jika diklik akan memanggil fungsi javascript `add_customer_post()`. Fungsi tersebut selanjutnya me-request file `add_customer_post.php` melalui Ajax dengan method POST dan menampilkan responnya pada elemen dengan `id="add_response"`.

`add_customer.php`

2. Isi dari fungsi javascript `add_customer_post()` adalah sebagai berikut. Tambahkan fungsi javascript tersebut pada file `ajax.js` lalu, include file `ajax.js` pada file `add_customer.php`. Lokasi file `add_customer_post.php` yang di-request relatif terhadap file `add_customer.php`. Perhatikan bahwa saat menggunakan method POST, URL tidak ditambahkan paremeter, tetapi data yang dikirimkan (isi form add customer) dilewatkan sebagai parameter pada header HTTP.

3. Isi dari file `add_customer_post.php` yang di-request adalah sebagai berikut. File tersebut menyimpan masukan isi form ke basis data, lalu menampilkan respon berupa konfirmasi berdasarkan hasil eksekusi query. Saat menggunakan method POST, data yang dikirimkan diakses melalui array superglobal `$_POST[]`.

`add_customer_post.php`

4. Panggil file `add_customer.php` di browser,lalu isi form dan klik tombol **Add**, perhatikan bahwa isi form akan disimpan ke basis data dan konfirmasi akan ditampilkan pada halaman tersebut tanpa melakukan load keseluruhan isi halaman.

## 3.5. Contoh AJAX untuk menampilkan data dari basis data

Berikut ini adalah contoh request ke server melalui Ajax menggunakan method GET untuk menampilkan detail data customer berdasarkan nama yang diplih oleh pengguna.

1. File `show_customer.php` menampilkan dropdown list berisi nama customer yang diambil dari tabel customer. Jika pengguna mengubah pilihan pada dropdown list tersebut, maka akan dipanggil fungsi javascript `showCustomer(this.value)`. Value (berupa customerid) yang dipilih dilewatkan sebagai parameter fungsi. Fungsi tersebut selanjutnya me-request file `get_customer.php` melalui Ajax dengan method GET dan menampilkan responnya pada elemen dengan `id="detail_customer"`.

`show_customer.php`

Tampilan dari file `show_customer.php` adalah sebagai berikut:

2. Isi dari fungsi javascript `showCustomer()` adalah sebagai berikut. Lokasi file `get_customer.php` yang di-request relatif terhadap file `show_customer.php`. Perhatikan bahwa saat menggunakan method GET, data yang dikirimkan (customerid) dilewatkan melalui URL. Fungsi `showCustomer()` memanggil fungsi `callAjax()` untuk melakukan request ke server melalui Ajax. Tambahkan kedua fungsi javascript tersebut pada file ajax.js lalu, include file ajax.js pada file `show_customer.php`.

`ajax.js`

3. Isi dari file get_customer.php yang di-request adalah sebagai berikut. File tersebut mengambil data customer dari basis data berdasarkan customerid yang dipilih, lalu menampilkan respon detail customer berdasarkan hasil eksekusi query. Saat menggunakan method GET, data yang dikirimkan diakses melalui array superglobal `$_GET[]`.

`get_customer.php`

4. Panggil file `show_customer.php` di browser, lalu pilih salah satu nama customer dari dropdown list, perhatikan bahwa detail customer akan ditampilkan pada halaman tersebut tanpa
melakukan load keseluruhan isi halaman.Tampilan file `show_customer.php` setelah dipilih salah satu nama customer adalah sebagai berikut:

# 4. Tugas

1. Selesaikanlah contoh penggunaan Ajax pada sub bab praktikum 3.2 – 3.5.
2. Buatlah file untuk pencarian data buku berdasarkan judul yang diketik, lalu menampilkan detail
buku pada halaman yang sama menggunakan Ajax.


# TODO
- [x] Content
- [ ] Second pass
- [ ] Proof read
- [ ] Appendix