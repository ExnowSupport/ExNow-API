## REST API introduction
Exnow provides an API for users to quickly access to exnow's trading system and implement programmed transactions. 

|Address     |Applicable functions    |
| ------ | ------ |
| https://api.exnow.com/public/v1/markets | Obtain ExNow trading pair list |
| https://api.exnow.com/public/v1/ticker  | Obtain ExNow single market real-time quotes |
| https://api.exnow.com/public/v1/depth | Obtain ExNow single market depth  |
| https://api.exnow.com//public/v1/trades  | Obtain ExNow order history |
| https://api.exnow.com/public/v1/kline  | Obtain ExNow K line candle stick chart |
| https://api.exnow.com/private/v1/balance | Obtain account asset information |
| https://api.exnow.com/private/v1/limitOrder | Place order |
| https://api.exnow.com/private/v1/cancelOrder | Cancel order |
| https://api.exnow.com/private/v1/entrusts | Obtain information about current and historical orders |
| https://api.exnow.com/private/v1/deals | Obtain transaction record information |



The following functions can be implemented through api：
Market information searching (K line, depth, real-time transaction, 24-hour market)
Account asset information searching
Place order and cancel order
Order history
All requests are base on the HTTPS protocol.
