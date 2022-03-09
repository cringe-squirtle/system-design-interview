
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
      - also get award 
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
      - vote?
      - List of Post
      - pageToken: ?number
- comment
  - columns
    - commentID: string
    - creatorID: string
    - parentID: string
    - content: string
    - isDeleted: boolean
  - create - input userID, postID, content, parentID
    - return Comment
  - edit - similar to get post
  - get - similar to get post
  - delete - do soft delete since tree structure - similar to delete post
  - List - similar to get post
- vote
  - column 
    - voteID: string, 
    - createID: string
    - targetID: tring
    - type: enum (up/ down)
  - create
    - if already created: delete
    - else: create take Vote return Vote
  - edit
    - take voteID, userID, type
    - return Vote
  - delete
    - take voteID, userID
    - return Vote



