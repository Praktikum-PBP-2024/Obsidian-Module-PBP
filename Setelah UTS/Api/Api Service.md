Dalam file `ApiService.kt` kita dapat mendefinisikan interface antara client [[Retrofit]] dan API server.


Berikut merupakan contoh API method


| Key      | Type   |
| -------- | ------ |
| username | String |
| password | String |

```kotlin
package com.example.request  
  
import retrofit2.Call  
import retrofit2.http.Body  
import retrofit2.http.Field  
import retrofit2.http.FormUrlEncoded  
import retrofit2.http.POST  
  
interface ApiService {  
  
    @FormUrlEncoded  
    @POST("login")  
    fun login(  
        @Field("username") username: String,  
        @Field("password") password: String  
    ): Call<LoginResponse>  
}
```
