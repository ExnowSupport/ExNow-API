## REST API 简介
exnow为用户提供了一套API，可以帮用户快速接入exnow的交易系统，实现程序化交易。

|访问地址	|适用功能	|
| ------ | ------ |
| https://api.exnow.com/public/v1/markets | 获取交易对列表 |
| https://api.exnow.com/public/v1/ticker  | 获取单一市场实时行情 |
| https://api.exnow.com/public/v1/depth | 获取单市场深度  |
| https://api.exnow.com//public/v1/trades  | 获取历史成交 |
| https://api.exnow.com/public/v1/kline  | 获取K线蜡烛图 |
| https://api.exnow.com/private/v1/balance | 获取账户资产信息 |
| https://api.exnow.com/private/v1/limitOrder | 下单 |
| https://api.exnow.com/private/v1/cancelOrder | 撤单 |
| https://api.exnow.com/private/v1/entrusts | 获取当前委单和历史委单信息 |
| https://api.exnow.com/private/v1/deals | 获取成交记录信息 |
| https://api.exnow.com/private/v1/orderDetails | 通过订单id获取订单详细信息 |
| https://api.exnow.com/private/v1/orderDeals | 通过订单id获取成交信息 |



通过API可以实现以下功能：

市场行情信息查询（K线、深度、实时成交、24小时行情）
账户资产信息查询
下单、撤单操作
订单信息查询 所有请求基于 HTTPS 协议。
