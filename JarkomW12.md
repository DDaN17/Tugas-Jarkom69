Tujuan Praktikum
Mahasiswa diharapkan dapat memahami mekanisme kerja protokol ICMP melalui pengamatan menggunakan aplikasi Wireshark.
ICMP
ICMP atau Internet Control Message Protocol berperan dalam mendukung proses komunikasi serta pengawasan jaringan. Adapun fungsi-fungsi utamanya antara lain:

Melakukan diagnosis terhadap jaringan untuk mengetahui status koneksi.
Memastikan kondisi jaringan baik dan memverifikasi bahwa host tujuan dapat diakses.
Menyampaikan laporan kesalahan (error reporting) apabila terjadi kendala dalam pengiriman paket.
Mendukung proses troubleshooting ketika terjadi gangguan pada jaringan.

ICMP Digunakan Untuk

Memeriksa keberadaan host dalam jaringan melalui perintah ping, guna memastikan apakah perangkat tujuan dalam keadaan aktif dan dapat terhubung.
Melacak jalur yang dilalui paket data dengan menggunakan traceroute/tracert, sehingga setiap router (hop) yang dilewati dapat diidentifikasi.
Menampilkan informasi kesalahan, contohnya pesan Destination Unreachable ketika tujuan tidak dapat dicapai.
Menyampaikan informasi terkait TTL yang sudah habis melalui pesan Time Exceeded saat paket melampaui batas hop yang ditentukan.

Hubungan IP dengan ICMP
ICMP berjalan berdampingan dengan protokol IP. Pada saat paket IP dikirimkan melalui jaringan, ICMP berperan menyampaikan pesan kontrol serta informasi kesalahan yang terkait dengan proses pengiriman tersebut. Dengan kata lain, ICMP tidak digunakan untuk mengangkut data milik pengguna, melainkan berfungsi membantu IP dalam mengawasi dan mengelola komunikasi di dalam jaringan.
Isi Paket ICMP
Sebuah paket ICMP tersusun atas beberapa komponen penting, yaitu:

Type

Mengindikasikan jenis pesan ICMP yang dikirimkan, seperti Echo Request, Echo Reply, atau Destination Unreachable.
Code

Memuat informasi tambahan yang lebih spesifik terkait jenis pesan ICMP tersebut.
Checksum

Berfungsi untuk memverifikasi integritas data serta mendeteksi adanya kesalahan pada paket.
Identifier

Berperan sebagai tanda pengenal untuk membedakan satu paket ICMP dengan paket ICMP lainnya.
Sequence Number

Mengindikasikan urutan pengiriman paket sehingga dapat dicocokkan dengan paket respons yang diterima.
Data/Payload

Memuat data tambahan yang menyertai pesan ICMP, contohnya data yang digunakan dalam proses ping.

Melalui komponen-komponen tersebut, ICMP membantu administrator jaringan dalam mengawasi konektivitas, mengidentifikasi kesalahan, dan menganalisis performa jaringan.
Analisis ICMP yang Dihasilkan Oleh Ping

Buka aplikasi Wireshark, lalu pilih interface jaringan Wifi yang digunakan.
Buka Command Prompt (CMD), kemudian jalankan perintah ping -n 10 www.ust.hk.
Hentikan proses capture pada Wireshark.
Masukkan kata icmp pada kolom filter.
Pilih salah satu paket ICMP Echo Request, lalu expand untuk melihat detailnya.
Pilih salah satu paket ICMP Echo Reply, lalu expand untuk melihat detailnya.

Kita Cek
Pesan ICMP yang dihasilkan program Ping
Berdasarkan hasil capture pada Wireshark, terlihat dua jenis pesan ICMP yang dihasilkan oleh program ping, yaitu Echo Request dan Echo Reply. Dari data yang terekam, dapat diketahui bahwa proses ping dijalankan sebanyak 10 kali, hal ini terlihat dari nilai sequence number yang berjalan mulai dari seq=1/256 hingga seq=10/2560. Mengingat setiap proses ping menghasilkan sepasang paket (satu request dan satu reply), maka total paket ICMP yang tercatat secara keseluruhan adalah 20 paket. Selain paket-paket ping tersebut, ditemukan pula satu paket bertipe Destination Unreachable yang dikirim oleh host 35.211.225.161, yang mengindikasikan bahwa port pada sisi tujuan tidak dapat diakses.
Format Isi Pesan ICMP

ICMP Echo Request
(Paket 413 — Frame 413, berukuran 74 byte, dikirim dari 192.168.68.155 menuju 143.89.209.9)

Type = 8 → mengindikasikan bahwa paket ini berjenis Echo Request atau permintaan ping
Code = 0 → mengartikan bahwa tidak ada keterangan error tambahan pada pesan ICMP ini
Checksum = 0x4d5a [correct] → nilai checksum valid, sehingga paket dipastikan tidak rusak selama proses pengiriman
Identifier = 1 (0x0001) → berfungsi sebagai penanda agar paket Echo Reply nantinya dapat dikenali sebagai balasan dari request ini
Sequence Number = 1 (0x0001) → mengindikasikan bahwa paket ini merupakan pengiriman ping yang pertama


ICMP Echo Reply
(Paket 414 — Frame 414, berukuran 78 byte, dikirim dari 143.89.209.9 menuju 192.168.68.155)

Type = 0 → mengindikasikan bahwa paket ini merupakan Echo Reply atau balasan dari ping
Code = 0 → menandakan tidak adanya informasi error tambahan pada paket balasan ini
Checksum = 0x555a [correct] → nilai checksum valid, sehingga paket reply diterima dalam kondisi data yang utuh
Identifier = 1 (0x0001) → memiliki nilai yang sama dengan paket request, sehingga sistem dapat mencocokkan balasan dengan permintaan yang bersangkutan
Sequence Number = 1 (0x0001) → mengindikasikan bahwa paket reply ini merupakan balasan atas paket request pertama
Response time = 74,827 ms → menunjukkan durasi waktu sejak request dikirim hingga reply diterima



Analisis ICMP yang Dihasilkan Oleh Traceroute

Buka kembali aplikasi Wireshark dan pilih interface Wifi.
Buka Command Prompt (CMD), lalu jalankan perintah tracert www.ust.hk.
Lakukan proses capture pada Wireshark.
Terapkan filter icmp pada kolom filter.
Pilih salah satu paket ICMP Echo Request, kemudian expand untuk melihat detailnya.
Pilih salah satu paket ICMP Time Exceeded (TTL), lalu expand untuk melihat detailnya.

Kita Cek
Pesan ICMP yang dihasilkan oleh program traceroute

ICMP Echo Request: digunakan untuk meminta respons dari setiap host atau router yang dilalui oleh paket.
ICMP Time Exceeded (TTL Expired): merupakan pesan yang dikirimkan oleh router pada saat nilai TTL suatu paket telah habis sebelum paket tersebut mencapai tujuan akhirnya.

Format dan Isi Pesan ICMP

ICMP Echo Request
(Paket 6610 — dikirim dari 192.168.68.155 menuju 143.89.209.9)

Type = 8 → menandakan paket ini berjenis Echo Request atau permintaan ping
Code = 0 → menunjukkan tidak adanya informasi tambahan ataupun error pada paket
Checksum = 0xf7ae [correct] → nilai checksum valid, sehingga paket dipastikan tidak rusak selama proses transmisi
Identifier = 1 (0x0001) → berfungsi sebagai tanda pengenal pada paket request ini
Sequence Number = 80 (0x0050) → mengindikasikan bahwa paket ini merupakan paket urutan ke-80


ICMP Time Exceeded
(Paket 6612 — dikirim dari 192.168.68.1 menuju 192.168.68.155)

Type = 11 → mengindikasikan bahwa paket ini bertipe Time Exceeded
Code = 0 → memiliki arti TTL exceeded in transit, yakni nilai TTL telah habis di tengah perjalanan paket
Checksum = 0xf4ff [correct] → menandakan paket diterima tanpa mengalami error
Source IP = 192.168.68.1 → merupakan alamat router yang mengirimkan pesan TTL exceeded
Destination IP = 192.168.68.155 → merupakan alamat host yang menjalankan traceroute
Time to Live = 1 → nilai TTL pada paket asli yang dikirimkan, mengindikasikan bahwa traceroute sedang berada pada penelusuran hop pertama
