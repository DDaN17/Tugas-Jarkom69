# Modul 10 - IP

Tujuan Praktikum
mahasiswa dapat mempelajari cara kerja protokol IP menggunakan Wireshark.

## 1. IP address
IP Address (Internet Protocol Address) adalah alamat unik yang digunakan untuk mengenali perangkat dalam jaringan. IP address berfungsi untuk membantu data dikirim ke perangkat tujuan dengan benar.

**Jenis-jenis**
- IPv4 : menggunakan 32-bit contoh:  192.168.184.1
- IPv6 : menggunakan 128-bit contoh: 2001:db8::1

Seperti ini

<img width="634" height="171" alt="{ACD97C13-AE0A-43D6-84A2-211A0565AB59}" src="https://github.com/user-attachments/assets/ddf5e0db-acb9-4990-9957-433b1e754fe9" />
/>

 Link-local IPv6 Address . . . . . : fe80::ca5b:cd0b:a9ca:2fd7%7
 IPv4 Address. . . . . . . . . . . : 192.168.1.9

## 2. Traceroute dari suatu website
Traceroute adalah metode yang digunakan untuk mengetahui jalur atau hop yang dilewati paket data dari komputer menuju server tujuan.

**Fungsi Traceroute**
 Menampilkan jalur (hop) yang dilewati data.
 Mengetahui waktu tempuh pada setiap hop.
 Membantu mendeteksi masalah jaringan.

**Cara Melihat Traceroute dari Website**
1. Buka CMD
2. Ketik tracert google.com
<img width="631" height="520" alt="{D2404E53-B7E9-447D-A7CA-CE0F58C106BC}" src="https://github.com/user-attachments/assets/27d69e4b-e0d1-4dc2-8b4e-6e53efa52995" />

Paket melewati 25 hop sebelum sampai ke server Google. Hop 1 (192.168.100.1) adalah router lokal / gateway Wi-Fi yang digunakan. Hop 2–3 (10.112.0.1 dan 180.250.252.69) adalah jaringan internal ISP. Hop 4–6 (180.240.190.77 dan 180.240.205.92) sudah masuk ke jaringan publik. Hop 7–12 (72.14.221.180 hingga 216.239.35.173) sudah masuk ke jaringan Google. RTO pada hop 13–24 terjadi karena router tidak merespon traceroute (firewall memblokir paket ICMP). Pada hop ke 25 paket berhasil sampai ke server Google (sa-in-f100.1e100.net = 74.125.200.100 = google.com). Waktu yang ditempuh relatif cepat dalam kisaran 1 ms – 40 ms, maka jaringan dalam kondisi yang baik.

## 3. ICMP, MTU, TTL
### ICMP (Internet Control Message Protocol)
ICMP (Internet Control Message Protocol) adalah protokol yang digunakan untuk memberikan informasi tentang kondisi jaringan, seperti pelaporan kesalahan dan pengecekan koneksi.

 Perintah ping untuk menguji koneksi antar perangkat.
 Traceroute/Tracert untuk mengetahui jalur yang dilewati paket data.
 Mengirim pesan kesalahan jika terjadi masalah pada pengiriman data.

### MTU (Maximum Transmission Unit)
MTU (Maximum Transmission Unit) adalah ukuran maksimum data yang dapat dikirim dalam satu frame jaringan. Pada jaringan Ethernet, MTU umumnya sebesar 1500 byte. Jika ukuran paket melebihi MTU, paket akan dipecah menjadi beberapa bagian yang disebut fragmentasi.

### TTL (Time To Live)
TTL (Time To Live) adalah batas jumlah router (hop) yang dapat dilewati oleh paket data. Setiap kali paket melewati router, nilai TTL berkurang 1. Jika TTL mencapai 0, paket akan dibuang dan router mengirim pesan ICMP Time Exceeded. TTL digunakan untuk mencegah paket terus berputar di jaringan akibat kesalahan routing.

## 4. Fragmentasi 
Fragmentasi adalah proses membagi paket IP menjadi beberapa bagian yang lebih kecil ketika ukuran paket melebihi nilai MTU jaringan.

Hasil Fragmentasi:
1. Buka Wireshark dan pilih jaringan wifi
2. Buka terminal masukkan ini "ping google.com -l 2000"
3. Kembali ke wireshark stop capture, lalu filter "ip.flags.mf == 1 || ip.frag_offset > 0"

<img width="595" height="357" alt="{456032F7-5820-4863-8256-E10CEACA6ECC}" src="https://github.com/user-attachments/assets/41fc71b0-1336-45cf-93d6-f584b752293e" />

Berdasarkan hasil capture menggunakan Wireshark, ditemukan paket dengan keterangan Fragmented IP protocol (proto=ICMP 1, off=0) yang menunjukkan terjadinya fragmentasi pada paket ICMP yang dikirim dari 192.168.100.132 menuju 74.125.200.101. Paket memiliki ukuran sebesar 1514 bytes yang melebihi batas MTU (±1500 byte) sehingga paket perlu dipecah menjadi beberapa fragment, dengan nilai Identification yang berbeda-beda (ID=7eff, ID=7f00, ID=7f01, ID=7f02) yang menandakan setiap kelompok fragment berasal dari satu paket ICMP yang unik. Nilai Fragment Offset (off=0) menunjukkan bahwa setiap paket yang terfragmentasi merupakan urutan fragment pertama, dan ditemukan keterangan Reassembled in #24571, #25056, #25834, #26292 yang menunjukkan bahwa masing-masing fragment berhasil digabung kembali. Sehingga dapat disimpulkan bahwa paket ICMP yang dikirim mengalami fragmentasi sebanyak 4 kali dalam rentang waktu sekitar 14 detik (03:31:13 – 03:31:27), dan meskipun setiap fragment berhasil di-reassemble, seluruh paket ping tidak mendapatkan respons dari host tujuan (no response found!) yang kemungkinan menandakan adanya pemblokiran atau ketidaktersediaan host tujuan.

## 5. IPv6 
IPv6 adalah versi terbaru dari Internet Protocol yang digunakan untuk komunikasi data di internet. IPv6 menggunakan alamat 128-bit, sehingga mampu menyediakan jauh lebih banyak alamat IP dibandingkan IPv4.

### Analisis IPv6 di Wireshark
1. Buka file ipv6_sample.pcap di wireshark

<img width="477" height="349" alt="{D9F72AF9-8350-40D6-BCA8-D393451F6038}" src="https://github.com/user-attachments/assets/de61fbf2-059b-438b-9bcc-34b3db756235" />

2. Filter "ipv6"

<img width="592" height="351" alt="{74A83015-E31F-46B5-8C4B-7CCD532F7EFF}" src="https://github.com/user-attachments/assets/17243e69-7c4b-4573-b034-0b2013239cd6" />

Hasil penyaringan menggunakan filter ipv6 pada Wireshark menunjukkan adanya trafik dengan protokol IPv6, yang ditunjukkan oleh keterangan Internet Protocol Version 6 pada panel detail paket serta susunan protokol eth:ethertype:ipv6:tcp:tls pada frame yang dianalisis. Hal ini juga diperkuat oleh alamat Source 2001:db8:1::10 dan Destination 2a00:1450:4009:80b:: yang ditulis dalam format heksadesimal dengan pemisah tanda titik dua (:), sesuai dengan karakteristik penulisan alamat IPv6.
Paket IPv6 tersebut dienkapsulasi di dalam frame Ethernet (Encapsulation type: Ethernet) dengan alamat MAC Source CIMSYS_33:44:55 dan MAC Destination 66:77:88:99:aa:bb. Pada bagian Next Header terlihat bahwa protokol lapisan berikutnya adalah TCP dengan tujuan port 443 (HTTPS), yang menandakan adanya komunikasi web yang dienkripsi melalui TLS/SSL. Ukuran frame tercatat sebesar 1468 bytes, dengan total 35 paket yang berhasil ditangkap selama proses capture.
Berdasarkan temuan tersebut, dapat disimpulkan bahwa komunikasi jaringan berbasis IPv6 berhasil teramati dengan baik. Namun, terdapat indikasi gangguan pada koneksi, yang ditunjukkan oleh banyaknya TCP Retransmission pada hampir seluruh paket (no. 3 sampai 21) dengan flag [PSH, ACK], serta munculnya keterangan TCP Previous segment not captured pada paket no. 2. Kondisi tersebut diduga disebabkan oleh ketidakstabilan jaringan atau kegagalan pengiriman paket pada percobaan awal.
