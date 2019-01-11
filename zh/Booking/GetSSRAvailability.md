<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Booking - GetSSRAvailability

### 1.1 功能描述
>简介：面向特定航班，获取有效的附加服务详细信息

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/booking](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|GetSSRAvailability
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y='
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
  sessionId	|String	|sessionId，由AirPricing接口应答产生
  routeType |Int    |数据来源信息，0:LF，1:tech house
  segments	|Object[]   |segments列表
      flightNumber	|String	|航班号
      depAirport	|String	|始发机场三字码
      arrAirport	|String	|到达机场三字码
      depDate	|String	|起飞日期,格式为：YYYYMMDD
      cabin	|String	|舱位代码

### 1.3 请求结果
```json
{
    "action": "GetSSRAvailability",
    "key": "xxxxxxxxxxxxxxxx",
    "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "timestamp": "1508143359.32",
    "version": "2.0.3",
    "request": {
        "sessionId": "dd0a785f24f4f70e9816969044df3605",
        "routeType": 1,
        "segments": [
            {
                "arrAirport": "KUL",
                "flightNumber": "D7317",
                "depAirport": "PEK",
                "depDate": "20171021",
                "cabin": "B"
            },
            {
                "arrAirport": "PEK",
                "flightNumber": "D7318",
                "depAirport": "KUL",
                "depDate": "20171027",
                "cabin": "W"
            }
        ]
    }
}
```
### 1.4 返回参数
Field       |Type       |Description
------------|-----------|-----------
status	|Number	|0:成功; 其他,失败
msg	|String	|提示信息,长度小于64
ssrs	|Object[]	|ssr列表
  flightno	|Number	|The flight number of the request segment
  ssrs	|Object[]	|SSR List for every segment
    applyType	|Number	|0: ALL, 1, PRE_BOOKING, 2: POST_BOOKING
    code	|String	|ssrcode唯一标示
    type	|String	|辅营的二字吗
    typeweight 	|Int	|辅营数量，如type等于行李的时候20，餐食的时候2
    desc	|String	|SSR 描述
    amount	|Number	|SSR 价格
    currency	|String	|币种，如USD
    unit 	|String	|辅营，如type等于行李的时候KG，LB，餐食的时候3，4
    img （optional）	|String	|图片url
       
### 1.5 返回结果
```json

{
    "status": 0,
    "msg": "Success",
    "ssrs": [
        {
            "ssrs": [
                {
                    "currency": "CNY",
                    "amount": 200,
                    "code": "PA20",
                    "name": "20",
                    "weight": 20,
                    "type": "XX",
                    "applyType": 1,
                    "unit": "KG",
                    "desc": ""
                },
                {
                    "currency": "CNY",
                    "amount": 200,
                    "code": "PB20",
                    "name": "宫保鸡丁",
                    "weight": 20,
                    "type": "DD",
                    "applyType": 2,
                    "unit": "1",
                    "desc": ""
                }
            ],
            "flightno": "AK216"
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
2101	|无可用SSR数据
### 1.7 错误状态码
```json
{"status": 1000, "msg": "ERROR MESSAGE" }
``` 
