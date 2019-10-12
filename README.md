# Lapres_Modul2_JA1

## Membuat Topologi Jaringan
### Sintaks topologi.sh
![topologi](https://user-images.githubusercontent.com/42793740/66701805-bace4380-ed2a-11e9-9725-13f9a35bfca1.PNG)
### Setting sysctl (nano /etc/sysctl.conf)
- Hilangkan tagar (#) dari bagian net.ipv4.ip_forward=1
![image](https://user-images.githubusercontent.com/42793740/66699984-00344600-ed16-11e9-86ed-ada8756052f3.png)
- Lalu jalankan sysctl -p untuk mengaktifkan perubahan

### Setting IP di semua UML (nano /etc/network/interfaces)

![interfacearticuno](https://user-images.githubusercontent.com/42793740/66701833-c02b8e00-ed2a-11e9-8dc6-7359ae37f983.PNG)

![interfacemewtwo](https://user-images.githubusercontent.com/42793740/66701834-c0c42480-ed2a-11e9-90a6-83d3fd2eb537.PNG)

![interfacemoltres](https://user-images.githubusercontent.com/42793740/66701835-c0c42480-ed2a-11e9-946c-010725e15f56.PNG)

![interfacepikachu](https://user-images.githubusercontent.com/42793740/66701836-c0c42480-ed2a-11e9-8ccb-4b60fcfa1ca0.PNG)

![interfacepsyduck](https://user-images.githubusercontent.com/42793740/66701837-c15cbb00-ed2a-11e9-851f-c8a0fcb3d655.PNG)

![interfacesnorlax](https://user-images.githubusercontent.com/42793740/66701838-c15cbb00-ed2a-11e9-8be4-fee7507dceff.PNG)

### Restart Network (service networking restart)
### Cek dengan ifconfig
### Jalankan tables.sh (iptables –t nat –A POSTROUTING –o eth0 –j MASQUERADE –s 192.168.0.0/16) agar bisa mengakses jaringan luar
### Export proxy pada setiap UML
![proxy](https://user-images.githubusercontent.com/42793740/66701803-ba35ad00-ed2a-11e9-9584-88d13a907acc.PNG)

### Instalasi bind
- Update package list (apt-get update)
- Install update (apt-get install bind9 -y)

## Soal
1. Membuat domain kanto.a1.com
- Konfigurasi pada Articuno (nano /etc/bind/named.conf.local)

![1](https://user-images.githubusercontent.com/42793740/66701809-bb66da00-ed2a-11e9-8054-569f0b4aad10.PNG)

- Buat folder (mkdir /etc/bind/jarkom)
- Copy file db.local (cp /etc/bind/db.local /etc/bind/jarkom/kanto.a1.com)
- Buka kanto.a1.com lalu edit

![1 1](https://user-images.githubusercontent.com/42793740/66701807-bace4380-ed2a-11e9-92e4-74d7ff33daa9.PNG)

- Setting nameserver di client

![1 2](https://user-images.githubusercontent.com/42793740/66701808-bace4380-ed2a-11e9-8383-e3da156a71ad.PNG)

2. Pembuatan alias http://www.kanto.a1.com
- Tambahkan pada file /etc/bind/jarkom/kanto.a1.com

![2](https://user-images.githubusercontent.com/42793740/66701811-bb66da00-ed2a-11e9-8c95-b27c87dc9df4.PNG)

3. Pembuatan Subdomain http://www.pallet.kanto.a1.com yang diatur di Articuno dan diarahkan ke Mewtwo
- Tambahkan pada file /etc/bind/jarkom/kanto.a1.com

![3](https://user-images.githubusercontent.com/42793740/66701813-bb66da00-ed2a-11e9-9217-8a33614a6292.PNG)

4. Pembuatan Reverse Domain
- Edit di Articuno (nano /etc/bind/named.conf.local)
- Tambah konfigurasi:

![4](https://user-images.githubusercontent.com/42793740/66701814-bbff7080-ed2a-11e9-99c1-f7f08f51a55a.PNG)

- Copy db.local ke file 73.151.10.in-addr.arpa (cp /etc/bind/db.local /etc/bind/jarkom/73.151.10.in-addr.arpa)
- Edit file 73.151.10.in-addr.arpa:
5. DNS server slave pada Moltres
- Edit file /etc/bind/named.conf.local di Articuno:

![5 1](https://user-images.githubusercontent.com/42793740/66701815-bbff7080-ed2a-11e9-9a9c-5994762fe186.PNG)

- Edit file /etc/bind/named.conf.local di Moltres

![5 2](https://user-images.githubusercontent.com/42793740/66701816-bbff7080-ed2a-11e9-83b8-3206f2f94021.PNG)

6. Subdomain http://pewter.kanto.a1.com yang didelegasikan di Moltres dan diarahkan ke Mewtwo
- Edit file /etc/bind/jarkom/kanto.a1.com di Articuno

![6 1](https://user-images.githubusercontent.com/42793740/66701817-bc980700-ed2a-11e9-8b42-e03e543dd135.PNG)

- Edit file /etc/bind/named.conf.options di Articuno lalu tambahkan allow-query{any;};

![6 2](https://user-images.githubusercontent.com/42793740/66701818-bc980700-ed2a-11e9-8432-9af9d4dbc4de.PNG)

- Edit file /etc/bind/named.conf.local di Articuno

![6 3](https://user-images.githubusercontent.com/42793740/66701819-bd309d80-ed2a-11e9-9756-159d4dc9b53f.PNG)

- Edit file /etc/bind/named.conf.options di Moltres

![6 4](https://user-images.githubusercontent.com/42793740/66701820-bdc93400-ed2a-11e9-8c7f-4eee7ee3c1e8.PNG)

- Edit file /etc/bind/named.conf.local di Moltres

![6 5](https://user-images.githubusercontent.com/42793740/66701821-bdc93400-ed2a-11e9-8094-5d3959f21b8a.PNG)

- Buat direktori delegasi dan copy file db.local di Moltres
```
mkdir /etc/bind/delegasi
cp /etc/bind/db.local /etc/bind/delegasi/pewter.kanto.a1.com
```
- Edit file pewter.kanto.a1.com

![6 6](https://user-images.githubusercontent.com/42793740/66701822-bdc93400-ed2a-11e9-96c0-6ff2fa11d8ac.PNG)

7. Buat domain http://vermilion.pewter.kanto.a1.com
- Edit file pewter.kanto.a1.com

![7](https://user-images.githubusercontent.com/42793740/66701823-be61ca80-ed2a-11e9-940d-514be6575316.PNG)

8. Mengatur web server dengan domain http://www.kanto.a1.com yang memiliki DocumentRoot pada /var/www/kanto.a1.com
- Install apache di Mewtwo (apt-get install apache2)
- Install php di Mewtwo (apt-get install php5)
- Edit file default (nano /etc/apache2/sites-available/default)

![8 1](https://user-images.githubusercontent.com/42793740/66701824-be61ca80-ed2a-11e9-8822-e0fbb0fadf07.PNG)

- Buat directory website (mkdir /var/www/kanto.a1.com)
- Pindah ke direktori /etc/apache2/sites-available dan copy file default ke file kanto.a1.com
- Edit file kanto.a1.com

![8 2](https://user-images.githubusercontent.com/42793740/66701825-be61ca80-ed2a-11e9-81e1-ad5c589e82c9.PNG)

- Aktifkan konfigurasi (a2ensite kanto.a1.com)
- Ganti DNS sesuai IP Articuno
- Download file pendukung dengan wget 10.151.36.234/kanto.com.zip di directory /var/www/kanto.a1.com
- Extract file .zip
9. Mod rewrite agar http://kanto.a1.com/index.php/home menjadi http://kanto.a1.com/home
- Aktifkan module rewrite (a2enmod rewrite)
- Pindah ke directory /var/www/kanto.a1.com dan buat file .htaccess dengan isi:

![9](https://user-images.githubusercontent.com/42793740/66701827-befa6100-ed2a-11e9-9238-f3d4ac01da55.PNG)

- Buka /etc/apache2/sites-available/kanto.a1.com lalu tambahkan:

![9 1](https://user-images.githubusercontent.com/42793740/66701826-befa6100-ed2a-11e9-85a3-bb864821e522.PNG)

10. Dibuat web dengan domain http://www.pallet.kanto.a1.com untuk menyimpan file dengan DocumentRoot /var/www/pallet.kanto.a1.com 
- Buat directory website (mkdir /var/www/pallet.kanto.a1.com)
- Pindah ke direktori /etc/apache2/sites-available dan copy file default ke file pallet.kanto.a1.com
- Edit file pallet.kanto.a1.com

![10 1](https://user-images.githubusercontent.com/42793740/66701828-bf92f780-ed2a-11e9-8295-be77ba0b39c8.PNG)

- Aktifkan konfigurasi (a2ensite pallet.kanto.a1.com)
- Download file pendukung dengan wget 10.151.36.234/pallet.kanto.com.zip di directory /var/www/pallet.kanto.a1.com
- Extract file .zip
11. Pada folder /public diperbolehkan directory listing tetapi folder didalamnya tidak diperbolehkan 
- Pada setiap sub-folder didalam folder public dibuat file .htaccess dengan isi:

![11 1](https://user-images.githubusercontent.com/42793740/66701829-bf92f780-ed2a-11e9-8f14-2961d0804e68.PNG)

12. Disediakan file 404.html untuk mengganti error default 404 dari apache
- Edit file /etc/apache2/sites-available/pallet.kanto.a1.com

![12 1](https://user-images.githubusercontent.com/42793740/66701830-bf92f780-ed2a-11e9-935d-39a14494db49.PNG)

![12 2](https://user-images.githubusercontent.com/42793740/66701831-c02b8e00-ed2a-11e9-8009-ddb9b5f8c41f.PNG)

13. 
