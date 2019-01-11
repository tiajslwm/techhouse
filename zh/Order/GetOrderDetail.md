<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Order - GetOrderDetail

### 1.1 功能描述
>简介： 获取订单列表

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/order](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|GetOrderDetail
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y='
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
    orderno	|String	|Order number
    email	|String	|Contact email
    cardIssuePlace    |String	|Credential issued country, country 2_letter code e.g. JP
    routeType |Int    |数据来源信息，0:LF，1:tech house

### 1.3 请求结果
```json
{
"action": "GetOrderList",
  "key": "xxxxxxxxxxxxxxxx",
  "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "timestamp": "1547016648.42",
  "version": "2.0.3",
  "request": {
    "orderno": "lf123123",
    "email": "xxxx@qq.com",
    "cardIssuePlace": "",
    "routeType": 1
  }
}
```
### 1.4 返回参数
Field       |Type       |Description
:------------|:-----------|:-----------
status	|Number	|0 for success, others for failure, please refer to status error appendix for detail
fromcity    |String   |出发城市
currency    |String     |币种
orderStatus |String |订单状态: TICKETED:已出票,PENDING:等待出票，NEEDPAY:等待支付
tocity  |String |到达城市
orderNo |String |订单号,最大 100 个字符
orderDate   |Int |下单时间
paymentDate |Int    |支付时间
totalCost   |String |订单总价
sessionId   |String |sessionId，由AirPricing接口应答产生
paymentCode |String |支付代码
routing	|Object	
  fares	|Object	|Journey fares
    passengerId	|Number	|Passenger Id
    fare	|Float	|Journey fare
    tax	|Float	|Journey tax
    currency	|String	|Currency information, 3_letter code e.g. USD
  fromSegments	|Object[]	
    carrier	|String	|Carrier IATA 2_letter code, must same to flightNumber carrier code, e.g. CA
    flightNumber	|String	|light number, e.g. CA123 if flight number begin with 0, must waived, e.g. CZ006 is return by CZ6
    depAirport	|String	|Departure airport IATA 3_letter code
    depTime	|String	|Departure date and time format: YYYYMMDDHHMM e.g. 201203100315 2012/03/10 03:15
    arrAirport	|String	|Arrival airport IATA 3_letter code
    arrTime	|String	|Arrival date and time, format:YYYYMMDDHHMM e.g. 201203101305 means 2012/03/10 13:05
    stopCities	|String	|Stop over city，use / for separate. TYO/OSA
    cabin	|String	|Cabin information
    cabinClass	|String	|Cabin class information
    aircraftCode	|String	|Aircraft Code
    codeShare	|Boolean	|Code share, true is code share
  retSegments	|Object[]	
    carrier	|String	|Carrier IATA 2_letter code, must same to flightNumber carrier code, e.g. CA
    flightNumber	|String	|Flight number, e.g. CA123 if flight number begin with 0, must waived, e.g. CZ006 is return by CZ6
    depAirport	|String	|Departure airport IATA 3_letter code
    depTime	|String	|Departure date and time format: YYYYMMDDHHMM e.g. 201203100315 2012/03/10 03:15
    arrAirport	|String	|Arrival airport IATA 3_letter code
    arrTime	|String	|Arrival date and time, format:YYYYMMDDHHMM e.g. 201203101305 means 2012/03/10 13:05
    stopCities	|String	|Stop over city，use / for separate. TYO/OSA
    cabin	|String	|Cabin information
    aircraftCode	|String	|Aircraft Code
    codeShare	|Boolean	|Code share, true is code share
passengers	|Object[]	|Object for Passenger information
  passengerId	|Number	|passengerId
  lastName	|String	|LastName
  firstName	|String	|FirstName MiddleName
  ageType	|Number	|Passenger type, 0:adult 1:child -1:student
  birthday	|String	|Birthday, format: YYYYMMDD
  gender	|String	|Gender, M: male F: female
  cardNum	|String	|Credential Number, maximum 15 char, most case is passport number
  cardType	|String	|Credential Type, PP for passport
  cardExpired	|String	|Credential expired date, format: YYYYMMDD
  nationality	|String	|nationality, 2_letter country code
contact	|Object	|Object for contact
  firstName	|Number	|FirstName MiddleName
  lastName	|Number	|LastName
  address	|String	|Detail address
  postcode	|Number	|postcode
  email	|String	|email
  mobile	|String	|mobile information, format country number + mobile number e.g.: 81 123412341234
ssrs （optional）	|Object	|Object for SSR
  flightNumber	|String	|Flight number
  ssrcode	|String	|SSR Code
  count	|Number	|SSR number
  passengerId	|Object	|Passenger Id
  amount	|Float	|SSR Price
  currency	|String	|Currency information, 3_letter code e.g. USD
seats （optional）	|Object[]	
  flightNumber	|String	|Flight number
  designator	|String	|Seat identifier
  passengerId	|String	|Passenger Id
  amount	|Float	|seat selection Price
  currency	|String	|Currency information, 3_letter code e.g. USD
tickets （optional）	|Object[]	|Ticket number list, empty if the order is not in 'TICKETED' state.
  passengerId	|Number	|Passenger Id
  flightNumber	|String	|Flight number
  firstName	|String	|FirstName
  lastName	|String	|LastName
  ticketNo	|String	|Ticket Number
  createTime	|String	|Ticketing Time
### 1.5 返回结果
```json
{
  "status": 0,
  "fromcity": "CAN",
  "currency": "USD",
  "orderStatus": "TICKETED",
  "tocity": "BKK",
  "orderNo": "1283517458781",
  "paymentDate": 0,
  "orderDate": 1545792659,
  "totalCost": 132,  
  "sessionId": "c90cc9162ad7269334b5244459c81982",
  "paymentCode": "ALIPAY",
  "tickets": [
    {
      "firstName": "XU",
      "ticketNo": "123",
      "flightNumber": "SL901",
      "lastName": "JUNHYUNG",
      "passengerId": "0",
      "createTime": 1545764947
    }
  ],
  "ssrs": [],
  "seats": [],
  "passengers": [
    {
      "cardExpired": "20191219",
      "cardType": "PP",
      "birthday": "19800116",
      "nationality": "CN",
      "cardIssuePlace": "CN",
      "passengerId": "0",
      "firstName": "XU",
      "ageType": 0,
      "gender": "M",
      "cardNum": "DDDD123",
      "lastName": "JUNHYUNG"
    }
  ],
  "contact": {
    "mobile": "+86 15585589941",
    "address": "",
    "postcode": "",
    "name": "JUNHYUNG/XU",
    "email": "zzxuhalu@qq.com"
  },
  "routing": {
    "retSegments": [],
    "fares": [
      {
        "fare": 106.34,
        "tax": 25.66,
        "passengerId": "0",
        "currency": "USD"
      }
    ],
    "fromSegments": [
      {
        "arrAirport": "DMK",
        "cabinclass": "Y",
        "pack_code": "",
        "operatingFlightno": "",
        "duration": 185,
        "flightNumber": "SL901",
        "stopCities": "",
        "codeShare": "false",
        "carrier": "SL",
        "depAirport": "CAN",
        "stopAirports": "",
        "arrTime": "201812280455",
        "depTime": "201812280250",
        "aircraftCode": "739",
        "cabin": "M",
        "operatingCarrier": ""
      }
    ]
  }
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
### 1.7 错误状态码
```json
{"status": 1000, "msg": "ERROR MESSAGE" }
``` 
