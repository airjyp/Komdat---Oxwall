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
1. Lakukan instalasi Ubuntu server di Virtualbox (Ubuntu-server.vdi), kemudian setting port forwarding http dengan port 8888 dan ssh dengan port 2222.
2. Nyalakan Ubuntu servernya, login dengan menggunakan user dan password student
3. Lakukan update server
```
$ sudo apt update
```

4. Install ssh pada Ubuntu server
```
$ sudo apt install ssh
```

5. Buka Ubuntu bash, kemudian login ke dalam server menggunakan SSH
```
$ ssh student@localhost –p 2222
```

6. Install seluruh kebutuhan sistem yang diperlukan seperti`Apache`, `PHP`, dan `MySQL`. 
```
$ sudo apt install apache2 
$ sudo apt install mysql-server
$ sudo apt install php
$ sudo apt install libapache2-mod-php 
$ sudo apt install php-mysql php-zip php-gd php-json php-readline php–mcrypt  php-mbstring php-xml php-ssh2
$ sudo service apache2 restart
```

7. Cek instalasi apache di http://localhost:8888/
8. Buat database untuk oxwall 
```
$ mysql –u root –p –e "
    CREATE DATABASE oxwall;
    GRANT ALL PRIVILEGES ON `oxwall`.* TO 'oxwall'@'localhost' IDENTIFIED BY 'student';
    FLUSH PRIVILEGES;"
```

9. Install terlebih dahulu zip untuk mengekstrak data oxwall
```
$ sudo apt install zip && sudo apt install unzip
```

10. Unduh oxwall
```
$ wget –c http://ow.download.s3.amazonaws.com/oxwall-1.8.4.1.zip
```

11. Setelah mengunduh oxwall, unzip oxwall tersebut 
```
$ unzip 0xwall-1.8.4.1.zip –d oxwall
```

12. Pindahkan folder oxwall
```
$ sudo mv oxwall /var/www/html
```

13. Tukar ownership direktori oxwall 
```
$ sudo chown –R www-data:www-data /var/www/oxwall
```

14. Karena oxwall menggunakan .htaccess dan secara default diblock oleh apache, maka perlu dilakukan beberapa konfigurasi

15. Aktifkan mod rewrite
```
$ sudo a2enmod rewrite 
$ sudo systemctl restart apache2
```

16. ini apaaaa
```
$ sudo nano /etc/apache2/sites-available/000-default.conf
```

17. Tambahkan ini tepat di bawah <VirtualHost *:80> untuk mengizinkan akses .htaccess
18. Restart apache, lalu cek halaman “localhost:888/oxwall”
```
$ sudo systemctl restart apache2
```

19. Ketika sudah masuk halaman oxwall, akan muncul peringatan mysql php extension belum terinstall, karena oxwall tidak bisa membaca php-mysql dari php 7, triknya yaitu menghapus requirement mysql pada oxwall
20. ini apaaaa
```
$sudo nano /var/www/html/oxwall/ow_install/files/requirements.txt
```

21. Hapus mysql pada file tersebut, save dengan ctrl+o
22. Cek kembali localhost:8888/oxwall , maka oxwall sudah bisa digunakan

# Konfigurasi

[`^ kembali ke atas ^`](#)

- Untuk menentukan konfigurasi umum, batasan upload file, batas memori yang diperlukan, dan ekstensi/format file yang dapat diupload , dapat dilakukan dengan membuka submenu Content settings yang terdapat pada menu Settings dan mengisi field sesuai kebutuhan.
![content_setting](https://github.com/airjyp/Komdat---Oxwall/blob/master/konfigurasi/content_setting.png)

- Kita dapat membatasi batas upload size untuk avatar pada user di submenu User setting 
![content_setting](https://github.com/airjyp/Komdat---Oxwall/blob/master/konfigurasi/user_setting.png)

- Untuk melengkapi dan melakukan improve pada aplikasi, kita dapat menambahkan fitur tertentu pada menu Available Plugins.
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(14).png)

- Untuk mengupload dan menambahkan plugin secara manual, dapat dilakukan pada menu Add New.
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(15).png)

- Kita dapat mempercantik tampilan aplikasi dengan menambahkan atau mengganti tema aplikasi pada submenu Themes di Appearance.
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(18).png)


# Maintenance

[`^ kembali ke atas ^`](#)

Maintenance dibutuhkan untuk melakukan improvisasi dan kualitas pada aplikasi. Salah satu dari aktivitas maintenance adalah melakukan modifikasi, memperbaiki fitur yang ada, maupun meningkatkan performa aplikasi kita. Oleh karena itu, kita perlu mengaktifkan fitur Maintenance mode saat akan melakukan maintenance, agar tidak ada client yang mengakses aplikasi selama proses maintenance berjalan. Berikut ini adalah langkah-langkah yang harus dilakukan :

1. Login ke dalam admin aplikasi kita.
2. Klik submenu special pages pada menu Pages.
![pages](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/pages.png)

3. Checked / Unchecked box untuk masuk ke dalam mode maintenance.
![maintenance](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/maintenance.png)

4. Untuk menyampaikan pesan yang ingin disampaikan kepada orang yang akan mengakses aplikasi web saat mode maintenance, kita dapat menambahkan pesan di Maintenance message.
5. Klik tombol save untuk menyimpan perubahan.



# Otomatisasi
[`^ kembali ke atas ^`](#)


# Cara Pemakaian
[`^ kembali ke atas ^`](#)

# Pembahasan
[`^ kembali ke atas ^`](#)

# Referensi
[`^ kembali ke atas ^`](#)

1. [About Oxwall](https://www.oxwall.com/about) - Oxwall




