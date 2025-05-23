# CRUD Siswa

#
# Cara mendeploy Aplikasi

## Langkah Pertama/Persiapan 
1. Download file psat di https://github.com/paknux/psat2425
2. Kemudian ekstrak file ke D
4. Buka visual studio code lalu masukan file yang telah di download dan simpan semua filenya (ctrl+s) dan buat file.env kosong
5. Masuk ke github dan buat repository baru (klik new berwarna hijau) lalu isi nama repository barunya (diisi sesuai keinginan atau psat2425)

contoh isi file .env 
 
DB_USER=admin
DB_PASS=P4ssw0rd123
DB_NAME=psat2425
DB_HOST=rdsku.czt6n8ylfvyb.us-east-1.rds.amazonaws.com


## Langkah Push ke GitHub
Buka Visual Studio Code dan buka new terminal, kemudian :
1. git -- version
2. git config --global user.name (username github anda) MeilianaArgi 
3. git config --global user.email (email yang digunakan untuk github) mlntdr58@gmail.com 
4. git init
5. git remote add origin (repository github anda) https://github.com/MeilianaArgi/psat2425
6. git add .
7. git branch -M main
8. git commit -m “first commit”
9. git push -u origin main

## Cara membuat Database di AWS (Aurora & RDS) 

Langkah-langkah:
1. Buka RDS kemudian Create Database 
2. Pilih engine yang akan digunakan: MySQL
3. Pada bagian Templates pilih opsi Free Tier lalu bisa pilih db.t3.micro 
4. Isi Database nama, username, dan password, kemudian confirm password 
5. Untuk Public Access pilih: No
6. Pastikan security group-nya mengizinkan akses dari IP-mu (port 3306)

## Langkah-langkah EC2 Instance
1. Pada Application and OS pilih: Ubuntu
2. Untuk Instance Type pilih: t2.micro
3. Pada Key Pair pilih: vockey
4. Untuk Security Group atur:
         • HTTP (80)
         • HTTPS (443)
         • Allow SSH (22)
         • IP 0.0.0.0/0

## Kemudian tambahkan Script Otomatis di "User Data" pada EC2 Instance 
```
#!/bin/bash
sudo apt update -y
sudo apt install -y apache2 php php-mysql libapache2-mod-php mysql-client
sudo rm -rf /var/www/html/{*,.*}
sudo git clone https://github.com/paknux/crudsiswa.git /var/www/html
sudo chmod -R 777 /var/www/html
echo DB_USER=admin > /var/www/html/.env
echo DB_PASS=P4ssw0rd123  >> /var/www/html/.env
echo DB_NAME=crudsiswa  >> /var/www/html/.env
echo DB_HOST=rds11tjkt1.czt6n8ylfvyb.us-east-1.rds.amazonaws.com >> /var/www/html/.env
sudo apt install openssl
sudo a2enmod ssl
sudo a2ensite default-ssl.conf
sudo systemctl reload apache2
```
## Akses atau Buka Manual di Terminal EC2

Langkah-langkah:
1. Klik menu Instance 
2. Klik Instance ID kemudian pilih Connect 
3. Scroll ke bagian paling lalu klik tombol Connect disebelah kanan bawah

## Untuk menjalankan otomatis.sh ada 2 cara:

1. Dieksekusi Langsung dengan perintah
```
        $ bash otomatis.sh 
```
2. Dibuat menjadi executable dan dieksekusi dengan perintah 
```
         $ chmod +x otomatis.sh
         $ ./otomatis.sh
```
## Jalankan

Jalankan dengan username dan password berikut:

• username: admin </br>
• password: 123

Gitu kali yaa