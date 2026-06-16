Modul 13 - ARP
Tujuan Praktikum

Mahasiswa diharapkan mampu memahami cara kerja protokol ARP melalui pengamatan langsung menggunakan aplikasi Wireshark.

ARP (Address Resolution Protocol)
Pengertian ARP

ARP atau Address Resolution Protocol adalah protokol jaringan yang bertugas menemukan dan menghubungkan alamat MAC dengan alamat IP dalam satu jaringan lokal (LAN). Keberadaannya sangat penting karena meski perangkat dikenali lewat alamat IP secara logis, pengiriman data aktual dalam jaringan lokal tetap bergantung pada alamat MAC sebagai identitas fisik perangkat.

Konsep ARP
ARP berfungsi sebagai jembatan yang menghubungkan dua jenis pengalamatan: IP dan MAC. Berkat protokol ini, suatu perangkat dapat mengetahui alamat fisik dari perangkat lain yang dituju, sehingga pengiriman data dalam jaringan lokal dapat berlangsung secara tepat sasaran.

Konsep Dasar ARP
Dalam model OSI, ARP menempati posisi di antara Network Layer (Layer 3) dan Data Link Layer (Layer 2). Ketika sebuah perangkat hendak berkomunikasi dengan perangkat lain dalam satu LAN, ia wajib mengetahui MAC Address tujuan terlebih dahulu. Apabila hanya alamat IP yang tersedia, ARP digunakan untuk mencari MAC Address yang sesuai.
Untuk menghindari pengulangan proses pencarian, hasil pemetaan antara IP dan MAC Address disimpan sementara dalam tabel yang disebut ARP Cache.

Mekanisme Kerja ARP

Perangkat pengirim menentukan alamat IP dari perangkat yang ingin dihubungi.
Sistem memeriksa ARP Cache untuk mengecek apakah MAC Address tujuan sudah pernah tersimpan sebelumnya.
Bila data tidak ditemukan, perangkat menyebarkan paket ARP Request secara broadcast ke seluruh anggota jaringan.
Perangkat yang memiliki alamat IP sesuai akan memberikan balasan berupa ARP Reply.
Balasan tersebut membawa informasi MAC Address milik perangkat tujuan.
Pengirim kemudian mencatat pasangan IP dan MAC Address tersebut ke dalam ARP Cache.
Setelah MAC Address diketahui, pengiriman data ke perangkat tujuan dapat dilakukan secara langsung.


Jenis Pesan pada ARP
ARP Request

ARP Request adalah pesan yang dikirim untuk menanyakan MAC Address dari suatu alamat IP tertentu. Pesan ini disebarkan secara broadcast sehingga semua perangkat dalam jaringan lokal dapat menerimanya.
ARP Reply

ARP Reply merupakan pesan balasan dari perangkat yang alamat IP-nya cocok dengan permintaan. Respons ini memuat informasi MAC Address dan dikirimkan langsung kepada perangkat yang mengajukan pertanyaan.
ARP Cache

ARP Cache adalah memori sementara yang menyimpan daftar pasangan alamat IP dan MAC Address yang telah diketahui. Dengan adanya ARP Cache, frekuensi pengiriman ARP Request dapat dikurangi, sehingga komunikasi jaringan menjadi lebih efisien dan cepat.

Analisis ARP pada Wireshark

Buka Command Prompt (CMD) dengan hak akses Administrator, lalu jalankan perintah arp -d * untuk menghapus seluruh entri dalam ARP Cache. Setelah ini, komputer akan memulai proses ARP dari awal saat mencoba berkomunikasi dengan perangkat lain di jaringan.

Buka aplikasi Wireshark, kemudian navigasikan ke menu Analyze → Enabled Protocols → IPv4 guna memastikan protokol IPv4 telah aktif dan siap dianalisis.
Mulai proses capture pada Wireshark.
Buka browser dan akses alamat http://gaia.cs.umass.edu/wireshark-labs/HTTP-ethereal-lab-file3.html.
Hentikan proses capture pada Wireshark.
Terapkan filter dengan mengetik: arp

<img width="1100" height="596" alt="image" src="https://github.com/user-attachments/assets/63e20137-dbfd-496c-bece-70d07631c088" />

Pilih salah satu paket hasil tangkapan untuk diperiksa lebih lanjut.

<img width="1600" height="627" alt="image" src="https://github.com/user-attachments/assets/ac2232de-36f4-4832-a9be-d610727b9f24" />

Dari hasil capture Wireshark, paket yang dipilih untuk dianalisis adalah ARP Request (Opcode = 1). Terlihat bahwa perangkat dengan IP 192.168.100.102 dan MAC address b8:3a:08:49:f3:d0 (diidentifikasi sebagai TendaTechnol_49:f3:d0) sedang mencari MAC address dari perangkat dengan IP 192.168.100.1. Karena MAC address tujuan belum diketahui, kolom Target MAC address diisi dengan nilai 00:00:00:00:00:00, sementara pada layer Ethernet, paket dikirim ke alamat broadcast ff:ff:ff:ff:ff:ff agar dapat diterima oleh semua perangkat dalam jaringan lokal.
Secara sederhana, paket ini menyampaikan pertanyaan: "Who has 192.168.100.1? Tell 192.168.100.102"
Dari analisis ini dapat disimpulkan bahwa ARP memainkan peran penting dalam komunikasi jaringan lokal, yakni menerjemahkan alamat IP menjadi alamat MAC sehingga frame Ethernet dapat dikirimkan ke tujuan yang tepat.
