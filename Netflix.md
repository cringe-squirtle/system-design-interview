# Netflix

### requirments
- primary user flow
- aggregate user activity
- recommendation system
- global, highly available
- 200 million user
- data: 
  - video 
  - user metadata
  - static content - name, description, cast, poster
  - logs


# data
- video
  - 10 k videos
  - resolution SD-10GB/h  HD-20GB/h
  - 1h average
  - 10k * 30 -> 300TB
- user
  - 100 bytes per user metadata
  - 100b * 1000(lifetime per user) = 100KB
  - 100KB * 200M = 20 TB

# Network flow
- bandwidth consumption
  - 10 M users at peek
  - 20 GB/h -> 20GB / 4000s -> 5MB/s
  - 5 MB/s per user * 10M -> **50TB/s**
- users -> servers-> CDN -> storage
- to have caching between CDN and storage
- netflex actual solution: have a layer in internet service provider to do CDN, cahcing
- user metadata
  - user-> load balancer-> servers with caching


# Storage
- use S3 or GCS for static content
- CDN, cloud flare,

# recommendation engine
- HDFS hadoop file system
- user -> HDFS
- mapReduce aggregate
- columns
  - userID
  - event
  - videoID
  - region, time, ..

