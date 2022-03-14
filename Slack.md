# Slack

### Requirement
- core communication, 1-to-1, 1-to-group
- one organization - multi channels- users
- unread and menttions
- cross-device sync
- backend
- 20 millions users
- 50k per org
- 50k per channel

### steps
- persistent storage
- real time messaging

### storage
- messages
  - columns: - id, channelID, senderID, sent_at, body, mentions
- channel:
- read_receipts
  - columns: -id, orgID, channelID, userID, lastSeeTime
- channel_last_activity
  - columns: -id, orgID, channelID, lastMessageTime


### Server
- clients -> load balancer -> servers -> Database
- pub / sub
  - servers -> kv store smart sharding for fast fetch
  - servers -> kafka topics -> servers -> LB -> to clients
