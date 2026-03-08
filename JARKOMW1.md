# Laporan Praktikum Week 1

Nama       : Dyandra Alifyan Nugroho  
NIM        : 103072400161  
Kelas      : IF-04-05  
Mata Kuliah: Jaringan Komputer  
__________________________________________


## Instalasi Wireshark (modul 1)

Awal dari praktikum ini dimulai dengan instalasi Wireshark. Ini adalah langkah penting agar bisa melanjutkan ke tugas-tugas berikutnya. Berikut adalah prosedur yang saya lakukan:

1. Kunjungi situs web resmi Wireshark melalui browser di alamat https://www.wireshark.org/download.html.
2. Unduh installer yang sesuai dengan OS yang digunakan (seperti Windows atau Linux), pastikan memilih versi stabil terbaru.
3. Setelah unduhan selesai, klik dua kali pada file installer untuk menjalankannya.
4. Ikuti panduan instalasi step by step hingga prosesnya berakhir; tentukan folder instalasi dan tunggu sampai selesai.

Instalasi berjalan tanpa kendala, hanya butuh waktu beberapa menit hingga Wireshark siap digunakan.

### Dokumentasi Instalasi
Saya mengambil beberapa screenshot selama proses instalasi untuk dokumentasi:

- Halaman download Wireshark:
<img width="1919" height="1031" alt="wiresharkWebsite" src="https://github.com/user-attachments/assets/73789bbd-9c3b-4b61-8ed4-3fe8f2abb1d7" />

- Langkah awal setup:
<img width="575" height="474" alt="installationSetupPart1" src="https://github.com/user-attachments/assets/7c5e6bdc-d63c-40bd-88b6-d473906f6d1c" />

- Persetujuan lisensi:
<img width="575" height="475" alt="installationSetupPart2" src="https://github.com/user-attachments/assets/0d5abcfe-c2a8-4cdb-98f7-33c80ce1258e" />

- Pemilihan fitur yang akan diinstal:
<img width="575" height="472" alt="installationSetupPart3" src="https://github.com/user-attachments/assets/923895c1-97c5-40b5-badf-89cab2291178" />

- Konfigurasi lokasi instalasi:
<img width="574" height="471" alt="installationSetupPart4" src="https://github.com/user-attachments/assets/66533e95-de90-424b-b3e7-4100e7fcea54" />

- Proses instalasi sedang berjalan:
 <img width="573" height="473" alt="installationSetupPart5" src="https://github.com/user-attachments/assets/ab990478-f520-4fa9-afcd-ddc9eb618816" />

 <img width="574" height="471" alt="installationSetupPart6" src="https://github.com/user-attachments/assets/35299949-503a-4b42-b616-d94919309a8d" />

 <img width="576" height="476" alt="installationSetupPart7" src="https://github.com/user-attachments/assets/9c74635f-096a-46dc-b5a2-2b5c54fed945" />

- Penambahan komponen WinPcap/Npcap:
 <img width="575" height="474" alt="installationSetupPart8" src="https://github.com/user-attachments/assets/9d053d99-0621-4395-8cd1-d68ee67e133c" />

- Tahap akhir instalasi:
 <img width="575" height="472" alt="installationSetupPart9" src="https://github.com/user-attachments/assets/a29b3f5b-d99f-4c62-8c0d-d5696a6ef8e2" />

- Instalasi berhasil diselesaikan:
<img width="575" height="473" alt="installationSetupDone" src="https://github.com/user-attachments/assets/d3b5c9c1-0ae7-4959-9054-5e91e161d664" />



## Tugas Praktikum Week 1 (modul 2)

Dengan Wireshark sudah terinstal, saya lanjut ke bagian kedua modul 2 yang fokus pada pengamatan interaksi HTTP GET dan response.

1. Buka aplikasi Wireshark dan pilih interface jaringan aktif (dalam kasus saya, Wi-Fi). Pastikan VPN dimatikan jika sedang aktif untuk menghindari gangguan dalam penangkapan paket.
2. Buka browser dan akses URL berikut: http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html. Halaman web tersebut menampilkan pesan singkat: "Congratulations! You've downloaded the first Wireshark lab file!"
3. Kembali ke Wireshark, masukkan kata "http" di kolom filter tanpa tanda kutip, kemudian tekan Enter untuk memfilter paket HTTP saja.
4. Cari entri dengan label "(text/html)" di daftar paket, lalu klik ikon panah untuk memperluas detailnya.
5. Pada bagian "Line-based text data", isi HTML yang diterima terlihat seperti ini:



6. Untuk mengakhiri, klik tombol stop capture di menu dan tutup sesi tangkapan tersebut.

Melalui aktivitas ini, saya belajar lebih dalam tentang mekanisme permintaan HTTP dari browser dan bagaimana respons ditampilkan dalam Wireshark.

### Lampiran
Screenshot-screenshot berikut diambil saat melakukan tugas praktikum:

- Antarmuka utama Wireshark setelah aplikasi diluncurkan:
  <img width="1919" height="1079" alt="tampilanWireshark" src="https://github.com/user-attachments/assets/1440a515-cfcc-47bf-b8a9-ec752294e84a" />

- Daftar paket yang berhasil ditangkap melalui koneksi Wi-Fi:
  <img width="1919" height="1079" alt="tampilanCaptureFromWifi" src="https://github.com/user-attachments/assets/7b2279bc-47a1-4d23-922a-f157e3cb5156" />

- Tampilan browser yang menunjukkan halaman lab sederhana:
  <img width="1919" height="1028" alt="tampilanBrowserPadaLinkHtml" src="https://github.com/user-attachments/assets/26d4d622-7d17-4ad9-8883-79f5bdf3d287" />

- Hasil filter paket menggunakan kata kunci "http":
  <img width="1919" height="1079" alt="tampilanCaptureFromWifiWithFilterHTTP" src="https://github.com/user-attachments/assets/a3b8f8e0-177b-41e6-b515-2be39c9147f8" />

- Isi dari "Line-based text data" yang berisi respons HTML:
  <img width="972" height="492" alt="lineBasedTextDataHtmlVer" src="https://github.com/user-attachments/assets/5cc3e036-5f8d-46ad-ba42-93aafc5e75d4" />
