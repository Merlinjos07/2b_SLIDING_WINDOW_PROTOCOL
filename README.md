# 2b IMPLEMENTATION OF SLIDING WINDOW PROTOCOL
## AIM
## ALGORITHM:
1. Start the program.
2. Get the frame size from the user
3. To create the frame based on the user request.
4. To send frames to server from the client side.
5. If your frames reach the server it will send ACK signal to client
6. Stop the Program
## PROGRAM
CLIENT 

```
import socket

# Create socket
c = socket.socket()

# Connect to server
c.connect(('localhost', 8000))

while True:
    # Receive data from server
    data = c.recv(1024).decode()

    # Stop if no data
    if not data:
        break

    # Display received frames
    print("Received Frames:", data)

    # Send ACK to server
    ack = "ACK received"
    c.send(ack.encode())

# Close connection
c.close()
```

SERVER

```
import socket

# Create socket
s = socket.socket()

# Bind and listen
s.bind(('localhost', 8000))
s.listen(5)

print("Waiting for connection...")

# Accept client
c, addr = s.accept()
print("Connected to:", addr)

size = int(input("Enter number of frames to send: "))
frames = list(range(size))

window_size = int(input("Enter Window Size: "))

i = 0

while i < len(frames):

    # Send window frames
    data = str(frames[i:i + window_size])

    c.send(data.encode())

    # Receive ACK
    ack = c.recv(1024).decode()

    if ack:
        print(ack)

    i += window_size

# Close connections
c.close()
s.close()
```
## OUPUT
CLIENT
<img width="1155" height="956" alt="image" src="https://github.com/user-attachments/assets/eb7f0924-8101-45b1-8fb7-585bdeb4214a" />
SERVER 
<img width="1166" height="939" alt="image" src="https://github.com/user-attachments/assets/154e067e-cebe-44b8-a513-7fb02156e93a" />

## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
