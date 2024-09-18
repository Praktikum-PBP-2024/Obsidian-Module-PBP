# KONEKSI PHP DAN MYSQL

# 1. Tujuan Praktikum

Setelah mengikuti praktikum ini mahasiswa diharapkan dapat memahami cara untuk:

1. Melakukan koneksi ke basis data MySQL dan menampilkan hasil query select ke halaman web.
2. Membuat halaman untuk CRUD (create, read, update, delete) data dari/ ke basis data.
3. Membuat file untuk login dan logout serta menambahkan penanganan pada file yang hanya dapat dibuka setelah login terlebih dahulu.
4. Menerapkan penggunaan client-state management (session) untuk membuat shopping cart.

# 2. Tools

Tools yang dibutuhkan adalah Apache web server, PHP, MySQL dan HTML/ PHP editor.

# 3. Langkah-Langkah Praktikum

Secara umum langkah-langkah untuk melakukan query ke database adalah:
1. Membuka koneksi ke basis data dan memilih database yang akan digunakan
3. Menyusun query
4. Mengeksekusi query
5. Menampilkan hasilnya
6. Menutup koneksi

Untuk melakukan koneksi ke MySQL dapat digunakan library mysqli. Library mysqli dapat digunakan dengan pendekatan prosedural maupun pendekatan beorientasi objek. Contoh fungsi-fungsi dalam library mysqli dapat dilihat pada tabel berikut

| Pendekatan Prosedural                                                                                                                                                                        | Pendekatan OO                                                                                                                                                                        | Keterangan                                                                                                                 |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | -------------------------------------------------------------------------------------------------------------------------- |
| `$con = mysqli_connect($db_host, $db_username, $db_password);`<br><br>Untuk pemilihan database sekaligus<br><br>`$con = mysqli_connect($db_host, $db_username, $db_password, $db_database);` | `$con = new mysqli($db_host, $db_username, $db_password);`<br><br>Untuk pemilihan database sekaligus<br><br>`$con = new mysqli($db_host, $db_username, $db_password, $db_database);` | Membangun koneksi ke database                                                                                              |
| `mysqli_select_db($con, $db_database);`                                                                                                                                                      | `$con->select_db($db_database);`                                                                                                                                                     | Memilih database yang akan digunakan                                                                                       |
| `mysqli_connect_errno();`                                                                                                                                                                    | `$con->connect_errno`                                                                                                                                                                | Mendapatkan status code connection. 0 jika no problem, selain itu ada kegagalan dalam koneksi.                             |
| `mysqli_connect_error();`                                                                                                                                                                    | `$con->connect_error`                                                                                                                                                                | Mengambil pesan error dari koneksi yang gagal                                                                              |
| `mysqli_error();`                                                                                                                                                                            | `$con->error`                                                                                                                                                                        | Mengembalikan pesan error saat melakukan query                                                                             |
| `$result = mysqli_query($con, $query);`                                                                                                                                                      | `$result  = $con->query($query);`                                                                                                                                                    | Mengeksekusi query `$query` dan menyimpan hasil di `$result`. `$result` di iterasi menggunakan fungsi `mysqli_fetch_array` |
| `$row = mysqli_fetch_array($result);`                                                                                                                                                        | `$row = $result->fetch_object();`                                                                                                                                                    | Mengambil setiap baris pada `$result`                                                                                      |
| `mysqli_num_rows($result));`                                                                                                                                                                 | `$result->num_rows;`                                                                                                                                                                 | Mengembalikan jumlah baris hasil query / row count                                                                         |
| `mysqli_close($con);`                                                                                                                                                                        | `$con->close()`                                                                                                                                                                      | Menutup koneksi database                                                                                                   |


Basis data yang digunakan yang digunakan adalah bookorama dengan struktur seperti berikut:

![[Pasted image 20240918064703.png]]

Sebelumnya buatlah file `db_login.php` yang digunakan untuk menyimpan data konfigurasi untuk koneksi ke basis data.Pada file tersebut dapat pula dibuatkan langsung objek untuk koneksi dan fungsi `test_input()` yang nantinya diperlukan untuk validasi masukan. File ini di-require pada file-file lain yang membutuhkan koneksi ke basis data.

`db_login.php`.
```php
<?php 
// TODO 1: Buatlah koneksi dengan database
$db_host = '';
$db_database = '';
$db_username = '';
$db_password = '';

$db = new mysqli($db_host, $db_username, $db_password, $db_database);
if ($db->connect_errno) {
    die("Could not connect to the database: <br />" . $db->connect_error);
}

function test_input($data) {
    $data = trim($data);
    $data = stripslashes($data);
    $data = htmlspecialchars($data);
    return $data;
}

```

## 3.1. Membuat Halaman untuk Menampilkan Data Customer

Ikuti langkah-langkah berikut untuk membuat halaman yang menampilkan data customer:
1. Berikut ini adalah contoh file yang digunakan untuk menampilkan data customer.
   
```php
<?php include('./header.php') ?>
<div class="card mt-5">
    <div class="card-header">Customers Data</div>
    <div class="card-body">
        <a href="add_customer.php" class="btn btn-primary mb-4">+ Add Customer Data</a>
        <br>
        <table class="table table-striped">
            <tr>
                <th>No</th>
                <th>Name</th>
                <th>Address</th>
                <th>City</th>
                <th>Action</th>
            </tr>
            <?php
            // TODO 1: Buat koneksi dengan database
            

            // TODO 2: Tulis dan eksekusi query ke database
            $query = "";
            // $result = ;

            if (!$result) {
                die("Could not query the database: <br />" . $db->error . '<br>Query: ' . $query);
            }

            // TODO 3: Parsing data yang diterima dari database ke halaman HTML/PHP


            echo '</table>';
            echo '<br>';
            echo 'Total Rows = ' . $result->num_rows;

            // TODO 4: Lakukan dealokasi variabel $result

            // TODO 5: Tutup koneksi dengan database
            
            ?>
    </div>
</div>
<?php include('./footer.php') ?>
```

Keterangan:
Link edit dan delete dibuat untuk setiap baris data, link tersebut menuju ke halaman untuk mengubah  (edit_customer.php) dan menghapus (confirm_delete_customer.php) data customer, dengan melewatkan customerid `(id=$row->customerid)` melalui alamat url. `customerid` yang dilewatkan selanjutnya dapat diakses oleh halaman yang dituju melalui `$_GET['id']`.

Tampilan dari file `view_customer.php` adalah sebagai berikut:

![[Pasted image 20240918064726.png]]

2. Ubahlah string query pada file `view_customer.php` menjadi:
3. Simpan dengan nama baru `view_customer2.php`.
4. Jalankan file `view_customer2.php`, apakah isi tabel customer dapat ditampilkan?
5. Ubahlah baris kode yang digunakan untuk menampilkan hasil eksekusi query seperti berikut:

6. Simpan dan jalankan kembali file `view_customer2.php`, apakah isi tabel customer dapat ditampilkan dengan benar?

## 3.2. Membuat Halaman Edit Customer

Halaman edit_customer.php menampilkan form untuk edit data customer dan form akan diproses
oleh file itu sendiri. Alur dari halaman edit ini adalah sebagai berikut:
1. Mengecek apakah user sudah melakukan submit form, jika belum maka akan ditampilkan form untuk edit yang sudah terisi dengan data customer dengan customerid tertentu yang diambil dari basis data.
2. Jika user sudah melakukan submit, maka dilakukan validasi isi form.
- Jika validasi berhasil, user akan di-redirect ke halaman `view_customer.php`.
- Jika validasi gagal, akan ditampilkan kembali halaman edit_customer.php dengan form yang telah terisi sesuai nilai yang dimasukkan user sebelumnya beserta pesan kesalahan validasi.

Buatlah file `edit_customer.php` seperti berikut:
```php
<?php

// TODO 1: Lakukan koneksi dengan database

// TODO 2: Buat variabel $id yang diambil dari query string parameter

// Memeriksa apakah user belum menekan tombol submit
if (!isset($_POST["submit"])) {
    // TODO 3: Tulislah dan eksekusi query untuk mengambil informasi customer berdasarkan id
    $query = 'FILL ME';
    // $result = ;


    if (!$result) {
        die("Could not query the database: <br />" . $db->error . '<br>Query: ' . $query);
    } else {
        while ($row = $result->fetch_object()) {
            $name = $row->name;
            $address = $row->address;
            $city = $row->city;
        }
    }

} else {
    $valid = TRUE;
    $name = test_input($_POST['name']);

    // Validasi terhadap field name
    if ($name == '') {
        $error_name = "Name is required";
        $valid = FALSE;
    } else if (!preg_match("/^[a-zA-Z ]*$/", $name)) {
        $error_name = "Only letters and white space allowed";
        $valid = FALSE;
    }

    // Validasi terhadap field address
    $address = test_input($_POST['address']);
    if ($address == '') {
        $error_address = "Address is required";
        $valid = FALSE;
    }

    // Validasi terhadap field city
    $city = $_POST['city'];
    if ($city == '' || $city == 'none') {
        $error_city = "City is required";
        $valid = FALSE;
    }

    // Update data into database
    if ($valid) {
        // TODO 4: Jika valid, update data pada database dengan mengeksekusi query yang sesuai
        $address = $db->real_escape_string($address);
        $query = "FILL ME";
        $result = $db->query($query);

        if (!$result) {
            die("Could not query the database: <br />" . $db->error . '<br>Query: ' . $query);
        } else {
            $db->close();
            header('Location: view_customer.php');
        }
    }
}
?>
<?php include('./header.php') ?>
<br>
<div class="card mt-4">
    <div class="card-header">Edit Customers Data</div>
    <div class="card-body">
        <form action="<?= htmlspecialchars($_SERVER['PHP_SELF']) . '?id=' . $id ?>" method="POST" autocomplete="on">
            <div class="form-group">
                <label for="name">Nama:</label>
                <input type="text" class="form-control" id="name" name="name" value="<?= $name; ?>">
                <div class="error"><?php if (isset($error_name)) echo $error_name ?></div>
            </div>
            <div class="form-group">
                <label for="name">Address:</label>
                <textarea class="form-control" name="address" id="address" rows="5"><?php echo $address; ?></textarea>
                <div class="error"><?php if (isset($error_address)) echo $error_address ?></div>
            </div>
            <div class="form-group">
                <label for="city">City:</label>
                <select name="city" id="city" class="form-control" required>
                    <option value="none" <?php if (!isset($city)) echo 'selected' ?>>--Select a city--</option>
                    <option value="Airport West" <?php if (isset($city) && $city == "Airport West") echo 'selected' ?>>Airport West</option>
                    <option value="Box Hill" <?php if (isset($city) && $city == "Box Hill") echo 'selected' ?>>Box Hill</option>
                    <option value="Yarraville" <?php if (isset($city) && $city == "Yarraville") echo 'selected' ?>>Yarraville</option>
                </select>
                <div class="error"><?php if (isset($error_city)) echo $error_city ?></div>
            </div>
            <br>
            <button type="submit" class="btn btn-primary" name="submit" value="submit">Submit</button>
            <a href="view_customer.php" class="btn btn-secondary">Cancel</a>
        </form>
    </div>
</div>
<?php include('./footer.php') ?>
<?php
$db->close();
?>
```

Selanjutnya, lakukan langkah-langkah sebagai berikut:
1. Panggil file `edit_customer.php` dan periksalah apakah validasi sudah dilakukan dengan benar dan perubahan data dapat disimpan di basis data.
2. Panggil kembali file `edit_customer.php`, lalu pada alamat isikan: Queen’s Street. Selanjutnya, submit dan periksalah apakah terdapat kesalahan dalam query?
3. Tambahkan baris kode berikut sebelum perintah query lalu simpan kembali.
4. Ulangi kembali langkah nomor 2, apakah update data berhasil dijalankan? Berikan penjelasan.


Tampilan dari file `edit_customer.php` untuk data customer tertentu adalah sebagai berikut:
![[Pasted image 20240918065217.png]]

## 3.3. Membuat Halaman Login

Halaman login.php menampilkan form untuk login sebagai admin dan form akan diproses oleh file itu
sendiri. Alur dari halaman login ini adalah sebagai berikut:

1. Mengecek apakah user sudah melakukan submit form, jika sudah maka isi form akan divalidasi.
	- Jika validasi berhasil, akan dicek apakah email dan password yang dimasukkan cocok dengan kombinasi email dan password yang ada di tabel admin.
		- Jika cocok, maka akan dibuat `$_SESSION["username"]` dan user akan di-redirect ke halaman admin.php.
		- Jika tidak cocok, maka user akan ditampilkan pesan kesalahan bahwa email dan password yang dimasukkan salah.
	- Jika validasi gagal, akan ditampilkan kembali halaman login.php dengan form yang telah terisi sesuai nilai yang dimasukkan user sebelumnya beserta pesan kesalahan validasi.
2. Jika user belum melakukan submit, maka ditampilkan form login yang masih kosong.

Buatlah file `login.php` seperti berikut:
```php
<!--
    Pada saat kita panggil file login.php dan diisikan data yang salah,
    validasi sudah dapat dijalankan.
    Pada saat kita panggil file login.php dan diisikan kombinasi email dan password yang salah,
    validasi sudah dapat dijalankan.
    Pada saat kita panggil file login.php dan diisikan kombinasi email dan password yang benar,
    halaman admin.php sudah dapat ditampilkan.
-->

<?php
// TODO 1: Buat sebuah sesi baru


// TODO 2 : Lakukan koneksi dengan database


// Memeriksa apakah user sudah submit form
if (isset($_POST['submit'])) {
    $valid = TRUE;

    // Memeriksa validasi email
    $email = test_input($_POST['email']);
    if ($email == '') {
        $error_email = 'Email is required';
        $valid = FALSE;
    } else if (!filter_var($email, FILTER_VALIDATE_EMAIL)) {
        $error_email = 'Invalid email format';
        $valid = FALSE;
    }

    // Memeriksa validasi password
    $password = test_input($_POST['password']);
    if ($password == '') {
        $error_password = 'Password is required';
        $valid = FALSE;
    }

    // Memeriksa validasi
    if ($valid) {
        // TODO 3: Buatlah query untuk melakukan verifikasi terhadap kredensial yang diberikan
        $query = "FILL ME";
        
        // TODO 4: Eksekusi query
        // $result = ;

        
        if (!$result) {
            die ("Could not query the database: <br />". $db->error);
        } else {
            if ($result->num_rows > 0) {
                $_SESSION['username'] = $email;
                header('Location: admin.php');
                exit;
            } else {
                echo '<span class="error">Combination of username and password are not correct.</span>';
            }
        }

        // TODO 5: Tutup koneksi dengan database
    }
}
?>
<?php include('./header.php') ?>
<br>
<div class="card mt-4">
    <div class="card-header">Login Form</div>
    <div class="card-body">
        <form method="POST" autocomplete="on" action="<?= htmlspecialchars($_SERVER['PHP_SELF']) ?>">
            <div class="form-group">
                <label for="email">Email:</label>
                <input type="email" class="form-control" id="email" name="email" value="<?php if (isset($email)) echo $email; ?>">
                <div class="error"><?php if (isset($error_email)) echo $error_email ?></div>
            </div>
            <div class="form-group">
                <label for="password">Password:</label>
                <input type="password" class="form-control" id="password" name="password" value="">
                <div class="error"><?php if (isset($error_password)) echo $error_password ?></div>
            </div>
            <br>
            <button type="submit" class="btn btn-primary" name="submit" value="submit">Login</button>
        </form>
    </div>
</div>
<?php include('./footer.php') ?>
```

Buatlah file `admin.php` seperti berikut:

```php
<?php 
// TODO 1: Inisialisasi session
session_start();

// TODO 2: Periksa apakah session dengan key username terdefinisi
if(!isset($_SESSION['username'])){
    header('Location: login.php');
    exit;
}

include('./header.php');
?>
<br>
<div class="card">
    <div class="card-header">Admin Page</div>
    <div class="card-body">
        <p>Welcome...</p>
        <p>You are logged in as <b><?= $_SESSION['username']; ?></b></p>
        <br><br>
        <a class="btn btn-primary" href="logout.php">Logout</a>
    </div>
</div>
<?php include('./footer.php') ?>

```

Buatlah file `logout.php` seperti berikut:

```php
<?php 
// TODO 1: Inisialisasi session

// TODO 2: Hapus username session

// TODO 3: Redirect ke halaman login
```

Jalankan file-file tersebut dengan cara sebagai berikut:
1. Panggil file `admin.php`, tanpa melakukan login terlebih dahulu. Cek apakah file dapat tersebut dapat ditampilkan? Berikan penjelasan.
2. Panggil file `login.php`, isikan data yang salah, periksalah apakah validasi sudah dapat dijalankan dengan benar.
3. Panggil file `login.php`, isikan kombinasi email dan password admin yang salah, periksalah apakah validasi sudah dijalankan dengan benar.
4. Panggil file `login.php`, isikan kombinasi email dan password admin yang benar, periksalah apakah halaman admin.php dapat ditampilkan.
5. Klik logout pada file `admin.php`, lalu panggil kembali file admin.php, setelah logout apakah file admin.php dapat ditampilkan? Berikan penjelasan.

## 3.4. Membuat Shopping Cart dengan Session

Pada bagian ini kita akan mencoba menggunakan session untuk menyimpan item-item yang dipilih oleh customer ke dalam shopping cart.
1. Buatlah file `view_books.php` untuk menampilkan daftar buku beserta link untuk menambahkannya ke shopping cart seperti tampilan berikut:

Link Add to Cart ditambahkan pada setiap record data buku, link tersebut menuju ke halaman show_cart.php dengan melewatkan parameter id yang diisi dengan isbn buku tersebut, seperti berikut:

![[Pasted image 20240918065521.png]]
Link Add to Cart ditambahkan pada setiap record data buku, link tersebut menuju ke halaman show_cart.php dengan melewatkan parameter id yang diisi dengan isbn buku tersebut, seperti berikut

2. Buatlah halaman `show_cart.php` menambahkan item ke shopping cart dan menampilkan isi shopping cart.
- Shopping cart disimpan dalam variabel `$_SESSION['cart']` berupa array asosiatif dengan indeks berupa id atau isbn buku dan value berupa quantity (qty) buku dengan isbn tersebut, contoh:
> `$_SESSION['cart'][ '0-672-31697-8'] = 2`
> `$_SESSION['cart'][ '0-672-31509-2'] = 1`
- Jika halaman show_cart.php dipanggil tanpa parameter di URL maka akan ditampilkan isi yang ada di dalam session `$_SESSION['cart']`.
- Jika halaman show_cart.php dipanggil dengan parameter di URL berupa id yang isinya isbn dari sebuah buku maka akan ditambahkan ke `$_SESSION['cart']`, misalnya `show_cart.php?id=0-672-31697-8`.

```php
<?php
// File         : show_cart.php
// Deskripsi    : Untuk menambahkan item ke shopping cart dan menampilkan isi shopping cart

session_start();
error_reporting(0);

$id = $_GET['id'];
if ($id != '') {
    if (!isset($_SESSION['cart'])) {
        $_SESSION['cart'] = array();
    }

    if (isset($_SESSION['cart'][$id])) {
        $_SESSION['cart'][$id]++;
    } else {
        $_SESSION['cart'][$id] = 1;
    }
}
?>
<?php include('./header.php') ?>
<br>
<div class="card mt-4">
    <div class="card-header">Shopping Cart</div>
    <div class="card-body">
        <br>
        <table class="table table-striped">
            <tr>
                <th>ISBN</th>
                <th>Author</th>
                <th>Title</th>
                <th>Price</th>
                <th>Qty</th>
                <th>Price * Qty</th>
            </tr>
            <?php
            require_once('./lib/db_login.php');
            $sum_qty = 0;
            $sum_price = 0;

            if (is_array($_SESSION['cart'])) {
                foreach ($_SESSION['cart'] as $id => $qty) {

                    // TODO 1: Tuliskan dan eksekusi query
                    $query = "FILL ME";
                    // $result = ;

                    if (!$result) {
                        die("Could not query the database: <br />" . $db->error . '<br>Query: ' . $query);
                    }

                    while ($row = $result->fetch_object()) {
                        echo '<tr>';
                        echo '<td>' . $row->isbn . '</td>';
                        echo '<td>' . $row->author . '</td>';
                        echo '<td>' . $row->title . '</td>';
                        echo '<td>$' . $row->price . '</td>';
                        echo '<td>' . $qty . '</td>';
                        echo '<td>$' . $row->price * $qty . '</td>';
                        echo '</tr>';

                        $sum_qty = $sum_qty + $qty;
                        $sum_price = $sum_price + ($row->price * $qty);
                    }
                }
                echo '<tr><td></td><td></td><td></td><td></td><td></td><td>$' . $sum_price . '</td>';
                $result->free();
                $db->close();
            } else {
                echo '<tr><td colspan="6" align="center">There is no item in shopping cart</td></tr>';
            }
            ?>
        </table>
        Total items = <?php echo $sum_qty ?><br><br>
        <a class="btn btn-primary" href="view_books.php">Continue Shopping</a>
        <a class="btn btn-danger" href="delete_cart.php">Empty Cart</a>
    </div>
</div>
<?php include('./footer.php') ?>
```

Tampilan dari halaman `show_cart.php` adalah seperti berikut:

![[Pasted image 20240918065933.png]]

Link Continue Shopping menuju ke halaman view_books.php, sedangkan link Empty Cart menuju ke halaman `delete_cart.php`.
3. Buatlah file delete_cart.php untuk mengosongkan isi `$_SESSION['cart']` lalu redirect ke halaman `view_books.php`.
```php
<?php 
// File         : delete_cart.php
// Deskripsi    : untuk menghapus session

// TODO 1: Inisialisasi data session

// TODO 2: Hapus session

// TODO 3: Redirect ke halaman show_cart.php
```
# 4. Tugas

1. Buatlah file untuk CRUD data berikut:
- `view_customer.php`, untuk menampilkan data pelanggan
- `edit_customer.php`, untuk edit data pelanggan
- `add_customer.php`, untuk menambah data customer baru
- `delete_customer.php`, untuk menghapus data customer tertentu.


2. Buatlah file untuk login seperti berikut:
- `login.php` seperti pada contoh di modul ini, jika berhasil redirect ke halaman view_customer.php.
- Tambahkan penanganan pada file `view_customer.php` sehingga file tersebut hanya dibuka oleh admin setelah berhasil login.
- Tambahkan link logout pada file `view_customer.php` untuk melakukan logout, lalu buatlah file `logout.php` seperti pada contoh di modul.

1. Buatlah file-file berikut untuk memproses shopping cart seperti yang dicontohkan di modul:
- `view_books.php`
- `show_cart.php`
- `delete_cart.php`
# TODO
- [x] Content
- [ ] Second pass
- [ ] Proof read
- [ ] Appendix