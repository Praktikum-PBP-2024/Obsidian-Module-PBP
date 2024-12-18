

```kotlin
package com.example.request

import okhttp3.Interceptor
import okhttp3.OkHttpClient
import okhttp3.Response
import retrofit2.Retrofit
import retrofit2.converter.gson.GsonConverterFactory

public class Client {
    companion object {

        var apiService: ApiService = rebuild_client("No Token")
        fun rebuild_client (token: String): ApiService {
            val client = OkHttpClient.Builder()
                .addInterceptor(ServiceInterceptor(token))
                .build()

            apiService = Retrofit.Builder()
                .client(client)
                .baseUrl("https://pbp-api.shariyl.cloud/api/")
                .addConverterFactory(GsonConverterFactory.create())
                .build()
                .create(ApiService::class.java)

            return apiService
        }
    }

    class ServiceInterceptor(token: String?) : Interceptor {
        var token = token
        override fun intercept(chain: Interceptor.Chain): Response  = chain.run {
            proceed(
                request()
                    .newBuilder()
                    .addHeader("Authorization", "Bearer " + token)
                    .build()
            )
        }
    }
}
```