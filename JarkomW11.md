Tujuan Praktikum
Mahasiswa diharapkan dapat memahami mekanisme kerja protokol DHCP melalui pengamatan menggunakan aplikasi Wireshark.
DHCP
Apa Itu DHCP?

## DHCP (Dynamic Host Configuration Protocol) 

merupakan sebuah protokol jaringan yang berfungsi untuk mendistribusikan konfigurasi jaringan secara otomatis kepada setiap perangkat yang terhubung. Informasi yang didistribusikan meliputi alamat IP, subnet mask, gateway, serta DNS server, sehingga pengguna tidak perlu melakukan pengaturan secara manual.
Kelebihan DHCP

Proses pemberian alamat IP berlangsung secara otomatis dan efisien.
Pengelolaan alamat IP menjadi lebih mudah dan terstruktur.
Mencegah terjadinya duplikasi atau konflik alamat IP antar perangkat.
Meminimalkan risiko kesalahan dalam konfigurasi jaringan.
Sangat sesuai diterapkan pada jaringan dengan jumlah perangkat yang banyak.

## Kekurangan DHCP

Alamat IP yang diperoleh perangkat bersifat dinamis dan dapat berubah sewaktu-waktu.
Membutuhkan konfigurasi server DHCP yang tepat agar dapat berjalan dengan baik.
Apabila server DHCP mengalami gangguan, klien tidak dapat memperoleh alamat IP.
Tingkat keamanan jaringan dapat menurun jika pengelolaan DHCP tidak dilakukan dengan baik.

## DORA
DORA merupakan rangkaian proses komunikasi antara klien dan server DHCP untuk memperoleh alamat IP secara otomatis. Proses ini terdiri atas empat tahapan, yaitu Discover, Offer, Request, dan Acknowledgement (ACK).
Langkah-langkah

Pertama-tama Unduh file melalui tautan http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip, kemudian ekstrak file hasil unduhan tersebut.
Lalu Buka file capture DHCP yang telah diekstrak menggunakan aplikasi Wireshark.

<img width="640" height="374" alt="{3D1B901C-5C83-462A-A96D-BAD81756B74F}" src="https://github.com/user-attachments/assets/f256426b-6169-4e9f-8358-628674d913eb" />

Terapkan filter dhcp agar hanya paket-paket DHCP saja yang ditampilkan.

<img width="648" height="365" alt="{838F50EC-6622-4A37-8380-364AB2737D0A}" src="https://github.com/user-attachments/assets/07fa56a2-ade1-4bb8-ad2c-1fc992bd0e5c" />

## Tahapan DORA

Discover – Pada tahap ini, klien mengirimkan pesan DHCP Discover untuk menemukan server DHCP yang tersedia di jaringan. Karena klien belum memiliki alamat IP, pesan tersebut dikirim dari alamat 0.0.0.0 dan disebarkan secara broadcast.
Offer – Setelah menerima pesan Discover, server DHCP akan merespons dengan mengirimkan DHCP Offer yang berisi tawaran alamat IP beserta konfigurasi jaringan lainnya.
Request – Klien memilih salah satu penawaran yang diterima, lalu mengirimkan DHCP Request sebagai bentuk persetujuan untuk menggunakan alamat IP tersebut.
Acknowledgement (ACK) – Sebagai tahap akhir, server mengirimkan DHCP ACK untuk mengonfirmasi bahwa alamat IP telah resmi diberikan kepada klien. Setelah itu, klien dapat mulai menggunakan jaringan.
