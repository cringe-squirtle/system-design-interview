# AlgoExpert

### Requirements
- core user flow
  - questions list
  - mark question completed
  - write code
  - run code
- 2-3 9s availability
- 1-3s latency for runing code
- supports 10k of users any tiem
- region - globally, primary focus US and India


### Flow
- home page, completion of purchase
- have database/API for user, questions

### Dividing work into 4
1. static UI content
2. Auth, payments (skip)
3. core user action, seeing questions/solutions, writing code
4. running code

### UI Static Content
- images in website
  - use **blob store**, Google Cloud Service or AWS S3
  - CDN for static content, for serving faster, reduce response time
    - Google Cloud CDN
    - Cloudflare

### Load Balance
- path based load balancing
- ACL api call for checking if user has access to AlgoExpert

### Data Base
- blob store
  - static question list
  - ACL check
  - do caching, because questions are accessed by user a lot of times
    - client side caching question list - client better experience - no latency
    - server side caching question list
      - 100 questions upperbound
      - 7 solutions/ languages - round to 10
      - 5000 bytes per language
      - 5k*10*100 ≈ 5MB reasonable in caching
      - 30 minutes eviction policy
- user created content
  - *Notes: index column increase the speed of searching in query* 
  - question status
    - columns: ID, user_ID(index), question_ID, completion_Status(enum) 
  - solutions
    - columns: ID, user_ID(index), question_ID(index), language, solution


### Requests
- debounce on UI to not issue request frequently, at least 2-5 seconds
- have multiple databases depending on regions 
  - to have asynchronous replication (every 6 hours) - in case user from US fly to India 
- to have a server for running code
  - 1st layer for rate limiting
    - to have rate limiting - might have request abuse
    - be able to run code every 3 seconds for good experience, 5 times every minute
    - implementing by key-value radius
  - 2nd layer for running code
    - not sending request to runing worker
    - javascript python>c++ java since no compile time
    - estimation 10 request per user per hour -->>> 10-100 workers depending on traffic

### Bonus
- loggings & monitoring
  - how many users
  - languages
