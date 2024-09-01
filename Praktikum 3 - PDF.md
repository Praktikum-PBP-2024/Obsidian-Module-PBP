# PEMROSESAN FORM

# 1. Tujuan Praktikum

Setelah mengikuti praktikum ini mahasiswa diharapkan dapat memahami cara untuk:
1. Membaca isi form dengan PHP menggunakan method GET maupun POST
2. Melakukan validasi input data dengan PHP
3. Menampilkan isi kembali form
# 2. Tools

Tools yang dibutuhkan untuk melakukan praktikum ini adalah Apache web server, PHP, MySQL dan text editor.
# 3. Langkah-Langkah Praktikum

## 3.1. Membaca isi form dengan PHP menggunakan method GET

1. Buatlah form input data mahasiswa seperti berikut menggunakan kode HTML dengan ketentuan berikut:

-  Gunakan submission method GET.
- Pemrosesan form dilakukan pada halaman yang sama, sehingga atribut action pada elemen `<form>` dikosongkan.
- Berikan nama pada setiap elemen input yang digunakan pada atribut name.
- Elemen input yang masukannya berupa single value diberi nama berupa teks biasa, sedangkan yang masukannya dapat berupa multiple values diberi nama sebagai array.

Berikut adalah potongan source code yang digunakan untuk membuat form seperti gambar di atas. 

`user_form_get.php`

```php
<div class="form-group">
	<label for="nama">Nama:</label>
	<input type="text" class-"form-control" id="nama" name="nama" maxlength="50">
</div>
<div class="form-group">
	<label for="email">Email:</label>
	<input type="email" class="form-control" id="email" name="email">
</div>
<div class="form-group">
	<label for="kota">Kota/ Kabupaten:</labe1>
	<select id="kota" name="kota" class="form-control">
		<option value="Semarang">Semarang</option>
		<option value="Jakarta">Jakarta</option>
		<option value="Bandung">Bandung</option>
		<option value="Surabaya">Surabaya</option>
	</select>
</div>
	<label>Jenis Kelamin:</label>
	<div class="form-check">
	<label class="form-check-label">
		<input type="radio" class="form-check-input" name="jenis_kelamin" value="pria">
		Pria
	</label>
</div>
<div class="form-check">
	<label class="form-check-label">
		<input type="radio" class="form-check-input" name="jenis_kelamin" value="wanita">
		Wanita
	</label>
</div>
<br>
<labe1>Peminatan:</label>
<div class="form-check">
	<label class="form-check-label">
		<input type="checkbox" class="form-check-input" name="minat[]" value="coding">
		Coding
	</label>
</div>
<div class="form-check">
	<label class="form-check-label">
		<input type="checkbox" class="form-check-input" name="minat[]" value="ux_design">
		UX
	</label>
</div>
<div class "form-check">
	<label class="form-check-label">
		<input type="checkbox" class="form-check-input" name="minat[]" value="data_science">
		Data Science
	</label>
</div>
<br>
<!-- submit, reset dan button -->
<button type="submit" class="btn" btn="primary" name="submit" value="submit">
	Submit
</button>
<button type "reset" class="btn btn-danger">
	Reset
</button>
</form>
```


2. Tambahkan kode PHP seperti berikut setelah kode untuk membuat form yang bertujuan untuk membaca dan menampilkan isian yang dimasukkan ke form tersebut. Karena menggunanakan method GET, maka isi form diakses melalui array `$_GET`.

```php
<?php
if (isset($_GET["submit"])){
	echo "<h3>Your Input:</h3>";
	echo 'Nama = '.$_GET('nama'].'<br />';
	echo 'Email = '.$_GET['email'].'<br />';
	echo 'Kota = '.$_GET['kota'].'<br />';
	echo 'Jenis Kelamin = '.$_GET['jenis kelamin'].'<br />';
	echo 'Minat = '.$_GET['minat'].'<br />';
	$minat = $_GET['minat'];
	if (!empty($minat)) {
		echo 'Peminatan yang dipilih: ';
		
		foreach($minat as Sminat_item) {
			echo '<br />'.$minat_item;
		}
	}
```

3. Buatlah sebuah folder bernama form di folder htdocs, lalu simpan file tersebut di folder form dengan nama `user_form_get.php`.
4. Jalankan file tersebut di web browser, perhatikan alamat url setelah form diisi dan di-submit.
5. Perhatikan pada field hobby, mengapa penamaan dan pengaksesannya berbeda dengan field lainnya?

## 3.2. Membaca isi form dengan PHP menggunakan method POST

1. Ubah file `user_form_get.php`, ganti nilai atribut method pada elemen `<form>` dengan POST.

```php
<form method="POST" autocomplete="on" action="">
```

2. Lalu, ubahlah kode PHP yang digunakan untuk membaca isi form dari `$_GET` menjadi `$_POST` seperti berikut:

```php
<?php
if (isset($_POST["submit"])){
	echo "<h3>Your Input:</h3>";
	echo 'Nama = '.$_POST('nama'].'<br />';
	echo 'Email = '.$_POST['email'].'<br />';
	echo 'Kota = '.$_POST['kota'].'<br />';
	echo 'Jenis Kelamin = '.$_POST['jenis kelamin'].'<br />';
	echo 'Minat = '.$_POST['minat'].'<br />';
	$minat = $_POST['minat'];
	if (!empty($minat)) {
		echo 'Peminatan yang dipilih: ';
		
		foreach($minat as Sminat_item) {
			echo '<br />'.$minat_item;
		}
	}
```

3. Simpan file tersebut dengan nama baru, yaitu `user_form_post.php`.
4. Jalankan file tersebut di web browser, perhatikan alamat url setelah form diisi dan di-submit.
5. Apa perbedaan antara method GET pada file `user_form_get.php` dan method POST pada file `user_form_post.php`?
6. Manakah yang lebih baik, method GET atau POST? Uraikan jawaban Anda.

## 3.3. Validasi form dengan PHP
Form pada file user_form_get.php maupun user_form_post.php belum ditambahkan penanganan validasi. Sebelumnya, tambahkan field alamat menggunakan elemen `<textarea>` setelah field email pada file `user_form_post.php`, sehingga tampilannya menjadi seperti berikut:

1. Tambahkan kode PHP berikut untuk menambahkan aturan validasi dan letakkan di bagian atas, sebelum kode untuk membuat form.

```php
<body>
<?php
if (isset($_POST['submit'])))(
//validasi nama: tidak boleh kosong, hanya dapat berisi huruf dan spasi
Snama = test_input($ POST('nama']);
if (empty ($nama) ) (
Serror_nama = "Nama harus diisi";
)elseif ((preg_natch("/^(a-zA-2 ]*$/",Snama)) (
Serror_nama = "Nama hanya dapat berisi huruf dan spasi";
//validasi email: tidak boleh kosong, format harus benar
Semail = test_input($_POST('enail))));
if (Semail == ' ) (
Serror_email = "Email harus diisi";
)elseif (!filter_var(Semail, FILTER VALIDATE EMAIL) (
Serror email = "Format email tidak benar";
//validasi alamat: tidak boleh kosong
Salamat = test_input ($_POST('alamat'));
if ($alamat == '') (
Serror alamat = "Alamat harus diisi";
//validasijonis kelamin: tidak boleh kosong
if ($jenis_kelamin =- ' ) ) (
Serror jenis kelamin = "Jenis kelamin harus diisi":
//validasi kota: tidak boleh kosong
$kota = $_POST['kota'];
if (Skota = '' || Skota a = = 'kota') [
Serror_kota = "Kota harus diisi";
//validasi minat: tidak boleh kosong
$minat= $_POST('minat'];
if (empty(Sminat))(
Serror minat = "Peminatan harus dipilih";
```

```php
function test input($data) {
	$data = trim($data);
	$data = stripslashes($data);
	Sdata = htmlspecialchars($data);
	return $data;
}
```

2. Tambahkan kode berikut pada setiap elemen input form untuk menampilkan pesan error. Berikut adalah contoh pada field nama dan email, tambahkan pula untuk field lainnya dengan cara yang sama.
```php
<div class="form-group">
	<label for="nama">Nama:<</label>
	<input type="text" class="form-control" id="nama" name="nama" maxlength="50">
	<div class="error"><?php if(isset(Serror nama)) echo Serror nama;?>></div>)
</div>
<div class="form-group">
	<label for="email">Email:</label>
	<input type="email" class="form-control" id="email" name="email">
	<div class="error"><?php if(isset(Serror email)) echo serror email;?>></div>
</div>
```
3. Simpan file tersebut dengan nama baru `user_form_post1.php`.
4. Jalankan file tersebut di web browser, kosongkan sebagian field, lalu submit, perhatikan apakah pesan error sudah ditampilkan dengan benar? Perhatikan apakah field yang sudah terisi sebelumnya dapat ditampilkan kembali? Mengapa?
5. Apakah peran fungsi `test_input($data)` pada proses validasi tersebut? Mengapa fungsi tersebut hanya dikenakan pada isian nama, email dan alamat, namun tidak dikenakan pada isian jenis kelamin, kota dan peminatan?
6. Bagaimanakah aturan validasi yang digunakan untuk mengecek agar isian tidak boleh kosong?

## 3.4. Menampilkan kembali isi form
Pada file `form_customer2.php` jika terjadi kesalahan maka isian form akan kembali kosong lagi. Untuk menampilkannya kembali tambahkan kode berikut pada setiap elemen input yang bersesuaian. Perhatikan bahwa cara yang digunakan berbeda untuk elemen input yang berbeda. 

Field nama (perhatikan kode yang diblok warna abu-abu):
```php
<div class "form-group">
	<label for="nama">Nama:</label>
	<input type="text" class="form-control" id="nama" name="nama" maxlength="50" value="<?php if(isset(Snama)) (echo Snama;) ?>">
	<div class="error"> 
		<?php if(isset($error_nama)) echo $error_nama; ?>
	</div>
</div>
```

Field alamat:
```php
<div class="form-group">
	<label for-"alamat">Alamat:</label>
	<textarea class="form-control" id="alamat" rows="3" name-"alamat">
	<?php if(isset(Salamat) (echo Salamat;) ?></textarea>
	<div class-"error"X?php if(isset (Serror alamat)) echo Serror alamat;?></div>
</div>
```

Field kota:
```php
<select id="kota" name-"kota" class="form-control">
<option value-"Semarang" <?php if (isset(Skota) && Skota="Semarang") echo
"selected="true" ; ?>>>Semarang</option>
<option value="Jakarta" <?php if (isset(Skota) && $kota="Jakarta") echo
"selected="true"'; ?>>Jakarta</option>
```

Lengkapi untuk option yang lainnya.

Field jenis kelamin:

```php
<div class="form-check">
<label class="form-check-label">
<input type-"radio" class="form-check-input" name="jenis_kelamin" value="pria"
	<?php 
		if (isset($jenis_kelamin) && $jenis_kelamin=="pria") echo "checked"
	?>
	>Pria
</label>
```

Lengkapi untuk opsi radio button jenis kelamin yang lainnya.

Field peminatan:

```php
<div class="form-check">
<label class="form-check-label">
<input type="checkbox" class-"form-check-input" name="minat[]" value="ux_design"
<7php if (isset(Sminat) ss in array('ux design',$minat)) echo 'checked'; 2>>UX Design
</label>
</div>
pi untuk pilihan checkbox minat yang lainnya.
```

Lengkapi untuk pilihan checkbox minat yang lainnya.

Setelah semua selesai, simpan dengan nama `user_form_post2.php`. Jalankan pada browser dan amati perbedaaanya dengan `user_form_post1.php`. Periksalah apakah isi form yang  ebelumnya sudah ditampilkan dengan benar.

# 4. Tugas

Selesaikanlah file 4 file yang langkah-langkahnya telah diuraikan pada bagian sebelumnya, yaitu:
- `user_form_get.php`
- `user_form_post.php`
- `user_form_post1.php`
- `user_form_post2.php`

Simpan keempat file tersebut dalam folder form.

Buatlah form seperti gambar berikut:

Aturan validasi:

- Semua field harus diisi. 
- NIS terdiri atas 10 karakter dan hanya boleh berisi angka 0..9.
- Jika siswa kelas X atau XI, maka program menampilkan pilihan ekstrakurikuler. Siswa wajib memilih kegiatan ekstrakurikuler yang diminati, minimal 1 maksimal 3. Jika kelas XII siswa tidak boleh mengikuti kegiatan ekstrakurikuler, sehingga program tidak perlu menampilkan kegiatan ekstrakurikuler.


# TODO
- [x] Content
- [ ] Second pass
- [ ] Proof read
- [ ] Appendix