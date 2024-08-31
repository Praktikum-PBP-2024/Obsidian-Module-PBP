# CLIENT SIDE SCRIPTING: JAVASCRIPT

# 1. Tujuan Praktikum

Setelah mengikuti praktikum ini mahasiswa diharapkan dapat melakukan client-side scripting pada halaman web menggunakan JavaScript.
# 2. Tools

Tools yang dibutuhkan untuk melakukan praktikum ini adalah web browser dan text editor(Notepad++).
# 3. Langkah - Langkah Praktikum

## 3.1. JavaScript Basic

Menuliskan teks `Hello world` ke layar menggunakan [`document.write`](https://developer.mozilla.org/en-US/docs/Web/API/Document/write) 

`01_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Javascript</h1>
	<script>
	document.write("Hello world!!!");
	</script>
</body>
</html>
```


Kode javacript dituliskan di antara tag `<script>...</script>` dan dapat dimasukkan di dalam tag `<head>` atau `<body>`. Kode JavaScript dapat pula ditulis secara eksternal.

Contoh penulisan JavaScript di dalam tag `<head>`.

`02_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
	<script>
	function myFunction() {
		document.getElementById("paragraf") .innerHTML = "Hypertext Markup Language";
	}
	</script>
</head>
<body>
	<p id="paragraf">HTML</p>
	<button type="button" onclick="myFunction()">Show Abbr</button>
</body>
</html>
```

Contoh penulisan kode JavaScript secara eksternal:

`myscript.js`
```js
function myFunction() {
	document.getElementById("paragraf").innerHTML = "Hypertext Markup Language"
}
```

`03_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
	<script src="js/myscript.js"></script>
</head>
<body>
	<p id="paragraf">HTML</p>
	<button type="button" onclick="myFunction()">Show Abbr</button>
</body>
</html>
```

Kondisional: statement `if-else`

`04_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Javascript</h1>
	<script>
	var page = "Home";
	if(page == "Home")  {
		document.write("You selected Home");
	} else if(page == "About") {
		document.write("You selected About") ;
	} else if(page == "News") {
		document.write ("You selected News")
	} else if(page == "Login") {
		document.write ("You selected Login")
	}else if(page == "Links"){
		document.write ("You selected Links");
	}
	</script>
</body>
</html>
```

Ubahlah statement `if-else` pada contoh sebelumnya menggunakan `switch-case` seperti berikut. Lalu simpan dengan nama `05_basic.html`.

`05_basic.html`
```html
<script>
var page = "Home";

switch (page) {
	case "Home":
		document.write("You selected Home");
		break;
	case "About":
		document.write("You selected About");
		break;
	case "News":
		document.write("You selected News");
		break;
	case "Login" :
		document.write("You selected Login");
		break;
	case "Links":
		document.write("You selected Links");
		break;
}
</script>
```

Perulangan: statement `while`

`06_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Looping: while</h1>
	<script>
	counter = 0;
	while (counter < 5) {
		document.write("Counter: " + counter + "<br />");
		counter++;
	}
	</script>
</body>
</html>
```

Perulangan: statement `do-while`

`07_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Looping: do-while</h1>
	<script>
	counter = 0;
    do {
		document.write("Counter: " + counter + "<br />");
		counter++;
	} while (counter < 5) 
	</script>
</body>
</html>
```

Perulangan: statement `for`

`08_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Looping: for</h1>
	<script>
	for (var counter=1; counter < 5; counter++){
		document.write("Counter: " + counter + "<br />");
	}
	</script>
	</body>
</html>
```

Array numerik

`09_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Array</h1>
	<script>
	var myArray = [];
	myArray[0] = 5 ;
	myArray[1] = 10;
	myArray[2] = 15 ;
	
	//dekalarasi array menggunakan keyword array()
	var myArray2 = Array("red", "yellow","green");
	
	//looping numeric array
	for(var i = 0; i < myArray2.length; i++){
		document.write("Array " + i + ": " + myArray2[i] + "<br />");
	}
	</script>
</body>
</html>
```

Array asosiatif

`10_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Array Asosiatif</h1>
	<script>
	//array asosiatif
	var myArray3 = {
		"html": "Hypertext Markup Language",
		"xml": "Extensible Markup Language",
		"css": "Cascading style Sheet"
	}
	
	//looping numeric array
	for(x in myArray3) {
		document.write("Array " + x + ": " + myArray3[x] + "<br />");
	}
	</script>
	</body>
</html>
```

Fungsi

`11_basic.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h1>Fungsi</h1>
	<script>
	var myArray = [];
	myArray[0] = 5;
	myArray[1] = 10;
	myArray[2] = 15;
	
	document.write("Jumlah seluruh elemen array adalah " + sumArray(myArray));
	
	function sumArray(x){
		var sum = 0;
		for (var i = 0; i < x.length; i++){
			sum = sum + x[i];
		}
		return sum;
	}
	</script>
</body>
</html>
```

## 3.2. Document Object Model (DOM)
DOM memungkinkan kita untuk mengakses elemen-elemen HTML yang ada di dalam sebuah halaman web. Di dalam DOM dokumen web direpresentasikan sebagai tree yang tersusun atas sejumlah objek(elemen) yang saling berhubungan. Setiap elemen memiliki method dan property.
### 3.2.1. Menemukan elemen HTML
Mengakses elemen HTML menggunakan fungsi [`getElementByld(element)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementById).

`01_dom.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<h2>Akses elemen menggunakan getElementById</h2>
	<p id="content">Belajar Document Object Model</p>
	<p id="demo"></p>
	<script>
		var x = document.getElementById("content");
		document.getElementById("demo").innerinnerHTML = "Isi teks : " + x.innerHTML;
	</script>
</body>
</html>
```

Mengakses elemen HTML menggunakakan fungsi [`getElementsByTagName(tag)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByTagName).

`02_dom.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
<h2>Akses elemen menggunakan getElementByTagName</h2>
	<p>Belajar Javascript</p>
	<p>Belajar Document Object Model</p>
	<p id="demo"></p>
	
	<script>
	var x = document.getElementsByTagName("p");
	
	document.getElementById("demo").innerHTML = "Isi teks[0]: " + x[0].innerHTML + "<br />" 
                                              + "Isi teks[1]: " + x[1].innerHTML;
	</script>
</body>
</html>
```

Mengakses elemen HTML menggunakan fungsi [`getElementsByClassName(class)`](https://developer.mozilla.org/en-US/docs/Web/API/Document/getElementsByClassName).

`03_dom.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<p class="content">Belajar Javascript</p>
	<p class="content">Belajar Document Object Model</p>
	<h2>Akses elemen menggunakan getElementByClassName</h2>
	<p id="demoClass"></p>
	<h2>Akses elemen menggunakan getElementByClassName</h2>
	<p id="demoSelector"></p>
	
	<script>
	var x = document.getElementsByClassName("content");
	
	document.getElementById("demoClass").innerHTML = "Isi teks[0]: " + x[0].innerHTML + "<br />" + 
	                                                 "Isi teks[1]: " + x[1].innerHTML;
	
	var y = document.querySelectorAll("p.content");
	document.getElementById("demoSelector").innerHTML = "Isi teks[0]: " + y[0].innerHTML + "<br />" +
	                                                    "Isi teks[1]: " + y[1].innerHTML;
	</script>
</body>
</html>
```

### 3.2.2. Mengubah elemen HTML

`04_dom.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
	<script>
	function ubahTextJudul() {
		document.getElementsByTagName("h2")[0].innerHTML = "Document Object Model";
	}
	function ubahGambar() {
		document.getElementById("logo").src = "images/html_logo.png";
	}
	function ubahAttribut() {
		document.getElementsByTagName("h2")[0].setAttribute("class", "judul");
		document.getElementById("logo").setAttribute("width",  300);
		document.getElementById("logo").setAttribute("height", 300);
	}
	function ubahElemenJudulMenjadiMerah() {
		document.getElementsByClassName("judul")[0].style.color = "red";
	}
	</script>
</head>
<body>
	<h2>Hypertext Markup Language</h2>
	<img id="logo" src="images/picture.jpg" alt="gambar">
	<button id="bta01" type="button" onclick="ubahTextJudul()">Ubah inner HTML</button>
	<button id="btn02" type="button" onclick="ubahGambar()">Ubah nilai atribut image</button>
	<button id="btn03" type="button" onclick="ubahAttribut()">Set nilai atribut baru</button>
	<button id="btn04" type="button" onclick="ubahElemenJudulMenjadiMerah()">Ubah style elemen</button>
</body>
</html>
```

Mengubah visibility elemen HTML menggunakan property style.visibility.

`05_dom.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
	<script>
	function hideImage() {
		document.getElementById("imgLogo").style.visibility = "hidden";
	}
	function showimage() {
		document.getElementById("imgLogo").style.visibility = "visible";
	}
	</script>
</head>
<body>
	<h2>Hypertext Markup Language</h2>
	<img id="imglogo" src="images/htal logo.pog" alt="gambar" style="width:200px;height:200px;border=0;">
	<br />
	<button id="btn01" type="button" onclick="hideImage()">Hide Image</button>
	<button id="btn02" type="button" onclick="showimage()">Show Image</button>
</body>
</html>
```

### 3.2.3. Menambah atau menghapus elemen HTML

Menambah elemen HTML dengan method [`createElement()`](https://developer.mozilla.org/en-US/docs/Web/API/Document/createElement) dan menghapus child dari sebuah
element dengan method [`removeChild()`](https://developer.mozilla.org/en-US/docs/Web/API/Node/removeChild).

`06_dom.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<p>Klik button "Create New Element" untuk membuat elemen BUTTON baru</p>
	<button onclick="createNewElement()">Create New Element</button>
	
	<ul id="myList">
		<li>HTML</li>
		<li>CSS</li>
		<li>Javascript</li>
	</ul>
	
	<p>Klik button "Remove Child Element" untuk menghapus child element list</p>
	<button onclick="removeChildElement()">Remove Child Element</button>
	
	<script>
	function createNewElement() {
		var btn = document.createElement("BUTTON");
		var t = document.createTextNode("CLICK ME");
		btn.appendChild(t);
		document.body.appendChild(btn);
	}
	function removeChildElement() {
		var list = document.getElementById("myList");
		list.removeChild(list.childNodes[1]);
	}
	</script>
</body>
</html>
```

### 3.2.4. Menambahkan event handler pada elemen HTML

`07_dom.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Belajar Javascript</title>
</head>
<body>
	<p>Adding Event Handler</p>
	<button id="btn01" type="button">Click Me</button>
	<p id="demo"></p>
	<script>
	document.getElementById("btn01").onclick = function(){
		document.getElementById("demo").innerHTML = "Sukses";
	}
	</script>
</body>
</html>
```

## 3.3. Form Validation

`01_form_validation.html`
```html
<!DOCTYPE html>
<html>
<head>
	<title>Form Login</title>
    <script>
	function validateForm() {
		var x = document.forms["formLogin"]["fusername"].value;
		var y = document.forms["formLogin"]["fpassword"].value;
		if (x == "" || y == "") {
			alert("Username and password harus diisi!");
			return false;
		}
	}
    </script>
</head>
<body>
	<h2>Login</h2>
    <form name="formLogin" action="process.php" method="post">
        Name: <input type="email" name="fusername" required="required" maxlength="30"/>
        <span id="errUsername"></span><br />
        Password: <input type="password" name="fpassword" required="required" maxlength="30" />
        <span id="errPassword"></span><br />
        <input type="button" value="Submit" onclick="validateForm()">
    </form>
</body>
</html>
```

Menggunakan method [`checkValidity()`](https://developer.mozilla.org/en-US/docs/Web/API/HTMLInputElement/checkValidity) dan property `validationMessage`

`02_form_validation.html`
```html
<!DOCTYPE htm1>
<html>
<head>
    <title>Form Login</title>
    <script>
    function validateForm() {
        var x = document.forms["formLogin"]["fusername"];
        var y = document.forms["formLogin"]["fpassword"];
        if (x.checkValidity() == false || y.checkValidity() == false) {
            document.getElementById("errUsername").innerHTML = x.validationMessage;
            document.getElementById("errPassword").innerHTML = y.validationMessage;
            return false;
        }
    }
    </script>
</head>
<body>
    <h2>Login</h2>
    <form name="formLogin" action="process.php" method="post">
        Name: <input type="email" name="fusername" required="required" maxlength="30"/>
        <span id="errUsername"></span><br />
        Password: <input type="password" name="fpassword" required="required" maxlength="30" />
        <span id="errPassword"></span><br />
        <input type="button" value="Submit" onclick="validateForm()">
    </form>
</body>
</html>
```

# Tugas

Buatlah form input tambah produk seperti gambar berikut:

![[tugas1_rip.png]]

Aturan validasi untuk form tersebut adalah sebagai berikut:

| Field            | Aturan validasi                                                                                                                                                                                                                                                                                                                                     |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Nama produk      | Harus diisi, minimal **5** karakter, maksimal **30** karakter                                                                                                                                                                                                                                                                                       |
| Deskripsi produk | Harus diisi, minimal **5** karakter, maksimal **100** karakter                                                                                                                                                                                                                                                                                      |
| Kategori         | Harus diisi<br>Pilihan: <br>- Baju<br>- Elektronik <br>- Alat Tulis                                                                                                                                                                                                                                                                                 |
| Sub Kategori     | Harus diisi, pilihan sesuai dengan kategori yang dipilih.<br>Jika kategori = **Baju**, pilihan sub kategori: <br>- Baju Pria<br>- Baju Wanita<br>- Baju Anak<br>Jika kategori = **Elektronik**, pilihan sub kategori:<br>- Mesin Cuci<br>- Kulkas<br>- AC<br>Jika kategori = **Alat Tulis**, pilihan sub kategori:<br>- Kertas<br>- Map<br>- Pulpen |
| Harga satuan     | Harus diisi, berupa nilai numerik                                                                                                                                                                                                                                                                                                                   |
| Grosir           | **Jika Ya, maka harga grosir harus diisi, jika tidak harga grosir dikosongkan**                                                                                                                                                                                                                                                                     |
| Harga grosir     | Harus diisi jika pilihan Grosir adalah Ya, berupa nilai numerik                                                                                                                                                                                                                                                                                     |
| Jasa kirim       | **Minimal jasa kirim yang dipilih adalah 3**                                                                                                                                                                                                                                                                                                        |
| Captcha          | Berisi huruf dari A-Z atau a-z sepanjang 5 karakter, di-generate secara random saat halaman di-load.<br><br>**Hint**: Mahasiswa dapat menggunakan fungsi [`String.fromCharCode`](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/String/fromCharCode) untuk mengubah angka kode ASCII ke<br>karakter ASCII         |

Simpan file tersebut dengan nama `js_validation_nim.html`

# TODO
- [x] Content
- [x] Second pass
- [x] Proof read
- [ ] Appendix