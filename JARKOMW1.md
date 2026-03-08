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
  ![Wireshark Website](../Asset/Image/wiresharkWebsite.png)
- Langkah awal setup:
  ![install setup part 1](../Asset/Image/installationSetupPart1.png)
- Persetujuan lisensi:
  ![install setup part 2](../Asset/Image/installationSetupPart2.png)
- Pemilihan fitur yang akan diinstal:
  ![install setup part 3](../Asset/Image/installationSetupPart3.png)
- Konfigurasi lokasi instalasi:
  ![install setup part 4](../Asset/Image/installationSetupPart4.png)
- Proses instalasi sedang berjalan:
  ![install setup part 5](../Asset/Image/installationSetupPart5.png)
  ![install setup part 6](../Asset/Image/installationSetupPart6.png)
  ![install setup part 7](../Asset/Image/installationSetupPart7.png)
- Penambahan komponen WinPcap/Npcap:
  ![install setup part 8](../Asset/Image/installationSetupPart8.png)
- Tahap akhir instalasi:
  ![install setup part 9](../Asset/Image/installationSetupPart9.png)
- Instalasi berhasil diselesaikan:
  ![install setup done](../Asset/Image/installationSetupDone.png)


## Tugas Praktikum Week 1 (modul 2)

Dengan Wireshark sudah terinstal, saya lanjut ke bagian kedua modul 2 yang fokus pada pengamatan interaksi HTTP GET dan response.

1. Buka aplikasi Wireshark dan pilih interface jaringan aktif (dalam kasus saya, Wi-Fi). Pastikan VPN dimatikan jika sedang aktif untuk menghindari gangguan dalam penangkapan paket.
2. Buka browser dan akses URL berikut: http://gaia.cs.umass.edu/wireshark-labs/INTRO-wireshark-file1.html. Halaman web tersebut menampilkan pesan singkat: "Congratulations! You've downloaded the first Wireshark lab file!"
3. Kembali ke Wireshark, masukkan kata "http" di kolom filter tanpa tanda kutip, kemudian tekan Enter untuk memfilter paket HTTP saja.
4. Cari entri dengan label "(text/html)" di daftar paket, lalu klik ikon panah untuk memperluas detailnya.
5. Pada bagian "Line-based text data", isi HTML yang diterima terlihat seperti ini:

```html
<html>\n
Congratulations! You've download the first Wireshark lab file!
</html>\n
```

6. Untuk mengakhiri, klik tombol stop capture di menu dan tutup sesi tangkapan tersebut.

Melalui aktivitas ini, saya belajar lebih dalam tentang mekanisme permintaan HTTP dari browser dan bagaimana respons ditampilkan dalam Wireshark.

### Lampiran
Screenshot-screenshot berikut diambil saat melakukan tugas praktikum:

- Antarmuka utama Wireshark setelah aplikasi diluncurkan:
  ![Tampilan Wireshark](../Asset/Image/tampilanWireshark.png)
- Daftar paket yang berhasil ditangkap melalui koneksi Wi-Fi:
  ![Tampilan Capture from Wi-Fi](../Asset/Image/tampilanCaptureFromWifi.png)
- Tampilan browser yang menunjukkan halaman lab sederhana:
  ![Tampilan Browser pada link html](../Asset/Image/tampilanBrowserPadaLinkHtml.png)
- Hasil filter paket menggunakan kata kunci "http":
  ![Tampilan Capture from Wi-Fi With Filter HTTP](../Asset/Image/tampilanCaptureFromWifiWithFilterHTTP.png)
- Isi dari "Line-based text data" yang berisi respons HTML:
  ![Line-Based Text Data: text/html](../Asset/Image/lineBasedTextDataHtmlVer.png)
  Gambar ini menunjukkan contoh output yang wajib dicantumkan dalam laporan.