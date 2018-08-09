# REST API    

## Start to use   

Representational State Transfer (REST) is an architectural style that defines a set of constraints to be used for creating web services. 
It is clearly structured, standards-compliant, easy to understand and easy to extend, and is being adopted by more and more websites.The advantages are as follows:
- in RESTful architecture, each URL represents a resource;
- some presentation layer passing this resource between the client and the server;
-  the client operates on the server side resources through four HTTP instructions to achieve "performance level state transformation".

Developers are suggested to use REST API for currency transactions or asset views.

## Request interaction    

The roots of REST access URL：`https://api.exnow.com/` 

All requests are based on the Https protocol, and the contentType in the request header should be set to: `application/json`   

Request interaction description
1. Request parameters: encapsulate parameters according to the interface request parameters.
2. Submit request parameters: the encapsulated request parameters are submitted to the server through POST or GET.
3. Server response: the server firstly verifies the parameter safety of the user request data, and then returns the response data to the user in JSON format according to the business logic after verification.
4. Data processing: processing server response data.

## API reference  

### Market api

Obtain ExNow market data


#### GET  public/v1/markets    Obtain ExNow trading pair list

URL `https://api.exnow.com/public/v1/markets`    

The sample

```
# Request
GET https://api.exnow.com/public/v1/markets
# Response
{
"success": true,
"data": [
"xrp_btc",
"mdt_eth",
"eth_btc",
"sky_btc",
"xrp_cnc",
"dash_btc",
"btc_cnc",
"sc_btc",
"dash_cnc",
"eth_cnc",
"fgc_eth"
]
}
```

Return value description    

```
data:Trading pair
```


#### GET public/v1/ticker   Obtain ExNow single market real-time quotes

URL `https://api.exnow.com/public/v1/ticker`    

The sample    

```
# Request
GET https://api.exnow.com/public/v1/ticker?market=eth_btc
# Response
{
"success": true,
"data": {
"volume": "24.3134",
"high": "0.000061",
"deal": "1.8160819157",
"last": "0.000061",
"low": "0.000061",
"open": "0.000061"
}
}
```

Return value description    

```
volume :volume 
high :high
deal：turnover
last：last
low:low
open:open
```

Request parameters    

|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|market|String|YES|eth_btc|

#### Get /public/v1/depth  Obtain ExNow single market depth

URL `https://api.exnow.com/public/v1/depth`    

The sample

```
# Request
GET https://api.exnow.com/public/v1/depth?market=eth_btc
# Response
{
"success": true,
"data": {
"stock_amount": "1998.0000",
"money_amount": "0e-10",
"asks": [
[
"0.000061",
"1998",
"0.121878"
]
],
"bids": []
}
}
```

Return value description    

```
stock_amount：Stock amount
money_amount：Money amount
asks：asks
bids：bids
```

Request parameters

|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|market|String|YES|eth_btc|


#### Get /public/v1/trades    Obtain ExNow order history

URL `https://api.exnow.com/public/v1/trades`    

The sample    

```
# Request
GET https://api.exnow.com/public/v1/trades?market=eth_btc&limit=2
# Response
{
"success": true,
"data": [
{
"amount": "2",
"price": "0.000061",
"id": 68779,
"time": 1533613048.9352081,
"type": "buy"
},
{
"amount": "10",
"price": "0.000061",
"id": 68778,
"time": 1533613048.93503,
"type": "buy"
} 
]
}
```

Return value description    

```
amount：Amount
price：Price
"time"：Time
"type":Business direction
```

Request parameters    

|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|market|String|YES|eth_btc|
|limit|int|否|获取条数（1-100之间）|

#### Get /public/v1/kline   Obtain ExNow K line candle stick chart

URL `https://api.exnow.com/public/v1/kline`    

The sample    

```
# Request
GET https://api.exnow.com/public/v1/kline?market=eth_btc&period=86400&since=0&size=100
# Response
{
"success": true,
"data": [
[
1529942400,  //The time stamp
"0.072401",  //open
"0.072427",  //high
"0.07185",  //low
"0.071967",  //close
"30.5411",  //volume
"2.2047955076"  //deal
],
[
1530028800,
"0.072309",
"0.072392",
"0.070601",
"0.07153",
"145.0783",
"10.3330219245"
],
]
}
```

Request parameters    
```
market:Trading pair
period：Period
since: Since
size: Size
```



### Contract transaction API

Used for exnow to quickly trade and query assets

####1. POST /v1/balance     Gets the exnow account asset information

URL `https://api.exnow.com/private/v1/balance` 

The sample    

```
# Request
POST https://api.exnow.com/private/v1/balance
# Response
"data": [
{
"available_fund": 9999901.46,
"coin_alias_code": "btc",
"coin_code": "btc",
"coin_en_name": "bitcoin",
"coin_logo": "",
"frozen_fund": 31,
"open_type": 1,
"show_decimal": 8,
"total_fund": 9999932.46
}],
"success": true
}
```

Return value description    

```
available_fund:Available fund
coin_alias_code：Coin alias code
coin_code：Coin code
coin_en_name：Coin English name
coin_logo：Logo
frozen_fund：Frozen fund
total_fund：Total fund

```

Request parameters    
```
{
"key":"5f57****12e39",
"time":"***",
"signature":"f369d****c3267"
}
```


|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|key|String|YES|ApiKey requested by the user|
|signature|String|YES|The signature of the request parameter is in the order md5(key_ user ID_skey_time)|
|time|String|YES|The time stamp|

####2. POST /v1/limitOrder     Place order  

URL `https://api.exnow.com/private/v1/limitOrder`

The sample    

```
# Request
POST https://api.exnow.com/private/v1/limitOrder
# Response
{
"data": true,
"success": true
}
```

Return value description    

```
date:true:  Data true
success: Success
```

Request parameters    
```
{
"key":"33fc0af****4d06465309ac0f4",
"time":"111",
"signature":"f5adcf4***b858532af62f2c0a8b",
"market":"eth_btc",
"side":"1",
"price":"6100",
"amount":"1"
}
```
|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|key|String|YES|ApiKey requested by the user|
|signature|String|YES|The signature of the request parameter is in the order md5(key_ user ID_skey_time)|
|time|String|YES|The time stamp|
|market|String|YES|Trading pair|
|side|String|YES|Direction 1: sell 2: buy|
|price|String|YES|Price|
|amount|String|YES|Trading quantity|


####3. PUT /v1/cancelOrder     Cancel order

URL `https://api.exnow.com/private/v1/cancelOrder`       

The sample    

```
# Request
POST https://api.exnow.com/private/v1/cancelOrder
# Response
{
"code": 200,
"result": "success"
}
```

Return value description    

```
code ：200
result ： Successful return
```

Request parameters    
```
{
"key":"33fc0af0a2135eb304d06465309ac0f4",
"time":"111",
"signature":"f5adcf4f8d3376b858532af62f2c0a8b",
"market":"eth_btc",
"userOrderId":"1531732308654004"
}
```

|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|key|String|YES|ApiKey requested by the user|
|signature|String|YES|The signature of the request parameter is in the order md5(key_ user ID_skey_time)|
|time|String|YES|The time stamp|
|market|String|YES|Trading pair|
|userOrderId|String|YES| Order id|

####4. POST /v1/entrusts    Get the user's current order (order history)

URL `https://api.exnow.com/private/v1/entrusts`  

The sample    

```
# Request
POST https://api.exnow.com/private/v1/entrusts
# Response
{
"data": [
{
"amount": 10,
"create_time": 1528966171000,
"deal_fee": 0,
"deal_money": 0,
"deal_stock": 0,
"maker_fee": 0.001,
"market": "btc_usdt",
"price": 1,
"side": 1,
"t": 1,
"taker_fee": 0.001,
"update_time": 1528966171000,
"user_id": 10004,
"user_order_id": "1528966171588504"
}
],
"page": {
"first_item_index": 0,
"page": 1,
"page_count": 1,
"page_size": 20,
"total": 1
},
"success": true
}
```

Return value description    

```
amount：Trading amount 
create_time：Trading time(ms)
price：Trading price
user_order_id：User order ID
side：Direction of sale (1: sell /2: buy)
deal_fee：Transaction fee
deal_money：deal money
deal_stock:deal stock
market: market trading pair
t：1: Limit 2: Market
```

Request parameters    
```
{
"key":"33fc0af0a2135eb304d06465309ac0f4",
"time":"111",
"signature":"f5adcf4f8d3376b858532af62f2c0a8b"，
"state":"1"}
```

|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|key|String|YES|ApiKey requested by the user|
|signature|String|YES|The signature of the request parameter is in the order md5(key_ user ID_skey_time)|
|time|String|YES|The time stamp|
|state|String|YES|1. Current order 2: order history|


####5. POST /v1/deals     Obtain successful transaction orders

URL `https://api.exnow.com/private/v1/deals`    

The sample    

```
# Request
POST https://api.exnow.com/v1/deals
# Response
{
"data": [
{
"amount": 1，
"deal": 0.73,
"deal_id": 421861,
"fee": 0.001,
"id": 1101,
"market": "eth_btc",
"oper_id": 1558913,
"order_id": 987486,
"price": 0.73,
"rival": 1,
"rival_fee": 0.00073,
"role": 2,
"side": 2,
"time": 1531733645000,
"user_id": 10004
}],
"page": {
"first_item_index": 0,
"page": 1,
"page_count": 55,
"page_size": 20,
"total": 1085
},
"success": true
}
```

Return value description    

```
result: Order transaction success or failure
amount：Amount 

```

Request parameters    
```
{
"key":"33fc0af0a2135eb304d06465309ac0f4",
"time":"111",
"signature":"f5adcf4f8d3376b858532af62f2c0a8b"
}
```

|Parameter names|    The parameter types|    Must fill in|    Description|
| :-----    | :-----   | :-----    | :-----   |
|key|String|YES|ApiKey requested by the user|
|signature|String|YES|The signature of the request parameter is in the order md5(key_ user ID_skey_time)|
|time|String|YES|The time stamp|


