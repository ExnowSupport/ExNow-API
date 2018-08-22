# REST API    

## 开始使用    

REST，即Representational State Transfer的缩写，是目前最流行的一种互联网软件架构。它结构清晰、符合标准、易于理解、扩展方便，正得到越来越多网站的采用。其优点如下：    
- 在RESTful架构中，每一个URL代表一种资源；    
- 客户端和服务器之间，传递这种资源的某种表现层；    
- 客户端通过四个HTTP指令，对服务器端资源进行操作，实现“表现层状态转化”。   

建议开发者使用REST API进行币币交易或者资产查看等操作。    
    
## 请求交互    

REST访问的根URL：`https://api.exnow.com/` 

所有请求基于Https协议，请求头信息中contentType需要统一设置为：`application/json`   
	
请求交互说明    
1. 请求参数：根据接口请求参数规定进行参数封装。    
2. 提交请求参数：将封装好的请求参数通过POST 或GET 方式提交至服务器。    
3. 服务器响应：服务器首先对用户请求数据进行参数安全校验，通过校验后根据业务逻辑将响应数据以JSON格式返回给用户。    
4. 数据处理：对服务器响应数据进行处理。 

## API参考  

### 行情 API 

获取Exnow行情数据  

#### GET  public/v1/markets    获取Exnow交易对列表

URL `https://api.exnow.com/public/v1/markets`	

示例	

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

返回值说明	

```
data:交易对
```


#### GET public/v1/ticker   获取Exnow单一市场实时行情

URL `https://api.exnow.com/public/v1/ticker`	

示例	

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

返回值说明	

```
volume :成交量
high :高
deal：成交额
last：收
low:低
open:开
```

请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|market|String|是|eth_btc|

#### Get /public/v1/depth  获取Exnow单市场深度

URL `https://api.exnow.com/public/v1/depth`	

示例	

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

返回值说明	

```
stock_amount：卖出总量
money_amount：买入总额
asks：卖单
bids：买单
```

请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|market|String|是|eth_btc|


#### Get /public/v1/trades   获取Exnow历史成交

URL `https://api.exnow.com/public/v1/trades`	

示例	

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

返回值说明	

```
amount：数量
price：价格
"time"：时间
"type":买卖方向
```

请求参数	

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|market|String|是|eth_btc|
|limit|int|否|获取条数（1-100之间）|

#### Get /public/v1/kline   获取Exnow K线蜡烛图

URL `https://api.exnow.com/public/v1/kline`	

示例	

```
# Request
GET https://api.exnow.com/public/v1/kline?market=eth_btc&period=86400&since=0&size=100
# Response
{
    "success": true,
    "data": [
        [
            1529942400,  //时间戳
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

请求参数	
```
market:交易对
period：区间
since:开始位置
size:条数
```



### 交易 API 

用于exnow快速进行交易、查询资产

####1. POST /v1/balance  获取exnow账户资产信息

URL `https://api.exnow.com/private/v1/balance` 

示例	

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

返回值说明	

```
available_fund:可用资金
coin_alias_code：币种别名
coin_code：币种code
coin_en_name：英文名
coin_logo：logo
frozen_fund：冻结资金
total_fund：资金总额

```

请求参数	
```
{
	"key":"5f57****12e39",
	"time":"***",
	"signature":"f369d****c3267"
}
```


|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|

####2. POST /v1/limitOrder   下单

URL `https://api.exnow.com/private/v1/limitOrder`

示例	

```
# Request
POST https://api.exnow.com/private/v1/limitOrder
# Response
{
    "data": true,
    "success": true
}
```

返回值说明	

```
date:true:成功
success:成功
```

请求参数	
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
|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|
|market|String|是|交易对|
|side|String|是|买卖方向 1：卖 2：买|
|price|String|是|价格|
|amount|String|是|买卖数量|


####3. PUT /v1/cancelOrder

URL `https://api.exnow.com/private/v1/cancelOrder`   	

示例	

```
# Request
POST https://api.exnow.com/private/v1/cancelOrder
# Response
{
    "code": 200,
    "result": "success"
}
```

返回值说明	

```
code ：200
result ： true代表成功返回
```

请求参数	
```
{
	"key":"33fc0af0a2135eb304d06465309ac0f4",
	"time":"111",
	"signature":"f5adcf4f8d3376b858532af62f2c0a8b",
	"market":"eth_btc",
	"user_order_id":"1531732308654004"
}
```

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|
|market|String|是|交易对|
|user_order_id|String|是| 订单id|

####4. POST /v1/entrusts    获取用户当前委单（历史委单）

URL `https://api.exnow.com/private/v1/entrusts`  

示例	

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

返回值说明	

```
amount：交易数量
create_time：交易时间(毫秒)
price：交易价格
user_order_id：交易ID
side：买卖方向（1：卖/2：买）
deal_fee：deal手续费
deal_money：成交额
deal_stock:成交量
market:交易对
t：1：限价 2：市价
```

请求参数	
```
{
	"key":"33fc0af0a2135eb304d06465309ac0f4",
	"time":"111",
	"signature":"f5adcf4f8d3376b858532af62f2c0a8b"，
	"state":"1"}
```

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|
|state|String|是|1：当前委单 2：历史委单|
|page|int|否|第几页（不填则为第一页）|


####5. POST /v1/deals

URL `https://api.exnow.com/private/v1/deals`  获取成交订单

示例	

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

返回值说明	

```
result:订单交易成功或失败
amount：数量

```

请求参数	
```
{
	"key":"33fc0af0a2135eb304d06465309ac0f4",
	"time":"111",
	"signature":"f5adcf4f8d3376b858532af62f2c0a8b"
}
```

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|
|page|int|否|第几页（不填则为第一页）|


####6. POST /v1/orderDetails

URL `https://api.exnow.com/private/v1/orderDetails`  通过订单id获取订单详情

示例	

```
# Request
POST https://api.exnow.com/v1/orderDetails
# Response
{
    "success": true,
    "data": {
        "id": 92,
        "create_time": 1531733645000,
        "update_time": 1531733645000,
        "market": "btc_usdt",
        "user_order_id": "1526522097165604",
        "state": 4,
        "userId": 10004,
        "t": 1,
        "side": 2,
        "price": "2",
        "amount": "2",
        "deal_stock": "2",
        "deal_money": "4",
        "deal_fee": "0.6"
    }
}
```

返回值说明	

```
create_time:订单创建时间
update_time: 订单更新时间,
market: 交易对,
user_order_id: 订单id,
state: 状态,
userId: 用户id,
t: 1限价,
side: 买卖方向 2卖,
price: 价格,
amount: 数量,
deal_stock: 成交数量,
deal_money: 成交总额,
deal_fee: 成交费用
```

请求参数	
```
{
	"key":"33fc0af0a2135eb304d06465309ac0f4",
	"time":"111",
	"signature":"f5adcf4f8d3376b858532af62f2c0a8b"，
	"user_order_id":"1526522097165604"
}
```

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|
|user_order_id|String|是|订单id|


####7. POST /v1/orderDeals

URL `https://api.exnow.com/private/v1/orderDeals`  通过订单id获取成交信息

示例	

```
# Request
POST https://api.exnow.com/v1/orderDeals
# Response
{
    "success": true,
    "data": [
        {
            "time": 1531733645000,
            "userId": 10004,
            "dealId": 29,
            "market": "scec_eth",
            "orderId": 38,
            "side": 1,
            "price": "0.0001",
            "amount": "1000",
            "deal": "0.1",
            "fee": "0.0001"
        }
           ]
 }
```

返回值说明	

```
time:成交时间
userId: 用户id,
market: 交易对
side: 买卖方向 2卖,
price: 价格,
amount: 数量,
deal: 总额,
fee: 手续费
```

请求参数	
```
{
	"key":"33fc0af0a2135eb304d06465309ac0f4",
	"time":"111",
	"signature":"f5adcf4f8d3376b858532af62f2c0a8b"，
	"user_order_id":"1526522097165604"
}
```

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|
|user_order_id|String|是|订单id|


