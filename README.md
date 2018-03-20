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
$ sudo chown –R www-data:www-data /var/www/html/oxwall
```

10. Buat database dan user untuk **Oxwall** 
```
$ mysql –u root –p –e "
    CREATE DATABASE oxwall;
    GRANT ALL PRIVILEGES ON `oxwall`.* TO 'oxwall'@'localhost' IDENTIFIED BY 'student';
    FLUSH PRIVILEGES;"
```

11. Karena oxwall menggunakan .htaccess dan secara default diblock oleh apache, maka perlu dilakukan beberapa konfigurasi Apache
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

12. Restart apache
```
$ sudo systemctl restart apache2
```

13. Ketika sudah masuk halaman oxwall, akan muncul peringatan mysql php extension belum terinstall, karena oxwall tidak bisa membaca php-mysql dari php 7, triknya yaitu menghapus requirement mysql pada oxwall
```
$sudo nano /var/www/html/oxwall/ow_install/files/requirements.txt
```

14. Hapus mysql pada file tersebut, save dengan ctrl+o
15. Cek kembali localhost:8888/oxwall , maka oxwall sudah bisa digunakan

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

Otomatisasi lain yang dapat digunakan pada oxwall yaitu otomatisasi task system menggunakan cron job. Cron job merupakan aplikasi "task scheduler" yang berfungsi untuk memanajemen task apa saja yang diperlukan dalam aplikasi seperti oxwall dan menjalankan task tersebut secara otomatis. Cron job diperlukan oleh oxwall agar admin tidak perlu mengatur aplikasi secara rutin.


# Cara Pemakaian
[`^ kembali ke atas ^`](#)

Berikut akan dijelaskan salah satu cara pemakaian oxwall bagi user baru:

1. Mengunjungi halaman utama oxwall, seperti tampilan di bawah ini.
![Halaman sebelum sign up](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/halaman%20sebelum%20login.png)

2. Klik Sign up lalu mengisi data registrasi yang tersedia setelah masuk ke halaman registrasi
![Form registrasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/form%20registrasi%20setelah%20diisi.png)

3. Setelah melakukan registrasi, user akan otomatis login ke oxwall dan diarahkan ke halaman beranda akun user tersebut.
![Halaman beranda](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/beranda.png)

4. User dapat masuk ke halaman profilnya sendiri dan juga dapat mengedit segala informasi yang sudah diisi pada form registrasi sebelumnya jika ada kesalahan isi.
![Lihat Profile](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/lihat%20profile.png)

5. Karena list user pada oxwall bersifat global, maka user dapat menambah pertemanan dengan user lain yang memiliki akun di oxwall dengan cara mengunjungi halaman browse user
![Halaman browse user](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/browse%20user.png)

6. Untuk dapat menambah pertemanan, user perlu untuk mengunjungi user lain yang ingin diajaka berteman lalu menekan button add friend
![Lihat profile user lain](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/lihat%20air.png)

7. User juga dapat mengirim pesan kepada user lain untuk menerima pertemanannya
![Send pm](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/send%20pm%20air.png)


# Pembahasan
[`^ kembali ke atas ^`](#)

**Oxwall** ditulis dalam bahasa pemrograman PHP yang support untuk penggunaan MySQL. **Oxwall** merupakan salah satu aplikasi web jejaring sosial media (CMS) yang cukup simple dan mudah digunakan dengan kelebihan diantaranya : 
- Tampilan cukup simple (minimalist) dan *light* saat digunakan.
- Tidak menggunakan memori terlalu besar.
- Design aplikasi yang responsif, sehingga dapat digunakan pada berbagai platforms.
- Fitur **Search** yang cukup detail, dapat mencari berdasarkan kriteria tertentu.
- Dapat dikustomisasi baik untuk situs keluarga, forum, maupun jaringan sosial secara enterprise.

Namun, setiap aplikasi pasti memiliki kekurangan dari segi tertentu, Kekurangan dari **Oxwall** ini adalah :
- Dari segi developer, aplikasi ini belum up-to-date, banyak fitur yang belum di*improve* seiring dengan teknologi aplikasi saat ini sehingga Oxwall tidak lebih baik dari aplikasi yang sudah berkembang saat ini.
- Tidak ada pengaturan yang baik pada pengelolaan privasi pengguna. Siapapun dapat melihat aktivitas maupun profil siapa saja.
- Dalam segi UX, pada saat melakukan sesi register terlalu banyak melakukan input data yang tidak dibutuhkan.



Apabila kira membandingkan **Oxwall** dengan jejaring sosial media seperti Facebook, CMS ini memiliki beberapa keunggulan dan kelemahan. Berikut adalah beberapa perbandingan antara Oxwall dengan Facebook ini :

- **Oxwall** menggunakan memori yang lebih ringan daripada **Facebook** karena modulnya lebih sedikit.
- **Facebook** memiliki plugin yang lengkap dan mendukung semua kustomisasi pada setiap fitur dibandingkan **Oxwall**.
- **Oxwall** memiliki fitur search yang detail berdasarkan kriteria tertentu, berbeda dengan **Facebook**
- **Facebook** memiliki pengguna yang jauh lebih banyak daripada **Oxwall** yang aktif pada forum-forum diskusi atau jejaring sosial yang bersifat enterprise. 


# Referensi
[`^ kembali ke atas ^`](#)

1. [About Oxwall](https://www.oxwall.com/about) - Oxwall
2. [Apache Override](https://www.digitalocean.com/community/tutorials/how-to-rewrite-urls-with-mod_rewrite-for-apache-on-ubuntu-16-04) - DigitalOcean
3. [Mysql PHP Problem](https://developers.oxwall.com/forum/topic/55994?page=1) - Oxwall Forum
4. [Cron Jobs Config](https://wiki.oxwall.com/install:cron) - Oxwall Wiki
5. [Oxwall Review](https://alternativeto.net/software/oxwall/reviews/) - Alternativeto
