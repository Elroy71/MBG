# Execution Plan

- [x] Open and read `https://bukaolshop.com/api-dokumentasi/?javascript#penjelasan-open-api`
  - [x] Scroll and capture screenshots
  - [x] Extract all text, endpoints, parameters, and code examples
- [x] Open and read `https://bukaolshop.com/api-dokumentasi/?php#closed-api`
  - [x] Scroll and capture screenshots
  - [x] Extract all text, endpoints, parameters, and code examples
- [x] Compile findings and report back

## Findings so far:
- The website is a standard Slate API documentation with a 3-column layout.
- The `javascript` and `php` tabs toggle visibility of code blocks.
- Code blocks are encapsulated in `div.highlight` elements, which contain `pre` elements with classes like `tab-javascript`, `tab-php`, and `tab-json`.
- Hidden elements (e.g., PHP blocks when JS is active) return empty string on `innerText` but can be extracted using `textContent`.
- Successfully extracted both Javascript and PHP documentation.

## Extracted API Documentation
(Saved to scratchpad. Scroll down to view the full extracted documentation)

<!-- DOCUMENTATION START -->
# Welcome Developer

Selamat datang di dokumentasi API bukaOlshop. Anda bisa menggunakan API bukaOlshop untuk mengelola berbagai fitur utama pada aplikasi bukaOlshop seperti produk, transaksi, member dan kategori.

Version 1.1

> Pembagian Endpoint
Pada API bukaOlshop, terdapat dua tipe API, yaitu Open API dan Closed API. Penjelasan keduanya bisa dilihat disini.


## Penjelasan Open API

Open API merupakan endpoint yang dapat pemilik olshop gunakan untuk mengakses data-data pada server bukaOlshop tanpa resiko di sisi keamanan akun. Open API ini dapat anda gunakan pada html di apk olshop langsung untuk keperluan mendapatkan data produk, kategori, transaksi, dan lain-lain.

Open API memungkinkan penyedia jasa desain halaman HTML untuk mengkostum tampilan sesuai permintaan client tanpa perlu meminta API key yang digunakan di Closed API, sehingga menghilangkan potensi peretasan pada akun pemilik olshop.

Open API dapat diakses secara unlimited pada paket PRO dan BISNIS, untuk paket LITE dan FREE terbatas hanya 100 request perhari.


## Penjelasan Closed API

Closed API merupakan endpoint yang memerlukan API key untuk mengakses data dan mengubah data di server bukaOlshop. API Key yang digunakan untuk mengakses Closed API ini sangat rentan dan harus di jaga dengan baik dan tidak diberikan ke siapapun karena endpoint ini dapat digunakan untuk menambah saldo member. Gunakan Closed API ini jika anda paham pemograman dan implementasi API, tidak disarankan untuk memberikan API key ke layanan pihak ketiga.

Closed API memiliki rate limit yang bisa dilihat disini


# OPEN API

Dokumentasi Open API.


# Main Endpoint

Berikut ini merupakan URL utama endpoint pada Open API bukaOlshop:

https://openapi.bukaolshop.net/v1

Anda harus menambahkan path tambahan sesuai bagian yang ingin anda request. Contoh: jika anda ingin mendapatkan list produk, maka url akan menjadi:

https://openapi.bukaolshop.net/v1/app/produk

Walaupun Open API ini dapat diletakkan dimanapun di HTML, kami tetap mewajibkan untuk menyertakan token didalam tiap request untuk membedakan tiap aplikasi.

Walaupun tidak ada resiko keamanan yang berarti, kami tidak menyarankan anda menyebarkan link endpoint yang terdapat token olshop anda ke tempat publik seperti di dalam grup.

> Semua request ke endpoint Open API ini dilakukan melalui method GET.

Cara menambahkan token ke URL endpoint


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET", "https://openapi.bukaolshop.net/v1/app/produk?token=xxxxxxxx", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      //this.readyState == 4 artinya request telah selesai
      //Hasil json berada di this.responseText
      console.log(this.responseText);
    }
};
xmlHttpRequest.send();
```

Contoh URL jika ada parameter request tambahan, misal ke page selanjutnya


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardhttps://openapi.bukaolshop.net/v1/app/produk?token=xxxxxxxx&page=2
```

> Token dapat didapatkan di aplikasi bukaOlshop versi terbaru, dibagian Tab TOKO, klik API & Callback, pindah kehalaman API, disitu anda akan mendapatkan token pada bagian Open API.


# GET DATA APLIKASI


## GET Daftar Produk

Contoh Request dengan javascript


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET", "https://openapi.bukaolshop.net/v1/app/produk?token=xxxxxxxx&page=1", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      console.log(this.responseText);
    }
};
xmlHttpRequest.send();
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "page": 1,
  "data": [
    {
      "id_produk": "2046567",
      "id_kategori": "2",
      "nama_produk": "pulsa telkom 20rb",
      "harga_produk": 21000,
      "harga_produk_asli": 0,
      "deskripsi_singkat": "",
      "deskripsi_panjang": "pulsa telkom",
      "kondisi_produk": "Ready Stock",
      "status_produk": "live",
      "stok": 600,
      "berat": 0,
      "tanggal": "2023-07-22 00:01:38",
      "ukuran": null,
      "warna": null,
      "gambar_utama": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/112299/441903822j.jpg",
      "list_gambar": [
        "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/112299/441903822j.jpg"
      ],
      "url_produk": "https://olshopgue.bukaolshop.site/produk/omni-2046567"
    },
    {
      "id_produk": "277074",
      "id_kategori": "2",
      "nama_produk": "Baju baru",
      "harga_produk": 40000,
      "harga_produk_asli": 0,
      "deskripsi_singkat": "desk singkat",
      "deskripsi_panjang": "desk panjang",
      "kondisi_produk": "Baru",
      "status_produk": "gangguan",
      "stok": 23,
      "berat": 100,
      "tanggal": "2020-11-16 01:26:27",
      "ukuran": ["L","M","XL"],
      "warna": ["Ungu","Biru","Hitam"],
      "gambar_utama": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/440277426c.jpg",
      "list_gambar": [
        "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/440277426c.jpg",
        "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/512421523d.jpg"
      ],
      "url_produk": "https://olshopgue.bukaolshop.site/produk/bag-277074"
    }
  ]
}
```

Summary: Daftar Produk

Description: Endpoint ini berfungsi untuk mendapatkan daftar produk yang ada di aplikasi bukaOlshop anda. Method yang digunakan pada endpoin ini yaitu GET.

Tiap request akan mengirimkan sebanyak 10 data produk. Jika ingin mendapatkan data di halaman selanjutnya, tambahkan parameter page kedalam parameter url endpoint. Parameter page diisi dengan format angka, misal 2, 3, 4 dst.


### HTTP Request

GET /app/produk


### Query Parameters


| Parameter | Wajib | Deskripsi | Tipe |
| --- | --- | --- | --- |
| token | Ya | Token dapat didapatkan di aplikasi bukaOlshop. | String |
| page | Ya | Posisi daftar halaman produk. | Integer |
| id_kategori | Tidak | Filter produk berdasarkan id_kategori | Integer |
| total_data | Tidak | Jumlah data yang dikirim perhalaman, isi dengan kelipatan 10. | Integer |
| cari_nama_produk | Tidak | Cari berdasarkan nama produk, pastikan hanya huruf, angka dan spasi | String |
| use_raw_html | Tidak | Berfungsi untuk mendapatkan deskripsi panjang tanpa menghilangkan tag html. Pastikan script anda dapat memproses teks dengan double/single quote atau teks dengan format html. | Boolean |

> Penjelasan total_data
Anda bisa menentukan berapa jumlah data yang server bukaOlshop kirim dalam sekali request. Nilai yang diterima yaitu kelipatan 10 sampai maksimal 100. Jika anda tidak mengisi bagian ini, maka default data yang dikirim yaitu 10 data.

Contoh, jika anda mengisi nilai 50, make page 1 akan menampilkan 50 data, page 2 juga akan 50 data, begitu seterusnya.


## GET Daftar Kategori

Contoh Request dengan javascript


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET", "https://openapi.bukaolshop.net/v1/app/kategori?token=xxxxxxxx", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      console.log(this.responseText);
    }
};
xmlHttpRequest.send();
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "data": [
    {
      "id_kategori": "2",
      "nama_kategori": "Sepatu",
      "gambar_kategori": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/666180ka.jpg",
      "url_kategori": "https://olshopgue.bukaolshop.site/kategori/sepatu-2",
      "tipe_kategori": "utama",
      "sub_kategori": [
        {
          "id_kategori": "5387",
          "nama_kategori": "Celana",
          "gambar_kategori": "https://storage1.bukaolshop.com/images/1/kategori/902346.jpg",
          "url_kategori": "https://olshopgue.bukaolshop.site/kategori/celana-5387",
          "tipe_kategori": "sub"
        },
        {
          "id_kategori": "23533",
          "nama_kategori": "hai",
          "gambar_kategori": "https://storage1.bukaolshop.com/images/1/kategori/902346.jpg",
          "url_kategori": "https://olshopgue.bukaolshop.site/kategori/hai-23533",
          "tipe_kategori": "sub"
        }
      ]
    },
    {
      "id_kategori": "55421",
      "nama_kategori": "Pulsa Cek",
      "gambar_kategori": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/528828ka.jpg",
      "url_kategori": "https://olshopgue.bukaolshop.site/kategori/pulsa-cek-55421",
      "tipe_kategori": "utama",
      "sub_kategori": []
    }
  ]
}
```

Summary: Daftar Kategori

Description: Endpoint ini berfungsi untuk mendapatkan daftar kategori yang ada di aplikasi bukaOlshop anda. Method yang digunakan pada endpoin ini yaitu GET. Semua data kategori akan dikirimkan tiap request.


### HTTP Request

GET /app/kategori


### Query Parameters


| Parameter | Wajib | Deskripsi | Tipe |
| --- | --- | --- | --- |
| token | Ya | Token dapat didapatkan di aplikasi bukaOlshop. | String |
| struktur | Tidak | Jika ingin tidak ada level antara kategori dan sub kategori, isi bagian ini. | Enum flat |


## GET Daftar Kostum Halaman

Contoh Request dengan javascript


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET", "https://openapi.bukaolshop.net/v1/app/kostumpage?token=xxxxxxxx", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      console.log(this.responseText);
    }
};
xmlHttpRequest.send();
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "data": [
    {
      "nama_page": "Nama Halaman",
      "icon_page": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/485323co.png",
      "url_kostum_page": "https://olshopgue.bukaolshop.site/digital/10576"
    },
    {
      "nama_page": "Test Halaman",
      "icon_page": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/698320co.png",
      "url_kostum_page": "https://olshopgue.bukaolshop.site/digital/24672"
    }
  ]
}
```

Summary: Daftar Kostum Halaman

Description: Endpoint ini berfungsi untuk mendapatkan daftar kostum halaman yang ada di aplikasi bukaOlshop anda. Method yang digunakan pada endpoin ini yaitu GET. Semua data kostum halaman akan dikirimkan tiap request.


### HTTP Request

GET /app/kostumpage


### Query Parameters


| Parameter | Wajib | Deskripsi | Tipe |
| --- | --- | --- | --- |
| token | Ya | Token dapat didapatkan di aplikasi bukaOlshop. | String |


## GET Daftar Slide

Contoh Request dengan javascript


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET", "https://openapi.bukaolshop.net/v1/app/slide?token=xxxxxxxx", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      console.log(this.responseText);
    }
};
xmlHttpRequest.send();
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "data": [
    {
      "url_gambar_slide": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/677893sl.jpg",
      "url_tujuan": "https://olshopgue.bukaolshop.site/digital/3"
    },
    {
      "url_gambar_slide": "https://bukaolshop.s3-id-jkt-1.kilatstorage.id/1/897133sl.jpg",
      "url_tujuan": null
    }
  ]
}
```

Summary: Daftar Gambar Slide

Description: Endpoint ini berfungsi untuk mendapatkan daftar gambar slide yang ada di aplikasi bukaOlshop anda. Method yang digunakan pada endpoin ini yaitu GET. Semua data gambar slide akan dikirimkan tiap request.


### HTTP Request

GET /app/slide


### Query Parameters


| Parameter | Wajib | Deskripsi | Tipe |
| --- | --- | --- | --- |
| token | Ya | Token dapat didapatkan di aplikasi bukaOlshop. | String |


# GET DATA USER


## GET Informasi User

Contoh Request dengan javascript


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET",
"https://openapi.bukaolshop.net/v1/user/info?token=xxxxxxxx&token_user={{token_user}}&id_user={{id_user}}", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      // hasil di this.responseText
    }
};
xmlHttpRequest.send();
```

Summary: Mendapatkan Informasi User

Description: Endpoint ini berfungsi untuk mendapatkan data tentang user yang sedang login di aplikasi. Data yang didapatkan berupa nama user, email user, catatan saldo, jumlah saldo, jumlah poin dan lain-lain.

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
    "code": 200,
    "status": "ok",
    "data": {
        "nama_user": "User name",
        "email_user": "user@gmail.com",
        "tanggal_lahir": "1998-11-08",
        "nomor_telepon": "62821288454822",
        "foto_profil": "link gambar",
        "tanggal_daftar": "2020-11-23",
        "status_akun": "aktif",
        "status_email": "belum_verifikasi",
        "nama_membership": "Basic reseller",
        "icon_membership": null,
        "block_akses_membership": "tidak_ada",
        "kode_referral": "MYREF",
        "status_nomor_hp": "belum_verifikasi",
        "jumlah_saldo": "50000",
        "jumlah_poin": "500"
    }
}
```

> Untuk mengakses endpoint ini, apk olshop harus memiliki versi patch 62.5.

> Tiap request harus menyertakan parameter token_user dengan nilai {{token_user}}
dan id_user dengan nilai {{id_user}}

Contoh mengirim token_user dan id_user ke link luar


**Contoh Code (Javascript):**
```javascript
Copy to Clipboard
window.location.replace("http://link_luar.com/cekuser.php?token_user={{token_user}}&id_user={{id_user}}");
```


### HTTP Request

GET /user/info


### Query Parameters


| Parameter | Wajib | Deskripsi | Tipe |
| --- | --- | --- | --- |
| token | Ya | Token dapat didapatkan di aplikasi bukaOlshop. | String |
| token_user | Ya | Isi dengan {{token_user}} | String |
| id_user | Ya | Isi dengan {{id_user}} | String |

> Shortcode {{token_user}} dan {{id_user}} akan otomatis di replace dengan nilai asil nya saat diakses di apk olshop. Shortcode ini baru akan berkerja jika anda meletakkan html langsung didalam aplikasi bukaOlshop, bukan melalui link yang mengarah ke website luar.

> Jika anda ingin mengakses data user melalui link pihak ketiga, atau menggunakan script di server sendiri, maka bisa melalui trik redirect link, contohnya bisa dilihat disamping.


## GET Catatan Saldo/Poin

Contoh Request dengan javascript


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET",
"https://openapi.bukaolshop.net/v1/user/catatan?token=xxxxxxxx&token_user={{token_user}}&id_user={{id_user}}&tipe=saldo", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      // hasil di this.responseText
    }
};
xmlHttpRequest.send();
```

Summary: Mendapatkan Data Catatan Saldo atau Poin

Description: Endpoint ini berfungsi untuk mendapatkan daftar catatan saldo/poin milik member. Tiap request akan mengirimkan sebanyak 10 data catatan. Jika ingin mendapatkan data di halaman selanjutnya, tambahkan parameter page kedalam parameter url endpoint. Parameter page diisi dengan format angka, misal 2, 3, 4 dst.

Secara default, data yang akan ditampilkan yaitu data saldo, jika ingin mendapatkan data poin,
tambahakan parameter tipe=poin pada request.

Jika anda ingin mendapatkan lebih dari 10 data per halaman, tambahkan parameter total_data dengan nilai kelipatan 10, misal 20, 30, 40 dst (max 100).

Pada hasil respon, bukaOlshop menyertakan parameter link_transaksi yang bisa anda letakkan pada link, tujuan link_transaksi yaitu untuk membuka halaman transaksi yang dimiliki oleh catatan saldo.

Contoh Respon tipe saldo


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "page": 1,
  "total_data":10,
  "data": [
    {
      "informasi_catatan": "Pengembalian saldo dari transaksi 875169634 yang otomatis dibatalkan.",
      "jumlah_dana": "3423",
      "tipe_jumlah": "tambah",
      "tipe_mutasi": "transaksi",
      "tanggal": "2023-07-27 15:17:11",
      "saldo_terakhir": "12114",
      "link_transaksi":"https:\/\/olshopgue.bukaolshop.site\/akun\/?page=transaksi&nomor=875169634",
      "nomor_pembayaran":"875169634",
      "catatan_saldo":""
    },
    {
      "informasi_catatan": "Member melakukan transaksi menggunakan saldo (#412512535474)",
      "jumlah_dana": "3423",
      "tipe_jumlah": "kurang",
      "tipe_mutasi": "transaksi",
      "tanggal": "2023-07-27 15:17:11",
      "saldo_terakhir": "8691",
      "link_transaksi":"https:\/\/olshopgue.bukaolshop.site\/akun\/?page=transaksi&nomor=412512535474",
      "nomor_pembayaran":"412512535474",
      "catatan_saldo":""
    }
  ]
}
```

Contoh Respon tipe poin


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "page": 1,
  "data": [
    {
      "kategori_poin": "Transaksi Selesai, Komisi untuk upline dari fitur referral",
      "tipe_jumlah": "tambah",
      "jumlah_poin": "8",
      "tanggal_poin": "2023-03-28 03:57:01",
      "total_poin_terakhir": "123",
      "link_transaksi": "https://olshopgue.bukaolshop.site/akun/?page=transaksi&nomor=96116232910"
    },
    {
      "kategori_poin": "Transaksi Selesai, Komisi untuk upline dari fitur referral",
      "tipe_jumlah": "tambah",
      "jumlah_poin": "62",
      "tanggal_poin": "2023-03-28 03:48:02",
      "total_poin_terakhir": "115",
      "link_transaksi": "https://olshopgue.bukaolshop.site/akun/?page=transaksi&nomor=78373232879"
    }
  ]
}
```


### HTTP Request

GET /user/catatan


### Query Parameters


| Parameter | Wajib | Deskripsi | Tipe |
| --- | --- | --- | --- |
| token | Ya | Token dapat didapatkan di aplikasi bukaOlshop. | String |
| token_user | Ya | Isi dengan {{token_user}} | String |
| id_user | Ya | Isi dengan {{id_user}} | String |
| page | Tidak | Posisi daftar halaman produk. | Integer |
| tipe | Tidak | Tipe catatan | Enum (saldo atau poin) |
| total_data | Tidak | Jumlah data yang dikirim perhalaman, isi dengan kelipatan 10. | Integer |


## GET Daftar Transaksi

Contoh Request dengan javascript


**Contoh Code (Javascript):**
```javascript
Copy to Clipboardvar xmlHttpRequest = new XMLHttpRequest();
xmlHttpRequest.open("GET",
"https://openapi.bukaolshop.net/v1/user/transaksi?token=xxxxxxxx&token_user={{token_user}}&id_user={{id_user}}", true);
xmlHttpRequest.onreadystatechange = function () {
    if (this.readyState == 4 && this.status == 200) {
      // hasil di this.responseText
    }
};
xmlHttpRequest.send();
```

Summary: Mendapatkan Daftar Transaksi User

Description: Endpoint ini berfungsi untuk mendapatkan daftar transaksi milik member. Tiap request akan mengirimkan sebanyak 10 data transaksi. Jika ingin mendapatkan data di halaman selanjutnya, tambahkan parameter page kedalam parameter url endpoint. Parameter page diisi dengan format angka, misal 2, 3, 4 dst.

Jika anda ingin mendapatkan lebih dari 10 data per halaman, tambahkan parameter total_data dengan nilai kelipatan 10, misal 20, 30, 40 dst (max 100).

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
    "code": 200,
    "status": "ok",
    "page": 1,
  "total_data":10,
    "data": [
        {
            "nomor_pembayaran": "875169634",
            "status_bayar": "di batalkan",
            "status_pengiriman": "di batalkan",
            "tanggal": "2023-07-27 15:17:11",
            "nama_barang": "Testing produk",
            "url_gambar_produk": "https:\/\/bukaolshop.s3-id-jkt-1.kilatstorage.id\/1\/67912029.jpg",
            "link_transaksi": "https:\/\/olshopgue.bukaolshop.site\/akun\/?page=transaksi&nomor=875169634"
        },
        {
            "nomor_pembayaran": "274679984",
            "status_bayar": "di batalkan",
            "status_pengiriman": "di batalkan",
            "tanggal": "2023-07-27 15:14:07",
            "nama_barang": "Testing produk",
            "url_gambar_produk": "https:\/\/bukaolshop.s3-id-jkt-1.kilatstorage.id\/1\/67912029.jpg",
            "link_transaksi": "https:\/\/olshopgue.bukaolshop.site\/akun\/?page=transaksi&nomor=274679984"
        }
    ]
}
```


### HTTP Request

GET /user/transaksi


### Query Parameters


| Parameter | Wajib | Deskripsi | Tipe |
| --- | --- | --- | --- |
| token | Ya | Token dapat didapatkan di aplikasi bukaOlshop. | String |
| token_user | Ya | Isi dengan {{token_user}} | String |
| id_user | Ya | Isi dengan {{id_user}} | String |
| page | Tidak | Posisi daftar halaman produk. | Integer |
| total_data | Tidak | Jumlah data yang dikirim perhalaman, isi dengan kelipatan 10. | Integer |

> Jika parameter link_transaksi dibuka didalam apk olshop, maka akan langsung dialihkan ke halaman detail transaksi bawaan apk olshop.


# CLOSED API

Dokumentasi Closed API.


# Main Endpoint

Berikut ini merupakan URL utama endpoint pada API bukaOlshop:

https://bukaolshop.net/api/v1

Anda harus menambahkan path tambahan sesuai bagian yang ingin anda request. Contoh: jika anda ingin mendapatkan detail produk, maka url akan menjadi:

https://bukaolshop.net/api/v1/produk/id


# Authentication

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"URL Endpoint API");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Tipe autentikasi yang digunakan pada API bukaOlshop yaitu : bearer

Anda perlu mengirim header Authorization setiap kali ingin mengakses API bukaOlshop, jika terdapat kesalahan pada autentikasi ini, maka server bukaOlshop akan mengirim respon 401 Unauthorized. Anda bisa mendapatkan API key di aplikasi android bukaOlshop dengan melakukan generate API key.

Berikut ini bentuk autentikasi yang harus dikirim pada header:

Authorization: Bearer API_KEY_ANDA_DISINI

> Harap menjaga baik-baik API key anda, API key bisa dikatakan password yang digunakan untuk mengakses data olshop anda.


# INFORMASI APLIKASI


## GET Informasi Aplikasi

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,
"https://bukaolshop.net/api/v1/aplikasi/info");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "nama_toko": "OlshopTest",
  "nama_aplikasi": "OlshopTest",
  "nama_package": "com.olshopgue",
  "icon_aplikasi": "https://xxxxxxxx/xxx/xxx/xxx/xxx.png",
  "masa_aktif_premium": "2021-09-16",
  "status_premium": "lite",
  "tanggal_daftar_aplikasi": "2019-11-08 20:29:30",
  "telah_verifikasi_identitas": false,
  "email_pemilik_olshop": "cek@gmail.com",
  "nama_pemilik_olshop": "testing user",
  "hp_pemilik_olshop": "082234327658",

}
```

Summary: Informasi Aplikasi Olshop

Description: Endpoint ini berfungsi untuk menampilkan detail informasi aplikasi olshop anda. Tidak ada parameter yang wajib dikirim pada endpoint ini.


### HTTP Request

GET /aplikasi/info


### Query Parameters

Tidak ada parameter


### Responses


| Code | Description |
| --- | --- |
| 200 | ok |


## GET Informasi Limit Request

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,
"https://bukaolshop.net/api/v1/aplikasi/info_limit");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "jumlah_request": 230
}
```

Summary: Informasi Aplikasi Olshop

Description: Endpoint ini berfungsi untuk menampilkan informasi limit request harian aplikasi.
Mengirim request ke endpoint ini tidak menambah limit harian aplikasi anda.


### HTTP Request

GET /aplikasi/info_limit


### Query Parameters

Tidak ada parameter


### Responses


| Code | Description |
| --- | --- |
| 200 | ok |


# PRODUK


## GET Daftar List Produk

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$query=http_build_query(
  array("page"=>'1')
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,
"https://bukaolshop.net/api/v1/produk/list?".$query);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "page": 1,
  "data": [
    {
      "id_barang": "509369",
      "id_kategori": "35023",
      "nama_barang": "Judul produk 1",
      "harga_barang": 5000,
      "kondisi_barang": "Baru",
      "status_produk": "live",
      "stok_barang": 7,
      "berat": 80,
      "tanggal": "2021-02-18 21:09:57",
      "url_gambar_barang": "url gambar"
    },
    {
      "id_barang": "439075",
      "id_kategori": "35023",
      "nama_barang": "Judul produk 2",
      "harga_barang": 6000,
      "kondisi_barang": "Baru",
      "status_produk": "gangguan",
      "stok_barang": 4,
      "berat": 46,
      "tanggal": "2021-01-14 19:33:19",
      "url_gambar_barang": "url gambar"
    }
  ]
}
```

Summary: Daftar Produk

Description: Endpoin ini berfungsi untuk mendapatkan daftar produk yang ada di aplikasi bukaOlshop anda. Method yang digunakan pada endpoin ini yaitu GET, dengan parameter yang wajib di isi yaitu page.

Parameter page ini merupakan halaman data produk, tiap halaman akan menampilkan 10 produk. Anda bisa mengisi parameter ini dengan angka 1 untuk mendapatkan 10 produk terbaru. Untuk melihat daftar produk selanjutnya, anda tinggal mengisi dengan angka 2, 3, 4 dan seterusnya.


### HTTP Request

GET /produk/list


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| page | query | Posisi daftar halaman produk | Yes | Integer |


### Responses


| Code | Description |
| --- | --- |
| 200 | ok |
| 400 | Bad Request, Pastikan anda memasukkan parameter page, isi parameter page tidak boleh 0 atau dibawah 0, dan tidak lebih dari 600. |


## GET Detail Produk

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

// Ganti 1234567 dengan id_barang
$query=http_build_query(
  array("id_barang"=>'1234567')
);

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,
"https://bukaolshop.net/api/v1/produk/id?".$query);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "id_barang": "176941",
  "nama_barang": "Produk 2",
  "harga_barang": 34344,
  "harga_barang_asli": 0,
  "kondisi_barang": "Baru",
  "status_produk": "live",
  "stok_barang": 43,
  "berat": 54,
  "tanggal": "2020-08-08 04:58:48",
  "merek": "",
  "sku": "",
  "ukuran": "",
  "warna": "",
  "id_kategori": "65258",
  "data_kategori": {
    "nama_kategori": "judul kategori",
    "gambar_kategori": "url gambar kategori"
  },
  "harga_grosir": [
    {
      "jumlah": "5",
      "harga": "60000"
    },
    {
      "jumlah": "6",
      "harga": "60000"
    }
  ],
  "lokasi_barang": {
    "id_origin": "43726",
    "nama_pengirim": "Nama pengirim",
    "provinsi": "Bali",
    "kota": "Badung",
    "kecamatan": "Abiansemal",
    "kode_pos": "",
    "no_hp": "082242235573"
  },
  "url_gambar": [
    "url gambar 1",
    "url gambar 2",
    "url gambar 3"
  ]
}
```

Summary: Detail Produk

Description: Endpoint ini berfungsi untuk mendapatkan detail produk anda. Method yang digunakan adalah GET and parameter yang wajib di isi adalah id_barang. Anda dapat menemukan id_barang pada endpoint Daftar Produk atau pada Detail Transaksi.


### HTTP Request

GET /produk/id


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_barang | query | id_barang untuk mendapatkan detail produk | Yes | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, Data produk ditemukan |
| 400 | Not Found, Data produk tidak ditemukan, pastikan id_barang yang anda input sudah benar |


## PATCH Edit Produk

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "id_barang"=>"563226",
  "nama_barang"=>"nama barang baru"
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/produk/id");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'PATCH');
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($post_body));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok - Data berhasil diubah",
  "id_barang": "563226"
}
```

Summary: Edit Produk

Description: Endpoint ini berfungsi untuk mengubah data produk anda. Method yang digunakan adalah PATCH and parameter yang wajib di-isi adalah id_barang. Anda dapat menemukan id_barang pada endpoint Daftar Produk atau pada Detail Transaksi.

Setelah anda memasukkan parameter id_barang, selanjutnya Anda cukup memasukkan parameter yang ingin diubah saja.


### HTTP Request

PATCH /produk/id


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_barang | Body | id_barang wajib diisi | Yes | String |
| nama_barang | Body |  | No | String |
| deskripsi_panjang | Body |  | No | String |
| deskripsi_singkat | Body |  | No | String |
| berat | Body |  | No | Integer |
| jumlah_stok | Body |  | No | Integer |
| status_produk | Body |  | No | String (live / gangguan / closed) |
| kondisi | Body |  | No | String |
| merek | Body |  | No | String |
| dalam_kotak | Body |  | No | String |
| garansi | Body |  | No | String |
| harga_barang | Body |  | No | Integer |
| harga_barang_asli | Body |  | No | Integer |
| sku | Body |  | No | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, Produk berhasil diupdate |
| 400 | Bad Request, Pastikan id_barang telah di isi dengan benar, dan pastikan anda memasukkan minimal 1 parameter tambahan yang ingin diubah |


## DELETE Hapus Produk

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "id_barang"=>"551305",
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/produk/id");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'DELETE');
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($post_body));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok",
   "id_barang": "551305"
 }
```

Summary: Hapus Produk

Description: Endpoint ini berfungsi untuk menghapus produk anda. Method yang digunakan adalah DELETE and parameter yang wajib di-isi adalah id_barang. Anda dapat menemukan id_barang pada endpoint Daftar Produk atau pada Detail Transaksi.


### HTTP Request

DELETE /produk/id


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_barang | Body | id_barang wajib diisi | Yes | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, Data berhasil dihapus |
| 400 | Not Found, Data id_barang yang ada input tidak ditemukan. |


## GET ID Kategori dan Lokasi

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/produk/id_upload");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok",
   "kategori": [
     {
       "id_kategori": "289821",
       "nama_kategori": "Nama kategori 1",
     },
     {
     "id_kategori": "247254",
     "nama_kategori": "Nama kategori 2",
     }
   ],
   "lokasi": [
     {
       "id_lokasi": "289821",
       "nama_pengirim": "Nama lokasi pengiriman 1",
       "tipe_lokasi": "digital",

     },
     {
       "id_lokasi": "289820",
       "nama_pengirim": "Nama lokasi pengiriman 2",
       "tipe_lokasi": "fisik",

     }
   ]
 }
```

Summary: Hapus Produk

Description: Endpoint ini berfungsi mendapatkan data id_kategori dan id_lokasi untuk keperluan upload produk melalui API. Endpoin ini tidak memerlukan parameter tambahan.


### HTTP Request

GET /produk/id_upload


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |


### Responses


| Code | Description |
| --- | --- |
| 200 | ok |


## POST Upload Produk

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
    "id_kategori"=>"26324",
    "id_lokasi"=>"18696",
    "jenis_barang"=>"digital",
    "nama_barang"=>"Ini judul produk API",
    "deskripsi_panjang"=>"ini deskripsi panjang",
    "deskripsi_singkat"=>"Lorem Ipsum is simply dummy text of the printing and typesetting industry. ",
    "harga_barang"=>"23000",
    "berat"=>"0",
    "stok_barang"=>"100",
    "url_gambar_barang_1"=>"https://images.tokopedia.net/img/cache/300-square/hDjmkQ/2024/11/23/9637116a-680b-4b5a-b005-2ee780bec297.jpg",
    "url_gambar_barang_2"=>"https://images.tokopedia.net/img/cache/300-square/VqbcmM/2023/5/13/05a7e448-5a0d-4405-a928-81e126a41419.jpg",
    "caption_catatan"=>"masukkan data nomor",
    "tipe_input"=>"angka_only",
    "harga_modal"=>"20000",
    "harga_barang_asli"=>"25000",
    "catatan_wajib_isi"=>"true",
    "batasi_max"=>"true",
    "produk_digital_khusus"=>"bulk",
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/produk/create");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, $post_body);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok - Data produk berhasil ditambahkan ke daftar antrian upload.Jika tidak ada kendala pada url gambar,produk akan muncul di aplikasi dalam kurun waktu 5-20 menit.Upload produk akan ditunda pada jam padat (5PM - 9PM)",
  "id_antrian": "3708a05bee8d8ffa6860"
   "nama_barang": "Ini judul produk API"
 }
```

Summary: Upload Produk

Description: Endpoint ini berfungsi untuk menambah produk baru pada olshop anda. Method yang digunakan adalah POST.


### HTTP Request

POST /produk/create


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_kategori | Body | id_kategori bisa didapatkan disini | Yes | Integer |
| id_lokasi | Body | id_lokasi bisa didapatkan disini | Yes | Integer |
| jenis_barang | Body | Jenis produk yang ingin diupload, isi dengan "fisik" atau "digital" | Yes | Enum (fisik/digital) |
| nama_barang | Body | Judul produk | Yes | String |
| deskripsi_singkat | Body |  | Yes | String |
| deskripsi_panjang | Body |  | Yes | String |
| harga_barang | Body | Harga produk yang dijual | Yes | Integer |
| stok_barang | Body |  | Yes | Integer |
| url_gambar_barang_1 | Body | URL gambar yang bisa diakses lewat internet | Yes | String |
| url_gambar_barang_2 | Body | URL gambar yang bisa diakses lewat internet | No | String(URL) |
| caption_catatan | Body | Caption catatan pembelian | No | String |
| tipe_input | Body | Tipe input jika jenis produk digital | No | Enum (angka_only/angka_huruf) |
| harga_modal | Body | Harga modal produk | No | Integer |
| harga_barang_asli | Body | Harga produk sebelum diskon (jika ada) | No | Integer |
| catatan_wajib_isi | Body |  | No | Boolean (true/false) |
| batasi_max | Body |  | No | Boolean (true/false) |
| produk_digital_khusus | Body |  | No | Enum ( none / pascabayar / pln_prabayar / bebas_nominal / bulk) |


### Responses


| Code | Description |
| --- | --- |
| 200 | ok - Data produk berhasil ditambahkan ke daftar antrian upload. |
| 400 | Bad Request, pastikan data sudah sesuai. Lihat penjelasannya di key "status" |


# MEMBER


## GET Daftar List Member

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$query=http_build_query(
  array("page"=>'1')
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/member/list?".$query);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok",
   "page": 1,
   "data": [
     {
       "id_user": "289821",
       "email_user": "cek5@gmail.com",
       "nama_user": "Cek5",
       "nomor_telepon": "082366489912",
       "foto_profil": "Url foto profil",
       "status_akun": "aktif",
       "tanggal_daftar": "2020-10-05 05:25:44"
     },
     {
       "id_user": "289820",
       "email_user": "cek4@gmail.com",
       "nama_user": "Cek4",
       "nomor_telepon": "082234327658",
       "foto_profil": "Url foto profil",
       "status_akun": "aktif",
       "tanggal_daftar": "2020-10-05 05:24:54"
     }
   ]
 }
```

Summary: Daftar List Member

Description: Endpoin ini berfungsi untuk mendapatkan daftar member yang ada di aplikasi bukaOlshop anda. Method yang digunakan pada endpoin ini yaitu GET, dengan parameter yang wajib di isi yaitu page.

Anda bisa mengisi parameter ini dengan angka 1 untuk mendapatkan 10 member terbaru. Untuk melihat daftar member selanjutnya, anda tinggal mengisi dengan angka 2, 3, 4 dan seterusnya.


### HTTP Request

GET /member/list


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| page | query | Posisi daftar halaman member | Yes | Integer |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK |


## GET Detail Member

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$query=http_build_query(
  array("email_user"=>'email_user@gmail.com')
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/member/id?".$query);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok",
   "id_user": "130173",
   "email_user": "email@gmail.com",
   "nama_user": "Nama user",
   "tanggal_lahir": "2000-01-01",
   "jenis_kelamin": "Laki-laki",
   "nomor_telepon": "0822882432535",
   "foto_profil": "",
   "status_akun": "verified",
   "kode_referral": "MYTANPA",
   "tanggal_daftar": "2020-09-26 02:16:33",
   "data_alamat": [
     {
       "nama_penerima": "Nama user",
       "kecamatan": "Abiansemal",
       "kota": "Badung",
       "provinsi": "Bali",
       "nomor_telepon": "4949",
       "kode_pos": "80351",
       "alamat_lengkap": "Alamat lengkap user"
     }
   ]
 }
```

Summary: Detail Member

Description: Endpoint ini berfungsi untuk mendapatkan detail member anda. Method yang digunakan adalah GET. Terdapat 2 cara untuk mendapatkan detail member anda, yaitu melalui email atau melalui id_user.

Anda dapat mengisi parameter id_user atau email_user, silahkan pilih salah satu.

Anda dapat menemukan id_user pada endpoint List Member ataupun pada endpoint transaksi.


### HTTP Request

GET /member/id


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_user | query | isi dengan id_user member | No | String |
| email_user | query | isi dengan email_user | No | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, Data ditemukan |
| 400 | Bad Request, Pastikan anda telah mengisi parameter id_user atau email_user, pilih salah satu. |
| 404 | Not Found, data tidak ditemukan |


## GET Saldo Member

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$query=http_build_query(
  array("id_user"=>'xxxxx')
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/member/saldo?".$query);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "id_user": "289820",
  "email_user": "cek4@gmail.com",
  "nama_user": "Nama member",
  "transaksi_terakhir": "2021-04-06 01:58:39",
  "jumlah_saldo": 90000,
  "riwayat_saldo": [
    {
      "informasi_catatan": "Member mendapatkan komisi referral sebagai Downline",
      "jumlah_dana": 10000,
      "tanggal": "2020-10-05 05:14:10"
    }
  ]
}
```

Summary: Informasi Saldo Member

Description: Endpoint ini berfungsi untuk mendapatkan detail saldo yang dimiliki member anda. Method yang digunakan adalah GET. Terdapat 2 cara untuk mendapatkan detail member anda, yaitu melalui email atau melalui id_user.

Anda dapat mengisi parameter id_user atau email_user, silahkan pilih salah satu.


### HTTP Request

GET /member/saldo


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_user | query | isi dengan id_user member | No | String |
| email_user | query | isi dengan email_user | No | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, Data ditemukan |
| 400 | Bad Request, Pastikan anda telah mengisi parameter id_user atau email_user, pilih salah satu. |
| 404 | Not Found, data tidak ditemukan |


## POST Kirim Notifikasi Member

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "email_user"=>"blabla@gmail.com",
  "judul_notifikasi"=>"Judul notifikasi anda",
  "pesan_notifikasi"=>"Pesan notifikasi anda",
  "url_gambar"=>"https://images.bukaolshop.com/developer/1/1ab38188996f95728.png"
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/member/notifikasi");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, $post_body);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "id_user": "289820",
  "status_gambar": "valid",
  "token_notifikasi": "626c3d67-0190-4a8a-b70f-d014223fd533"
}
```

Summary: Kirim Notifikasi ke Member

Description: Endpoint ini berfungsi untuk mengirim notifikasi ke APK olshop member anda. Method yang digunakan adalah POST.

Parameter yang wajib di-isi yaitu id_user atau email_user (pilih salah satu), judul_notifikasi, pesan_notifikasi

Anda juga dapat mengirim gambar yang akan dimuncukan pada notifikasi Android, saat ini gambar hanya bisa muncul pada notifikasi dan belum bisa muncul didalam APK olshop. URL gambar yang diinputkan wajib menggunakan image host yang sudah bukaOlshop sediakan di aplikasi bukaOlshop.


### HTTP Request

POST /member/notifikasi


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_user | query | isi dengan id_user member | No | String |
| email_user | query | isi dengan email_user | No | String |
| judul_notifikasi | body | Isi judul notifikasi | Yes | String |
| pesan_notifikasi | body | Isi pesan notifikasi | Yes | String |
| url_gambar | body | URL gambar notifikasi dari image host bukaOlshop (opsional) | No | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, Data berhasil disimpan |
| 400 | Bad Request, Pastikan anda telah mengisi parameter id_user atau email_user, pilih salah satu. |


## POST Ubah Saldo Member

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "email_user"=>"blabla@gmail.com",
  "tipe"=>"tambah",
  "jumlah"=>20000,
  "notifikasi"=>true
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/member/saldo");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, $post_body);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok - Saldo berhasil ditambah",
   "id_user": "289820",
   "email_user": "emailuser@gmail.com",
   "nama_user": "Nama user",
   "jumlah": 30000,
   "tipe": "tambah",
   "id_perubahan": "456406"
 }
```

Summary: Ubah Saldo Member

Description: Endpoint ini berfungsi untuk mengubah jumlah saldo yang dimiliki member anda. Method yang digunakan adalah POST.

Parameter yang wajib di-isi yaitu id_user atau email_user (pilih salah satu), tipe, dan jumlah.

Jika anda ingin mengirim notifikasi perubahan saldo ini ke user, tambahkan parameter notifikasi dengan nilai true


### HTTP Request

POST /member/saldo


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_user | body | isi dengan id_user member | No | String |
| email_user | body | isi dengan email_user | No | String |
| tipe | body | isi dengan tambah atau kurang | Yes | Enum tambah/kurang |
| jumlah | body | isi dengan jumlah saldo yang ingin ditambah | No | Integer |
| pin | body | Jika ingin memvalidasi perubahan saldo dengan pin member, tambahkan parameter pin yang berisi PIN yang diinputkan oleh member | No | String 6 digit PIN |
| catatan_saldo | body | Catatan/informasi mengenai perubahan saldo | No | String |
| notifikasi | body | Isi dengan nilai true jika anda ingin mengirim notifikasi ke user | No | Boolean |
| judul_notifikasi | body | Isi judul notifikasi (opsional) | No | String |
| pesan_notifikasi | body | Isi pesan notifikasi (opsional) | No | String |

> Jika pengurangan jumlah saldo lebih besar dari pada saldo member sekarang, maka pengurangan akan ditolak, dan anda akan mendapatkan respon 403 - Forbidden.

> Pilih salah satu antara id_user atau email_user, tidak perlu isi kedua parameter tersebut.


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, data saldo berhasil diubah |
| 400 | Bad Request, Pastikan anda telah mengisi parameter id_user atau email_user, pilih salah satu. |
| 403 | Forbidden, Pengurangan lebih besar dari jumlah saldo member |
| 404 | Not Found, data tidak ditemukan |


## POST Konfirmasi TopUp Member

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "token_topup"=>"xxxxxxxxxxxxxxxxxxxx",
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/member/topup");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, $post_body);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok - Saldo berhasil ditambah",
   "id_user": "289820",
   "email_user": "emailuser@gmail.com",
   "nama_user": "Nama user",
   "jumlah": 30000,
   "tipe": "tambah",
   "id_perubahan": "456406"
 }
```

Summary: Konfirmasi Penambahan topup saldo member

Description: Endpoint ini berfungsi untuk melakukan konfirmasi topup saldo member anda, anda memerlukan parameter token_topup yang hanya bisa didapatkan dengan melakukan override halaman topup saldo. Method yang digunakan adalah POST.

Parameter yang wajib di-isi yaitu token_topup.

bukaOlshop menambahkan kolom parameter baru bernama validasi_jumlah_topup. Kolom ini berfungsi untuk memastikan kembali jumlah topup yang akan ditambahkan ke saldo user. Jika nilai validasi_jumlah_topup berbeda dengan nilai total_topup yang ada di server bukaOlshop, maka topup akan ditolak. Fitur ini untuk memastikan tidak ada perbedaan data antara server anda dengan server bukaOlshop


### HTTP Request

POST /member/topup


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| token_topup | body | Isi dengan token_topup. Nilai token_topup hanya bisa anda dapatkan jika melakukan override halaman topup. | Yes | String |
| validasi_jumlah_topup | body | Isi dengan total_topup. Nilai total_topup hanya bisa anda dapatkan jika melakukan override halaman topup. | No | Integer |
| notifikasi | body | Isi dengan nilai true jika anda ingin mengirim notifikasi ke user | No | Boolean |
| judul_notifikasi | body | Isi judul notifikasi (opsional) | No | String |
| pesan_notifikasi | body | Isi pesan notifikasi (opsional) | No | String |

> Jumlah topup yang akan masuk ke member anda yaitu dari perhitungan jumlah topup + kode unik.


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, data saldo berhasil diubah |
| 400 | Bad Request, Parameter token_topup belum di isi |
| 404 | Not Found, data tidak ditemukan |
| 400 | gagal - Jumlah konfirmasi topup anda tidak cocok dengan jumlah yang ada di server bukaOlshop |


# CHAT


## POST Kirim pesan

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "id_user"=>"xxxx",
  "pesan_teks"=>"ini adalah pesan anda"
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/chat/create");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, $post_body);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
    "code": 200,
    "status": "ok - Pesan berhasil dikirim",
    "id_user": "130173",
    "email_user": "emailuser@gmail.com",
    "nama_user": "Nama User",
    "id_barang": "257304",
    "pesan_teks": "Assalamualaikum, Apa kabar?"
  }
```

Summary: Kirim pesan ke member

Description: Endpoint ini berfungsi untuk mengirim pesan ke member anda.

Parameter yang wajib di-isi yaitu id_user atau email_user (pilih salah satu), dan parameter pesan_teks.

Parameter yang wajib di-isi yaitu token_topup.

> Secara default, pesan akan dikirim sebagai chat umum. Jika anda ingin mengirim sebagai chat produk, maka anda perlu memasukkan parameter id_barang.


### HTTP Request

POST /chat/create


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_user | body | isi dengan id_user member | Yes | String |
| pesan_teks | body | Masukkan pesan anda disini | Yes | String |
| id_barang | body | Masukkan id_barang jika anda ingin mengirim sebagai chat produk. | No | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, Pesan berhasil dikirim |
| 400 | Bad Request, Pastikan anda telah mengisi parameter id_user. Pastikan anda juga sudah mengisi parameter pesan_teks. |
| 404 | Not Found, data tidak ditemukan |


# TRANSAKSI


## GET Daftar List Transaksi

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$query=http_build_query(
  array("page"=>'1')
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/transaksi/list?".$query);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
    "code": 200,
    "status": "ok",
    "data": [
      {
        "nomor_pembayaran": "2853130173354",
        "id_user": "130173",
        "status_bayar": "pending",
        "status_pengiriman": "belum diproses",
        "tanggal": "2020-10-12 01:15:04"
      },
      {
        "nomor_pembayaran": "81168130173359",
        "id_user": "130173",
        "status_bayar": "lunas",
        "status_pengiriman": "selesai",
        "tanggal": "2020-10-05 05:31:56"
      }
    ]
  }
```

Summary: Daftar Transaksi

Description: Endpoint ini berfungsi untuk menampilkan daftar transaksi pada aplikasi olshop anda. Method yang digunakan pada endpoint ini yaitu GET.

Parameter yang wajib di-isi adalah parameter page. Tiap page akan menampilkan 10 transaksi dengan urutan waktu terbaru. Anda dapat mengisi parameter page ini dengan angka (dimulai dari angka 1).


### HTTP Request

GET /transaksi/list


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| page | query | Posisi daftar halaman transaksi | Yes | Integer |
| id_user | body | isi dengan id_user member | Yes | String |
| filter_status | query | Filter berdasarkan status transaksi, pending,diproses,atau lunas | No | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, data berhasil ditemukan. |
| 400 | Bad Request, Pastikan anda telah mengisi parameter page, nilai parameter tidak boleh dibawah 1 dan tidak lebih dari 600 |


## GET Detail Transaksi

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$query=http_build_query(
  array("nomor_pembayaran"=>'xxxxxxxxxxxxx')
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/transaksi/id?".$query);
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
   "code": 200,
   "status": "ok",
   "nomor_pembayaran": "74879326",
   "id_user": "2343",
   "status_bayar": "lunas",
   "status_pengiriman": "diproses",
   "bank_penerima": "BCA",
   "terakhir_update": "2021-02-27 19:48:38",
   "tanggal_buat": "2021-02-24 04:16:11",
   "potongan": 0,
   "kode_unik": 0,
   "total_membership": 15500,
   "total_transaksi": 1079949,
   "data_pesanan": [
     {
       "ekspedisi": "JNE OKE",
       "ongkos_kirim": 43000,
       "nama_pengirim": "Nama saya 1",
       "provinsi": "Riau",
       "kota": "Pekanbaru",
       "kecamatan": "Bukit Raya",
       "no_hp": "085279462345",
       "kode_pos": "28112",
       "data_produk": [
         {
           "id_transaksi": "xxxxx",
           "id_barang": "513039",
           "nama_barang": "barang 1",
           "jumlah_barang": 1,
           "total_harga": 10000,
           "catatan": "catatan pesanan",
           "nomor_resi": "xxxxxxxxxxxxxxxxxxxx",
           "catatan_tambahan": {
             "nama_varian": "Varian 123",
             "opsi": [
                 "UNGU","MERAH","BIRU"
               ]
             }
         }
       ]
     },
     {
       "ekspedisi": "JNE OKE",
       "ongkos_kirim": 12000,
       "nama_pengirim": "Nama saya 2",
       "provinsi": "Bali",
       "kota": "Badung",
       "kecamatan": "Abiansemal",
       "no_hp": "085723453462",
       "kode_pos": "80351",
       "data_produk": [
         {
           "id_transaksi": "xxxxx",
           "id_barang": "196552",
           "nama_barang": "barang 2",
           "jumlah_barang": 1,
           "total_harga": 50000,
           "catatan": " \nVarian : Vairan 1\n",
             "nomor_resi": ""
         },
         {
           "id_transaksi": "xxxxx",
           "id_barang": "196552",
           "nama_barang": "barang 3",
           "jumlah_barang": 1,
           "total_harga": 949449,
           "catatan": " \nVarian : Varian 3\n",
           "nomor_resi": "123456789"
         }
       ]
     }
   ]
 }
```

Summary: Detail Transaksi

Description: Endpoint ini berfungsi untuk mendapatkan detail transaksi pada olshop anda. Method yang digunakan pada endpoint ini yaitu GET.

Anda wajib memasukkan parameter nomor_pembayaran. Nomor pembayaran dapat anda temukan di endpoint list transaksi atau di aplikasi bukaOlshop anda.


### HTTP Request

GET /transaksi/id


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| nomor_pembayaran | query | Nomor pembayaran transaksi | Yes | String |


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, data berhasil ditemukan. |
| 400 | Bad request, pastikan anda telah memasukkan parameter nomor_pembayaran dengan benar |
| 404 | Not Found, data nomor pembayaran yang anda masukkan tidak ditemukan |


## PATCH Edit Status Transaksi

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "nomor_pembayaran"=>"xxxxxxxxxxxxx",
  "status_transaksi"=>"lanjut"
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/transaksi/id");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'PATCH');
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($post_body));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok",
  "nomor_pembayaran": "74879326",
  "statu_bayar_awal": "lunas",
  "status_pengiriman_awal": "diproses",
  "status_bayar_terbaru": "lunas",
  "status_pengiriman_terbaru": "dikirim"
}
```

Summary: Edit Status Transaksi

Description: Endpoint ini berfungsi untuk mengubah status transaksi pada olshop anda.


### HTTP Request

PATCH /transaksi/id


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| nomor_pembayaran | body | Nomor pembayaran transaksi | Yes | String |
| status_transaksi | body | Isi dengan nilai lanjut,kembali,selesai,diproses, batal, batal_dan_refund atau lunas | Yes | String |

Penjelasan Parameter

Untuk mengubah status transaksi, Anda cukup memasukkan 2 parameter yaitu:

- nomor_pembayaran
- status_transaksi

> Parameter status_transaksi memiliki 7 nilai yang telah ditetapkan, yaitu lanjut, kembali, lunas, selesai,diproses, batal dan batal_dan_refund.

Berikut penjelasan kelima nilai tersebut:

- lanjut, nilai ini berfungsi untuk melanjutkan status transaksi ke tahap selanjutnya. Contoh, jika metode bayar transaksi menggunakan transfer bank dan memiliki status bayar pending, maka jika anda memasukkan nilai lanjut akan membuat transaksi berubah menjadi lunas, setelah lunas status akan menjadi diproses, dan setelah diproses status akan berubah menjadi dikirim dan seterusnya sampai status pengiriman selesai.
- kembali, nilai ini merupakan kebalikan dari nilai lanjut. Jika anda memasukkan nilai ini, maka status transaksi akan dikembalikan ke tahap sebelumnya. Contoh, jika status transaksi sekarang adalah dikirim, maka status akan berubah menjadi diproses, dan dari status diproses akan dirubah menjadi lunas dan seterusnya.
- lunas, nilai ini merupakan jalan pintas untuk membuat status pembayaran menjadi lunas.
- diproses, nilai ini merupakan jalan pintas untuk membuat status transaksi menjadi diproses.
- selesai, nilai ini merupakan jalan pintas untuk menyelesaikan sebuah transaksi (status pembayaran menjadi lunas dan status pengiriman menjadi selesai.
- batal, nilai ini untuk membuat status transaksi menjadi dibatalkan
- batal_dan_refund, nilai ini untuk membuat status transaksi menjadi dibatalkan dan secara otomatis mengembalikan uang ke saldo member. Refund hanya berlaku jika status bayar transaksi bukan "di batalkan"

Nilai-nilai pada parameter status_transaksi diatas dibuat agar tidak terjadi kesalahan pada input yang anda lakukan.


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, perubahan berhasil dilakukan. |
| 400 | Bad Request, pastikan ada telah mengisi parameter nomor_pembayaran dan status_transaksi |
| 404 | Not Found, data tidak ditemukan |

> Parameter status_bayar_awal dan status_pengiriman_awal merupakan status transaksi sebelum adanya perubahan. Parameter status_bayar_terbaru dan status status_pengiriman_terbaru merupakan status transaksi terbaru yang mana perubahan telah dilakukan.


## PATCH Edit Resi Transaksi

Contoh request dengan PHP


**Contoh Code (PHP):**
```php
Copy to Clipboard$token="API KEY ANDA";
$header=  array("Authorization: Bearer ".$token );

$post_body=array(
  "id_transaksi"=>"xxxx",
  "nomor_resi"=>"xxxxxxxxxxxxxxxxxxxx"
);
$ch = curl_init();
curl_setopt($ch, CURLOPT_URL,"https://bukaolshop.net/api/v1/transaksi/id");
curl_setopt($ch, CURLOPT_HTTPHEADER, $header);
curl_setopt($ch, CURLOPT_CUSTOMREQUEST, 'PATCH');
curl_setopt($ch, CURLOPT_POST, TRUE);
curl_setopt($ch, CURLOPT_POSTFIELDS, json_encode($post_body));
curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);

$hasil = curl_exec($ch);
curl_close ($ch);
echo $hasil;
```

Contoh Respon


**Contoh Code (JSON):**
```json
Copy to Clipboard{
  "code": 200,
  "status": "ok - nomor resi berhasil diubah",
}
```

Summary: Edit Resi Transaksi

Description: Endpoint ini berfungsi untuk mengubah nomor resi transaksi pada olshop anda.


### HTTP Request

PATCH /transaksi/id


### Query Parameters


| Name | Located in | Description | Required | Type |
| --- | --- | --- | --- | --- |
| id_transaksi | body | Nomor id_transaksi | Yes | String |
| nomor_resi | body | Isi dengan nomor resi anda | Yes | String |
| harga_modal | body | Isi dengan harga modal produk | No | Integer/Number |

> Parameter id_transaksi dapat anda temukan di endpoint GET Detail Transaksi


### Responses


| Code | Description |
| --- | --- |
| 200 | OK, perubahan berhasil dilakukan. |
| 400 | Bad Request, pastikan ada telah mengisi parameter id_transaksi dan nomor_resi |
| 404 | Not Found, data tidak ditemukan |


# Callback bukaOlshop


## Apa itu Callback?

Dalam istilah API, Callback merupakan sebuah proses dimana sebuah service mengirim data ke service lainnya, baik itu diluar ruang lingkup aplikasi maupun di dalam internal aplikasi.

Jika dalam API, anda melakukan pemanggilan ke API bukaOlshop, lalu server bukaOlshop akan merespon dengan data yang anda minta. Sedangkan, Callback merupakan kebalikan dari hal tersebut.

Server bukaOlshop akan mengirimkan data ke URL endpoint yang sudah anda inputkan. Data-data tersebut akan dikirim jika ada event tertentu yang terjadi didalam aplikasi, yang kemungkinan anda butuhkan untuk memproses suatu event secara mandiri.

Contoh, jika member melakukan pemesanan didalam aplikasi, maka server bukaOlshop akan mengirimkan data ke URL anda mengenai data pesanan yang baru saja terjadi. Atau bisa juga member telah melakukan konfirmasi pembayaran, anda dapat mendapatkan data konfirmasi tersebut secara langsung dengan adanya callback.

Lihat skema dibawah ini:



Dengan adanya callback, anda dapat mengetahui jika ada pesanan baru yang masuk dan memutuskan sendiri, apa yang anda ingin lakukan dengan data tersebut. Contohnya:

- Melakukan pemesanan produk digital pada layanan lain, jika status transaksi telah lunas.
- Melakukan pengecekan rekening agar pembayaran dapat dikonfirmasi otomatis.
- Menyimpan data transaksi di database pribadi untuk keperluan pendataan.


## Alur kerja Callback pada bukaOlshop

Berikut ini akan dijelaskan alur teknis cara kerja callback pada aplikasi bukaOlshop.

Callback transaksi baru Pada bagian ini, server bukaOlshop akan mengirim data jika ada transaksi baru yang telah dibuat oleh member anda. Data tersebut akan dikirim ke URL yang telah anda inputkan di aplikasi bukaOlshop.

Disamping ini contoh data transaksi baru yang dikirimkan oleh server bukaOlshop ke URL anda:

- tipe_callback dapat berisi dua nilai, yaitu transaksi_baru , dan perubahan_status_transaksi. Disini anda bisa cek apakah callback merupakan transaksi baru atau perubahan status transaksi. Namun, untuk meminimalisir kesalahan, ada baiknya anda memasukkan dua URL yang berbeda antara transaksi baru dan perubahan status transaksi.
- secret_key_callback merupakan sebuah kode rahasia yang bisa anda dapatkan pada aplikasi android bukaOlshop. Kode ini akan dikirimkan tiap server mengirim data ke URL anda. Anda harus membandingkan kode yang dikirim server, dengan kode yang anda terima di aplikasi bukaOlshop, jika kode nya sama, artinya callback tersebut dikirim oleh server bukaOlshop, dan jika berbeda, artinya kode tersebut telah berubah atau ada pihak lain yang mencoba mengirimkan data palsu ke URL anda.
- nomor_pembayaran merupakan id pada transaksi yang telah dilakukan member. Anda bisa mengecek data lengkapnya API bukaOlshop di endpoint detail_transaksi.
- status_transaksi akan menampilkan data status pembayaran/pengiriman pada transaksi. Dengan data ini, anda bisa cek apakah ingin meneruskan proses atau tidak. Contoh jika status transaksi telah lunas, maka anda bisa melanjutkan proses untuk pembelian produk digital pada layanan yang lain. status_transaksi memilik 2 nilai yaitu:
- tipe_transaksi merupakan tipe untuk mengecek apakah transaksi ini dapat anda langsung proses secara otomatis atau tidak. tipe_transaksi ini memiliki 7 nilai yaitu:

COD MANUAL , COD JNT , DELIVERY COD , DELIVERY , PRODUK DIGITAL , EKSPEDISI MULTI_PENGIRIMAN

Berikut ini merupakan Sequence Diagram yang bisa anda gunakan untuk dalam memproses data callback:

Misal anda ingin mengotomatisasi proses pembelian PPOB, anda bisa mendapatkan data yang di inputkan member pada field "catatan". Disarankan untuk tidak menggunakan fitur varian pada produk digital agar lebih mudah mengetahui informasi produk melalui id_barang.

> Perlu diingat, anda perlu memvalidasi terlebih dulu data catatan apakah sudah sesuai atau belum. Contoh, jika anda ingin mengotomatisasi pembelian pulsa, anda perlu mengecek apakah data pada catatan sudah benar merupakan nomor Hp atau bukan.


# Rate Limit

bukaOlshop menerapkan rate limit pada API untuk mencegah penyalahgunaan API yang dapat terjadi. Rate limit merupakan batasan anda melakukan request ke API bukaOlshop setelah anda melakukannya dalam jumlah tertentu. Rate limit ini akan di reset setiap hari, jadi jika anda telah mencapai limit yang telah ditentukan, anda dapat melakukan request pada hari berikutnya.

Jika anda telah mencapat limit yang telah ditentukan, maka server akan merespon dengan kode 429 - Too Many Requests. Sebaiknya anda melakukan pengecekan pada server anda apakah code yang di terima merupakan kode 429 atau tidak.

Gambar dibawah ini merupakan daftar rate limit yang diterapkan pada API bukaOlshop:




# Errors Code

> Lihat penjelasan mengenai HTTP Request di Wikipedia

API bukaOlshop menggunakan kode respons HTTP standart, berikut ini beberapa respon yang mungkin akan anda terima:


| Error Code | Meaning |
| --- | --- |
| 400 | Bad Request -- Data yang anda input salah, pastikan anda menginput data yang wajib di isi dengan benar. |
| 401 | Unauthorized -- API key anda salah, atau Authorization header tidak dikirim dengan benar. |
| 403 | Forbidden -- Autentikasi berhasil, namun anda tidak memiliki hak untuk melihat data. |
| 404 | Not Found -- Data yang anda cari tidak ditemukan. |
| 405 | Method Not Allowed -- Anda mencoba mengakses endpoint dengan method yang salah. |
| 429 | Too Many Requests -- Anda melakukan terlalu banyak request saat bersamaan, atau kuota request perhari anda telah habis. |
| 500 | Internal Server Error -- sedang terjadi masalah pada server, silahkan coba lagi nanti. |
| 503 | Service Unavailable -- Server bukaOlshop sedang offline atau maintenance, silahkan coba lagi nanti. |
<!-- DOCUMENTATION END -->


