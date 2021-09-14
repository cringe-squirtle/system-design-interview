# Design Instagram
 
#### similar: flickr, picasa
 
### requirements:
- user be able to upload/download/view photos/videos
- user be able to search based on photo/video titles
- user be able to follow other users
- system be able to gen display users' new feed consisting of top photos
- service highly available
- low/acceptable latency for new feed generation
- system be highly reliable, uploaded photos/videos never be lost


### design considerations
- users be able upload unlimited photos, efficient management of storage
- low latency
- reliability

### capacity estimation
- assume 500M users, 1M daily active users
- 2M new photos/day, 20 new photos/sec
- avg photo sie =200kb
- 1 day photo storage 2M*200kb = 400gb
- total space for 10 years=> 400 * 365 * 10 = 1425TB

### high level design
- scenrios -> upload photos and view/search photos
- object storage servers to store photos/videos
- database servers to store metadata information of photos/videos


### model design
- photo table: photoID, userID, path, width, height, creationDate
- user table: userID, name, email, DOB, creationDate, lastLogin
- follow table: userID1, userID2

### data size estimation
- assume each row of user table 4+20+32+4+4+4 = 68bytes
- 500M users => 500*68≈ 32GB
- assume each row of photo 4+4+256+4+4+4+4+4 = 284 bytes
- 10 years => 1.88 TB
- userFollow table, each row 8 bytes
- 500 million users each follow 500 users:
- 500 * 500 * 8 = 1.82 TB
- total space 32gb + 1.88tb + 1.82tb  = 3.7 tb


### split servers for read and write
- 500 connections for a server, then at max 500 threads to process uploads and reads


### reliability and redundancy
- multiple replicas of services in system to aviod single point failure
- run a redundant secondary copy of service, no on service, but will take control after fail


### data sharding
- partitioning based on userID
- 3.7TB for 1TB/shard=> at least 4 shards, but use 10 for better performance and scalability
- generate photoID=> auto-increment or UUID to make unique
- handle hot users, handle user with a lot of photos, handle one user to multiple shards, handle shard server down or latency
- partitioning based on photoID, will solve above issues
- gen photoID-> a separate db to store photoID, select its auto increament id for photo id
- this key-gen DB single point of failure?

### ranking and news feed generation
soket, pull, push, hybrid












