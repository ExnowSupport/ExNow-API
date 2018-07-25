# REST API    

## 开始使用    

REST，即Representational State Transfer的缩写，是目前最流行的一种互联网软件架构。它结构清晰、符合标准、易于理解、扩展方便，正得到越来越多网站的采用。其优点如下：    
- 在RESTful架构中，每一个URL代表一种资源；    
- 客户端和服务器之间，传递这种资源的某种表现层；    
- 客户端通过四个HTTP指令，对服务器端资源进行操作，实现“表现层状态转化”。   

建议开发者使用REST API进行币币交易或者资产查看等操作。    
    
## 请求交互    

REST访问的根URL：`https://api.exnow.com/v1` 

所有请求基于Https协议，请求头信息中contentType需要统一设置为：`application/x-www-form-urlencoded`   
	
请求交互说明    
1. 请求参数：根据接口请求参数规定进行参数封装。    
2. 提交请求参数：将封装好的请求参数通过POST 或GET 方式提交至服务器。    
3. 服务器响应：服务器首先对用户请求数据进行参数安全校验，通过校验后根据业务逻辑将响应数据以JSON格式返回给用户。    
4. 数据处理：对服务器响应数据进行处理。 

## API参考  

### 合约交易 API 

用于exnow快速进行交易、查询资产

####1. POST /v1/balance  获取exnow账户资产信息

URL `https://api.exnow.com/v1/balance` 

示例	

```
# Request
POST https://api.exnow.com/v1/balance
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

URL `https://api.exnow.com/v1/limitOrder`

示例	

```
# Request
POST https://api.exnow.com/v1/limitOrder
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

URL `https://api.exnow.com/v1/cancelOrder`   	

示例	

```
# Request
POST https://api.exnow.com/v1/cancelOrder
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

####4. POST /v1/entrusts    获取用户当前委单

URL `https://api.exnow.com/v1/entrusts`  

示例	

```
# Request
POST https://api.exnow.com/v1/entrusts
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
	"signature":"f5adcf4f8d3376b858532af62f2c0a8b"
}
```

|参数名|	参数类型|	必填|	描述|
| :-----    | :-----   | :-----    | :-----   |
|key|String|是|用户申请的apiKey|
|signature|String|是|请求参数的签名 使用md5(key_用戶ID_skey_time)顺序不可改变|
|time|String|是|时间戳|


####5. POST /v1/deals

URL `https://api.exnow.com/v1/deals`  获取成交订单

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
