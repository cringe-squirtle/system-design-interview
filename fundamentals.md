
# Fundamentals

## What
- design uber, messager, youtube etc..
- question interviewer
  - kind of functionality to support
  - what system to build
  -  risk to evaluate
  -  etc
- 主觀， not 客觀正確 or 客觀不正確， 
  - to reason of desgin
  - to defend your position

## Client -- Server Model
- clent
  - A machine or process that requests data or service from a server
- server
  - A machine or process that provides data or service for a client, usually by listening for incoming network calls
- note: client and server can be in a single machine or piece of software.
- client--server model
  - clients requesting data or service from servers and servers providing data or service to clients
- IP Address
  - consist of 4 numbers(a.b.c.d, range 0- 255)
- port
  - for multiple programs to listen for new network connections on the same machine without colliding.
  - range 0 - 2^16
  - ports 0 - 1023 aer reserved for system ports and shouldn't be used by user-level processes
- DNS
  - Domain Name System
  - translate from domain names to IP addresses
  - machines make a DNS query to a well known entity responsible for returning the IP address of the requested domain name in the responses

### Network Protocol
- IP 
  - internet protocol
  - outlines how almost all machine-to-machine communications should happen in the world. 
  - TCP, UDP, HTTP are built on top of IP
- TCP
  - allows for ordered, reliable data delivery between machines over the public internet by creating a connection
  - usually implemented in the kernel, exposes sockets to applications that they can use to stream data through an open connection
- HTTP
  - HyperTextTransferProtocol
  - implemented on top of TCP
  - client make HTTP requests and servers respond with a response
- IP Packet
  - an IP packet is effectively the smallest unit used to describe data being sent over IP
  - IP header - contains the source and destination IP addresses as well as other information related to the netword
  - payload - just the data being sent over the network
