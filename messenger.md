# Facebook Messenger


### about 
- text based messaging services, 
- can chat with their facebook friends
- from web, cell phone, computer


### requirements
- support one to one conversations
- keep track of online/offline statuses of users
- support persistent storage of chat history
- realtime chatting with minimum latency
- highly consistent, users be able to see the same history
- highly available 
- group chats
- push notifications


### capacity estimation
- 500 million daily users, 40 messages/user daily, 20 billion messages/day
- storage estimation:
    - 100 bytes per message
    - 20 billion * 100 bytes ≈ 2TB/day
    - 5 years -> 2TB * 365 * 5 = 3650 TB
- bandwidth estimation:
    - 2TB/86400sec ≈ 25MB/s
    - message go in and go out-> 25*2 = 50mb/s


### high level design
- chat server be central piece
- userA sends message to userB via chat server
- server receives message then sends acknowledgment to userA
- server stores message in db sends message to userB
- userB receiveds message then sends acknowledgetment to server
- server notifies userA that message has be delievered.

### detailed component design
- receive incoming messages and deliver outgoing messages
- store retrieve messages from the db
- keep a record of which user is online or has gone offline, notify all relevant users about these status changes
- 
- message handling
    - pull model, users periodically ask server if there are new message
        - to minimize latency, needs to request server very frequently and most time will get empty feedback if no pending new message and it takes a lot of resources
    - push model, user keep a connection open with server nd depend upon the server to notify them when there are new messages
        - ASAP server recieves a message it can immediately pass the message to the intended user
        - maintain open-connection with server: webSockets, long polling.  
        - long polling-request with expectation that the server may not respond immediately, holds request until recieve new info then respond to user
        - to track all opened connections, server keeps a hashtable, with userID as key and connection object as value,
        - user gone offline: if receiver disconnected the server notify the sender about the deliver failure.  long-poll request time out.  expect a reconnect from the user.  also can allow server to retry autoly to send the message.  or once receiver reconnects. or let receiver resend mannually.
        - if have 500million connections at anytime, then need 50k concurrent connections and 10k servers
        - user load balancer in front of chat servers to track if server holds the connection to user.  map each userid to a server to redirect the request
        - process deliver message
            - store message in db
            - send message to receiver
            - send acknolegement to sender
        - maintaining the sequencing of the messages:
            - store timestamp with each message
            - 
    - storing and retriveing the messages from the database
        - start a separate thread to store the message
        - send asynchronous request to db to store the message
    - storage system to use: no mysql or mongodb because read/write a row eachtime update/sends a message
    - use HBase is column oriented key-value nosql database thant store multiple values against one key into multiple columns
    - clients paginate while fetching data from the server page size depends on screen size(phones, laptop, webs)
    - manage users status
        - user starts app, pull current status of all friends
        - sends message to other who offline, send a failure to the sender then update teh status on the client
        - clients pull status from server about friends, non-frequent because server is broadcasting status (live for a while)
        - 
    

### data partitioning
 - distribute it onto multiple database servers
 - partitioning based on userID
 - 4tb per db shard 3.6pB/4TB≈ 900 for 5 years then we have 1k shards
 - related single-point failure, hot user. etc
 - partining based on messageID: get a range of messages will be slow->bad decision
 - 
 

### Cache
- cache for a user be entirely reside on one machine

### fault tolerance and replication

### group chat
- modal: groupchatID, maintain a list of people, load balancer direct each group chat message based on groupChatID

### puch notifications
- enables users to send messages to offline users
- have a notification server, to send message to manufacturer's push notification esrver, which let users to opt-in from there device for notifications...
 















