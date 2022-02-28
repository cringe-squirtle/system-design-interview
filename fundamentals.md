
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
### Caching
- cache
  - a piece of hardware of software that stores data, typically meant to retrieve that data faster than otherwise
  - often used to store responses to network requests as well as results of computationlly-long operations
  - data in a cache can become stale if the main source of truth for that data gets updated and the cache doesn't
- cache hit
  - when requested data is found in a cache
- cache miss
  - requested data could have been found in a cache but isn't
  - used to refer to a negative consequence of a system failure or a poor design choice
- cache eviction policy
  - values get evicted or removed from a cache
  - LRU - least-recently used
  - FIFO
  - LFU - least-frequently used
- content delivery network
  - CDN - acts like a cache for your servers
  - web applications can be slow for users in a region if your servers located only in another region
  - CDN has servers all around the world - latency be far better than your server
  - PoPs - points of presence
  - cloudflare
  - google cloud CDN

### Proxy
- forward proxy
  - server sits between a client and servers and acts on behalf of the client, typically used to mask the client's identity
- Reverse Proxy
  - server sits between a client and servers and acts on behalf of the server, typically used for logging, loading balance, or caching
- Nginx
  - popular webserver used as a reverse proxy and load balancer

### Load Balancer
- load balancer
  - a type of reverse proxy
  - distributes traffic across servers
  - in many parts of a system, DNS layer, database layer, etc
- Server Selection Strategy
  - how load balancer chooses servers when distributing traffic amongst multiple servers
  - strategies:
    - round-robin
    - random selection
    - performance-based selection
    - IP-based routing - to maximize caching usage, redirect some requests always to a cached server
- Hot Spot
  - workload might be spread unevenly
  - can happen if sharding key or hashing function are suboptimal
  - some servers receive a lot more traffic than others
- Nginx

### Hashing
- consisten hashing
 - minimizes the number of keys that need to be remapped when a hash table gets resized
 - often used by load balancers to distribute traffic to servers
 - minimizes the number of requests that get forwarded to different servers when new servers are added or when existing servers are brought down
- Rendezvous Hashing
  - highest random weight hashing
  - allows for minimal re-distribution of mappings when a server goes down
- SHA
  - Secure Hash Algorithms
  - cryptographic hash functions used in the industry


### Relational Databases
- Relational Database
  - data is stored following a tabular formt
  - supports powerful. querying using SQL
- Non-Relational Database
  - free of imposed, tabular-like structure
  - often referred to as NoSQL databases
- SQL
  - Structured Query Language
  - though, not every relation database supports SQL
- NoSQL database
  - any database that is not SQL-compatible is called NoSQL
- ACID Transaction
  - Atomicity - transaction will either all succeed or all fail, no in-between state
  - Consistency 
    - transaction cannot bring the database to an invalid state
    - after transaction is committed or rolled back, the rules for each record will still apply
    - also named Strong Consistency
  - Isolation - multiple transactions execution concurrently will have the same effect as if they had been executed sequentially
  - Durability - Any committed transaction is written to no-volatile storage, will not be undown by a crash, power loss or network partition
- Database Index
  - allows db to perform certain queries much faster
  - exist to reference structured data
  - create an index on one or multiple columns in your database to greatly speed up read queries that you run very often, with downside of slightly longer writes to your database.
- Strong Consistency
  - consistency of ACID, opposed to Eventual Consistency
- Eventual Consistency
  - reads might return a view of the system that is stale
  - guarantees that the state of the database will eventually reflect writes within a time period
