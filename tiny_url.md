### wut tinyurl
[https://www.educative.io/courses/grokking-the-system-design-interview/m2ygV4E81AR](https://www.educative.io/courses/grokking-the-system-design-interview/m2ygV4E81AR)
->[https://tinyurl.com/rxcsyr3r](https://tinyurl.com/rxcsyr3r)

### requirements
1. generate a shorter and unique by given url
2. user will be redirected to original link
3. user be able to pick custom short link
4. links will expire, user be able to specify expiration time
5. system highly available
6. minimal latency
7. link non-guessable

### capacity estimation

#### speed estimates
1. 500M new url shortening /mon
2. -> 100:1 r/w 100*500M = 50B
3. speed 500m/(30*24*3600) ≈ 200 urls/s
4. 200*100 = 20k/s


#### storage estimates
1. assume 5 years, 500m new urls /month
2. total 5*500%12 = 30b
3. assume 500bytes each -> 30b*500bytes = 15TB.         

#### bandwidth estimates
1. 200 urls /s ->200*500bytes = 100kb/s
2. with r/w 100kb/s * 100 ≈ 10mb/s

#### memory estimates
1. 20k requests/s * 3600*24 = 1.7b /day
2. cashe 20%: 1.7b*500bytes*20% ≈ 170gb 	    `cache 20%`

### APIs
1. createURL(api_dev_key, original_url, custom_url = None, username=None, expire_date=None)
	return shortened url otherwise error
2. deleteURL(api_dev_key, url_key)
3. limit user abuse by api_dev_key

### Database Design
url table, user table

### algorithm to encode
unique hash MD5 or SHA256

base64, length of the characters -> 64^n possible strings

#### issues
1. same url=>same shortened non acceptable
2. parts of url are url-encoded

#### solve
1. appended increasing sequence number make it unique then generate
2. append userid

#### generating keys
1. gen then store in db
2. mark used when used to keep unique
3. memory estimates
4. multiple service single point failure(standby server)
5. each app server caches some keys from key-db


### data partition
1. range based partitioning, partition based on hash key's first letter
2. hash based partitioning, based on mapping hash to [1...256]

### cache
1. memory: 20%* of daily traffic, mordern day server 256gb, smaller servers for hot urls
2. eviction policy - least recently used

### security and permissions
1. user create private and allow some users to access
2. then create permission level 
3. separate table to store userIDs with permission to specific url



