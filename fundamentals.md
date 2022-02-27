
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
  - Transmission control protocol, on top of IP
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

### Storage
- Databases
  - use disk or memory
  - do record data and query data
  - some databases only keep records in memory - then those records may be lost forever if the machine or process dies
  - need persistence of data - thus cannot use memory - write data to disk - will remain through power loss or network partition
  - be permanent
- Disk
  - HDD or SDD
  - data written to disk will persist through power failures and general machine crashed
  - disk - non-volatile storage
  - SDD vs HDD, SDD is far faster, expensive
  - HDD typically used for data that's rarely accessed or updated, but stored for a long time
  - SDD for data frequently accessed and updated
- Memory
  - RAM - Random Access Memory
  - data in memory will be lost when process dies
- Persistent Storage
  - refer to disk usually
  - any form of storage that persists if the process in charge of managing it dies

### Latency and throughput
- latency
  - the time it takes for a certain operation to complete in a system
  - reading 1 MB from RAM: 0.25 ms
  - reading 1 MB from SSD: 1 ms
  - transfer 1 MB from Network: 10 ms
  - reading 1 MB from HDD: 20 ms
  - inter-Continental Round Trip: 150 ms
- Throughput
  - nmber of operations a system can handle properly per time unit.
  - e.g. measured in requests per second

### Availability
- Availability
  - how fault tolerance of a system
  - usually measured in percentages
- High Availability
  - used to describe systems that have particularly high levels of availability
  - 5 nines or more
- Nines
  - per year
  - 99%: 87.7 hours
  - 99.9% 8.8 hours
  - 99.99% 52.6 minutes
  - 99.999% 5.3 minutes
- Redundancy
  - the process of replicating parts of a system in an effort to make it more reliable
- SLA - service-level agreement
  - guarantees given to a customer by a service provider
  - make guarantees on a system's availability
  - are made up of one or multiple SLOs
- SLO - service-level-objective
  - guarantee given to a customer by a service provider
  - make guarantees on a system's availability, amongst other things
  - SLOs constitue an SLA
