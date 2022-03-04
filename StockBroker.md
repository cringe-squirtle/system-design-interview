
# Stock Broker

### Requirements
- support trading stocks, like robinhood
- no margin system
- market orders only, current price
- no tax generation, no listing orders, no deposit/withdraw, just place trade API call
- assume have SQL table for custome balances (to build)
- millions of customers, millions of trades perday
- region, US only
- high availability
- will interacting with exchange API, will take in a callback for reject/acceept

### step down
- API calls, inputs outpus, signatures
- how backend server be like
- handle execute trades

### API Call
- placeTrade
  - input (customerID, stockTicker, buySellType, quantity)
  - output - orderID, stockTick, buySellType, quantity, exchangeStatus(placed, etc), created_at(timestamp)

### Backend Server
- tables
  - trades
    - columns - ID, customerID, stockID, type, quantity, status, created_at, reason
    - index - customerID,
  - balance
    - columns - ID, customerID, amount, last_modified,
- servers
  - API calls - load balancer - servers - workers - exchange
  - no need caching
  - round-robin load balancing
  - servers
    - take calls and store trades to database
    - push customer, orders to wokers
  - workers
    - subscribe to server chanels
    - execute to exchange
    - response to servers
- request estimation
  - 4000 * 8 / 10000 ≈ 30 trades / second
  - 100 topics / second --> 100 clusters

### handle exchange callback
- sql / progress
  - select * from trades where customerID = chanelID and status in (placed or in_progress) order by created_at asc limit 1;
  - update placed to in_progress
  - make submit to exchange
  - callback 
    - if status is not in_progress: roll back
    - update status to filled / rejected
    - if not reject, update balance deduce quantity * stock price
    - update trade reason
    - get execute_at
    - notify pub/sub, so the pub/sub system will pick next trade
- periodically check if there's order not being exchanged
