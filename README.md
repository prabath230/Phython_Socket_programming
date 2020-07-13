# Phython_Socket_programming
Phython Socket (client ,server)
Socket API Overview
Python’s socket module provides an interface to the Berkeley sockets API. This is the module that we’ll use and discuss in this tutorial.
The primary socket API functions and methods in this module are:
•	socket()
•	bind()
•	listen()
•	accept()
•	connect()
•	connect_ex()
•	send()
•	recv()
•	close()
TCP Sockets
As you’ll see shortly, we’ll create a socket object using socket.socket() and specify the socket type as socket.SOCK_STREAM. When you do that, the default protocol that’s used is the Transmission Control Protocol (TCP). This is a good default and probably what you want.
Why should you use TCP? The Transmission Control Protocol (TCP):
•	Is reliable: packets dropped in the network are detected and retransmitted by the sender.
•	Has in-order data delivery: data is read by your application in the order it was written by the sender.
In contrast, User Datagram Protocol (UDP) sockets created with socket.SOCK_DGRAM aren’t reliable, and data read by the receiver can be out-of-order from the sender’s writes.
Why is this important? Networks are a best-effort delivery system. There’s no guarantee that your data will reach its destination or that you’ll receive what’s been sent to you.
Network devices (for example, routers and switches), have finite bandwidth available and their own inherent system limitations. They have CPUs, memory, buses, and interface packet buffers, just like our clients and servers. TCP relieves you from having to worry about packet loss, data arriving out-of-order, and many other things that invariably happen when you’re communicating across a network.
In the diagram below, let’s look at the sequence of socket API calls and data flow for TCP:
 

TCP Socket Flow (Image source)
The left-hand column represents the server. On the right-hand side is the client.
Starting in the top left-hand column, note the API calls the server makes to setup a “listening” socket:
•	socket()
•	bind()
•	listen()
•	accept()
A listening socket does just what it sounds like. It listens for connections from clients. When a client connects, the server calls accept() to accept, or complete, the connection.
The client calls connect() to establish a connection to the server and initiate the three-way handshake. The handshake step is important since it ensures that each side of the connection is reachable in the network, in other words that the client can reach the server and vice-versa. It may be that only one host, client or server, can reach the other.
In the middle is the round-trip section, where data is exchanged between the client and server using calls to send() and recv().
At the bottom, the client and server close() their respective sockets.
