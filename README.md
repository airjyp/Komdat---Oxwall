<h5 align="center"><img src="https://www.hostpapa.in/assets/lp/oxwall_logo_big.png"></h5>

[Sekilas Tentang](#sekilas-tentang) | [Instalasi](#instalasi) | [Konfigurasi](#konfigurasi) | [Otomatisasi](#otomatisasi) | [Cara Pemakaian](#cara-pemakaian) | [Pembahasan](#pembahasan) | [Referensi](#referensi)
:---:|:---:|:---:|:---:|:---:|:---:|:---:

# Sekilas Tentang
[`^ kembali ke atas ^`](#)

**Oxwall** adalah perangkat lunak forum yang didistribusikan di bawah Common Public Attribution License. Ini digunakan sebagai platform untuk jejaring sosial dan situs komunitas. Inti perangkat lunak Oxwall default berisi fitur komunitas dasar yang mencakup konten upload / sharing, jaringan teman, profil dan tata letak halaman, pengelolaan pengguna dan konten, SEO built-in.

# Instalasi
[`^ kembali ke atas ^`](#)

#### Kebutuhan Sistem :
- Virtualbox 2.6
- Ubuntu server 16.04
- Ubuntu bash di windows

#### Proses Instalasi :
1. Lakukan update server
```
$ sudo apt update
```

2. Install ssh pada Ubuntu server
```
$ sudo apt install ssh
```

3. Login ke dalam server menggunakan SSH menggunakan ubuntu bash (Windows)
```
$ ssh student@localhost –p 2222
```

4. Install seluruh kebutuhan sistem yang diperlukan seperti`Apache`, `PHP`, dan `MySQL`. 
```
$ sudo apt install apache2 
$ sudo apt install mysql-server
$ sudo apt install php
$ sudo apt install libapache2-mod-php 
$ sudo apt install php-mysql php-zip php-gd php-json php-readline php–mcrypt php-mbstring php-xml php-ssh2
$ sudo service apache2 restart
```

5. Install terlebih dahulu zip untuk mengekstrak data Oxwall.
```
$ sudo apt install zip && sudo apt install unzip
```

6. Unduh **Oxwall** ke dalam direktori.
```
$ wget –c http://ow.download.s3.amazonaws.com/oxwall-1.8.4.1.zip
```

7. Ekstrak file yang telah diunduh ke dalam direktori yang diinginkan. 
```
$ unzip 0xwall-1.8.4.1.zip –d oxwall
```

8. Pindahkan folder oxwall
```
$ sudo mv oxwall /var/www/html
```

9. Mengubah ownership direktori oxwall ke webserver 
```
$ sudo chown –R www-data:www-data /var/www/oxwall
```

10. Buat database dan user untuk **Oxwall** 
```
$ mysql –u root –p –e "
    CREATE DATABASE oxwall;
    GRANT ALL PRIVILEGES ON `oxwall`.* TO 'oxwall'@'localhost' IDENTIFIED BY 'student';
    FLUSH PRIVILEGES;"
```

14. Karena oxwall menggunakan .htaccess dan secara default diblock oleh apache, maka perlu dilakukan beberapa konfigurasi Apache
```
$ sudo a2enmod rewrite 
$ sudo systemctl restart apache2
$ sudo nano /etc/apache2/sites-available/000-default.conf

<VirtualHost *:80>
<Directory /var/www/html>
    Options Indexes FollowSymLinks MultiViews
    AllowOverride All
    Require all granted
</Directory>
```

15. Restart apache
```
$ sudo systemctl restart apache2
```

16. Ketika sudah masuk halaman oxwall, akan muncul peringatan mysql php extension belum terinstall, karena oxwall tidak bisa membaca php-mysql dari php 7, triknya yaitu menghapus requirement mysql pada oxwall
```
$sudo nano /var/www/html/oxwall/ow_install/files/requirements.txt
```

17. Hapus mysql pada file tersebut, save dengan ctrl+o
18. Cek kembali localhost:8888/oxwall , maka oxwall sudah bisa digunakan

# Konfigurasi

[`^ kembali ke atas ^`](#)

- Untuk menentukan konfigurasi umum, batasan upload file, batas memori yang diperlukan, dan ekstensi/format file yang dapat diupload , dapat dilakukan dengan membuka submenu **Content settings** yang terdapat pada menu **Settings** dan mengisi field sesuai kebutuhan.
     
     ![content_setting](https://github.com/airjyp/Komdat---Oxwall/blob/master/konfigurasi/content_setting.png)

- Kita dapat membatasi batas upload size untuk avatar pada user di submenu **User settings**. 
     
     ![content_setting](https://github.com/airjyp/Komdat---Oxwall/blob/master/konfigurasi/user_setting.png)

- Untuk melengkapi dan melakukan improve pada aplikasi, kita dapat menambahkan fitur tertentu di submenu **Available Plugins** pada menu **Plugins**.
     
     ![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(14).png)

- Untuk mengupload dan menambahkan plugin secara manual, dapat dilakukan pada menu **Add New**.
     
     ![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(15).png)

- Kita dapat mempercantik tampilan aplikasi dengan menambahkan atau mengganti tema aplikasi pada submenu **Themes** di **Appearance**.
     
     ![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(18).png)


# Maintenance

[`^ kembali ke atas ^`](#)

Maintenance dibutuhkan untuk melakukan improvisasi dan kualitas pada aplikasi. Salah satu dari aktivitas maintenance adalah melakukan modifikasi, memperbaiki fitur yang ada, maupun meningkatkan performa aplikasi kita. Oleh karena itu, kita perlu mengaktifkan fitur Maintenance mode saat akan melakukan maintenance, agar tidak ada client yang mengakses aplikasi selama proses maintenance berjalan. Berikut ini adalah langkah-langkah yang harus dilakukan :

1. Login ke dalam admin aplikasi kita.
2. Klik submenu **Special pages** pada menu **Pages**.

     ![pages](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/pages.png)

3. Checked / Unchecked box untuk masuk ke dalam mode maintenance.

     ![maintenance](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/maintenance.png)

4. Untuk menyampaikan pesan yang ingin disampaikan kepada orang yang akan mengakses aplikasi web saat mode maintenance, kita dapat menambahkan pesan pada field **Maintenance message**.
5. Klik tombol **Save** untuk menyimpan perubahan.



# Otomatisasi
[`^ kembali ke atas ^`](#)

Salah satu cara yang bisa digunakan untuk menginstall oxwall dengan cepat yaitu dengan menggunakan layanan web-hosting provider, salah satunya yaitu **Installatron**,berikut cara menginstall oxwall menggunakan installatron:

1. Mengunjungi **Installatron**
2. Search oxwall pada installatron, seperti gambar berikut ini

    ![Installatron](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/otomatisasi%20review.png)

3. klik tombol **Install this application** lalu mengisi informasi yang tersedia pada form

    ![form](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/otomatisasi%20install.png)

4. Tunggu hingga proses instalasi selesai.


# Cara Pemakaian
[`^ kembali ke atas ^`](#)

# Pembahasan
[`^ kembali ke atas ^`](#)

# Referensi
[`^ kembali ke atas ^`](#)

1. [About Oxwall](https://www.oxwall.com/about) - Oxwall
2. [Apache Override](https://www.digitalocean.com/community/tutorials/how-to-rewrite-urls-with-mod_rewrite-for-apache-on-ubuntu-16-04) - DigitalOcean
3. [Mysql PHP Problem](https://developers.oxwall.com/forum/topic/55994?page=1) - Oxwall Forum
4. [Cron Jobs Config](https://wiki.oxwall.com/install:cron) - Oxwall Wiki



