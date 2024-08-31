# SINTAKS DASAR PHP
# 1. Tujuan Praktikum
Setelah mengikuti praktikum ini mahasiswa diharapkan dapat memahami sintaks dasar PHP
untuk:
1) Menampilkan teks PHP ke web browser.
2) Menggunakan variabel dan konstanta di PHP.
3) Membuat kode PHP untuk contoh kasus kondisional
4) Menggunakan kode PHP untuk contoh kasus perulangan
5) Membuat fungsi dan melakukan pemanggilan fungsi dengan PHP.
6) Mendefinisikan array dengan PHP, mengakses elemen array melalui perulangan dan memahami beberapa fungsi sorting araay di PHP.

# 2. Tools
Tools yang dibutuhkan untuk melakukan praktikum ini adalah Apache web server dan PHP,
text editor.

# 3. Langkah-Langkah Praktikum
## 3.1. Praktikum 1 : Menampilkan teks PHP ke browser
Bagian ini bertujuan untuk membuat program PHP yang pertama, yang akan menampilkan text ke web browser. Tulislah program di bawah ini pada editor text dan simpanlah dengan nama “welcome.php” di direktori `C:\xampp\htdoc\pwi1`.

```php
<html>
<head>
	<title>Hello World</title>
</head>
<body>
<?php
	echo "<h2>Selamat datang di Praktikum PWI</h2><br />";
	echo "Hari ini parktikum : \"Sintaks Dasar PHP\"";
?>
</body>
</html>
```

## 3.2. Praktikum 2: Variabel dan konstanta
Bagian ini bertujuan untuk mempelajari penggunaan variabel dan menampilkan nilai variabel, serta membedakan lingkup variabel, yaitu lokal, statik, global dan super global.

```php
//assign nilai ke variabel
$a = 15;
echo 'Variabel a berisi : '.$a.'<br />';

$a = 'Pemrograman Web dan Internet';
echo 'Variabel a berisi : '.$a.'<br />';
```

Variabel lokal
```php
// Define a function
function diskon(){
	$harga = 1000;
	$harga = 0.2 * $harga;
}
$harga = 2000;
diskon();

echo 'harga = '.$harga.'<br />';
```

Berapakah nilai harga yang ditampilkan? Mengapa?
Variabel global
```php
// Define a function
function diskon1(){
	// Define harga as a global variable
	global $harga;
	
	// Multiply harga by 0.8
	$harga = 0.8 * $harga;
}

// Set harga
$harga = 2000;

// Call the function
diskon1();

// Display the age
echo 'harga = '.$harga.'<br />';
```

Berapa harga yang ditampilkan? Mengapa?
Variabel statik
```php
// Define the function
function diskon2(){
	// Define harga as a static variable
	static $harga = 1000;
	
	$harga = 0.8 * $harga;
	
	echo 'harga = '.$harga.'<br />';
}

// Set harga to 2000
$harga = 30;

// Call the function twice
diskon2();
diskon2();

// Display the harga
echo 'harga = '.$harga.'<br />';
```

Berapa harga yang ditampilkan? Mengapa?

Variabel super global
```php
echo htmlentities($_SERVER["PHP_SELF"]);
```

Konstanta

```php
define("PWI", "Permograman Web dan Internet ");
echo 'Hari ini sedang praktikum '.PWI.'<br />';

$constant_name = "PWI";

echo 'Hari ini sedang praktikum '.constant($constant_name).'<br />';

//konstanta bawaan PHP
echo 'File yang sedang diproses "'.__FILE__.' pada baris "'.__LINE__ .'"<br />';
```

## 3.3. Praktikum 3 : Conditional

Single `if-else`
```php
$lulus = TRUE;
if ($lulus){
	echo 'Selamat Anda Lulus. <br/>';
}else{
	echo 'Maaf, Anda gagal. Silakan mencoba lagi. <br />';
}
```

Multiple `if-else`
```php
$nilai = 60;
if ($nilai >= 80 && $nilai <= 100){
	echo 'Nilai : A <br />';
}elseif ($nilai >= 60 && $nilai < 80){
	echo 'Nilai : B <br />';
}elseif ($nilai >= 40 && $nilai < 60){
	echo 'Nilai : C <br />';
}elseif ($nilai >= 20 && $nilai < 40){
	echo 'Nilai : D <br />';
}elseif ($nilai >= 0 && $nilai < 20){
	echo 'Nilai : E <br />';
}else{
	echo 'Invalid nilai <br />';
}
```

Cobalah `$nilai` dengan beberapa nilai yang lain, misalkan $86$, $68$, $59$, $30$, $11$, $0$, $110$, $-98$, `"abc"`. Bagaimana hasilnya?

```php
Switch
$nilai = 'AB';
switch ($nilai) {
	case "A":
		echo "Sangat Baik. <br />";
		break;
	case "B":
		echo "Baik. <br />";
		break;
	case "C":
		echo "Cukup. <br />";
		break;
	case "D":
		echo "Kurang. <br />";
		break;
	case "E":
		echo "Tidak Lulus. <br />";
		break;
	default:
		echo "Invalid nilai! <br />";
}
```

Cobalah `$nilai` dengan beberapa nilai yang lain, misalkan `B`, `C`, `D`, `E`, `AB`. Bagaimana hasilnya? Hapus setiap statement ‘break’ pada kode program di atas dan cobalah isi `$nilai` dengan
beberapa nilai seperti sebelumnya. Bagaimana hasilnya?

## 3.4. Praktikum 3 : Looping

`for` Loop
```php
$harga = 1000;
echo '<table border="1">';
echo '<tr>
<td>No</td>
<td>Diskon</td>
<td>Harga Setelah Diskon</td>
</tr>';

for ($i = 1; $i <= 10; $i++){
	echo '<tr>';
	echo '<td>'.$i.'</td>';
	
	$diskon = $i * 0.1;
	echo '<td>'.($diskon*100).' % </td>';
	
	$harga_diskon = $harga - ($harga * $diskon);
	echo '<td>'.$harga_diskon.'</td>';
	echo '</tr>';
}

echo '</table>';
```

Buatlah kode program yang sama dengan kode program diatas menggunakan perulangan
`while` dan `do-while`.

## 3.5. Praktikum 3 : Function

```php
//contoh fungsi yang tidak mengembalikan nilai (disebut juga prosedur)
function print_mhs($nama, $nim, $prodi){
	echo 'Nama: '.$nama.'<br />';
	echo 'NIM: '.$nim.'<br />';
	echo 'Prodi: '.$prodi.'<br />';
}
print_mhs('Alfa','123456123','Ilmu Komputer/ Informatika');
```

```php
//menghitung harga setelah diskon
//parameter input: harga dan diskon
function hitung_diskon($harga,$diskon){
	$harga = $harga - ($harga*$diskon/100);
	return $harga;
}

//contoh pemanggilan fungsi
$harga = 10000;
$diskon = 20;
$harga_diskon = hitung_diskon($harga,$diskon);
echo 'Harga sebelum diskon = '.$harga.'<br />';
echo 'Harga setelah diskon = '.$harga_diskon.'<br />';
```

```php
//menghitung harga setelah diskon
//parameter input: harga dan diskon (nilai default=10)
function hitung_diskon2($harga,$diskon=10){
	$harga = $harga - ($harga*$diskon/100);
	return $harga;
}

//contoh pemanggilan fungsi
$harga = 10000;
$harga_diskon = hitung_diskon2($harga);
echo 'Harga sebelum diskon = '.$harga.'<br />';
echo 'Harga setelah diskon = '.$harga_diskon.'<br />';
```

```php
//menghitung harga setelah diskon
//harga sebagai parameter input dan output
function hitung_diskon3(&$harga,$diskon){
	$harga = $harga - ($harga*$diskon/100);
	return $harga;
}

//contoh pemanggilan fungsi
$harga = 10000;
$diskon = 20;
echo 'Harga sebelum diskon = '.$harga.'<br />';

hitung_diskon3($harga,$diskon);
echo 'Harga setelah diskon = '.$harga.'<br />';
```

Amati perbedaan pada masing-masing fungsi tersebut!

Contoh fungsi rekursif untuk menghitung nilai faktorial dari sebuah bilangan.
```php
function faktorial($n) {
	if ($n == 0){
		return 1;
	} else {
		return $n * faktorial($n-1);
	}
}
```

Simpan kelima fungsi tersebut dalam sebuah file bernama fungsi.php.
Buat sebuah file baru bernama panggil_fungsi.php untuk melakukan pemanggilan fungsi
tersebut dan isikan kode program seperti berikut:

```php
require_once("fungsi.php");

//pemanggilan fungsi hitung_diskon
$harga = 10000;
$diskon = 20;
$harga_diskon = hitung_diskon($harga,$diskon);
echo 'Harga sebelum diskon = '.$harga.'<br />';
echo 'Harga setelah diskon = '.$harga_diskon.'<br />';

//pemanggilan fungsi faktorial
print(faktorial(4));
```

## 3.6. Praktikum 3 : Array

Numeric array

```php
//assignment melalui array identifier
for ($i=0;$i<10;$i++){
	$diskon[] = $i * 5;
}
//assignment menggunakan fungsi array
//$diskon = array(0, 10, 20, 30, 40, 50, 60, 70, 80, 90);

//cek apakah sebuah variabel bertipe array
if (is_array($diskon)) {
	echo 'Array';
	else
	echo 'Not Array';
	//menampilkan isi array
	$n = sizeof($diskon);
	for($i = 0; $i <= $n - 1; $i++){
	echo 'Diskon hari ke-'.($i+1).' = '.$diskon[$i].' % <br />';
}
```

Coba urutkan array di atas menggunakan fungsi pengurutan `sort()`, `asort()` dan `ksort()`. Bagaimana perbedaaanya?

Assosiative array
```php
//assignment menggunakan fungsi array
$bulan = array(
    'jan' => 'Januari',
	'feb' => 'Februari',
	'mar' => 'Maret',
	'apr' => 'April',
	'mei' => 'Mei',
	'jun' => 'Juni',
	'jul' => 'Juli',
	'agu' => 'Agustus',
	'sep' => 'Sepetember',
	'okt' => 'Oktober',
	'nov' => 'November',
	'des' => 'Desember'
);

foreach($bulan as $kode_bulan => $nama_bulan){
	echo 'Kode bulan "'.$kode_bulan.'" => "'.$nama_bulan.'"<br />';
}
```

Coba urutkan array di atas menggunakan fungsi pengurutan `sort()`, `asort()` dan `ksort()`. Bagaimana perbedaaanya?

# 4. Latihan

Diketahui sebuah array mahasiswa seperti berikut:
```php
$array_mhs = array(
	'Abdul' => array(89,90,54),
	'Budi' => array(78, 60, 64),
	'Nina' => array(67, 56, 84),
	'Budi' => array(87, 69, 50),
	'Budi' => array(98, 65, 74)
);
```

Indeks pada array berupa nama mahasiswa.

Isi setiap elemen `array_mhs` berupa array yang terdiri atas kumpulan nilai untuk tiap mahasiswa.

Soal:
Buatlah sebuah fungsi bernama `print_mhs($array_mhs)` untuk menampilkan data mahasiswa  yang ada pada array_mhs seperti berikut.

![[Pasted image 20240831133312.png]]

Sebelumnya, buatlah fungsi terpisah bernama fungsi `hitung_rata($array)` untuk menghitung nilai rata-rata elemen array dan gunakan fungsi tersebut pada fungsi `print_mhs($array_mhs)`.

# TODO
- [x] Content
- [x] Second pass
- [ ] Proof read
- [ ] Appendix