# Modul 4 DNS
Tujuan Praktikum
- mahasiswa dapat mempelajari cara kerja protokol DNS menggunakan Wireshark.

## DNS
DNS (Domain Name System) adalah sistem yang mengubah nama domain (seperti google.com) menjadi alamat IP. DNS bekerja dengan mengirim permintaan ke server DNS lokal, lalu menerima hasilnya.

Nslookup adalah perintah yang digunakan untuk melakukan query ke server DNS guna mendapatkan informasi tentang domain atau host, seperti alamat IP, nama domain, dan record DNS lainnya. Perintah ini bekerja dengan mengirim permintaan ke server DNS tertentu, lalu menampilkan hasil responsnya kepada pengguna.

### Contoh Penggunaannya:
1) Perintah nslookup [www.mit.edu](http://www.mit.edu) digunakan untuk mengecek apakah domain tersebut terdaftar dan memiliki alamat IP. Perintah ini mengirim permintaan ke server DNS lalu menampilkan hasilnya. Jika hasilnya domain tidak ditemukan, berarti domain tersebut tidak terdaftar di sistem DNS.
<p align="center">
  <img width="481" height="345" alt="image" src="https://github.com/user-attachments/assets/8a4273b7-e483-44e5-b4b3-858ab8cfc720" width="600"/>
</p>

2) Perintah nslookup -type=NS mit.edu digunakan untuk mengetahui Name Server (NS) yang menangani domain mit.edu. Perintah ini mengirim permintaan ke server DNS untuk melihat server mana saja yang mengelola domain tersebut.
<p align="center">
  <img width="743" height="592" alt="image" src="https://github.com/user-attachments/assets/d65c3a84-ff67-4051-9db4-687187d13d54" width="600"/>
</p>


3) tulis nslookup [www.aiit.or.kr](http://www.aiit.or.kr) bitsy.mit.edu digunakan untuk mencari informasi DNS dari domain
<p align="center">
  <img width="655" height="296" alt="image" src="https://github.com/user-attachments/assets/d3bac046-04bf-4de7-ab75-8fa896090f85" width="600"/>
</p>


## Pertanyaan
1. Mencari IP server web di Asia
- Perintah : nslookup tokopedia.com
- Domain : www.tokopedia.com
- Alamat IP : 47.74.244.18
<p align="center">
  <img width="446" height="186" alt="image" src="https://github.com/user-attachments/assets/5ca6629f-a896-4255-b3c7-367898d2e73b" width="600"/>
</p>

2. Mencari DNS otoritatif universitas di Eropa
- Perintah : nslookup -type=NS ox.ac.uk
<p align="center">
<img width="952" height="488" alt="image" src="https://github.com/user-attachments/assets/c20ee883-fdc0-4c32-803a-83fbd5f259b7" width="600"/>
</p>

3. Mencari mail server Yahoo melalui DNS tertentu
- Perintah : nslookup -type=MX yahoo.com 8.8.8.8
<p align="center">
<img width="827" height="358" alt="image" src="https://github.com/user-attachments/assets/212a2e07-18b3-4b97-a392-917639b40963" width "600"/>
</p>


Ipconfig
Ipconfig digunakan untuk mengelola informasi DNS yang tersimpan di komputer (host). Komputer dapat menyimpan hasil DNS yang baru saja didapat. Untuk melihat data yang tersimpan, setelah prompt C:> masukkan perintah berikut:

1) Tulis "ipconfig /all" digunakan untuk menampilkan informasi lengkap konfigurasi jaringan pada komputer, seperti nama host, status jaringan, alamat IP, subnet mask, gateway, DNS server, dan informasi lain dari adaptor jaringan.
<img width="700" height="1044" alt="{F956874D-EEB2-4158-882F-E8C70A3F5A52}" src="https://github.com/user-attachments/assets/af14e71e-787d-45b5-b908-d8d318971424" />
<img width="698" height="474" alt="{24740678-6315-4905-AC3D-362F6EF2BFC4}" src="https://github.com/user-attachments/assets/c8d9119e-1296-4736-bd77-897274763ef9" />

2) Tulis "ipconfig /all > networkinfo.txt" digunakan untuk menampilkan semua informasi konfigurasi jaringan lalu menyimpannya ke file networkinfo.txt, sehingga bisa dibaca atau dianalisis tanpa harus melihat di Command Prompt.
<img width="347" height="75" alt="{89CB3B9E-CB0D-40D5-8043-535A2BB1855A}" src="https://github.com/user-attachments/assets/00f49ddb-8030-4d73-a55f-a12d4a58555e" />

3) setelah itu tulis "ipconfig /displaydns" Fungsinya untuk menampilkan dns
<img width="737" height="908" alt="{507C6BE0-E798-4E2C-BCAF-A7091B0BA077}" src="https://github.com/user-attachments/assets/c0c85bac-c472-4414-98c3-4af8cea67e8f" />

4) selanjutnya tulis "ipconfig /flushdns" digunakan untuk menghapus cache DNS di komputer. Dengan menghapus cache ini, sistem akan mengambil ulang data DNS terbaru dari server, dan biasanya dipakai untuk mengatasi masalah koneksi atau error DNS.
<img width="362" height="122" alt="{1A34A2D1-DC31-46CF-8394-B3D7B707FC59}" src="https://github.com/user-attachments/assets/7534d354-6b37-40c6-8b3e-a7e09b15b540" />


Tracing DNS dengan Wireshark
Mempelajari cara memantau dan menganalisis paket data DNS yang dikirim dan diterima oleh komputer, sehingga kita bisa melihat bagaimana permintaan domain dikirim ke server dan bagaimana responsnya diterima. Hal ini berguna untuk memahami cara kerja DNS dan membantu dalam troubleshooting jaringan.

## A. Analisis DNS Request dan Response pada Akses Website (www.ietf.org)
langkah-langkah untuk tracing DNS dengan Wireshark:

1) Buka command prompt (CMD) dan ketikan ipconfig untuk menyalin IP Address "192.168.1.104"
<img width="531" height="177" alt="{6F0B9D76-B07E-444A-9CBE-EDB1B9E06B2A}" src="https://github.com/user-attachments/assets/0ec01bf3-996c-478c-b4ea-5d23694b1d80" />

2) Buka aplikasi wireshark kemudian pilih jaringan wifi. Setelah itu filter IP Address "
<img width="1918" height="1006" alt="{14532FB5-0462-4979-A6A3-7B4C8C19431B}" src="https://github.com/user-attachments/assets/5fd4422a-8b05-41d4-8476-7fa6f52ebcdd" />

3) Buka browser http://www.ietf.org/
<img width="1920" height="1045" alt="{DBA05BB5-7128-4489-9BD6-C014BFBA6731}" src="https://github.com/user-attachments/assets/cb2bd5f9-6698-455e-8cfa-89ba11643cde" />

4) Tambahkan filter lagi ip.addr == 192.168.1.104 && dns.qry.name contains "ietf"
<img width="852" height="450" alt="{133297C9-B3AD-4856-B4D1-957B33925A4B}" src="https://github.com/user-attachments/assets/81bc1b6f-247e-4d7c-a170-41f5a9d794ec" />

## Pertanyaan
1. Apakah DNS menggunakan UDP atau TCP?
<img width="955" height="538" alt="image" src="https://github.com/user-attachments/assets/4ce99455-b7e2-494c-afd6-1356de8362ce" />


Dari percobaan yang di lakukan terlihat DNS menggunakan TCP

2. Port tujuan pada DNS request & port sumber pada DNS response
<img width="955" height="538" alt="image" src="https://github.com/user-attachments/assets/a1751e46-f315-40da-9187-874085248f6c" />

Source Port ke 53 (dari server DNS)

Destination Port ke 63199 (kembali ke client)

## B. Analisis DNS Menggunakan Perintah nslookup (www.mit.edu)
Berikut langkah-langkah untuk tracing DNS dengan Wireshark:

1. Buka command prompt (CMD) dan ketikan nslookup www.mit.edu
<img width="481" height="345" alt="image" src="https://github.com/user-attachments/assets/e2080b5f-753b-47ae-81fe-f292b920b270" />


2. Buka aplikasi wireshark kemudian pilih jaringan wifi. Setelah itu filter DNS, lalu ambil data dari Standard query (request) dan Standard query response dari www.mit.edu
<img width="1600" height="948" alt="image" src="https://github.com/user-attachments/assets/ad5a9e08-f748-4e8c-8caa-40cf45fd5663" />

## Pertanyaan
 1. Port tujuan request dan port sumber dari response
<img width="958" height="310" alt="image" src="https://github.com/user-attachments/assets/013858a8-971a-4fe3-89a2-15da7b510529" />


DNS request = destination: 53
<img width="953" height="248" alt="image" src="https://github.com/user-attachments/assets/8c40eb23-b721-40f8-974a-868a50103345" />



DNS response = Source: 53

2. Alamat IP request
<img width="1600" height="947" alt="image" src="https://github.com/user-attachments/assets/16d2bff3-8230-45bd-97fe-dd32352eb9a1" />


Pada percobaan tersebut terlihat bahwa request DNS dikirim ke alamat IP 192.168.1.104

3. Type dan answer request
<img width="1600" height="951" alt="image" src="https://github.com/user-attachments/assets/25dc951c-f2fc-413c-8aae-71005ed9d00f" />

Pada percobaan yang dilakukan, terlihat bahwa tipe yang muncul adalah AAAA , yaitu untuk mencari alamat IPv6. Pesan ini belum berisi jawaban karena masih berupa permintaan untuk mencari alamat IPv6 dari domain [www.mit.edu](http://www.mit.edu).

## C. Analisis DNS Record NS Menggunakan nslookup (mit.edu)
1. Buka CMD ketikan nslookup -type=NS mit.edu

<img width="743" height="592" alt="image" src="https://github.com/user-attachments/assets/f2d7e73d-4282-4afb-8ccb-355e361eecf1" />

2. Buka Wireshark lalu pilih wifi, setelah itu pada bagian filter ketik dns untuk memunculkan bagian dns saja<img width="1600" height="947" alt="image" src="https://github.com/user-attachments/assets/15996b2a-d315-4e56-9b77-97d57d74b1fc" />


3. Ambil data dari Standard query (request) dan Standard query response dari NS mit.edu
<img width="1600" height="948" alt="image" src="https://github.com/user-attachments/assets/e73f6e6d-ff86-48de-bc3d-b5daf90c0f40" />


## Pertanyaan 
1. Alamat IP request
<img width="1600" height="25" alt="image" src="https://github.com/user-attachments/assets/febdc9bb-459b-4923-8380-1137f13952db" />


2. Ketik dan jawab permintaan
<img width="1600" height="949" alt="image" src="https://github.com/user-attachments/assets/c85cd631-9152-4536-a72b-2bb51f7fea83" />


Pada percobaan terlihat bahwa tipe request DNS adalah NS, yang berarti belum berisi jawaban karena masih berupa permintaan saja.

3. Jawab Respon
<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/39d8d40c-7694-49d0-8d66-31702e5921a5" />


## D. Analisis DNS Menggunakan Server Tertentu (www.aiit.or.kr bitsy.mit.edu)
1. Buka CMD ketikan nslookup www.aiit.or.kr bitsy.mit.edu
<img width="655" height="296" alt="image" src="https://github.com/user-attachments/assets/60257192-1386-4559-89d5-99e196dcbab5" />


2. Buka Wireshark lalu pilih wifi, setelah itu pada bagian filter ketik dns untuk memunculkan bagian dns saja
<img width="1600" height="947" alt="image" src="https://github.com/user-attachments/assets/d9586920-0653-4116-bddd-4bc8175d69cc" />

3. Ambil data dari Standard query (request) dari www.aiit.or.kr
<img width="1600" height="947" alt="image" src="https://github.com/user-attachments/assets/d7d51c4c-6d7d-42ac-ad3d-3ead0b08b212" />




## Pertanyaan
1. Alamat IP request
<img width="1600" height="961" alt="image" src="https://github.com/user-attachments/assets/5b26e1b3-c1cc-440a-a9d8-9636ad37b235" />

Pesan permintaan DNS dikirim ke alamat IP 192,168.1.1 Alamat tersebut merupakan server bitsy.mit.edu yang ditentukan secara manual pada perintah nslookup, sehingga bukan merupakan DNS server lokal

2. Type dan answers request
<img width="1600" height="950" alt="image" src="https://github.com/user-attachments/assets/536356e9-9d83-4a6c-ba65-44db73bfa573" />


Tipe DNS request adalah A (Address Record). Pesan ini tidak mengandung jawaban karena hanya berupa permintaan

3. Berdasarkan hasil di Command Prompt, muncul “DNS request timed out” yang berarti server DNS tidak memberikan respons terhadap permintaan yang dikirim.
<p align="center">
  <img width="493" height="160" alt="{964CA9CD-9ED4-4356-9240-3655AD2E028E}" src="https://github.com/user-attachments/assets/62fd5523-37e2-4f8c-a20b-0d0d9df3d7e4" width="600"/>
</p>
