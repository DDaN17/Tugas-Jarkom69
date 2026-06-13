# Modul 5 UDP

Tujuan Praktikum
Kita sebagai mahasiswa dapat mempelajari cara kerja protokol UDP menggunakan Wireshark.

## UDP
UDP (User Datagram Protocol) adalah salah satu protokol di lapisan transport pada model TCP/IP yang digunakan untuk mengirim data secara langsung tanpa perlu membangun koneksi terlebih dahulu. Artinya, sebelum data dikirim, tidak ada proses “jabat tangan” seperti pada TCP data bisa langsung dikirim begitu saja.

## Langkah-Langkah Praktikum
1. Download file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip
<img width="275" height="113" alt="{37EB4BD6-3B78-4DD1-B7AD-7573A8418A89}" src="https://github.com/user-attachments/assets/b8b19e38-fa13-4aee-b577-b0a14d8787b4" />

2. Extract file dan cari file http-ethereal-trace-5
<img width="386" height="84" alt="{0C2CC633-491F-476F-AC47-9AAFE468EA76}" src="https://github.com/user-attachments/assets/78a09540-d4d1-416c-b4d4-e75294783bde" />

3. Klik kanan pada file tersebut, kemudian buka dengan wireshark
   <img width="795" height="401" alt="{00D60670-364C-43FD-BE2E-7C7AE33E0BD4}" src="https://github.com/user-attachments/assets/1558e8d2-dd31-4fa1-8927-57d1cbe6e42b" />


4. Lakukan filter UDP dan pilih salah satu paket UDP
   <img width="796" height="400" alt="{65836DA3-9C92-4DCF-A693-9C382476D661}" src="https://github.com/user-attachments/assets/3edb2290-52f7-4af1-a4f8-bddab228765f" />


### Menjawab Pertanyaan
1) Field UDP
   <img width="796" height="476" alt="{CEEBCD03-F645-479E-8513-F43145771674}" src="https://github.com/user-attachments/assets/4c5488ce-994e-4d27-a802-ef59092c2bc8" />

  Terdapat 4 field : Source Port, Destination Port, Length, Checksum
   
2. Panjang masing - masing dari dari field yang ada pada soal 1 yaitu :
   a. Source port: 2 byte
   b. Destination port: 2 byte
   c. Lenght: 2 byte
   d. Checksum: 2 byte 
   e. karena Header UDP selalu memiliki ukuran tetap 8 byte dan pada percobaan di atas ada 4 field jadi setiap field              memiliki panjang 2 byte

3) Length
<img width="288" height="168" alt="{88E0A093-B91E-4DA5-B3D7-D1D0E1A0053E}" src="https://github.com/user-attachments/assets/c5404fc0-1db3-4e13-9c18-98cbee1710f9" />

Pada foto tersebut terlihat bahwa nilai Length adalah 58. 

4) Jumlah maksimum byte UDP
Header UDP memiliki ukuran tetap sebesar 8 byte, sementara ukuran maksimum paket IP adalah 65.535 byte. Pada IPv4, header IP umumnya berukuran 20 byte. Jadi, untuk menghitung kapasitas maksimum data (payload) UDP, kita kurangi total ukuran paket IP dengan header IP dan header UDP:

65.535 − 20 − 8 = 65.507 byte.

Dengan demikian, ukuran maksimum payload yang bisa dikirim menggunakan UDP adalah 65.507 byte.

5) Port terbesar
Nomor port terbesar pada protokol UDP adalah 65535. karena field **source port** dan **destination port** di header UDP masing-masing memiliki ukuran 16 bit. Dengan 16 bit, nilai maksimum yang bisa direpresentasikan adalah 2¹⁶ − 1, yaitu 65535.

Jadi, rentang nomor port UDP berada dari 0 sampai 65535.

6) Nomor protokol UDP
   <img width="710" height="266" alt="{DE6B69E2-4C22-4766-828C-61947CACDE61}" src="https://github.com/user-attachments/assets/24ff0c39-614e-4018-972e-1f1be0871e7a" />

Nomor protokol UDP adalah 17 (desimal) atau 0x11 (heksadesimal)

7) Hubungan port
<img width="536" height="132" alt="{6693A3A8-373E-4BFF-9D8C-39A361D804D0}" src="https://github.com/user-attachments/assets/353ab0c1-776f-4e85-a5f1-9d0c6e52d51f" />


    Jawab:
   REQUEST Source Port : 4336 & Destination Port : 161
   RESPONSE Source Port : 161 & Destination Port : 4336
   Nomor port pada paket balasan merupakan kebalikan dari paket permintaan, di mana port sumber dan tujuan saling bertukar
