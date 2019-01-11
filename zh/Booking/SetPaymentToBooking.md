<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Booking - SetPaymentToBooking

### 1.1 功能描述
>简介：对于每次预定流程， 都需要设置相应的支付方式。<br>
注意事项：此接口结果依赖于GetBookingPaymets的结果。

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/booking](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|SetPaymentToBooking
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y='
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
  sessionId	|String	|sessionId，由AirPricing接口应答产生
  routeType |Int    |数据来源信息，0:LF，1:tech house
  paymentCode |String    |支付代码
  payCurrency   | String  |支付币种

### 1.3 请求结果
```json
{
"action": "GetSeatAvailability",
  "key": "xxxxxxxxxxxxxxxx",
  "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "timestamp": "1547016648.42",
  "version": "2.0.3",
  "request": {
    "sessionId": "77935418d55fd48629be0643557121f4",
    "routeType": 1,
    "paymentCode": "AG",
    "payCurrency": "USD"
  }
}
```
### 1.4 返回参数
Field       |Type       |Description
:------------|:-----------|:-----------
status	|Number	|0,成功;其他,失败
msg	|String	|提示信息,长度小于 64
totalCost	|Float	|需要支付的金额
currency	|String	|货币类型三字码
       
### 1.5 返回结果
```json
 {
     "status": 0,
     "totalCost": 10826.4,
     "msg": "Success",
     "currency": "JPY"
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
2301	|支付方式不支持
### 1.7 错误状态码
```json
{"status": 1000, "msg": "ERROR MESSAGE" }
``` 
