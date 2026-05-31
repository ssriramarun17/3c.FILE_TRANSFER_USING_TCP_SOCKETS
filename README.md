# 3c.CREATION FOR FILE TRANSFER USING TCP SOCKETS
## AIM
To write a python program for creating File Transfer using TCP Sockets Links
## ALGORITHM:
1. Import the necessary python modules.
2. Create a socket connection using socket module.
3. Send the message to write into the file to the client file.
4. Open the file and then send it to the client in byte format.
5. In the client side receive the file from server and then write the content into it.
## PROGRAM
### server.py
```python
import socket

# Create socket
server = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Server details
host = "127.0.0.1"
port = 5555

# Bind and listen
server.bind((host, port))
server.listen(1)

print("Server waiting for connection...")

# Accept client
client, addr = server.accept()
print("Connected to:", addr)

# File to send
filename = input("Enter file name to send: ")

try:
    with open(filename, "rb") as file:
        while True:
            data = file.read(1024)

            if not data:
                break

            client.send(data)

    print("File sent successfully")

except FileNotFoundError:
    print("File not found")

# Close connections
client.close()
server.close()
```
### client.py
```python
import socket

# Create socket
client = socket.socket(socket.AF_INET, socket.SOCK_STREAM)

# Server details
host = "127.0.0.1"
port = 5555

# Connect to server
client.connect((host, port))

print("Connected to server")

# File name to save
save_name = input("Enter name to save file: ")

# Receive and save file
with open(save_name, "wb") as file:
    while True:
        data = client.recv(1024)

        if not data:
            break

        file.write(data)

print("File received successfully")

# Close connection
client.close()
```
## OUPUT
<img width="1919" height="981" alt="Screenshot 2026-05-25 084731" src="https://github.com/user-attachments/assets/5749a1db-b75a-4577-8084-59d395a353cb" />


## RESULT
Thus, the python program for file transferring using TCP Pockets has been executed successfully
