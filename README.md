# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download
## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download
## Algorithm
1.Start the program.
2.Get the frame size from the user
3.To create the frame based on the user request.
4.To send frames to server from the client side.
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
6.Stop the program



1.Start the program.
<BR>
2.Get the frame size from the user
<BR>
3.To create the frame based on the user request.
<BR>
4.To send frames to server from the client side.
<BR>
5.If your frames reach the server it will send ACK signal to client otherwise it will send NACK signal to client.
<BR>
6.Stop the program
<BR>
## Program 
server.py
```
import socket
s = socket.socket()
s.bind(("127.0.0.1",12345))
s.listen(1)
print("Server running...")
while True:
    c,addr = s.accept()
    request = c.recv(1024).decode()
    print("Request received")
    if "GET" in request:
        f = open("index.html","r")
        data = f.read()
        f.close()
        response = "HTTP/1.1 200 OK\n\n" + data
        c.send(response.encode())
    elif "POST" in request:
        data = request.split("\n\n")[1]
        f = open("upload.txt","w")
        f.write(data)
        f.close()
        c.send("HTTP/1.1 200 OK\n\nFile Uploaded".encode())
    c.close()
```
client.py
```
import socket
s = socket.socket()
s.connect(("127.0.0.1",12345))
ch = input("1.Download 2.Upload : ")
# Download webpage
if ch == "1":
    req = "GET / HTTP/1.1\nHost: localhost\n\n"
    s.send(req.encode())
    data = s.recv(4096)
    print(data.decode())
# Upload file
else:
    msg = input("Enter data to upload: ")
    req = "POST / HTTP/1.1\nHost: localhost\n\n" + msg
    s.send(req.encode())
    data = s.recv(1024)
    print(data.decode())
s.close()
```
## OUTPUT
<img width="1329" height="810" alt="image" src="https://github.com/user-attachments/assets/3b1bbed1-bb84-4225-b717-5749e31d0a54" />
<img width="788" height="432" alt="image" src="https://github.com/user-attachments/assets/d56ab1f9-a872-4496-8d41-06fe65d75662" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
