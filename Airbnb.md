
# Airbnb
- host + renter

### Requirement
- host - create + delete
- renter - browse + booking
- once user book a property, other user cannot see it for the booking period
- 15 mins lock under booking for user to checkout
- geo (lat longt) + date
- 50 M users
- 1 M listings
- 1 region

### servers
- network graph
  - hosts -> load balancer (round robin) -> servers -> db
  - renters -> load balancer (round robin) -> servers -> db

- store a table of reservations
  - have expiration
  - reserved 15 mins for user to checkout
  - if no checkout, expire
  - else reserved 
  - reserved property are not able to be seen by other users with the booking period

### storage
- quadtree - (over engineering 1M not big, e.g. google map with far more locations better to have quadtree)
  - for fast latency
  - for locations 
- listings - SQL
