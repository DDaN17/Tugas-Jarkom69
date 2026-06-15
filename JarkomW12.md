Tujuan Praktikum
Mahasiswa diharapkan dapat memahami mekanisme kerja protokol ICMP melalui pengamatan menggunakan aplikasi Wireshark.


## ICMP


ICMP atau Internet Control Message Protocol berperan dalam mendukung proses komunikasi serta pengawasan jaringan. Adapun fungsi-fungsi utamanya antara lain:

Melakukan diagnosis terhadap jaringan untuk mengetahui status koneksi.
Memastikan kondisi jaringan baik dan memverifikasi bahwa host tujuan dapat diakses.
Menyampaikan laporan kesalahan (error reporting) apabila terjadi kendala dalam pengiriman paket.
Mendukung proses troubleshooting ketika terjadi gangguan pada jaringan.

## ICMP Digunakan Untuk

Memeriksa keberadaan host dalam jaringan melalui perintah ping, guna memastikan apakah perangkat tujuan dalam keadaan aktif dan dapat terhubung.
Melacak jalur yang dilalui paket data dengan menggunakan traceroute/tracert, sehingga setiap router (hop) yang dilewati dapat diidentifikasi.
Menampilkan informasi kesalahan, contohnya pesan Destination Unreachable ketika tujuan tidak dapat dicapai.
Menyampaikan informasi terkait TTL yang sudah habis melalui pesan Time Exceeded saat paket melampaui batas hop yang ditentukan.

## Hubungan IP dengan ICMP

ICMP berjalan berdampingan dengan protokol IP. Pada saat paket IP dikirimkan melalui jaringan, ICMP berperan menyampaikan pesan kontrol serta informasi kesalahan yang terkait dengan proses pengiriman tersebut. Dengan kata lain, ICMP tidak digunakan untuk mengangkut data milik pengguna, melainkan berfungsi membantu IP dalam mengawasi dan mengelola komunikasi di dalam jaringan.

 ## Isi Paket ICMP
 
Sebuah paket ICMP tersusun atas beberapa komponen penting, yaitu:


Type mengindikasikan jenis pesan ICMP yang dikirimkan, seperti Echo Request, Echo Reply, atau Destination Unreachable.
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

## Analisis ICMP yang Dihasilkan Oleh Ping

Buka aplikasi Wireshark, lalu pilih interface jaringan Wifi yang digunakan.
Buka Command Prompt (CMD), kemudian jalankan perintah ping -n 10 www.ust.hk.

<img width="474" height="313" alt="{E688A9FF-2230-446C-978B-C31BF7801853}" src="https://github.com/user-attachments/assets/fca7c3a7-bd0b-4db2-b2ef-f3b8b52258a0" />

Hentikan proses capture pada Wireshark.
Masukkan kata icmp pada kolom filter.

<img width="287" height="32" alt="{6029D549-FC4D-40E7-9ECC-E2FBCC84F652}" src="https://github.com/user-attachments/assets/1ee9ca8c-3c83-4071-bb1a-ebe0f89df56c" />

Pilih salah satu paket ICMP Echo Request, lalu expand untuk melihat detailnya.

<img width="1144" height="724" alt="{D84BCBE2-191A-46DC-AF3F-76AB0E314F0F}" src="https://github.com/user-attachments/assets/73af55b6-4886-40c5-a3c5-fa2035b46af3" />

Pilih salah satu paket ICMP Echo Reply, lalu expand untuk melihat detailnya.

<img width="1145" height="744" alt="{0922BC62-D840-458F-BD5F-FAE08F239BAE}" src="https://github.com/user-attachments/assets/da93cbc1-f2fa-4525-8af9-4b53fc57d932" />

ICMP Echo Request (Frame 25)
(Frame 25 — 74 bytes, src: 192.168.1.9 → dst: 143.89.209.9)

Type = 8 → menandakan paket ini berjenis Echo Request atau permintaan ping
Code = 0 → tidak terdapat informasi tambahan atau error pada paket
Identifier (BE) = 1 (0x0001) → berfungsi sebagai penanda agar Echo Reply dapat dikenali sebagai balasan dari request yang sama
Sequence Number (BE) = 1 (0x0001), (LE) = 256 (0x0100) → menunjukkan bahwa paket ini merupakan pengiriman ping yang pertama
Time to Live = 128 → nilai TTL awal yang diset oleh sistem operasi pengirim (default Windows)


ICMP Echo Reply (Frame 26)
(Frame 26 — 74 bytes, src: 143.89.209.9 → dst: 192.168.1.9)

Type = 0 → menandakan paket ini merupakan Echo Reply atau balasan dari ping
Code = 0 → tidak terdapat informasi tambahan atau error pada paket balasan
Checksum = 0x555a [correct] → nilai checksum valid, sehingga paket reply diterima dalam kondisi data utuh
Identifier (BE) = 1 (0x0001), (LE) = 256 (0x0100) → identifier sama dengan paket request, sehingga sistem dapat mencocokkan balasan dengan permintaan sebelumnya
Sequence Number (BE) = 1 (0x0001), (LE) = 256 (0x0100) → menunjukkan bahwa paket reply ini merupakan balasan untuk paket request pertama, sesuai informasi [Request frame: 25]
Time to Live = 44 → nilai TTL paket reply saat diterima, lebih rendah dari TTL awal di sisi server karena melewati beberapa hop
Response time = 103,737 ms → waktu yang dibutuhkan dari saat request dikirim hingga reply diterima
Data = 32 bytes, berisi payload abcdefghijklmnopqrstuvwabcdefghi, yaitu pola payload default yang digunakan oleh program ping pada Windows


Analisis ICMP yang Dihasilkan Oleh Traceroute

Buka kembali aplikasi Wireshark dan pilih interface Wifi.
Buka Command Prompt (CMD), lalu jalankan perintah tracert www.ust.hk.

<img width="973" height="482" alt="{866FC23D-405D-4576-9D89-66946185770E}" src="https://github.com/user-attachments/assets/58871ef7-200d-43e3-adc4-685a142a318c" />

Lakukan proses capture pada Wireshark.
Terapkan filter icmp pada kolom filter.

<img width="287" height="32" alt="{6029D549-FC4D-40E7-9ECC-E2FBCC84F652}" src="https://github.com/user-attachments/assets/1ee9ca8c-3c83-4071-bb1a-ebe0f89df56c" />

Pilih salah satu paket ICMP Echo Request, kemudian expand untuk melihat detailnya.

<img width="1146" height="696" alt="{C8A5EFC5-290F-4152-92E9-AF6BD7CA724A}" src="https://github.com/user-attachments/assets/92a3e621-a2df-4b1f-8efb-6f207466a895" />

Pesan ICMP yang dihasilkan oleh program traceroute

ICMP Echo Request: digunakan untuk meminta respons dari setiap host atau router yang dilalui paket, dengan nilai TTL yang dinaikkan secara bertahap (1, 2, 3, dst.) pada setiap probe untuk memetakan jalur menuju tujuan.
ICMP Time-to-live Exceeded (TTL Expired): merupakan pesan yang dikirimkan oleh router ketika nilai TTL suatu paket habis sebelum mencapai tujuan akhir. Pesan ini menyertakan salinan header IP dan ICMP dari paket asli yang menyebabkan TTL tersebut habis.

Format dan Isi Pesan ICMP

ICMP Echo Request (Frame 177826 — paket asli yang disalin ke dalam pesan Time-to-live exceeded)
(106 bytes, src: 192.168.1.9 → dst: 143.89.209.9)

Type = 8 → menunjukkan paket ini merupakan Echo Request atau permintaan ping
Code = 0 → tidak terdapat informasi tambahan/error pada paket
Identifier (BE) = 1 (0x0001), (LE) = 256 (0x0100) → digunakan sebagai penanda paket request
Sequence Number (BE) = 11 (0x000b), (LE) = 2816 (0x0b00) → menunjukkan bahwa paket ini merupakan probe traceroute yang ke-11
Time to Live = 1 → menandakan traceroute sedang menelusuri hop pertama (TTL akan habis setelah satu kali lompatan)
Total Length (IP) = 92 bytes, dengan Data sebesar 64 bytes berisi nilai 0 seluruhnya — ukuran payload default tracert di Windows, berbeda dari payload ping yang berukuran 32 bytes


ICMP Time-to-live Exceeded (Frame 177829)
(134 bytes, src: 192.168.1.1 → dst: 192.168.1.9)

Type = 11 → menunjukkan paket ini bertipe Time-to-live exceeded
Code = 0 → memiliki arti "Time to live exceeded in transit", yakni TTL telah habis di tengah perjalanan paket
Checksum = 0xf4f4 [correct] → menandakan paket diterima tanpa error
Unused = 00000000 → bagian header yang tidak digunakan/direservasi pada pesan tipe ini
Source Address = 192.168.1.1 → alamat router pertama (gateway lokal) yang mendeteksi TTL habis dan mengirimkan pesan ini
Destination Address = 192.168.1.9 → alamat host yang menjalankan traceroute
Paket ini menyertakan salinan header IP dan ICMP dari Echo Request asli (Frame 177826) sebagai payload-nya, sehingga pengirim traceroute dapat mengetahui probe mana yang direspons oleh router pada hop tersebut
