# Ex.No:1a  			Study of Socket Programming

## Aim: 
To implement the study of socket programming
## Introduction:
Socket programming plays a vital role in network communication by enabling data exchange between computers over a network. It serves as the foundation for many modern applications, allowing efficient interaction between client and server systems. This study focuses on the basic principles of socket programming, highlights its real-world applications, and presents a practical example to illustrate its implementation in a clear and understandable manner.
## Understanding Socket Programming:
Socket programming is a fundamental concept in network communication that uses sockets as endpoints for data exchange between devices. Each socket is uniquely identified by an IP address and a port number, enabling communication between a client and a server. There are two primary types of sockets: **Stream Sockets**, which offer reliable, connection-oriented communication using protocols like TCP, and **Datagram Sockets**, which provide connectionless communication using UDP and are suitable for applications where speed is more important than reliability.

## Key Concepts in Socket Programming:
Here is a clear and improved version of your content with better structure and wording:

---

### **1. Sockets**

* A socket is a software-based communication endpoint used in networking.
* It is uniquely identified by a combination of an IP address and a port number.
* Sockets are mainly classified into two types: **Stream Sockets** and **Datagram Sockets**.
* Stream Sockets use a connection-oriented approach (TCP) and ensure reliable data transfer.
* Datagram Sockets use a connectionless approach (UDP) and operate on a best-effort basis without guaranteed delivery.



### **2. Client–Server Model**

* Socket programming is commonly based on the client–server architecture.
* The server waits for incoming connection requests from clients.
* The client initiates communication by sending requests to the server.
* Servers are passive entities, while clients are active participants in communication.



### **3. TCP/IP Protocol**

* Socket communication relies on the **Transmission Control Protocol (TCP)** and **Internet Protocol (IP)**.
* TCP ensures reliable, ordered, and error-checked delivery of data.
* IP is responsible for addressing and routing data packets across networks.



### **4. Basic Socket Functions**

* Socket programming uses system-defined functions to manage communication.
* These functions help in creating and handling connections and data transfer.
* Commonly used functions include:

  * `socket()` – creates a new socket
  * `bind()` – assigns an IP address and port to the socket
  * `listen()` – waits for incoming connections
  * `accept()` – accepts a connection request
  * `connect()` – establishes a connection to a server
  * `send()` – sends data
  * `recv()` – receives data


## Server-Side Operations:

•	Servers create a socket using socket() and bind it to a specific IP address and port using bind().
•	They then listen for incoming connections with listen() and accept connections with accept().
•	Once a connection is establi
•	shed, servers can send and receive data using send() and recv().

## Client –Server Operations

Clients create a socket using socket() and connect to a server using connect().
After establishing a connection, clients can send and receive data using send() and recv().

## Use Cases of Socket Programming:
Socket programming finds applications in various domains, including web development, file transfer protocols, online gaming, and real-time communication. It is the foundation for protocols like HTTP, FTP, and SMTP, which power the internet. Socket programming enables the development of both server and client applications, facilitating the exchange of information between devices in a networked environment.
## Example Use Cases:
1. **Web Servers**
   Web servers use socket programming to manage incoming HTTP requests from clients and deliver web pages and other content efficiently.

2. **Chat Applications**
   Messaging and chat applications rely on sockets to enable real-time communication between users over a network.

3. **File Transfer**
   Protocols such as FTP (File Transfer Protocol) use socket programming to transfer files between clients and servers reliably.

4. **Networked Games**
   Online multiplayer games depend on sockets to support continuous communication between game clients and servers for real-time interaction.

5. **Remote Procedure Calls (RPC)**
   RPC mechanisms allow a program to execute code on a remote system, often using socket programming to handle the communication between devices.


## progrmme:
```
import socket
import threading
import time

PORT = 6000


def handle_client(conn, addr):
    print(" Connected to Saveetha Engineering College Server by:", addr)

    try:
        questions = [
            " Welcome to Saveetha Engineering College!",
            " What is your name?",
            " Which department are you from?"
        ]

        for q in questions:
            conn.sendall(q.encode())   
            
            reply = conn.recv(1024)    
            print(" Client says:", reply.decode())

        print(" Conversation finished with:", addr)

    except Exception as e:
        print("Error:", e)

    finally:
        conn.close()



def server():
    s = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    s.setsockopt(socket.SOL_SOCKET, socket.SO_REUSEADDR, 1)
    s.bind(("127.0.0.1", PORT))
    s.listen(5)

    print(" Saveetha Engineering College Server is running...")

    while True:
        conn, addr = s.accept()
        threading.Thread(target=handle_client, args=(conn, addr), daemon=True).start()



def client():
    time.sleep(1)

    c = socket.socket(socket.AF_INET, socket.SOCK_STREAM)
    c.connect(("127.0.0.1", PORT))

    try:
        
        replies = [
            "Good morning Sir!",                 
            "My name is kanagadharini ",              
            "I am from Computer Science Engineering"  
        ]

        for i in range(3):
            question = c.recv(1024)
            print("Server:", question.decode())

            print("Client:", replies[i])   
            c.sendall(replies[i].encode())

        print(" Client conversation completed")

    except Exception as e:
        print("Client Error:", e)

    finally:
        c.close()



threading.Thread(target=server, daemon=True).start()
threading.Thread(target=client).start()
```
## output:
<img width="1200" height="196" alt="2026-04-28 (1)" src="https://github.com/user-attachments/assets/cbb36c5a-9ba2-46dc-b06a-2d4ba4331f48" />

## Result:
Thus the study of Socket Programming Completed Successfully
