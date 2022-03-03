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
  - use *blob store*, Google Cloud Service or AWS S3
  - CDN for static content, for serving faster, reduce response time
    - Google Cloud CDN
    - Cloudflare
    - 


