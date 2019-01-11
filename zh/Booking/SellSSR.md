<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Booking - SellSSR

### 1.1 功能描述
>简介：面向特定航班，添加附加服务

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/booking](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|SellSSR
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y='
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
  sessionId	|String	|sessionId，由AirPricing接口应答产生
  routeType |Int    |数据来源信息，0:LF，1:tech house
  ssrs	|Object[]	
    flightNumber	|String	|航班号
    depAirport	|String	|始发机场三字码
    arrAirport	|String	|到达机场三字码
    depDate	|String	|起飞日期,格式为：YYYYMMDD
    cabin	|String	|舱位代码
    ssrcode	|String	|ssrcode
    count	|Number	|数量
    passengerId	|Object	|乘客ID，等同于SetPassengers设置的passengerId

### 1.3 请求结果
```json
{
  "action": "SellSSR",
  "key": "xxxxxxxxxxxxxxxx",
  "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "timestamp": "1547004532000",
  "request": {
   "sessionId": "dd0a785f24f4f70e9816969044df3605",
   "routeType": 1,
    "ssrs": [
      {
        "flightNumber": "FD3425",
        "depAirport": "DMK",
        "arrAirport": "CNX",
        "depDate": "20190210",
        "cabin": "O",
        "ssrcode": "PA15",
        "count": 1,
        "passengerId": 0
      }
    ]
  }
}
```
### 1.4 返回参数
Field       |Type       |Description
------------|-----------|-----------
status	|Number	|0,成功;其他,失败
msg	|String	|提示信息,长度小于 64
totalCost	|Number	|需要支付货币
currency	|String	|货币类型三字码
       
### 1.5 返回结果
```json
 {
     "status": 0, 
     "msg": "Success", 
     "sessionId": "d1a734123fb6d248d59429cc00b86dff", 
     "totalCost": 47.0, 
     "currency": "USD",
 }
```

### 1.6 状态码
状态码       |说明
:------------|:-----------
1000	|通用系统错误
1001	|Request请求缺少参数
1002	|无效的Action
1003	|超时请重试
1004	|Request请求参数错误
1005	|系统错误
1101	|加密校验失败，signature错误
1102	|商户已禁用，请联系账户管理员
2002	|Session中无有效行程
2003	|Session中无乘客
2009	|PassengerID不存在，通常SellSSR或AssignSeat之前需要调用SetPassenger
2102	|请求中的 Code 和GetSSRAvailibility 的不一致
### 1.7 错误状态码
```json
{"status": 1000, "msg": "ERROR MESSAGE" }
``` 
