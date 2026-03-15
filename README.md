# 2c.SIMULATING ARP /RARP PROTOCOLS
## AIM
To write a python program for simulating ARP protocols using TCP.
## ALGORITHM:
## Client:
1. Start the program
2. Using socket connection is established between client and server.
3. Get the IP address to be converted into MAC address.
4. Send this IP address to server.
5. Server returns the MAC address to client.
## Server:
1. Start the program
2. Accept the socket which is created by the client.
3. Server maintains the table in which IP and corresponding MAC addresses are
stored.
4. Read the IP address which is send by the client.
5. Map the IP address with its MAC address and return the MAC address to client.

## PROGRAM - ARP
```
import socket

s = socket.socket()
host = socket.gethostname()
port = 5000

s.bind((host, port))
s.listen(1)

print("ARP Server Waiting for Connection...")

conn, addr = s.accept()
print("Connected from:", addr)

arp_table = {
    "192.168.1.1": "AA:BB:CC:DD:EE:01",
    "192.168.1.2": "AA:BB:CC:DD:EE:02",
    "192.168.1.3": "AA:BB:CC:DD:EE:03"
}

ip = conn.recv(1024).decode()

if ip in arp_table:
    mac = arp_table[ip]
else:
    mac = "MAC Address Not Found"

conn.send(mac.encode())
conn.close()
import socket

s = socket.socket()
host = socket.gethostname()
port = 5000

s.connect((host, port))

ip = input("Enter IP Address: ")

s.send(ip.encode())

mac = s.recv(1024).decode()

print("MAC Address is:", mac)

s.close()
```
## OUPUT - ARP
<img src="https://img.sanishtech.com/u/afa364ab4143c9b2426ead641eadf794.png" alt="Screenshot 2026-03-15 111315" width="1920" height="1080" loading="lazy" style="max-width:100%;height:auto;">
## PROGRAM - RARP

```
import socket

s = socket.socket()
host = socket.gethostname()
port = 6000

s.bind((host, port))
s.listen(1)

print("RARP Server Waiting for Connection...")

conn, addr = s.accept()
print("Connected from:", addr)

rarp_table = {
    "AA:BB:CC:DD:EE:01": "192.168.1.1",
    "AA:BB:CC:DD:EE:02": "192.168.1.2",
    "AA:BB:CC:DD:EE:03": "192.168.1.3"
}

mac = conn.recv(1024).decode()

if mac in rarp_table:
    ip = rarp_table[mac]
else:
    ip = "IP Address Not Found"

conn.send(ip.encode())
conn.close()
import socket

s = socket.socket()
host = socket.gethostname()
port = 6000

s.connect((host, port))

mac = input("Enter MAC Address: ")

s.send(mac.encode())

ip = s.recv(1024).decode()

print("IP Address is:", ip)

s.close()

```
## OUPUT -RARP
<img src="https://img.sanishtech.com/u/49fc18ba9355dc2054f76882d66c77d4.png" alt="Screenshot 2026-03-15 112635" loading="lazy" style="max-width:100%;height:auto;">
## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
