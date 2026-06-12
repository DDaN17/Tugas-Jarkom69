# Modul 5 UDP

Tujuan Praktikum
- Kita sebagai mahasiswa dapat mempelajari cara kerja protokol UDP menggunakan Wireshark.

## UDP
UDP (User Datagram Protocol) adalah salah satu protokol di lapisan transport pada model TCP/IP yang digunakan untuk mengirim data secara langsung tanpa perlu membangun koneksi terlebih dahulu. Artinya, sebelum data dikirim, tidak ada proses “jabat tangan” seperti pada TCP data bisa langsung dikirim begitu saja.

## Langkah-Langkah Praktikum
1. Download file http://gaia.cs.umass.edu/wireshark-labs/wireshark-traces.zip

  
3. Extract file dan cari file http-ethereal-trace-5
   
4. Klik kanan pada file tersebut, kemudian buka dengan wireshark
   
5. Lakukan filter UDP dan pilih salah satu paket UDP
   



### Menjawab Pertanyaan
1) Field UDP
   
   Jawab: Terdapat 4 field : Source Port, Destination Port, Length, Checksum
   
2. Panjang masing - masing dari dari field yang ada pada soal 1 yaitu :
   - Source port: 2 byte
   - Destination port: 2 byte
   - Lenght: 2 byte
   - Checksum: 2 byte 
   - di karenakan Header UDP selalu memiliki ukuran tetap 8 byte dan pada percobaan di atas ada 4 field jadi setiap field memiliki panjang 2 byte

3) Length
   
   Pada foto tersebut terlihat bahwa nilai Length  adalah 58. Artinya, panjang total paket UDP terdiri dari payload sebesar 50 byte ditambah header UDP sebesar 8 byte, sehingga 50 + 8 = 58. Dengan demikian, nilai Length memang menunjukkan ukuran keseluruhan paket UDP, yaitu gabungan antara header dan payload.

4) Jumlah maksimum byte UDP
   Jawab: Header UDP memiliki ukuran tetap sebesar 8 byte, sementara ukuran maksimum paket IP adalah 65.535 byte. Pada IPv4, header IP umumnya berukuran 20 byte. Jadi, untuk menghitung kapasitas maksimum data (payload) UDP, kita kurangi total ukuran paket IP dengan header IP dan header UDP:

   65.535 − 20 − 8 = 65.507 byte.

   Dengan demikian, ukuran maksimum payload yang bisa dikirim menggunakan UDP adalah 65.507 byte.

5) Port terbesar
    Jawab: Nomor port terbesar pada protokol UDP adalah 65535. Hal ini karena field **source port** dan **destination port** di header UDP masing-masing memiliki ukuran 16 bit. Dengan 16 bit, nilai maksimum yang bisa direpresentasikan adalah 2¹⁶ − 1, yaitu 65535.

   Jadi, rentang nomor port UDP berada dari 0 sampai 65535.

6) Nomor protokol UDP
   
   Jawab: Nomor protokol UDP adalah 17 (desimal) atau 0x11 (heksadesimal)

7) Hubungan port


    Jawab:
    - REQUEST -> Source Port : 4336 & Destination Port : 161
    - RESPONSE -> Source Port : 161 & Destination Port : 4336
    - Nomor port pada paket balasan merupakan kebalikan dari paket permintaan, di mana port sumber dan tujuan saling bertukar
