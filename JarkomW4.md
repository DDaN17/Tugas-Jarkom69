# Modul 4 DNS
Nama       : Dyandra
NIM        : 103072400161 
Kelas      : IF-04-05  
Mata Kuliah: Jaringan Komputer  

Tujuan Praktikum
- mahasiswa dapat mempelajari cara kerja protokol DNS menggunakan Wireshark.

## DNS
DNS (Domain Name System) adalah sistem yang mengubah nama domain (seperti google.com) menjadi alamat IP. DNS bekerja dengan mengirim permintaan ke server DNS lokal, lalu menerima hasilnya.

## 4.2 Nslookup
Nslookup adalah perintah yang digunakan untuk melakukan query ke server DNS guna mendapatkan informasi tentang domain atau host, seperti alamat IP, nama domain, dan record DNS lainnya. Perintah ini bekerja dengan mengirim permintaan ke server DNS tertentu, lalu menampilkan hasil responsnya kepada pengguna.

### Contoh Penggunaannya:
1) Perintah nslookup [www.mit.edu](http://www.mit.edu) digunakan untuk mengecek apakah domain tersebut terdaftar dan memiliki alamat IP. Perintah ini mengirim permintaan ke server DNS lalu menampilkan hasilnya. Jika hasilnya domain tidak ditemukan, berarti domain tersebut tidak terdaftar di sistem DNS.
<p align="center">
  <img src= width="600"/>
</p>

2) Perintah nslookup -type=NS mit.edu digunakan untuk mengetahui Name Server (NS) yang menangani domain mit.edu. Perintah ini mengirim permintaan ke server DNS untuk melihat server mana saja yang mengelola domain tersebut.
<img width="743" height="592" alt="image" src="https://github.com/user-attachments/assets/d65c3a84-ff67-4051-9db4-687187d13d54" />



3) tulis nslookup [www.aiit.or.kr](http://www.aiit.or.kr) bitsy.mit.edu digunakan untuk mencari informasi DNS dari domain <img width="655" height="296" alt="image" src="https://github.com/user-attachments/assets/d3bac046-04bf-4de7-ab75-8fa896090f85" />


## Pertanyaan
1. Mencari IP server web di Asia
- Perintah : nslookup tokopedia.com
- Domain : www.tokopedia.com
- Alamat IP : 47.74.244.18
<p align="center">
  <img src="https://github.com/user-attachments/assets/afe7f114-6f3e-44b0-aa8b-e31d080ddd01" width="600"/>
</p>

2. Mencari DNS otoritatif universitas di Eropa
- Perintah : nslookup -type=NS ox.ac.uk
![3b973efd-9238-43be-8fc7-0b97908537ec](https://github.com/user-attachments/assets/fdaf7dd8-345a-4d46-a164-77694394215b)

3. Mencari mail server Yahoo melalui DNS tertentu
- Perintah : nslookup -type=MX yahoo.com 8.8.8.8
![c37f8f31-f382-43bf-964b-f2f623b02383](https://github.com/user-attachments/assets/31809d8a-06d1-4385-8236-b85be2da6a1d)


## 4.3 Ipconfig
Ipconfig digunakan untuk mengelola informasi DNS yang tersimpan di komputer (host). Komputer dapat menyimpan hasil DNS yang baru saja didapat. Untuk melihat data yang tersimpan, setelah prompt C:> masukkan perintah berikut:

1) Tulis "ipconfig /all" digunakan untuk menampilkan informasi lengkap konfigurasi jaringan pada komputer, seperti nama host, status jaringan, alamat IP, subnet mask, gateway, DNS server, dan informasi lain dari adaptor jaringan.
![82105b20-e900-44f1-8db8-5b3f23528501](https://github.com/user-attachments/assets/75fbb0f0-f9d0-4a70-a02d-2019f51d58bd)

2) Tulis "ipconfig /all > networkinfo.txt" digunakan untuk menampilkan semua informasi konfigurasi jaringan lalu menyimpannya ke file networkinfo.txt, sehingga bisa dibaca atau dianalisis tanpa harus melihat di Command Prompt.
![96d18130-f67f-4d43-af75-50d8e2157673](https://github.com/user-attachments/assets/704a370a-22c9-4111-b996-21908299e008)

3) habis itu tulis "ipconfig /displaydns" Fungsinya untuk menampilkan dns
![209cffc3-2927-4df1-b5cf-7fc76b98a4e7](https://github.com/user-attachments/assets/d31c3dc3-c0be-4ac2-b07c-c06ac3053a0b)

4) selanjutnya tulis "ipconfig /flushdns" digunakan untuk menghapus cache DNS di komputer. Dengan menghapus cache ini, sistem akan mengambil ulang data DNS terbaru dari server, dan biasanya dipakai untuk mengatasi masalah koneksi atau error DNS.
![8e95b9dc-1dd8-4644-bc35-24adac154571](https://github.com/user-attachments/assets/039db82e-a2ad-4ba3-9cd4-9106fac8c1e8)

# 4.4 Tracing DNS dengan Wireshark
Mempelajari cara memantau dan menganalisis paket data DNS yang dikirim dan diterima oleh komputer, sehingga kita bisa melihat bagaimana permintaan domain dikirim ke server dan bagaimana responsnya diterima. Hal ini berguna untuk memahami cara kerja DNS dan membantu dalam troubleshooting jaringan.

## A. Analisis DNS Request dan Response pada Akses Website (www.ietf.org)
Berikut langkah-langkah untuk tracing DNS dengan Wireshark:

1) Buka command prompt (CMD) dan ketikan ipconfig untuk menyalin IP Address "192.168.1.104"
![cb78eb20-ad87-4ef1-b17e-f3383995bfb4](https://github.com/user-attachments/assets/113fc00d-47c0-4795-895c-2090fc485bb9)

2) Buka aplikasi wireshark kemudian pilih jaringan wifi, karena kita menggunakan wifi. Setelah itu filter IP Address "
![87058418-1c40-4c41-b67a-4f1f6060a36e](https://github.com/user-attachments/assets/f49928a9-3ce0-468e-88a2-b82f21a50284)

3) Buka browser http://www.ietf.org/
![5662412e-df6d-4397-ad74-8ab15b5f9495](https://github.com/user-attachments/assets/dd1aa45f-db67-45cf-953d-cd4edb13b610)

4) Tambahkan filter lagi ip.addr == 192.168.1.104 && dns.qry.name contains "ietf"
![14ca8ff6-2317-4ab4-8bff-0401d7af7fb2](https://github.com/user-attachments/assets/9885f7c1-a88c-4a78-b513-6f042969a47a)

## Pertanyaan
1. Apakah DNS menggunakan UDP atau TCP?
![71487c76-a598-47b7-9853-7cdba3ec646b](https://github.com/user-attachments/assets/e7ac18f6-dfad-403b-92f6-3ac6f37d061e)

Dari percobaan yang di lakukan terilhat bahwa DNS menggunakan TCP

2. Port tujuan pada DNS request & port sumber pada DNS response
![71487c76-a598-47b7-9853-7cdba3ec646b](https://github.com/user-attachments/assets/e7ac18f6-dfad-403b-92f6-3ac6f37d061e)

Source Port → 53 (dari server DNS)

Destination Port → 63199 (kembali ke client)

## B. Analisis DNS Menggunakan Perintah nslookup (www.mit.edu)
Berikut langkah-langkah untuk tracing DNS dengan Wireshark:

1. Buka command prompt (CMD) dan ketikan nslookup www.mit.edu
![91b3eb7d-ece3-4194-b766-ad7aa5e08633](https://github.com/user-attachments/assets/163d9ba4-bca2-4f80-aaca-1bb9645d5647)

2. Buka aplikasi wireshark kemudian pilih jaringan wifi, karena kita menggunakan wifi. Setelah itu filter DNS, lalu ambil data dari Standard query (request) dan Standard query response dari www.mit.edu
![2d0c3659-591f-4806-b8b4-ef7e30d8b502](https://github.com/user-attachments/assets/999e6bbe-def1-4f9a-b4e7-756c7fd25cdb)

## Pertanyaan
 1. Port tujuan request dan port sumber dari response
![03aaa354-5d6e-4ccd-90d7-c1334ad47293](https://github.com/user-attachments/assets/38bc1582-88b8-42d5-9208-0e0ce17be64c)

- DNS request = destination: 53
![2e7bc122-9a70-4972-96d0-25df0ad2d87e](https://github.com/user-attachments/assets/6c9e3693-d9c8-4bc0-9358-1eda78bfdac5)

- DNS response = Source: 53

2. Alamat IP request
![e425ea4a-1a4b-443b-9326-eeaf90757f74](https://github.com/user-attachments/assets/291db277-b63e-4ee4-80b4-e821b1a43d4f)

Pada perjobaan tersebut terlihat bahwa request DNS dikirim ke alamat IP 192.168.1.104

3. Type dan answer request
![46266650-0691-4200-8829-b160be42b5c5](https://github.com/user-attachments/assets/71e4635d-06f6-4886-8004-34bb583a1f2f)

Pada percobaan yang dilakukan, terlihat bahwa tipe yang muncul adalah AAAA (IPv6 Address Record), yaitu untuk mencari alamat IPv6. Pesan ini belum berisi jawaban karena masih berupa permintaan (query) untuk mencari alamat IPv6 dari domain [www.mit.edu](http://www.mit.edu).

## C. Analisis DNS Record NS Menggunakan nslookup (mit.edu)
1. Buka CMD ketikan nslookup -type=NS mit.edu
![a05da96d-e2fa-4615-ba26-406200b33ebb](https://github.com/user-attachments/assets/80998167-398e-40d6-8a83-9fdc20ca3314)

2. Buka Wireshark lalu pilih wifi, setelah itu pada bagian filter ketik dns untuk memunculkan bagian dns saja
![5586f131-531e-4e56-bbf9-c1196989d3a2](https://github.com/user-attachments/assets/b1f64d02-cecc-4155-bc5c-94346ff65591)

3. Ambil data dari Standard query (request) dan Standard query response dari NS mit.edu
![ee0853fd-5505-417f-bc70-90862e212aee](https://github.com/user-attachments/assets/a1284b5a-4725-4e5c-925d-bee15cfc08f1)


## Pertanyaan 
1. Alamat IP request
![f39b8711-7bed-4c29-9d8a-8573cd556646](https://github.com/user-attachments/assets/e39348c2-36d9-4360-8bc3-0294458377d1)

2. Ketik dan jawab permintaan
![d1eed941-30b0-4beb-8a37-4f1986d162a2](https://github.com/user-attachments/assets/d568c711-4aae-40d8-98ea-91c3ec44221c)

Pada percobaan terlihat bahwa tipe request DNS adalah NS, yang berarti belum berisi jawaban karena masih berupa permintaan saja.

3. Jawab Respon
![07c464ee-4d2b-4684-b5a4-bda36c8363b1](https://github.com/user-attachments/assets/8077af74-01b4-4a8e-9d4c-c8e5fed7813f)

## D. Analisis DNS Menggunakan Server Tertentu (www.aiit.or.kr bitsy.mit.edu)
1. Buka CMD ketikan nslookup www.aiit.or.kr bitsy.mit.edu
![186b7acc-c965-40f9-8792-2a81927d3c84](https://github.com/user-attachments/assets/619f0785-384b-47cf-9705-94da4bc67199)


2. Buka Wireshark lalu pilih wifi, setelah itu pada bagian filter ketik dns untuk memunculkan bagian dns saja
![5586f131-531e-4e56-bbf9-c1196989d3a2](https://github.com/user-attachments/assets/b1f64d02-cecc-4155-bc5c-94346ff65591)

3. Ambil data dari Standard query (request) dari www.aiit.or.kr
![9e350ae2-c24d-4431-9413-b61b75aeb522](https://github.com/user-attachments/assets/59cbb937-3989-49e2-9cbe-85f6ea146876)


## Pertanyaan
1. Alamat IP request
![72ef48ea-a973-4837-a046-ff4610fa0e29](https://github.com/user-attachments/assets/ecb09d2d-00d1-4d32-a41f-c8c981b52cf7)

Pesan permintaan DNS dikirim ke alamat IP 192,168.1.1 Alamat tersebut merupakan server bitsy.mit.edu yang ditentukan secara manual pada perintah nslookup, sehingga bukan merupakan DNS server lokal

2. Type dan answers request
![3a08bb46-4542-4e10-a2a9-c1897247d7f5](https://github.com/user-attachments/assets/a34b4dba-21f3-42c9-b2ca-48383f698510)

Tipe DNS request adalah A (Address Record). Pesan ini tidak mengandung jawaban karena hanya berupa permintaan

3. Berdasarkan hasil di Command Prompt, muncul “DNS request timed out” yang berarti server DNS tidak memberikan respons terhadap permintaan yang dikirim.
<p align="center">
  <img src="https://github.com/user-attachments/assets/10f41eb8-61f7-4fca-963a-7d1b65ff5e49" width="600"/>
</p>
