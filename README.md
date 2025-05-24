# Praktikum 1-3 <img src=https://seeklogo.com/images/E/elephpant-mascot-php-logo-4C78D1AC4E-seeklogo.com.png width="120px" >

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


# Praktikum 2: Framework Lanjutan (CRUD) - CodeIgniter 4 #

Tujuan
1. Mampu memahami konsep dasar Model.
2. Mampu memahami konsep dasar CRUD.
3. Mampu membuat program sederhana menggunakan Framework Codeigniter4.
   
Instruksi Praktikum
1. Persiapkan text editor misalnya VSCode.
2. Buka kembali folder dengan nama lab7_php_ci pada docroot webserver (htdocs)
3. Ikuti langkah-langkah praktikum yang akan dijelaskan berikutnya.
   
Langkah-langkah Praktikum

### Persiapan. ###
Untuk memulai membuat aplikasi CRUD sederhana, yang perlu disiapkan adalah database
server menggunakan MySQL. Pastikan MySQL Server sudah dapat dijalankan melalui
XAMPP.

### Membuat Database: Studi Kasus Data Artikel ###
![Tabel Database](https://github.com/user-attachments/assets/4c9126d8-800d-431f-b974-859847e11074)

```php
CREATE DATABASE lab_ci4;
```

```php
CREATE TABLE artikel (
  id INT(11) auto_increment,
  judul VARCHAR(200) NOT NULL,
  isi TEXT,
  gambar VARCHAR(200),
  status TINYINT(1) DEFAULT 0,
  slug VARCHAR(200),
  PRIMARY KEY(id)
);
```

### Konfigurasi Koneksi Database ###
- Gunakan file .env untuk mengatur parameter koneksi ke database, lalu sesuaikan pengaturannya sesuai dengan kebutuhan proyek.

![Konfigurasi koneksi](https://github.com/user-attachments/assets/7ef37148-7eee-4d9a-819c-643475ac9d13)

### Membuat Model ###
- Langkah berikutnya adalah membuat Model yang akan digunakan untuk mengelola data Artikel. Buatlah file baru dengan nama ArtikelModel.php di dalam folder app/Models.

```php
<?php
namespace App\Models;

use CodeIgniter\Model;

class ArtikelModel extends Model
{
    protected $table = 'artikel';
    protected $primaryKey = 'id';
    protected $useAutoIncrement = true;
    protected $allowedFields = ['judul', 'isi', 'status', 'slug', 'gambar'];
}
```

### Membuat Controller ###
Silakan buat Controller baru dengan nama Artikel.php dan simpan di dalam folder app/Controllers.

```php
<?php

namespace App\Controllers;

use App\Models\ArtikelModel;

class Artikel extends BaseController
{
    public function index()
    {
        $title = 'Daftar Artikel';
        $model = new ArtikelModel();
        $artikel = $model->findAll();
        return view('artikel/index', compact('artikel', 'title'));
    }
}
```

### Membuat View ###
Buat folder baru bernama artikel di dalam direktori app/views, lalu buat file baru bernama index.php di dalam folder tersebut.

```php
<?= $this->include('template/header'); ?>

<?php if($artikel): foreach($artikel as $row): ?>
<article class="entry">
    <h2<a href="<?= base_url('/artikel/' . $row['slug']);?>"><?= $row['judul']; ?></a>
</h2>
    <img src="<?= base_url('/gambar/' . $row['gambar']);?>" alt="<?= $row['judul']; ?>">
    <p><?= substr($row['isi'], 0, 200); ?></p>
</article>
<hr class="divider" />
<?php endforeach; else: ?>
<article class="entry">
    <h2>Belum ada data.</h2>
</article>
<?php endif; ?>

<?= $this->include('template/footer'); ?>
```

Selanjutnya buka browser kembali, dengan mengakses url http://localhost:8080/artikel

![portalberita](https://github.com/user-attachments/assets/3afdead0-e467-4ad8-9759-1e4263214c40)

Belum ada data yang muncul. Coba tambahkan beberapa data ke dalam database supaya datanya bisa ditampilkan.

```
INSERT INTO artikel (judul, isi, slug) VALUE
('Artikel pertama', 'Lorem Ipsum adalah contoh teks atau dummy dalam industri percetakan dan penataan huruf atau typesetting. Lorem Ipsum telah menjadi standar contoh teks sejak tahun 1500an, saat seorang tukang cetak yang tidak dikenal mengambil sebuah kumpulan teks dan mengacaknya untuk menjadi sebuah buku contoh huruf.','artikel-pertama'),
('Artikel kedua', 'Tidak seperti anggapan banyak orang, Lorem Ipsum bukanlah teks-teks yang diacak. Ia berakar dari sebuah naskah sastra latin klasik dari era 45 sebelum masehi, hingga bisa dipastikan usianya telah mencapai lebih dari 2000 tahun.', 'artikel-kedua');
```

Lakukan refresh pada browser untuk melihat hasil yang telah ditampilkan.
![portalberita2](https://github.com/user-attachments/assets/29f98977-244e-4a39-8fa4-fbaa3ba478b4)

### Membuat Tampilan Detail Artikel ###
Saat judul berita diklik, tampilannya akan berpindah ke halaman berbeda. Untuk itu, tambahkan fungsi baru bernama **view()** di dalam Controller **Artikel**.

```php
public function view($slug)
{
    $model = new ArtikelModel();
    $artikel = $model->where([
        'slug' => $slug
    ])->first();

    // Menampilkan error apabila data tidak ada.
    if (!$artikel)
    {
        throw PageNotFoundException::forPageNotFound();
    }

    $title = $artikel['judul'];
    return view('artikel/detail', compact('artikel', 'title'));
}
```

### Membuat View Detail ###
- Buatlah view baru untuk halaman detail dengan nama detail.php di dalam folder app/views/artikel/.

```php
<?= $this->include('template/header'); ?>

<article class="entry">
    <h2><?= $artikel['judul']; ?></h2>
    <img src="<?= base_url('/gambar/' . $artikel['gambar']);?>" alt="<?=
$artikel['judul']; ?>">
    <p><?= $row['isi']; ?></p>
</article>

<?= $this->include('template/footer'); ?>
```

### Membuat Routing untuk artikel detail ###
- Buka kembali file **app/config/Routes.php**, lalu tambahkan routing baru yang mengarah ke halaman detail artikel.
```php
$routes->get('/artikel/(:any)', 'Artikel::view/$1');
```

![Artikel2](https://github.com/user-attachments/assets/d0990eda-5bfe-40e1-8ea7-9ab02a541fbc)

### Membuat menu admin ###
Menu admin adalah untuk proses CRUD data artikel. Buat method baru pada Controller Artikel dengan nama admin_index().
```php
public function admin_index()
{
    $title = 'Daftar Artikel';
    $model = new ArtikelModel();
    $artikel = $model->findAll();
    return view('artikel/admin_index', compact('artikel', 'title'));
}
```

Selanjutnya buat view untuk tampilan admin dengan nama admin_index.php

```php
<?= $this->include('template/admin_header'); ?>

<table class="table">
    <thead>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>AKsi</th>
        </tr>
    </thead>
    <tbody>
    <?php if($artikel): foreach($artikel as $row): ?>
    <tr>
        <td><?= $row['id']; ?></td>
        <td>
            <b><?= $row['judul']; ?></b>
            <p><small><?= substr($row['isi'], 0, 50); ?></small></p>
        </td>
        <td><?= $row['status']; ?></td>
        <td>
            <a class="btn" href="<?= base_url('/admin/artikel/edit/' . $row['id']);?>">Ubah</a>
            <a class="btn btn-danger" onclick="return confirm('Yakin menghapus data?');" href="<?= base_url('/admin/artikel/delete/' . $row['id']);?>">Hapus</a>
        </td>
    </tr>
    <?php endforeach; else: ?>
    <tr>
        <td colspan="4">Belum ada data.</td>
    </tr>
    <?php endif; ?>
    </tbody>
    <tfoot>
        <tr>
            <th>ID</th>
            <th>Judul</th>
            <th>Status</th>
            <th>AKsi</th>
        </tr>
    </tfoot>
</table>

<?= $this->include('template/admin_footer'); ?>
```

Tambahkan routing untuk menu admin seperti berikut:

```php
$routes->group('admin', function($routes) {
    $routes->get('artikel', 'Artikel::admin_index');
    $routes->add('artikel/add', 'Artikel::add');
    $routes->add('artikel/edit/(:any)', 'Artikel::edit/$1');
    $routes->get('artikel/delete/(:any)', 'Artikel::delete/$1');
});
```


Akses menu admin dengan url http://localhost:8080/admin/artikel

![Admin](https://github.com/user-attachments/assets/0b77f112-6615-4652-abfa-5415c196db28)


### Membuat Data Artikel ###

Tambahkan fitur baru berupa method add() dalam Controller Artikel untuk mendukung fungsionalitas penambahan artikel.

```php
public function add()
{
    // validasi data.
    $validation = \Config\Services::validation();
    $validation->setRules(['judul' => 'required']);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid)
    {
        $artikel = new ArtikelModel();
        $artikel->insert([
            'judul' => $this->request->getPost('judul'),
            'isi' => $this->request->getPost('isi'),
            'slug' => url_title($this->request->getPost('judul')),
        ]);
        return redirect('admin/artikel');
    }
    $title = "Tambah Artikel";
    return view('artikel/form_add', compact('title'));
}
```

Lanjutkan dengan membuat file view bernama form_add.php yang berisi form untuk menambahkan data baru.

```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <input type="text" name="judul">
    </p>
    <p>
        <textarea name="isi" cols="50" rows="10"></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

![form_add](https://github.com/user-attachments/assets/74ef0d1c-8cd8-499e-9471-93e69dcd070e)

### Mengubah Data ###

Lengkapi Controller Artikel dengan sebuah fungsi tambahan bernama edit() guna menangani perubahan data.

```php
public function edit($id)
{
    $artikel = new ArtikelModel();

    // validasi data.
    $validation = \Config\Services::validation();
    $validation->setRules(['judul' => 'required']);
    $isDataValid = $validation->withRequest($this->request)->run();

    if ($isDataValid)
    {
        $artikel->update($id, [
            'judul' => $this->request->getPost('judul'),
            'isi' => $this->request->getPost('isi'),
        ]);
        return redirect('admin/artikel');
    }

    // ambil data lama
    $data = $artikel->where('id', $id)->first();
    $title = "Edit Artikel";
    return view('artikel/form_edit', compact('title', 'data'));
}
```

Selanjutnya, buat tampilan form untuk mengedit data dan simpan dengan nama form_edit.php.

```php
<?= $this->include('template/admin_header'); ?>

<h2><?= $title; ?></h2>
<form action="" method="post">
    <p>
        <input type="text" name="judul" value="<?= $data['judul'];?>" >
    </p>
    <p>
        <textarea name="isi" cols="50" rows="10"><?=$data['isi'];?></textarea>
    </p>
    <p><input type="submit" value="Kirim" class="btn btn-large"></p>
</form>

<?= $this->include('template/admin_footer'); ?>
```

![form_edit2](https://github.com/user-attachments/assets/041b01ee-837d-43c4-a4f5-389f8106b84e)

### Menghapus Data ###

Tambahkan method baru dengan nama delete() pada Controller Artikel untuk menangani proses penghapusan data.

```php
public function delete($id)
{
    $artikel = new ArtikelModel();
    $artikel->delete($id);
    return redirect('admin/artikel');
}
```

# Praktikum 3: View Layout dan View Cell #

## Langkah-Langkah Praktikum ##

### Persiapan ###

- Buka folder lab7_php_ci yang sudah digunakan pada praktikum sebelumnya.

- Jalankan text editor seperti VSCode untuk mulai mengerjakan.

### Membuat Layout Utama ###

- Di dalam direktori app/Views/, buat folder baru dan beri nama layout.

- Selanjutnya, buat file baru bernama main.php di dalam folder layout.

- Isi file main.php dengan struktur layout utama yang akan menjadi template dasar tampilan web.

```php
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title><?= $title ?? 'My Website' ?></title>
    <link rel="stylesheet" href="<?= base_url('/style.css');?>"> 
</head>
<body>
    <div id="container">
        <header><h1>Layout Sederhana</h1></header>
        <nav>
            <a href="<?= base_url('/');?>" class="active">Home</a>
            <a href="<?= base_url('/artikel');?>">Artikel</a>
            <a href="<?= base_url('/about');?>">About</a>
            <a href="<?= base_url('/contact');?>">Kontak</a>
        </nav>
        <section id="wrapper">
            <section id="main">
                <?= $this->renderSection('content') ?>
            </section>
            <aside id="sidebar">
                <?= view_cell('App\\Cells\\ArtikelTerkini::render') ?>
                <!-- Widget lainnya -->
            </aside>
        </section>
        <footer><p>&copy; 2021 - Universitas Pelita Bangsa</p></footer>
    </div>
</body>
</html>
```

### Modifikasi File View ###

Sesuaikan file app/Views/home.php agar menggunakan layout utama yang baru dibuat.

```php
<?= $this->extend('layout/main') ?>

<?= $this->section('content') ?>
<h1><?= $title; ?></h1>
<hr>
<p><?= $content; ?></p>

<?= $this->endSection() ?>
```

### Menampilkan Data Dinamis dengan View Cell ###
View Cell merupakan fitur yang memungkinkan penggunaan tampilan sebagai komponen yang bisa dipakai berulang kali. Fitur ini sangat cocok untuk elemen-elemen seperti sidebar, widget, atau menu navigasi yang sering muncul di berbagai halaman.

### Membuat class view cell ###
- Buat folder baru bernama Cells di dalam direktori app/.

- Kemudian, buat file ArtikelTerkini.php di dalam folder app/Cells/ dengan kode seperti berikut:

```php
namespace App\Cells;

use CodeIgniter\View\Cell;
use App\Models\ArtikelModel;

class ArtikelTerkini extends Cell
{
    public function render()
    {
        $model = new ArtikelModel();
        $artikel = $model->orderBy('created_at', 'DESC')->limit(5)->findAll();
        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```

### Membuat view untuk view cell ###
- Buat folder components di dalam app/Views/.

- Buat file artikel_terkini.php di dalam folder tersebut.

```php
<h3>Artikel Terkini</h3>
<ul>
<?php foreach ($artikel as $row): ?>
    <li><a href="<?= base_url('/artikel/' . $row['slug']) ?>"><?= $row['judul'] ?></a></li>
<?php endforeach; ?>
</ul>
```

### Pertanyaan dan Tugas ###
## 1. Sesuaikan data dengan praktikum sebelumnya, perlu melakukan perubahan field pada database dengan menambahkan tanggal agar dapat mengambil data artikel terbaru.##
```php
ALTER TABLE artikel ADD COLUMN created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP;
```

![1](https://github.com/user-attachments/assets/595c7c6d-d6b6-4321-a743-c5433bdcb027)

## 2. Selesaikan programnya sesuai Langkah-langkah yang ada. Anda boleh melakukan improvisasi.##

## 3. Apa manfaat utama dari penggunaan View Layout dalam pengembangan aplikasi?##
View Layout menyediakan metode untuk menciptakan struktur tampilan yang konsisten pada seluruh halaman aplikasi. Dengan menggunakan layout, pengembang hanya perlu membuat satu file kerangka HTML (termasuk header, sidebar, dan footer), kemudian konten halaman dapat disisipkan ke dalam kerangka tersebut. Manfaat penggunaan layout antara lain:

- Efisiensi waktu pengembangan

- Kemudahan dalam pemeliharaan tampilan

- Pengurangan duplikasi kode

## 4. Jelaskan perbedaan antara View Cell dan View biasa.##
1. Fungsi:
View Layout berperan sebagai template utama yang mengatur struktur tampilan secara keseluruhan, sedangkan View Cell adalah komponen modular yang dapat dipanggil di dalam tampilan.

2. Fleksibilitas:
View Layout digunakan untuk membangun halaman penuh, sementara View Cell lebih cocok digunakan untuk bagian kecil seperti sidebar atau widget.

3. Pemakaian:
View Layout biasanya diterapkan dengan metode extend() dan renderSection(), sedangkan View Cell dipanggil menggunakan fungsi view_cell().

4. Contoh Penggunaan:
View Layout digunakan untuk membuat layout utama website yang mencakup header, footer, dan sidebar, sedangkan View Cell cocok untuk menampilkan elemen seperti daftar artikel terbaru, widget pencarian, dan lain-lain.

## 5. Ubah View Cell agar hanya menampilkan post dengan kategori tertentu.##
### Tahapan:
- Masukkan field kategori ke tabel artikel.

```php
ALTER TABLE artikel ADD kategori VARCHAR(50);
```
![2](https://github.com/user-attachments/assets/2ed906d3-2c7a-4479-980d-77f8cb2ebc17)

- Perbarui method render dengan menambahkan parameter kategori.

```php
public function render($kategori = null)
{
    $model = new ArtikelModel();
    $query = $model->orderBy('created_at', 'DESC');

    if ($kategori) {
        $query->where('kategori', $kategori);
    }

    $artikel = $query->limit(5)->findAll();

    return view('components/artikel_terkini', ['artikel' => $artikel]);
}
```

- Isi setiap kolom di tabel bisa dilakukan secara manual atau melalui fitur tambah artikel.

- Modifikasi View Cell agar bisa memfilter data berdasarkan kategori.

- Buka file app/Cells/ArtikelTerkini.php lalu ubah fungsi render() menjadi seperti berikut:

```php
<?php

namespace App\Cells;

use App\Models\ArtikelModel;

class ArtikelTerkini
{
    public function render($kategori = null)
    {
        $model = new ArtikelModel();

        $query = $model->orderBy('created_at', 'DESC')->limit(5);
        if ($kategori) {
            $query->where('kategori', $kategori);
        }

        $artikel = $query->findAll();

        return view('components/artikel_terkini', ['artikel' => $artikel]);
    }
}
```

- Pada file app/Views/layout/main.php, panggil View Cell beserta parameter kategori.

```php
<?= view_cell('App\\Cells\\ArtikelTerkini::render', ['kategori' => 'Teknologi']) ?>
```

- Tambahkan pengaturan route agar URL /kategori/teknologi berfungsi dengan baik.

```php
$routes->get('/kategori/(:segment)', 'Artikel::kategori/$1');
``

- Siapkan view kategori.php di dalam folder app/Views/artikel/.

```php
<?= $this->extend('layout/main') ?>
<?= $this->section('content') ?>

<h2><?= $title ?></h2>
<ul>
    <?php foreach ($artikel as $row): ?>
        <li>
            <a href="<?= base_url('/artikel/' . $row['slug']) ?>">
                <?= esc($row['judul']) ?>
            </a>
        </li>
    <?php endforeach; ?>
</ul>

<?= $this->endSection() ?>
```

### Screenshot Hasil###
![Olahraga2](https://github.com/user-attachments/assets/862f8397-b3a2-4e80-85d4-1aff74048c43)

![Teknologi2](https://github.com/user-attachments/assets/ef82fb05-6f6d-44dd-9f68-3209e58b2641)








