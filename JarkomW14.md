# Modul 14 - WIFI

Tujuan Praktikum

Mahasiswa diharapkan mampu memahami cara kerja protokol Wi-Fi melalui pengamatan dan analisis langsung menggunakan Wireshark.

Wi-Fi
Materi pada pertemuan ini membahas jaringan Wi-Fi yang mengacu pada standar IEEE 802.11, yaitu sekumpulan protokol internasional yang dikembangkan oleh Institute of Electrical and Electronics Engineers guna mengatur transmisi data pada jaringan nirkabel di lapisan fisik maupun lapisan MAC.
Dalam implementasinya, jaringan Wi-Fi umumnya beroperasi pada dua pita frekuensi, yaitu 2,4 GHz dan 5 GHz, yang masing-masing memiliki keunggulan dan keterbatasan tersendiri. Pita 2,4 GHz dikenal memiliki jangkauan yang lebih luas dan kemampuan lebih baik dalam menembus hambatan fisik seperti dinding, namun kecepatannya relatif terbatas dan lebih rentan terhadap interferensi akibat banyaknya perangkat rumah tangga yang berbagi spektrum yang sama. Sebaliknya, pita 5 GHz mampu menghadirkan throughput yang lebih tinggi dengan tingkat interferensi yang lebih rendah, sehingga lebih ideal untuk aplikasi yang sensitif terhadap latensi seperti streaming video maupun online gaming, walaupun jangkauannya lebih pendek dan penetrasi terhadap penghalang fisik lebih lemah.
Komponen penting lainnya dalam jaringan nirkabel adalah Access Point (AP), yang berfungsi sebagai perangkat perantara untuk menghubungkan klien nirkabel ke infrastruktur jaringan kabel sekaligus memperluas area cakupan sinyal. Ketika pengguna berpindah lokasi, perangkat secara otomatis akan terhubung ke AP dengan sinyal terkuat di sekitarnya tanpa memerlukan pengaturan ulang secara manual.
Konsep yang tak kalah penting adalah Beacon Frame, yaitu paket yang dikirimkan secara berkala oleh AP sebagai sinyal keberadaan jaringan kepada perangkat-perangkat di sekitarnya. Pada Wireshark, beacon frame dapat ditampilkan menggunakan filter berikut:
wlan.fc.subtype == 8 && wlan.fc.type == 0

Analisis Beacon Frame
Pada tahap ini dilakukan pemeriksaan terhadap file Wireshark_802_11.pcap.

<img width="625" height="258" alt="{F094CB4E-59AA-4AFC-9785-1A08A462E8C0}" src="https://github.com/user-attachments/assets/11ac965e-bcfe-4642-86e8-24fa60312c46" />

Berdasarkan data yang tampil di Wireshark, Beacon Frame dikirimkan secara konsisten dalam interval sekitar 102 milidetik (Time delta from previous displayed frame: 102.350000 ms). Total paket yang berhasil ditangkap mencapai 2.364 paket, dengan 762 paket yang muncul setelah filter diterapkan.
Hasil ekspansi detail pada Frame 100 mengungkap sejumlah parameter teknis berikut:

<img width="331" height="357" alt="{5203529A-BC71-4A04-BCA7-5C177801F204}" src="https://github.com/user-attachments/assets/0d12d594-5696-42a2-b180-535295dff186" />

PHY Type (802.11b HR/DSSS): Lapisan fisik yang digunakan mengacu pada standar 802.11b dengan modulasi High-Rate Direct Sequence Spread Spectrum.
Short Preamble (False): Nilai False menunjukkan bahwa sistem menggunakan Long Preamble untuk menjaga kompatibilitas dengan perangkat generasi lama, meskipun berdampak pada penurunan efisiensi kecepatan.
Channel 6 / Frequency 2437 MHz: Jaringan beroperasi pada kanal 6 dalam spektrum 2,4 GHz.
Signal Strength / Noise Level: Sinyal yang diterima tercatat sebesar -30 dBm (sangat baik), dengan tingkat noise -100 dBm, menghasilkan Signal-to-Noise Ratio sebesar 70 dB.
Data Rate: Kecepatan pengiriman frame saat itu adalah 1,0 Mb/s.

Pemeriksaan Tagged Parameters:

SSID Parameter Set: Nama jaringan Wi-Fi yang teridentifikasi adalah "30 Munroe St".
Supported Rates: Kecepatan yang didukung AP meliputi 1, 2, 5,5, dan 11 Mbps.
Extended Supported Rates: Kecepatan tambahan yang didukung standar yang lebih baru berkisar antara 6 Mbps hingga 54 Mbps.


Analisis Transfer Data
Untuk mengamati proses perpindahan data, diterapkan filter berdasarkan alamat IP server:

<img width="423" height="353" alt="{09E4E25C-8208-4D55-AF88-5B11B18478CF}" src="https://github.com/user-attachments/assets/5fe6e6bd-54a4-4a7b-82b2-061744e5d455" />

ip.addr == 128.119.245.12
Hasil analisis menunjukkan adanya proses Three-Way Handshake TCP (SYN → SYN-ACK → ACK) yang dimulai pada Frame 474, dilanjutkan dengan paket HTTP GET pada Frame 480 untuk mengunduh berkas teks /wireshark-labs/alice.txt melalui protokol HTTP/1.1.
Dari inspeksi lebih lanjut, paket data dikemas menggunakan protokol IEEE 802.11 beserta radiotap header, kemudian diteruskan melalui lapisan Logical-Link Control (LLC) menuju IPv4 dengan alamat sumber klien 192.168.1.109 dan alamat tujuan server 128.119.245.12. Paket HTTP GET ini dikirimkan pada frekuensi 2.437 MHz (Kanal 6, 2,4 GHz) menggunakan standar 802.11g (ERP) dengan kecepatan data 48,0 Mb/s, kekuatan sinyal -38 dBm, dan SNR sebesar 62 dB.

Analisis Association & Disassociation
Filter yang digunakan untuk menampilkan paket asosiasi:
wlan.fc.type_subtype == 0

<img width="490" height="384" alt="{B9619DAA-AB1A-49DF-A0F6-343C61F2869A}" src="https://github.com/user-attachments/assets/9eec0b95-2e5c-4c25-aab1-4446d2ff509c" />

Paket Asosiasi Awal — Frame 1750

<img width="580" height="360" alt="{E1E43E20-1713-4530-BE99-7CDD7F310A1D}" src="https://github.com/user-attachments/assets/9e918b14-84d5-416a-847f-000c4470930d" />

Perangkat Intel_d1:b6:4f (00:13:02:d1:b6:4f) mengirimkan Association Request kepada AP CiscoLinksys_f5:ba:bb (00:18:39:f5:ba:bb) dengan SSID "linksys_SES_24086". Rincian frame yang ditemukan adalah sebagai berikut:

Type/Subtype: Association Request (0x0000)
Frame Control Field: 0x0000
Duration: 314 mikrodetik
Sequence Number: 1607
BSS Id: CiscoLinksys_f5:ba:bb (00:18:39:f5:ba:bb)
WLAN Flags: ........C

Paket Asosiasi Akhir — Frame 2162

<img width="528" height="355" alt="{74B0E6B1-A0E5-4F67-A6B4-00FB41A9830A}" src="https://github.com/user-attachments/assets/02a0c2a5-2489-4feb-ad0a-00e5354ea7bb" />

Pada frame ini, klien yang sama (Intel_d1:b6:4f) telah berpindah lokasi dan mengirimkan Association Request baru ke AP yang berbeda, yaitu CiscoLinksys_f7:1d:51 (00:16:b6:f7:1d:51), dengan SSID "30 Munroe St". Rincian frame-nya adalah:

Type/Subtype: Association Request (0x0000)
Frame Control Field: 0x0000
Duration: 44 mikrodetik
Sequence Number: 1648
BSS Id: CiscoLinksys_f7:1d:51 (00:16:b6:f7:1d:51)
WLAN Flags: ........C

Perbandingan kedua frame tersebut memperlihatkan adanya perpindahan asosiasi klien dari AP dengan SSID "linksys_SES_24086" (Frame 1750) ke AP dengan SSID "30 Munroe St" (Frame 2162), yang mencerminkan mekanisme roaming antar Access Point secara otomatis.
Association Response — Frame 2166
Respons asosiasi dianalisis menggunakan filter:

<img width="431" height="279" alt="{78C13961-6B19-4FA7-8605-B2C7CE3BACE4}" src="https://github.com/user-attachments/assets/8b20e312-6aad-48a8-bf76-7b93c458f0f4" />

wlan.fc.type_subtype == 1
Ditemukan Frame 2166 sebagai Association Response dengan detail berikut:

Type/Subtype: Association Response (0x0001)
Frame Control Field: 0x1000
Duration: 314 mikrodetik
Sequence Number: 3728
Receiver Address: Intel_d1:b6:4f (00:13:02:d1:b6:4f)
Transmitter Address: CiscoLinksys_f7:1d:51 (00:16:b6:f7:1d:51)
BSS Id: CiscoLinksys_f7:1d:51 (00:16:b6:f7:1d:51)

Pada frame ini, Transmitter Address terisi dengan MAC Address milik AP CiscoLinksys_f7:1d:51, yang menandakan bahwa Access Point telah menyetujui dan mengonfirmasi permintaan koneksi dari klien Intel_d1:b6:4f.

Di sini, Transmitter Address diisi oleh MAC Address milik perangkat pengirim respon, yaitu CiscoLinksys_f7:1d:51, sebagai tanda bahwa Access Point menyetujui permintaan koneksi dari klien (Intel_d1:b6:4f).
