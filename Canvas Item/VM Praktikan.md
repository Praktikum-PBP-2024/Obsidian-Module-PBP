# VM Praktikan

^b306e4

VM yang diberikan kepada praktikan untuk digunakan secara bebas untuk mencoba mendeploy aplikasi yang sudah dikerjakan. ^f076ca

VM Spec yang diberikan:

| Spec    | Value  |
| ------- | ------ |
| CPU     | 4 Vcpu |
| RAM     | 2 GiB  |
| Storage | 10 GiB |

Untuk mengakses vm dilakukan dengan cara ini:

contoh nim mahasiswa: $24060121130\underline{063}$

Pertama Ambil 3 digit terakhir, untuk contoh diatas: $063$, kita akan sebut ini sebagai $n$

Lalu lakukan kalkulasi sederhana dengan menambahkan $n$ dengan $22000$
$$\text{port} = 22000 + n = 22063$$

untuk mengakses ssh akses dengan command ssh seperti ini

```sh
ssh atmin@nim.shariyl.cloud -p port
```

atau jika menggunakan contoh diatas

```sh
ssh atmin@24060121130063.shariyl.cloud -p 22063
```

untuk mengakses web server cukup mengakses

https://nim.shariyl.cloud

atau jika menggunakan contoh

https://24060121130063.shariyl.cloud