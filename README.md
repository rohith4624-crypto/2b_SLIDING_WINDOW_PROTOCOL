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
Server:
```
import socket

skt = socket.socket()
skt.bind(('localhost', 1234))
skt.listen(5)
print("Waiting for server connection...")
c, addr = skt.accept()

while True:
    try:
        size = int(input("Enter number of frames to send: "))
        if size > 0:
            break
        print("Enter a positive number.")
    except ValueError:
        print("Invalid input! Enter numbers only.")

frames = list(range(size))

while True:
    try:
        window = int(input("Enter Window Size: "))
        if 0 < window <= size:
            break
        print("Enter a valid window size.")
    except ValueError:
        print("Invalid input! Enter numbers only.")

start = 0

while start < len(frames):
    end = min(start + window, len(frames))
    c.send(str(frames[start:end]).encode())
    ack = c.recv(1024).decode()
    if ack:
        print(ack)
    start = end

c.close()
skt.close()

```
Client:
```

import socket

s = socket.socket()
s.connect(('localhost', 1234))

while True:
    data = s.recv(1024).decode()

    if not data:
        break

    print("Received frames:", data)
    s.send("Acknowledgement received from the server".encode())

s.close()

```
## OUPUT
server 


<img width="367" height="387" alt="Screenshot 2026-11-02 134405" src="https://github.com/user-attachments/assets/504b4630-126f-4d7c-b7ee-795da4cb7b0d" />


Client 


<img width="383" height="512" alt="Screenshot 2026-11-02 134357" src="https://github.com/user-attachments/assets/fba8dda6-e70d-4e48-b758-7070dbe9474b" />


## RESULT
Thus, python program to perform stop and wait protocol was successfully executed
