# Pertemuan ke 2 <img src=https://seeklogo.com/images/E/elephpant-mascot-php-logo-4C78D1AC4E-seeklogo.com.png width="120px" >

## Profil
|  |  |
| -------- | --- |
| **Nama** |Raditya Tansy Lizara |
| **Kelas** | TI.23.A.5 |
| **Mata Kuliah** | Pemrograman Web 2 |

# Praktikum 1: PHP Framework (Codeigniter)

## Langkah-langkah Praktikum
## Persiapan
Berikut beberapa ekstensi yang perlu diaktifkan:

• php-json ekstension untuk bekerja dengan JSON;

• php-mysqlnd native driver untuk MySQL;

• php-xml ekstension untuk bekerja dengan XML;

• php-intl ekstensi untuk membuat aplikasi multibahasa;

• libcurl (opsional), jika ingin pakai Curl.

Untuk mengaktifkan ekstentsi tersebut, melalu XAMPP Control Panel, pada bagian Apache
klik Config -> PHP.ini

### Catatan : mulai dari PHP 7.0, ekstensi JSON biasanya sudah termasuk secara bawaan.
![alt text](image/ekstensi1.png)


Setelah itu, kalian bisa mencari ekstensi yang diperlukan. Jika ada ekstensi yang belum aktif, kalian bisa mengaktifkannya melalui XAMPP Control Panel dengan masuk ke bagian Apache, lalu klik Config dan pilih PHP.ini.

![alt text](image/ekstensi2.png)

![alt text](image/intl.png))
* Sebagai contoh, di sini ekstensi extension=intl belum aktif. Untuk mengaktifkannya, cukup hapus tanda ; (titik koma) di awal baris ekstensi tersebut. Setelah itu, simpan kembali file tersebut dan lakukan restart pada Apache web server.

## Instalasi Codeigniter 4

Instalasi CodeIgniter 4 bisa dilakukan dengan dua metode, yaitu secara manual atau menggunakan Composer. Pada praktikum ini, kita akan menggunakan metode manual.

Pertama, unduh CodeIgniter melalui situs resminya di https://codeigniter.com/download

Setelah itu, ekstrak file ZIP tersebut ke folder htdocs/lab11_ci

Ganti nama folder codeigniter4-framework-v4.x.xx menjadi ci4

Terakhir, buka browser dan akses alamat http://localhost/lab11_ci/ci4/public/


![Screenshot 2025-03-13 135606](https://github.com/user-attachments/assets/03f69c21-4a9a-4f7b-83e4-7f5267718c06)


## Menjalankan CLI (Command Line Interface)
Codeigniter 4 menyediakan CLI untuk mempermudah proses development. Untuk mengakses CLI buka Shell pada XAMPP.

![Screenshot 2025-03-13 135805](https://github.com/user-attachments/assets/c627f06a-7e6e-40fc-9076-294812d4c80a)


Sesuaikan lokasi direktori ke folder proyek yang sedang dikerjakan (misalnya: cd htdocs/lab11_ci/ci4)

Untuk menjalankan CLI CodeIgniter, kamu bisa menggunakan perintah berikut:

### php spark
![Screenshot 2025-03-13 135856](https://github.com/user-attachments/assets/bea2b38d-957b-4104-a0b9-40827380f4a4)


## Mengaktifkan Mode Debugging
Codeigniter 4 menyediakan fitur debugging untuk memudahkan developer untuk mengetahui pesan error apabila terjadi kesalahan dalam membuat kode program.

Secara default fitur ini belum aktif. Ketika terjadi error pada aplikasi akan ditampilkan pesan kesalahan seperti berikut.

![Screenshot 2025-03-13 140423](https://github.com/user-attachments/assets/11bc4a29-a941-4c3f-954b-4d0be68103ed)


Semua error akan ditampilkan dengan cara yang sama. Agar lebih mudah dalam mengidentifikasi jenis error yang terjadi, kita perlu mengaktifkan mode debugging dengan mengatur nilai variabel environment CI_ENVIRONMENT menjadi development.

![CI_ENVIRONMENT](https://github.com/user-attachments/assets/81c6ea8a-4468-4ad4-83dc-e73e4fe61fb3)


Ubah nama file env menjadi .env kemudian buka file tersebut dan ubah nilai variable
CI_ENVIRONMENT menjadi development.
#### Catatan : Kadang, CodeIgniter tidak membaca file .env karena masih dikomentari, pastikan tidak ada tanda # di depan CI_ENVIRONMENT.

![Parse Erorr](https://github.com/user-attachments/assets/b60e4a62-e038-44b1-a62e-cc0210d363ce)


Contoh error yang terjadi. Untuk mencoba error tersebut, ubah kode pada file
app/Controller/Home.php hilangkan titik koma pada akhir kode return view('welcome_message').
![Controller](https://github.com/user-attachments/assets/d8d2bf70-631d-4bf8-9f2f-089dfe4ea517)

## Memahami konsep MVC
CodeIgniter menerapkan konsep MVC, singkatan dari Model-View-Controller. MVC adalah arsitektur yang sering digunakan dalam pengembangan aplikasi karena memisahkan kode program berdasarkan fungsinya, yaitu logika proses, data, dan tampilan.

Logika proses ditempatkan dalam folder Controller, Data dikelola dalam folder Model, dan Tampilan antarmuka dikelola dalam folder View.

CodeIgniter juga menggunakan pendekatan pemrograman berorientasi objek dalam penerapan konsep MVC ini. Model berisi kode yang bertugas memodelkan data, baik yang berasal dari database maupun sumber lainnya.
View berisi bagian kode yang menangani tampilan antarmuka pengguna. Dalam aplikasi web, ini biasanya melibatkan HTML dan CSS.

Controller berfungsi sebagai pengatur logika proses. Ia menghubungkan antara View dan Model, menerima request dari pengguna, memproses data, lalu menampilkan hasil melalui View.

## Routing dan Controller
Routing adalah proses untuk mengatur jalur dari sebuah request agar dapat diarahkan ke bagian atau fungsi tertentu yang akan memprosesnya. Dalam framework CodeIgniter 4 (CI4), routing berperan penting untuk menentukan Controller mana yang akan menangani suatu request.
Controller sendiri merupakan class atau script yang bertugas merespons permintaan tersebut.

Di CodeIgniter, setiap request yang masuk melalui file index.php akan diteruskan ke Router, lalu oleh router tersebut diarahkan ke Controller yang sesuai.

File konfigurasi untuk Router berada di app/config/Routes.php.
![Routers](https://github.com/user-attachments/assets/d522d906-925f-48b2-9f3e-19f33b627a42)


Pada file tersebut kita dapat mendefinisikan route untuk aplikasi yang kita buat.
Contoh:
```` python
$routes->get('/', 'Home::index');
````
Kode tersebut akan mengarahkan rute untuk halaman home.

#### Membuat Route Baru.
Tambahkan kode berikut di dalam Routes.php
```` python
$routes->get('/about', 'Page::about');
$routes->get('/contact', 'Page::contact');
$routes->get('/faqs', 'Page::faqs');
````
Untuk mengetahui route yang ditambahkan sudah benar, buka CLI dan jalankan perintah berikut.

php spark routes
![PHP Spark Router](https://github.com/user-attachments/assets/7cf3c723-4353-42f2-8b31-22820889dd7b)


Selanjutnya coba akses route yang telah dibuat dengan mengakses alamat url http://localhost:8080/about
![404](https://github.com/user-attachments/assets/4247cf80-282f-438e-9945-ea2ccd84969d)


Ketika diakses akan mucul tampilan error 404 file not found, itu artinya file/page tersebut tidak ada. Untuk dapat mengakses halaman tersebut, harus dibuat terlebih dahulu Contoller yang sesuai dengan routing yang dibuat yaitu Contoller Page.

#### Membuat Controller
Selanjutnya adalah membuat Controller Page. Buat file baru dengan nama page.php pada direktori Controller kemudian isi kodenya seperti berikut.

```` python
<?php

namespace App\Controllers;

class Page extends BaseController
{
    public function about()
    {
        echo "Ini halaman About";
    }
    public function contact()
    {
        echo "Ini halaman Contact";
    }
    public function faqs()
    {
        echo "Ini halaman FAQ";
    }
}
````

![alt text](image/about.png)

#### Auto Routing
Secara default fitur autoroute pada Codeiginiter sudah aktif. Untuk mengubah status autoroute dapat mengubah nilai variabelnya. Untuk menonaktifkan ubah nilai true menjadi false.

```` python
$routes->get('page/tos', 'Page::tos');
$routes->setAutoRoute(true);
````

Tambahkan method baru pada Controller Page seperti berikut.
```` python
public function tos()
{
    echo "ini halaman Term of Services";
}
````

Method ini belum ada pada routing, sehingga cara mengaksesnya dengan menggunakan alamat: http://localhost:8080/page/tos
![alt text](image/tos.png)

### Membuat View
Selanjutnya adalam membuat view untuk tampilan web agar lebih menarik. Buat file baru dengan nama about.php pada direktori Views (app/Views/about.php) kemudian isi kodenya seperti berikut.
```` python
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
</head>

<body>
    <h1><?= $title; ?></h1>
    <hr>
    <p><?= $content; ?></p>
</body>

</html>
````

Ubah method about pada class Controller Page menjadi seperti berikut:
``` python
    public function about()
    {
        return view('about', [
            'title' => 'Halaman About',
            'content' => 'Ini adalah halaman about yang menjelaskan tentang isi halaman ini.'
        ]);
    }
```

Kemudian lakukan refresh pada halaman tersebut.

![alt text](image/About2.png)

### Membuat Layout Web dengan CSS
Pada dasarnya layout web dengan css dapat diimplamentasikan dengan mudah pada codeigniter. Yang perlu diketahui adalah, pada Codeigniter 4 file yang menyimpan asset css dan javascript terletak pada direktori public.

Buat file css pada direktori public dengan nama style.css

![alt text](image/style.png)

Kemudian buat folder template pada direktori view kemudian buat file header.php dan footer.php

File app/Views/template/header.php
```python
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <title><?= $title; ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css'); ?>">
</head>

<body>
    <div id="container">
        <header>
            <h1>Layout Sederhana</h1>
        </header>
        <nav>
            <a href="<?= base_url('/'); ?>" class="active">Home</a>
            <a href="<?= base_url('/artikel'); ?>">Artikel</a>
            <a href="<?= base_url('/about'); ?>">About</a>
            <a href="<?= base_url('/contact'); ?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main"></section>
```

File app/Views/template/footer.php
```python
</section>
<aside id="sidebar">
    <div class="widget-box">
        <h3 class="title">Widget Header</h3>
        <ul>
            <li><a href="#">Widget Link</a></li>
            <li><a href="#">Widget Link</a></li>
        </ul>
    </div>
    <div class="widget-box">
        <h3 class="title">Widget Text</h3>
        <p>Vestibulum lorem elit, iaculis in nisl volutpat,
            malesuada tincidunt arcu. Proin in leo fringilla, vestibulum mi porta,
            faucibus felis. Integer pharetra est nunc, nec pretium nunc pretium ac.</p>
    </div>
</aside>
</section>
<footer>
    <p>&copy; 2021 - Universitas Pelita Bangsa</p>
</footer>
</div>
</body>

</html>
```

Kemudian ubah file app/Views/about.php seperti berikut.
```python
<?= $this->include('template/header'); ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>
<?= $this->include('template/footer'); ?>
```

Selanjutnya refresh tampilan pada alamat http://localhost:8080/about

![Screenshot 2025-03-13 142448](https://github.com/user-attachments/assets/ebb95f40-087d-4923-8ce0-c9ff25ed2451)

