# Introduction to Cross-Platform Mobile Application Development Framework

Pengembangan aplikasi mobile lintas platform mengacu pada proses pembuatan aplikasi yang dapat berjalan di beberapa sistem operasi (seperti iOS dan Android) dengan menggunakan satu basis kode.

## Keuntungan:
- Code Reusability: Menulis kode sekali, digunakan di mana-mana
- Cost-Effective: Mengurangi kebutuhan tim terpisah untuk setiap platform
- Reduced time-to-market: Proses pembangunan dan pembaruan lebih cepat
- Consistency: Memberikan pengalaman pengguna yang seragam di berbagai platform

## Tantangan:
- Performance Limitations: Mungkin tidak setara dengan aplikasi native untuk tugas yang membutuhkan banyak sumber daya
- Platform-Specific Features: Beberapa fitur native mungkin sulit diakses atau membutuhkan penyesuaian tambahan
- UI/UX Variability: Menyediakan tampilan dan nuansa yang benar-benar native di semua platform bisa menjadi tantangan

## Jenis
- Web-based Mobile Apps: codebase di server, UI dipanggil melalui URL menggunakan komponen webview
- Hybrid Mobile Apps: codebase di device, diinstal sekaligus dengan aplikasi
- Cross-platform Mobile Apps: codebase dituliskan menggunakan bahasa pemrograman tertentu dan dirender menyesuaikan dengan target platformnya

## Kerangka kerja populer:
- Flutter (dart)
- React Native (JSX)
- Xamarin (C#)
- Ionic (HTML, CSS, JS)
- Apache Cordova (HTML, CSS, JS)
- Unity (C#, Lua)

# Praktikum

![[Pasted image 20241127023918.png]]


## Modifikasi 1

`App.kt`
```kotlin
import androidx.compose.runtime.*  
  
@Composable  
fun App() {  
    Login_1()  
}
```


`Login_1.kt` (buat file baru)
```kotlin

import androidx.compose.foundation.Image  
import androidx.compose.foundation.border  
import androidx.compose.foundation.text.BasicTextField  
import androidx.compose.ui.graphics.Color  
import androidx.compose.ui.text.TextStyle  
import androidx.compose.ui.text.font.FontWeight  
import androidx.compose.ui.text.input.VisualTransformation  
import org.jetbrains.compose.resources.painterResource  
import androidx.compose.material.*  
import androidx.compose.foundation.layout.*  
import androidx.compose.runtime.*  
import androidx.compose.ui.*  
  
import androidx.compose.ui.unit.dp  
  
@Composable  
fun Login_1() {  
    MaterialTheme {  
        var showContent by remember { mutableStateOf(false) }  
        var username by remember { mutableStateOf("") }  
        var password by remember { mutableStateOf("") }  
        Column(  
            modifier = Modifier  
                .fillMaxSize()  
                .padding(16.dp),  
            horizontalAlignment = Alignment.CenterHorizontally,  
            verticalArrangement = Arrangement.Center  
        ) {  
            Image(  
                painter = painterResource(Res.drawable.compose_multiplatform),  
                contentDescription = "Logo",  
                modifier = Modifier.size(150.dp)  
            )  
            Spacer(modifier = Modifier.height(32.dp))  
            BasicTextField(  
                value = username,  
                onValueChange = { username = it },  
                textStyle = TextStyle(fontWeight = FontWeight.Normal),  
                modifier = Modifier  
                    .fillMaxWidth()  
                    .border(1.dp, Color.Gray)  
                    .padding(16.dp),  
                decorationBox = { innerTextField ->  
                    Box(Modifier.padding(8.dp)) {  
                        if (username.isEmpty()) {  
                            Text("Username", style = TextStyle(color = Color.Gray))  
                        }  
                        innerTextField()  
                    }  
                }            )  
            Spacer(modifier = Modifier.height(16.dp))  
            BasicTextField(  
                value = password,  
                onValueChange = { password = it },  
                textStyle = TextStyle(fontWeight = FontWeight.Normal),  
                modifier = Modifier  
                    .fillMaxWidth()  
                    .border(1.dp, Color.Gray)  
                    .padding(16.dp),  
                visualTransformation = VisualTransformation.None,  
                decorationBox = { innerTextField ->  
                    Box(Modifier.padding(8.dp)) {  
                        if (password.isEmpty()) {  
                            Text("Password", style = TextStyle(color = Color.Gray))  
                        }  
                        innerTextField()  
                    }  
                }            )  
            Spacer(modifier = Modifier.height(32.dp))  
            Button(  
                onClick = { /* Handle sign in logic */ },  
                modifier = Modifier.fillMaxWidth()  
            ) {  
                Text("Sign In", modifier = Modifier.padding(8.dp))  
            }  
        }    
    }  
}
```



## Modifikasi 2 | Menggunakan navigator

`App.kt`
```kotlin

import androidx.compose.runtime.*  
import cafe.adriel.voyager.navigator.Navigator  
  
@Composable  
fun App() {  
    Navigator(  
        screen = Login()  
    )  
}
```


`Login_2.kt` (buat file baru)
```kotlin
import androidx.compose.material.*  
import androidx.compose.foundation.layout.*  
import androidx.compose.runtime.*  
import androidx.compose.ui.*  
  
import androidx.compose.foundation.Image  
import androidx.compose.foundation.border  
import androidx.compose.foundation.text.BasicTextField  
import androidx.compose.ui.graphics.Color  
import androidx.compose.ui.text.TextStyle  
import androidx.compose.ui.text.font.FontWeight  
import androidx.compose.ui.text.input.VisualTransformation  
  
import org.jetbrains.compose.resources.painterResource  
import androidx.compose.ui.unit.dp  
import cafe.adriel.voyager.core.screen.Screen  
import cafe.adriel.voyager.navigator.LocalNavigator  
import cafe.adriel.voyager.navigator.currentOrThrow   
  
class Login_2() : Screen {  
    @Composable  
    override fun Content() {  
        val navigator = LocalNavigator.currentOrThrow // baru  
        MaterialTheme {  
            var showContent by remember { mutableStateOf(false) }  
            var username by remember { mutableStateOf("") }  
            var password by remember { mutableStateOf("") }  
            Column(  
                modifier = Modifier  
                    .fillMaxSize()  
                    .padding(16.dp),  
                horizontalAlignment = Alignment.CenterHorizontally,  
                verticalArrangement = Arrangement.Center  
            ) {  
                Image(  
                    painter = painterResource(Res.drawable.compose_multiplatform),  
                    contentDescription = "Logo",  
                    modifier = Modifier.size(150.dp)  
                )  
                Spacer(modifier = Modifier.height(32.dp))  
                BasicTextField(  
                    value = username,  
                    onValueChange = { username = it },  
                    textStyle = TextStyle(fontWeight = FontWeight.Normal),  
                    modifier = Modifier  
                        .fillMaxWidth()  
                        .border(1.dp, Color.Gray)  
                        .padding(16.dp),  
                    decorationBox = { innerTextField ->  
                        Box(Modifier.padding(8.dp)) {  
                            if (username.isEmpty()) {  
                                Text("Username", style = TextStyle(color = Color.Gray))  
                            }  
                            innerTextField()  
                        }  
                    }            )  
                Spacer(modifier = Modifier.height(16.dp))  
                BasicTextField(  
                    value = password,  
                    onValueChange = { password = it },  
                    textStyle = TextStyle(fontWeight = FontWeight.Normal),  
                    modifier = Modifier  
                        .fillMaxWidth()  
                        .border(1.dp, Color.Gray)  
                        .padding(16.dp),  
                    visualTransformation = VisualTransformation.None,  
                    decorationBox = { innerTextField ->  
                        Box(Modifier.padding(8.dp)) {  
                            if (password.isEmpty()) {  
                                Text("Password", style = TextStyle(color = Color.Gray))  
                            }  
                            innerTextField()  
                        }  
                    }            )  
                Spacer(modifier = Modifier.height(32.dp))  
                Button(  
                    onClick = { navigator.push(Home()) }, // baru  
                    modifier = Modifier.fillMaxWidth()  
                ) {  
                    Text("Sign In", modifier = Modifier.padding(8.dp))  
                }  
            }        
        }    
    }  
}
```

`Home.kt`

```kotlin
import androidx.compose.animation.AnimatedVisibility  
import androidx.compose.foundation.Image  
import androidx.compose.foundation.border  
  
import androidx.compose.foundation.lazy.LazyColumn  
import androidx.compose.foundation.lazy.items  
import androidx.compose.foundation.text.BasicTextField  
  
  
import androidx.compose.ui.graphics.Color  
import androidx.compose.ui.text.TextStyle  
import androidx.compose.ui.text.font.FontWeight  
import androidx.compose.ui.text.input.TextFieldValue  
import androidx.compose.ui.text.input.VisualTransformation  
import org.jetbrains.compose.resources.painterResource  
import org.jetbrains.compose.ui.tooling.preview.Preview  
  
import androidx.compose.material.*  
import androidx.compose.foundation.layout.*  
import androidx.compose.runtime.*  
import androidx.compose.ui.*  
  
import androidx.compose.ui.unit.dp  
import cafe.adriel.voyager.core.screen.Screen  
import cafe.adriel.voyager.navigator.LocalNavigator  
import cafe.adriel.voyager.navigator.currentOrThrow  
  
  
class Home() : Screen {  
    @Composable  
    override fun Content() {  
        MaterialTheme {  
            Column (modifier = Modifier.fillMaxSize()) {  
                Text("Welcome to Homepage")  
            }  
        }    }  
}
```