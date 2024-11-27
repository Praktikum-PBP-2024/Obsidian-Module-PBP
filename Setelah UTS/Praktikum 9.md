# UI Compose


## What the hell is that `onValueChange = {member = it}`? | Intro to Lambda Function in Kotlin
Mari kita breakdown secara perlahan. Silahkan hover di `onValueChange`.

```powershell
value-parameter onValueChange: (String) -> Unit
-----------------------------------------------
the callback that is triggered when the input service updates the text. An updated text comes as a parameter of the callback
```

Hint dari intellisense di atas memberikan informasi `onValueChange` bertipe `(String) -> Unit`. Ini merupakan tipe data function yang menerima satu argumen `String` dan mereturn sebuah `Unit`[1]. Lebih tepatnya lagi ini adalah fungsi lambda kotlin. Di kotlin untuk mendefinisikan lambda dapat ditulis sebagai berikut

```kotlin
{ x, y -> x + y } // Lambda with two parameters (x and y) 
{ x -> x * x } // Lambda with one parameter
```

Contoh di atas merupakan varian yang parameter fungsinya ditulis secara eksplisit. Bagaimana dengan implisit? Khusus untuk implisit dengan satu parameter, kotlin menggunakan keyword it sebagai cara untuk mengakses argumen pertama. Berikut merupakan fungsi kuadrat yang ditulis dengan style implisit ini

```kotlin
{ it * it } // Implicit lamba function
```

Bentuknya sudah mulai mirip dengan `onValueChange = {member = it}`. Singkatnya ini merupakan lambda function yang merubah attribute `member` [2] dengan argumen pertama yang disuplai ketika `onValueChange` di panggil.


[1] `Unit`? Tipe data apa itu? Di fungsi yang kita define kita tidak mereturn apa apa padahal. Jika kamu menduga `Unit` adalah `void` di C anda benar.

[2] **attribute** `member`? Bagaimana lambda function bisa membaca dan mengubah attribute dari suatu object? .... The real thing is... lambda function merupakan sebuah objek... dan sebelum fungsi tersebut

> *Sejujurnya style syntax kotlin bisa dibilang unik dan fancy, tapi menurutku straight up stupid dari sisi readibility. Arrow function yang tujuannya compacy is much better untuk menandakan sebuah fungsi. Sure* `{/* code here */}` *looks clean AF, BUT WHAT THE FUCK IS IT MEANS.* `() => {}` *so much better in term of meaning and readibility ?*

