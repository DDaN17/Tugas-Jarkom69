# Modul 9  WEB SERVER

Tujuan Praktikum
mahasiswa dapat mempelajari cara kerja protokol Web Server menggunakan Wireshark.

## Web Server
Web server adalah bagian penting dalam komunikasi di internet. Web server bertugas menerima permintaan dari pengguna melalui browser, lalu mengirimkan halaman web atau data yang diminta. Komunikasi ini biasanya menggunakan protokol HTTP yang berjalan di atas TCP.

##
Tujuan Praktikum 
 Mahasiswa bisa membuat program web server sederhana berbasis TCP socket programming

## Langkah-Langkah
  1. mebuat folder week9
  2. Membuat file serverweb.py di VScode
  3. code :

```python
from socket import *
import sys

# membuat socket server (TCP)
serverSocket = socket(AF_INET, SOCK_STREAM)

# Prepare a server socket
serverPort = 6789
serverSocket.bind(('', serverPort))
serverSocket.listen(1)

while True:
    # Establish the connection
    print('Ready to serve...')
    connectionSocket, addr = serverSocket.accept()

    try:
        # menerima request dari client
        message = connectionSocket.recv(1024).decode()
        print(message)

        # mengambil nama file
        filename = message.split()[1]

        # membuka file
        f = open(filename[1:])
        outputdata = f.read()

        # Send HTTP header
        connectionSocket.send("HTTP/1.1 200 OK\r\n".encode())
        connectionSocket.send("Content-Type: text/html\r\n".encode())
        connectionSocket.send("\r\n".encode())

        # kirim isi file
        for i in range(len(outputdata)):
            connectionSocket.send(outputdata[i].encode())

        connectionSocket.send("\r\n".encode())
        connectionSocket.close()

    except IOError:
        # kirim 404 jika file tidak ada
        connectionSocket.send("HTTP/1.1 404 Not Found\r\n".encode())
        connectionSocket.send("Content-Type: text/html\r\n".encode())
        connectionSocket.send("\r\n".encode())
        connectionSocket.send("<html><body><h1>404 Not Found</h1></body></html>".encode())

        # tutup koneksi
        connectionSocket.close()

serverSocket.close()
sys.exit()
```
  4. Setelah itu membuat file HelloWorld.html
  5. lalu diisi
```html
<html>
<head>
    <title>Test Server</title>
</head>
<body>
    <h1>Hello World!</h1>
    <p>Ini hasil server Python TCP</p>
</body>
</html>
```

## Hasilnya
1. Kita buka terminal lalu ketik ini "py serverweb.py" lalu di enter
2. Setelah itu Buka browser ketikan URL "http://localhost:6789/HelloWorld.html"
3. Maka akan muncul tampilan seperti ini:

<img width="1056" height="608" alt="{996FDE65-A590-4BF0-9655-98CB93F94C35}" src="https://github.com/user-attachments/assets/748e94ca-a551-4dc1-8cf6-a1469b04b46e" />

4. Lalu buka tab lainnya dan ketikkan "http://localhost:6789/salah.html"
5. Maka akan muncul tampilan seperti ini:

<img width="1062" height="614" alt="{3DBF482E-9531-4148-91E3-C322D563BEC5}" src="https://github.com/user-attachments/assets/aeff84a3-4275-4035-a0e1-4f53cc12be38" />

Server akan menampilkan pesan "404 Not Found" jika file yang diminta tidak tersedia. Hal ini menunjukkan bahwa server dapat menangani permintaan yang berhasil maupun yang gagal dengan baik.

Program dimulai dengan membuat socket TCP menggunakan library socket. Setelah itu, server dijalankan pada port tertentu dan menunggu koneksi dari klien. Saat klien terhubung, server menerima request HTTP dan membaca nama file yang diminta. Jika file ditemukan, server mengirimkan respons 200 OK beserta isi file HTML. Jika file tidak ditemukan, server mengirimkan respons 404 Not Found. Program ini hanya dapat melayani satu klien pada satu waktu karena menggunakan metode single-threaded.

## Latihan Web Tambahan
Disini kita membuat server dan web kita sendiri.
1. Buka VScode dan masuk ke folder tadi
2. buka file server.py
3. Tulis ulang codenya seperti ini:

```python
from socket import *
import threading

def handle_client(connectionSocket):
    try:
        # menerima pesan user
        message = connectionSocket.recv(1024).decode() # decode = 10101010 = "message"

        # index.html, hello.html
        # message isinya = /GET /index.html HTTP/1.1
        message = message[4:15]
        print(message)
        # filename = message.split()[1]

        # membuka index.html serta menghilangkan "/"
        f = open(message[1:])

        # membaca file html
        outputData = f.read()

        # kirim respon
        connectionSocket.send(
            "HTTP/1.1 200 OK\r\n\r\n".encode()
        )

        # kirim data
        connectionSocket.sendall(outputData.encode())

        # tutup koneksi
        connectionSocket.close()
    
    except IOError:
        # kirim respon bila tidak ditemukan
        connectionSocket.send(
            "HTTP/1.1 404 Not Found\r\n\r\n".encode()
        )

        # kirim data
        connectionSocket.send(
            "<h1>404 Not Found</h1>".encode()
        )

        # tutup koneksinya
        connectionSocket.close()


serverSocket = socket(AF_INET, SOCK_STREAM)
serverSocket.bind(('', 6789))
serverSocket.listen(5) # dapat menerima sebanyak 5 client
print("[SYSTEM] server is running...")

while True:
    connectionSocket, addr =  serverSocket.accept()

    # membuat thread dan target threadnya, beseerta parameter
    thread = threading.Thread(
        target = handle_client,
        args = (connectionSocket,)
        )
    # menjalankan
    thread.start()
```
4. lalu kita buat "index.html" nya
5. tulis seperti ini:

```html
<html>
<head>
    <title>SELAMAT DATANG</title>
</head>
<body>
    <h1>Hallo</h1>
    <p>Disini web servernya sudah bisa</p>
</body>
</html>
```

## Hasilnya
1. Seperti tadi kita buka terminal lalu ketik "py serverweb.py" lalu di enter
2. Setelah itu Buka browser ketikan URL "http://localhost:6789/Index.html"
3. Maka akan muncul tampilan seperti ini:

<img width="617" height="240" alt="{739D5CFD-52D7-40E9-8DF2-A116FEF1B1C2}" src="https://github.com/user-attachments/assets/bfb6da37-f124-430a-bfc9-6679cb558fe6" />


4. Selesai

Server menggunakan multithreading untuk melayani beberapa klien secara bersamaan. Setiap koneksi dijalankan pada thread terpisah sehingga server dapat menangani banyak permintaan tanpa harus menunggu proses sebelumnya selesai.
