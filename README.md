# php-2KEN-auth v1.0 Public Version
plugin simpel untuk menggantikan session.<br>
untuk memahami penjelasan dibawah pastikan anda sudah memahami cara-cara pemanggilan dalam PHP.<br>
database 2KEN_auth.sqlite3 harus dalam 1 folder yang sama dengan 2KEN_auth.php `WAJIB!!!`<br>
```
requirements:
-> PHP 7+
-> Sqlite3 (php library)

syarat:
-> file .sqlite3 harus 1 pemilik dengan izin baca/tulis
-> folder tempat 2 file ini berada harus 1 pemilik dengan izin baca/tulis
```
<br>
<br>

# Cara Menggunakan

## Cara Penggunaan, untuk memanggil.

```
<?php
include 'path/to/2ken_auth/2ken_auth.php';
use Tools\Auth\Cookie as auth;
```
tidak harus dengan cara diatas, tapi simpelnya begitu.
<br>
<hr>


## Cara penggunaan untuk Set Data.
```
<?php
$array_data = array(
                "user_type"  =>  "value" /*default*/,
                "user_id"    =>  "value" /*default*/,
                "app_name"   =>  "value" /*default*/,
                
                "other_key"  =>  "custom value",
                "other_key"  =>  "custom value",
                "other_key"  =>  "custom value",
                "other_key"  =>  "custom value",
);

auth\SET(true,$array_data);
```
**user_type** : isi se kreatifnya aja, ini identifier untuk yang mau dipake nanti.
<br>
**user_id** : udah kebaca jelas ini apaan.
<br>
**app_name** : identifikasi untuk pemanggilan, misal cookie ini mau dipakai untuk aplikasi web, ya kasi nama apa gitu. terus mau set lainnya untuk aplikasi react ya set app name berbeda. ini dinamis ya, sekreatifnya aja.
<br>
```
"other_key"  =>  "custom value",
```
nah diatas ini akan menjadi json. dan semua data array akan jadi json, jadi ini dinamis ya mau diapain aja keynya mau diisi apa sama valuenya apa.
<br>
<hr>

## untuk memberitahu udah login atau belum
```
<?php
auth\GET(true,'app_name');
```
nah diatas akan return data `false` dan `true` , jika yang keluar `false` sudah berarti belum login/belum ada datanya, kalau yang keluar hasilnya `true` ya udah login. contoh penggunaanya
```
<?php
if(auth\GET(true,'app_name') == false){
    #code mau redirect ke login atau bikin loginya disini boleh.
}
```
fungsi diatas bisa juga ditulis seperti dibawah ini:
```
<?php
if(auth\GET(true,'app_name') != false){
    #code mau redirect ke login atau bikin loginya disini boleh.
}

```

beigtu pula sebaliknya untuk ngecek login
<br>
<hr>

## mendapatkan data token dan token_ip
```
<?php
$data     = auth\Fetch('app_name');
$token    = $data['token'];
$token_ip = $data['token_ip'];
```
return array yak. kalau gak penting banget gausa dipakai wkwk nyusahin udah ada fitur FetchData dibawah.
<br>
<hr>

## mendapatkan data yang sudah disimpan ke `$array_data` tadi sebagai JSON.
```
<?php
$data = auth\FetchData('app_name');
```
inget **return**nya `JSON` <br>
supaya bisa dipake di php, anu convert ke array lagi.
```
<?php
$data         = auth\FetchData('app_name');
$data_array   = json_decode($data,true);
$custom_val   = $data_array["other_key"];
```
inget kan `other_key` diatas tadi? nah bisa digunain disini.
<br>
<hr>

## untuk logout
didalam script logout tiggal dikasih kode
```
<?php
auth\DEL(true);
```
