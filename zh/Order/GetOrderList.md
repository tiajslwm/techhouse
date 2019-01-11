<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Order - GetOrderList

### 1.1 功能描述
>简介： 获取订单列表

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/order](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|Commit
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y='
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
    startTime	|String	|起始时间,格式为 '2017-07-01T00:00:00+08:00'
    endTime	|String	|终止日期,格式为 '2017-07-01T00:00:00+08:00'
    routeType |Int    |数据来源信息，0:LF，1:tech house
    orderStatus （optional）	|String	|订单状态: TICKETED:已出票,PENDING:等待出票，NEED_PAYMENT:等待支付

### 1.3 请求结果
```json
{
"action": "GetOrderList",
  "key": "xxxxxxxxxxxxxxxx",
  "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "timestamp": "1547016648.42",
  "version": "2.0.3",
  "request": {
    "startTime": "2017-07-01T00:00:00+08:00",
    "endTime": "2017-07-01T00:00:00+08:00",
    "routeType": 1,
    "orderStatus": "TICKETED"
  }
}
```
### 1.4 返回参数
Field       |Type       |Description
:------------|:-----------|:-----------
status	|Number	|0,成功;其他,失败
msg	|String	|提示信息,长度小于 64
bookingList	|Object[]	|订单列表
  orderNo	|String	|订单号
  orderStatus	|String	|订单状态
  createTime	|String	|订单创建时间
       
### 1.5 返回结果
```json
{
    "status": 0,
    "msg": "success",
    "bookingList": [
      {
        "orderNo": "lf123123123",
        "orderStatus": "TICKETED",
        "createTime": "1547016648.42"
      }
    ]
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
2005	|GetOrderList请求格式错误：日期格式错误
2006	|GetOrderList请求格式错误：未知的订单状态
### 1.7 错误状态码
```json
{"status": 1000, "msg": "ERROR MESSAGE" }
``` 
