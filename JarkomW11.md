Tujuan Praktikum
mahasiswa dapat mempelajari cara kerja protokol DHCP menggunakan Wireshark.

## DHCP
Apa Itu DHCP? DHCP (Dynamic Host Configuration Protocol) adalah protokol yang digunakan untuk memberikan konfigurasi jaringan secara otomatis kepada perangkat yang terhubung ke jaringan. Konfigurasi yang diberikan meliputi IP Address, subnet mask, gateway, dan DNS server, sehingga pengguna tidak perlu mengaturnya secara manual.

Kelebihan DHCP
1. Pemberian IP address menjadi otomatis dan cepat.
2. Memudahkan pengelolaan alamat IP.
3. Menghindari konflik IP address.
4. Mengurangi kesalahan konfigurasi.
5. Cocok untuk jaringan dengan banyak perangkat.

Kekurangan DHCP
1. IP address perangkat dapat berubah-ubah.
2. Memerlukan server DHCP yang dikonfigurasi dengan baik.
3. Jika server DHCP bermasalah, klien tidak dapat memperoleh IP address.
4. Keamanan dapat berkurang jika pengelolaannya kurang baik.

## DORA
DORA adalah proses komunikasi antara klien dan server DHCP untuk mendapatkan IP address secara otomatis. DORA terdiri dari empat tahap, yaitu Discover, Offer, Request, dan Acknowledgement (ACK).

**Langkah-langkah**
1. Download dan setelah itu ekstrak file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
2. Buka file DHCP menggunakan Wireshark

<img width="1600" height="945" alt="image" src="https://github.com/user-attachments/assets/656099ca-98da-4dc7-96d3-271c13c27edc" />

3. Gunakan filter dhcp untuk menampilkan paket DHCP saja

<img width="1918" height="1138" alt="image" src="https://github.com/user-attachments/assets/e05e3015-bad2-4098-b36a-358d55cc7021" />

##  Tahapan DORA

1. Discover

   Client mengirim pesan DHCP Discover untuk mencari server DHCP yang tersedia. Karena belum memiliki IP address, paket dikirim menggunakan alamat 0.0.0.0 dan bersifat broadcast.

2. Offer

   Server DHCP merespons dengan DHCP Offer, yang berisi penawaran IP address dan konfigurasi jaringan lainnya.

3. Request

   Client memilih salah satu penawaran lalu mengirim DHCP Request sebagai tanda persetujuan untuk menggunakan IP address tersebut.

4. Acknowledgement (ACK)

   Server mengirim DHCP ACK untuk mengonfirmasi pemberian IP address. Setelah itu, client dapat mulai menggunakan jaringan.
