# Modul 7 SOCKET PROGRAMMING

Tujuan Praktikum
mahasiswa dapat mempelajari cara kerja protokol Socket Programing menggunakan Wireshark.

## Socket Programing
Socket programming merupakan cara yang digunakan untuk menghubungkan dua atau lebih komputer dalam sebuah jaringan, di mana socket berperan sebagai jalur pertukaran informasi. Dalam mekanisme ini, terdapat dua komponen utama yang bekerja secara berlawanan, yakni client sebagai pihak yang mengajukan permintaan, dan server sebagai pihak yang menerima sekaligus merespons permintaan tersebut. Proses komunikasinya dapat berjalan melalui dua jenis protokol, yaitu TCP yang mengutamakan kestabilan dan memastikan data sampai ke tujuan dengan benar, serta UDP yang mengedepankan kecepatan meski tidak menjamin keberhasilan pengiriman data. Melalui pendekatan ini, setiap perangkat yang terhubung dalam jaringan dapat saling mengirim dan menerima data secara langsung satu sama lain.

## Implementasi TCP
### TCP Client
```python
from socket import * # import all libary

serverName = "localhost" # alamat server
serverPort = 12000 # membuat port untuk komunikasi

clientSocket = socket(AF_INET, SOCK_STREAM) # membuat socket ipv4 dan TCP
clientSocket.connect( # menghubungkan socket ke server
    (serverName, serverPort)
)

print("[SYSTEM] Masukan pesan") # pesan yang akan dikirim ke server

running = True # variabel untuk menjalankan program, jika false program akan berhenti
while running: # loop agar program terus berjalan
    modifiedMessage = clientSocket.recv(2048) # menerima pesan dari server, 2048 adalah ukuran buffer
    print("[SERVER] pesan : ", modifiedMessage.decode()) # decode untuk mengubah byte menjadi string

clientSocket.close() # menutup socket
print("[SYSTEM] socket ditutup")
```

### TCP Server
```python
from socket import * # import all library 

serverPort = 12000  # membuat port untuk komunikasi
serverSocket = socket(AF_INET, SOCK_STREAM) # membuat socket ipv4 dan TCP
serverSocket.setsockopt(SOL_SOCKET, SO_REUSEADDR, 1)
serverSocket.bind( #menghubungkan socket dengan alamat dan port
    ('', serverPort) # alamat kosong 
)

serverSocket.listen(1) # server siap menerima 1 koneksi dari client
print("[SYSTEM] server TCP siap digunakan") # menampilkan pesan server siap digunakan

running = True # variabel untuk menjalankan program, jika false program akan berhenti
while running: # loop agar program terus berjalan
    connectionSocket, addr = serverSocket.accept() # menerima koneksi dari client, addr untuk menyimpan alamat client
    while True: # loop untuk menerima pesan dari client
        message = connectionSocket.recv(2448).decode() # menerima pesan dari client, decode untuk mengubah byte menjadi string

        if not message: # jika pesan kosong, berarti client sudah keluar
            break

        if message.lower() == "exit": # pesan "exit" untuk keluar dari program
            print("[SYSTEM] client ingin keluar") # menampilkan pesan client ingin keluar
            running = False # ubah variabel running menjadi false untuk keluar dari loop
            break

        modifiedMessage = message.upper() # mengubah pesan menjadi capslock
        print("[SERVER] diterima: ",modifiedMessage) # menampilkan pesan yang diterima dari client

        connectionSocket.send( # mengirim pesan ke client 
            modifiedMessage.encode() # encode untuk mengubah string menjadi byte
        )
        
    connectionSocket.close() # menutup koneksi dengan client
serverSocket.close() # menutup socket
```

### Alur TCP
1. Server dijalankan terlebih dahulu
2. Client melakukan koneksi ke server
3. Client mengirim data
4. Server memproses data
5. Server mengirim hasil ke client
6. Client menampilkan hasil
7. Jika kita ketik exit kita akan keluar dan server berhenti

Output Contoh di terminal:
<img width="928" height="152" alt="{76BD0AF5-5BF8-4439-BF21-43F7EB645FDB}" src="https://github.com/user-attachments/assets/668512e9-08a5-4247-bfc4-e53fdf8a88af" />

## Implementasi UDP
### UDP Client
```python
from socket import *
import traceback

try:
    serverName = 'localhost'
    serverPort = 13000
    clientSocket = socket(AF_INET, SOCK_DGRAM)

    print("[SYSTEM] Masukkan pesan (ketik 'exit' untuk keluar)\n", flush=True)

    while True:
        message = input("> ")

        if not message:
            continue

        clientSocket.sendto(message.encode(), (serverName, serverPort))

        if message.lower() == 'exit':
            print("[SYSTEM] Keluar dari program.")
            break

        balasan, _ = clientSocket.recvfrom(2048)
        print(f"[SERVER] pesan: {balasan.decode()}\n")

    clientSocket.close()
    print("[SYSTEM] Socket ditutup.")

except Exception as e:
    print(f"\n[ERROR] {e}")
    traceback.print_exc()

finally:
    input("\nTekan Enter untuk keluar...")
```

### UDP Server
```python
from socket import *
import traceback

try:
    serverName = 'localhost'
    serverPort = 13000
    clientSocket = socket(AF_INET, SOCK_DGRAM)

    print("[SYSTEM] Masukkan pesan (ketik 'exit' untuk keluar)\n", flush=True)

    while True:
        message = input("> ")

        if not message:
            continue

        clientSocket.sendto(message.encode(), (serverName, serverPort))

        if message.lower() == 'exit':
            print("[SYSTEM] Keluar dari program.")
            break

        balasan, _ = clientSocket.recvfrom(2048)
        print(f"[SERVER] pesan: {balasan.decode()}\n")

    clientSocket.close()
    print("[SYSTEM] Socket ditutup.")

except Exception as e:
    print(f"\n[ERROR] {e}")
    traceback.print_exc()

finally:
    input("\nTekan Enter untuk keluar...")
```
### Alur UDP
1. Server dijalankan
2. Client langsung mengirim data tanpa koneksi
3. Server menerima data
4. Server memproses
5. Server mengirim balasan
6. Client menerima hasil
7. Jika kita ketik exit kita akan keluar dan server berhenti

Output Contoh di terminal:
<img width="1014" height="189" alt="{2FA3AA96-C944-4AEF-A07F-B6C8CD4B6709}" src="https://github.com/user-attachments/assets/31f4e2ec-568e-4682-8a63-921369fa0c53" />

