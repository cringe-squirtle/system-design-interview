# Yelp
### about
- proximity server
- for seeking nearby attractions as places, events, etc..


### requirements
- storing infomation different places
- CRUD for places
- given user location, user be able to find all nearby places with a given radius
- user be able to add feedback/review to a place, pictures, text, rating
- user be able to search in real-time minimum latency
- service support heavy search load, greater than add a new place


### scale estimation
- assume 500M places
- assume 100k queries/s per second (QPS)
- assume 20% growth of places and QPS each year


### database
- place table
    - location id 8bytes
    - name 256 bytes
    - latitu 8bytes
    - longi 8 bytes
    - description 512 bytes
    - category 1 byte
    - total ≈ 793 bytes
- review table
    - location id 8 bytes
    - review id 4 bytes unique to each location
    - review text 512 bytes
    - rating 1 bytes


### api
- search(api_dev_key, search_text, user_location, radius, maximum_results, category, sort, page) return JSON of list of info of place


### search algorithm
- store search index
- split map into grids, winthn a specific range of longitude and latitude
- keep index in memory in hashtable 
- memory for storing index: 4byte of grid * 200M grid + 8byte location * 500M locations ≈ 4GB
- dynamic size grids: when a grid reach some threshold, split the grid into 4 pieces
- tree structure : doubly linked list for leafs for searching neighboring grids
-

### data partitioning
- partition tree
- sharding based on regions issues: hot regions, some regions storing more places
- sharding based on locationID: need a central server to aggregate all results from different sharding servers


### single point failure


### load balancing 
- if a server is overloaded or slow, load balancer does not send new requests to the server








