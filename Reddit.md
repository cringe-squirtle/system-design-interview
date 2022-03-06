
# Reddit

### Requirement
- given
  - User | userID: string,...
  - Subreddit | subredditID: string

- write posts, commenting, upvote, downvote


### Step
- define entity
- define API methods/endpoints

### Entities / API
- post
  - columns
    - postID:string, 
    - userID:string, 
    - createdTime:number, 
    - subredditID:string, 
    - title: string
    - description: string
    - votesCount: number 
  - create
    - input (Post)
      - userID:string, ACL
      - subredditID:string, 
      - title: string
      - description: string
    - output
      - Post
  - get
    - input - postID, userID(ACL)
    - output - Post
  - Edit
    - input 
      - postID, 
      - userID(ACL)
      - title: string
      - description: string
    - output - Post
  - Delete
    - input
      - postID, 
      - userID(ACL)
    - output - void / Post
  - List - search
    - input
      - userID: string
      - subredditID: string
      - pageSize?: ?number
      - pageStart?: ?number
    - output 
      - List<Post>
      - pageToken: ?number
- comment
  - columns
    - commentID: string
    - creatorID: string
    - parentID: string
    - content: string
    - voteID: number
    - isDeleted: boolean
  - create
  
  
  
