## REST API introduction
Exnow provides an API for users to quickly access to exnow's trading system and implement programmed transactions. 

|Address     |Applicable functions    |
| ------ | ------ |
| https://api.exnow.com/public/v1/markets | 获取交易对列表 |
| https://api.exnow.com/public/v1/ticker  | 获取单一市场实时行情 |
| https://api.exnow.com/public/v1/depth | 获取单市场深度  |
| https://api.exnow.com//public/v1/trades  | 获取历史成交 |
| https://api.exnow.com/public/v1/kline  | 获取K线蜡烛图 |
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
