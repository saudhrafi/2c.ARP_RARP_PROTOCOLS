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

### CLIENT

```
import socket

client_socket = socket.socket()

client_socket.connect(('localhost', 8000))

print("Connected to ARP Server")

while True:

    ip = input("Enter Logical(IP) Address: ")

    client_socket.send(ip.encode())

    mac = client_socket.recv(1024).decode()

    print("MAC Address:", mac)
```

### SERVER

```
import socket

server_socket = socket.socket()

server_socket.bind(('localhost', 8000))
server_socket.listen(1)

print("Waiting for connection...")

conn, addr = server_socket.accept()
print("Connected with:", addr)

address = {
    "165.165.80.80": "6A:08:AA:C2",
    "165.165.79.1": "8A:BC:E3:FA"
}

while True:

    ip = conn.recv(1024).decode()

    if not ip:
        break

    print("Requested IP Address:", ip)

    try:
        conn.send(address[ip].encode())
    except KeyError:
        conn.send("Not Found".encode())

conn.close()
server_socket.close()
```

## PROGRAM - RARP

### CLIENT

```
import socket

client_socket = socket.socket()

client_socket.connect(('localhost', 9000))

print("Connected to RARP Server")

while True:

    mac = input("Enter MAC Address: ")

    client_socket.send(mac.encode())

    ip = client_socket.recv(1024).decode()

    print("Logical(IP) Address:", ip)
```

### SERVER
```
mport socket

server_socket = socket.socket()

server_socket.bind(('localhost', 9000))
server_socket.listen(1)

print("Waiting for connection...")

conn, addr = server_socket.accept()
print("Connected with:", addr)

address = {
    "6A:08:AA:C2": "192.168.1.100",
    "8A:BC:E3:FA": "192.168.1.99"
}

while True:

    mac = conn.recv(1024).decode()

    if not mac:
        break

    print("Requested MAC Address:", mac)

    try:
        conn.send(address[mac].encode())
    except KeyError:
        conn.send("Not Found".encode())

conn.close()
server_socket.close()
```

## OUTPUT - ARP
<img width="1920" height="1080" alt="ARP" src="https://github.com/user-attachments/assets/4b1f57ce-b2e1-48f9-9880-cd6bfb67313e" />


## OUPUT - RARP

<img width="1920" height="1080" alt="RARP" src="https://github.com/user-attachments/assets/06ed29ec-135e-4992-953a-f95ad9d99abe" />

## RESULT
Thus, the python program for simulating ARP protocols using TCP was successfully 
executed.
