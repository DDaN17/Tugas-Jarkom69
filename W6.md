# Modul 6 TCP

Tujuan Praktikum
mahasiswa dapat mempelajari cara kerja protokol TCP menggunakan Wireshark.

## TCP
TCP (Transmission Control Protocol) merupakan protokol pada lapisan transport yang bersifat connection-oriented, yaitu proses pengiriman data harus diawali dengan pembentukan koneksi terlebih dahulu. TCP memastikan data dikirim secara andal melalui penggunaan mekanisme seperti sequence number, acknowledgment, flow control, dan congestion control.

## Analisis Transfer File Menggunakan Protocol TCP

1. Pertama-tama Download file http://gaia.cs.umass.edu/wireshark-labs/alice.txt

   <img width="437" height="52" alt="{9DD095DD-E392-40C8-94F9-C2507236D51B}" src="https://github.com/user-attachments/assets/b132f911-8593-4e4a-b6cd-9ed3e8ad7b8f" />

2. Buka browser http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html dan pilih file alice.txt
   <img width="1915" height="309" alt="{BE3E27B3-3447-4EFF-A6D7-519EE5AA0948}" src="https://github.com/user-attachments/assets/f1fe3643-2709-4feb-9783-e56d338d37bf" />

3. Buka wireshark, kemudian pilih wif dan start
  <img width="976" height="513" alt="{47A820FF-913A-49C3-9881-4139910A1061}" src="https://github.com/user-attachments/assets/a772c4be-bde4-487b-ae4c-f61faa61063d" />

4. Kembali ke browser klik Upload alice.txt hingga muncul tampilan “Congratulations”
   <img width="970" height="262" alt="{6AAAA5E4-B05B-4B93-B5C6-AA97D7D115FB}" src="https://github.com/user-attachments/assets/fa6a448d-d3a9-4f01-adec-9fe6d313312f" />

5. Stop wireshark kemudian ketik tcp di bagian filter 
    
   <img width="974" height="311" alt="{58A51C8B-8C00-4992-8E22-59175DFA1672}" src="https://github.com/user-attachments/assets/ab21de79-eee5-44e9-b21a-c9f6612ec57c" />

    
     Paket yang muncul terdiri dari segmen TCP dan beberapa paket HTTP. Hal ini menunjukkan bahwa proses upload file dilakukan menggunakan protokol HTTP, yang berjalan di atas protokol TCP. TCP berperan memastikan data terkirim dengan aman dan berurutan, sedangkan HTTP digunakan untuk menangani proses pertukaran data antara client dan server saat file diunggah.
    
     Paket SYN digunakan untuk memulai koneksi TCP antara client dan server melalui proses *three-way handshake*, sehingga koneksi dapat dipastikan siap sebelum pertukaran data dilakukan. Paket ini tidak digunakan untuk mengirim file secara langsung. Setelah koneksi berhasil terbentuk, file akan dikirim dalam beberapa segmen kecil melalui TCP. Pembagian data menjadi bagian-bagian kecil ini bertujuan agar proses pengiriman lebih efisien, mudah dikontrol, serta membantu memastikan seluruh data dapat diterima dengan benar oleh tujuan.
    
   <img width="645" height="311" alt="{D2FB6DC8-E100-4E18-BAF6-DC98062B8C67}" src="https://github.com/user-attachments/assets/b9e4bb92-69cd-4903-bbd4-31dac143508b" />

    
     Setelah proses upload selesai, server akan mengirimkan respons HTTP/1.1 200 OK. Pesan ini menandakan bahwa file telah berhasil diterima dan diproses oleh server tanpa kendala. Lalu halaman web menampilkan pesan “Congratulations” sebagai tanda bahwa proses upload file berhasil dilakukan dengan sukses.

### Menjawab Pertanyaan
1) IP dan port TCP komputer klien mencari data di filter "HTTP" dan pilih paket POST
     IP Server: 128.119.245.12
    
      <img width="697" height="382" alt="{1300375B-A14E-4612-A0FA-8506B5A69AF5}" src="https://github.com/user-attachments/assets/890bbf81-f345-441e-b34e-022f2562cfa9" />

     Port server : 54470
   
     <img width="682" height="247" alt="{850E75A1-F616-45A6-A534-B78153B29A5F}" src="https://github.com/user-attachments/assets/f98712e4-af2e-4487-9e1c-b8b8e97045ce" />


2) IP dan port TCP server mencari data di filter "HTTP" dan pilih paket HTTP/1.1 200 OK

      <img width="727" height="400" alt="{0D497B57-3087-47D5-929C-78D09679DD6F}" src="https://github.com/user-attachments/assets/e53c0a82-b9d7-4c84-9a4f-bf82fe4cade8" />

      
     IP Server: 192.168.100.132
    
     Port server : 80

#  Dasar TCP
## Berikut Langkah-Langkahnya:
1. Download dan extrak file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
   <img width="878" height="33" alt="{557F9B27-D9A9-4891-B638-FE12E5B4BE4B}" src="https://github.com/user-attachments/assets/da65d7da-06ff-4d0c-beac-0492c957a9df" />

2. Buka file dan pilih paket paket tcp-ethereal-trace-1, buka dengan wireshark
   <img width="725" height="190" alt="{2474AA42-5BEA-4B56-B539-6C1D9736A905}" src="https://github.com/user-attachments/assets/ab7a7fd1-4a08-4b3d-b3b1-4ab09d9aacb1" />

### Menjawab Pertanyaan
1) Nomor urut SYN, mencari data di filter tcp.flags.syn == 1 && tcp.flags.ack == 0
    
      <img width="723" height="193" alt="{186D0D81-CC6A-45C7-86F4-CEF45F81BB74}" src="https://github.com/user-attachments/assets/a962bc39-67b0-452a-b3b1-05123fcab81e" />

     Nomor urut pada segmen TCP SYN adalah 0. Segmen ini teridentifikasi sebagai SYN karena memiliki flag SYN pada bagian TCP Flags.

      <img width="698" height="566" alt="{F08DF495-1BB4-433B-843F-4C3E62F0C2AF}" src="https://github.com/user-attachments/assets/ca3c9618-2e28-430a-b130-33ff269b55d3" />

      
2) SYN-ACK, mencari data di filter tcp.flags.syn == 1 && tcp.flags.ack == 1

      <img width="727" height="91" alt="{4101AA77-44AD-4AA8-82BF-380469DD49CF}" src="https://github.com/user-attachments/assets/2c22bc80-c688-44c4-b703-99628209d36b" />

     Nomor urut (sequence number) pada segmen SYN-ACK adalah 0, sedangkan nilai acknowledgment adalah 1. Nilai acknowledgment diperoleh dari sequence number pada segmen SYN sebelumnya yang ditambah 1. Segmen ini dapat diidentifikasi sebagai SYN-ACK karena memiliki flag SYN dan ACK pada bagian TCP Flags

      <img width="697" height="612" alt="{D25449DD-0606-4411-8F7E-2E3879196C27}" src="https://github.com/user-attachments/assets/5362733f-2ac5-4ad8-b11e-17adc6fb25d0" />


3) Sequence number POST, mencari data di filter tcp.port == 1161 && tcp contains "POST"

      <img width="722" height="62" alt="{BF61FCB3-D373-4D4C-A65B-D55443C00EC3}" src="https://github.com/user-attachments/assets/56154d52-2718-429c-9d2b-a3042101affa" />
      
     Nomor urut segmen TCP yang berisi perintah HTTP POST adalah 1

      <img width="682" height="620" alt="{20314E8F-C51B-41A9-B70C-05AE5398329E}" src="https://github.com/user-attachments/assets/0f10e227-c42f-47d8-9a3e-1dd9c35073b2" />

4) 6 segmen pertama dan RTT

      <img width="696" height="486" alt="{464CAD26-9BF7-41B4-8989-71F84A4402AE}" src="https://github.com/user-attachments/assets/caa3f4e6-815c-4a76-a4d7-1b99198959ac" />


     Nilai RTT (Round Trip Time) diperoleh dari selisih waktu antara saat segmen TCP dikirim dan saat acknowledgment (ACK) diterima kembali. Berdasarkan grafik Round Trip Time, nilai RTT berada pada kisaran sekitar 100 ms hingga 300 ms. Perbedaan nilai RTT ini menunjukkan bahwa kondisi jaringan selama proses transfer tidak selalu stabil, sehingga waktu yang dibutuhkan paket untuk pergi dan kembali dapat berubah-ubah.

5) Panjang 6 segmen
   
      <img width="690" height="342" alt="{61CF4E30-E6FE-49CE-AA03-4908DA361C42}" src="https://github.com/user-attachments/assets/82dcf9a9-c22a-4835-a283-be3f97e77adc" />

     Panjang 6 segmen adalah 7865 byte

6) Buffer receiver
    
      <img width="425" height="266" alt="{C00EA9AA-DD35-4835-8333-2EFB12B80743}" src="https://github.com/user-attachments/assets/dc5c18fa-34ae-462c-bea6-637b12bb2673" />

     Nilai minimum ruang buffer yang tersedia pada penerima adalah 17520 byte, yang terlihat dari nilai window size pada segmen TCP
  
7) Retransmission

      <img width="353" height="365" alt="{102E004C-39C3-47C9-B650-CB30629EF0A8}" src="https://github.com/user-attachments/assets/1f989ac8-6766-4a30-87b9-a50da53b5616" />

     Tidak ditemukan retransmission / ditemukan retransmission. Hal ini dapat dilihat dari tidak adanya / adanya label “TCP Retransmission” pada Wireshark.

8) ACK behavior

      <img width="343" height="363" alt="{09819772-C4DC-4011-A143-40B3573C4A6E}" src="https://github.com/user-attachments/assets/3444cb70-bec8-4130-9d10-ea9b72e4f009" />

     Jumlah data yang di-ACK tidak tetap dan bisa banyak. Penerima dapat mengakui beberapa segmen sekaligus, tidak selalu satu per satu
  
9) Thoroughtput

      <img width="694" height="478" alt="{8A5C6803-4934-4F2D-A48F-86FCEF42FD84}" src="https://github.com/user-attachments/assets/f508d658-9159-4785-9ff2-d411f1edb320" />

     Throughput merupakan jumlah data yang berhasil ditransfer dalam setiap satuan waktu. Berdasarkan grafik throughput, kecepatan transfer data meningkat secara bertahap hingga mencapai sekitar 200 kbps sampai 270 kbps. Hal ini menunjukkan bahwa performa koneksi TCP selama proses pengiriman data berjalan cukup baik dan mampu menjaga laju transfer data secara stabil.

# Congestion Control pada TCP
## Berikut Langkah-Langkahnya dan Menjawab Pertanyaan:
1. Identifikasi Slow Start & Congestion Avoidance (file tcp-ethereal-trace-1)

     Buka file tcp-ethereal-trace-1 dengan wireshark
     Filter "TCP"
     Klik Statistics - TCP Stream Graph - Time-Sequence Graph (Stevens)
      <img width="666" height="459" alt="{96AB43BC-EB92-4DCA-B3BE-A9231FF7099E}" src="https://github.com/user-attachments/assets/eda0a2af-69d0-4238-8cb3-f24c1b7ad832" />
     Fase slow start terjadi pada awal koneksi (sekitar 0 hingga ±1 detik) dengan pertumbuhan data secara eksponensial hingga mencapai threshold, lalu berubah menjadi fase congestion avoidance dengan pertumbuhan linear. Data nyata menunjukkan sedikit perbedaan dari teori karena dipengaruhi kondisi jaringan seperti delay dan variasi ACK. Secara keseluruhan, koneksi TCP pada grafik terlihat cukup stabil karena tidak ada penurunan drastis yang menunjukkan *packet loss* besar atau *timeout*, meskipun grafik tidak sepenuhnya mulus seperti model TCP ideal.

2. Identifikasi Slow Start & Congestion Avoidance (alice.txt)

     Start wireshark
     Upload file alice.txt ke http://gaia.cs.umass.edu/wireshark-labs/TCP-wireshark-file1.html
     Kembali ke wireshark dan filter "TCP"
     Klik Statistics - TCP Stream Graph - Time-Sequence Graph (Stevens)
      <img width="672" height="459" alt="{E0C3C600-A84A-4F25-AC87-71FBB5A7F6F2}" src="https://github.com/user-attachments/assets/38e54070-a50b-4c97-9539-b9cdd8596800" />
     Pada grafik kedua, fase slow start terjadi di awal koneksi dengan pertumbuhan eksponensial yang lebih cepat, kemudian segera beralih ke fase congestion avoidance. Hal ini menunjukkan bahwa koneksi Wi-Fi memiliki respon yang lebih cepat dibanding sebelumnya, tetapi juga lebih rentan terhadap variasi delay. Secara umum koneksi tetap stabil, meskipun perilakunya tidak sepenuhnya sesuai dengan model TCP ideal karena dipengaruhi kondisi jaringan nirkabel.
