# 5a_Create_Socket_for_HTTP_for_webpage_upload_and_download

### Name: Pranitha S
### Reg. No.: 212225040312

## AIM :
To write a PYTHON program for socket for HTTP for web page upload and download

## Algorithm

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

~~~
import socket

s = socket.socket()
s.bind(("localhost",8080))
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
~~~

client.py

~~~
import socket

s = socket.socket()
s.connect(("localhost",8080))

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
~~~

index.html

~~~
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Welcome Page</title>
</head>
<body>
    <h1>Welcome to the Python HTTP Server!</h1>
    <p>This is the default page served by the server.</p>

</body>
</html>
~~~

## OUTPUT

### Download

<img width="1389" height="280" alt="Screenshot 2026-03-12 082236" src="https://github.com/user-attachments/assets/5a8b20d5-e98f-44d3-ab82-4c4e8b7bcf6f" />

<img width="1388" height="463" alt="Screenshot 2026-03-12 082206" src="https://github.com/user-attachments/assets/987abbc7-ff6e-4a9e-bccd-ff6073913f49" />

### Upload

<img width="1604" height="441" alt="Screenshot 2026-03-12 082534" src="https://github.com/user-attachments/assets/1d408a20-ef25-432b-a6f1-14b4d4f4c33e" />

<img width="1393" height="256" alt="Screenshot 2026-03-12 082435" src="https://github.com/user-attachments/assets/bd20700a-aacb-4338-b44b-d557745e4e1b" />

## Result
Thus the socket for HTTP for web page upload and download created and Executed
