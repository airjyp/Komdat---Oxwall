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

Terdapat beberapa konfigurasi dalam aplikasi web Oxwall ini, diantaranya:
- konfigurasi dashboard
- konfigurasi appearance
- konfigurasi user
- konfigurasi pages
- konfigurasi plugin

## konfigurasi dashboard

- untuk mengatur tampilan halaman dashboard admin, kita dapat melakukan customize this page pada menu dashboard
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(16).png)

## konfigurasi appearance

- untuk mempercantik tampilan aplikasi, kita dapat menambahkan atau mengganti tema aplikasi pada menu appearance -> themes
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(18).png)

- untuk melakukan kustomisasi pada theme, dapat dilakukan pada menu appearance -> customize
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(19).png)


## konfigurasi user

- untuk mencari user 
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(2).png)

- untuk menambahkan moderator
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(3).png)

- untuk menambahkan user role dan melakukan permission 
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(4).png)

- untuk menambahkan fitur change, rearrange, dan profile question
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(5).png)

- untuk memblokir user ke dalam daftar
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(6).png)

- Untuk melakukan mass mailing
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(7).png)

## konfigurasi pages

- Untuk menambahkan item pada page, dapat dilakukan di menu pages -> manage pages
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(9).png)

- Untuk mempercantik tampilan web saat dijelajahi, kita dapat mengaktifkan splash screen di menu pages -> special pages. Kita juga dapat melakukan maintenance page
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(10).png)

- Untuk melakukan kustomisasi komponen yang pada tampilan profil user, dilakukan pada menu pages -> user profile
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(11).png)

- Selain itu, kita juga dapat mengatur tampilan dashboard user.  
![konfigurasi](https://github.com/airjyp/Komdat---Oxwall/blob/master/Screenshots/Screenshot%20(12).png)

## konfigurasi plugin


# Maintenance

[`^ kembali ke atas ^`](#)

# Otomatisasi
[`^ kembali ke atas ^`](#)


# Cara Pemakaian
[`^ kembali ke atas ^`](#)

# Pembahasan
[`^ kembali ke atas ^`](#)

# Referensi
[`^ kembali ke atas ^`](#)

1. [About Oxwall](https://www.oxwall.com/about) - Oxwall




