<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Booking - LowFareSearch

### 1.1 功能描述
>简介：通过LowFareSearch接口，可以根据相关搜索参数获取搜索结果。
注意事项：默认最大返回时间10秒，可以在1秒～60秒之间按需求定制最大返回时限，根据最大返回时限，控制有限时间内可返回的结果数量。

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/booking](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|LowFareSearch
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y=' 加密测试地址：http://encode-decode.com/aes-256-cbc-encrypt-online/
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
    tripType	|String	|行程类型1:单程2:往返;
    fromCity	|String	|出发地 IATA 三字码代码
    toCity	|String	|目的地城市 、到达城市 IATA 三字码代码
    fromDate	|String	|去程,格式为 YYYYMMDD
    retDate	|String	|回程日期,格式为 YYYYMMDD(单程为空)
    currency |String |请求币种，如USD
    adultNumber（optional）	|String	|成人人数，小于9
    childNumber（optional）	|String	|儿童人数，小于9
    timeout（optional）	|Int	|接口访问的超时时间，单位：秒
    sync（optional）	|int	|如果选用“异步搜索”设置为0; 否则设置为1或不用传此参数
    searchId（optional）	|int	|如果选用“异步搜索”设置, 第二次及以后的异步搜索请求都需要传此参数，参数值为第一次请求返回结果中的searchId
### 1.3 请求结果
```json
{
    "action": "LowFareSearch",
    "key": "xxxxxxxxxxxxxxxx",
    "timestamp": "1466134420.74",
    "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "version": "2.0.3",
    "request": {
        "tripType": "1",
        "fromCity": "BKK",
        "toCity": "CNX",
        "fromDate": "20130729",
        "retDate": "",
    }
}
```
### 1.4 返回参数
Field       |Type       |Description
------------|-----------|-----------
status	|Number	|0为成
msg	|String	|提示信息,长度小于 64
searchId	|String	|searchId
carriers	|Object[]	|航司返回结果信息
  statuscode	|int	|状态码，大于等于0为成功(0为当天无航班，大于0为航班数)，小于0为失败
  carriercode	|String	|航司代码
routings	|Object[]	|行程及报价信息
  adultFare	|Float	|成人单价
  adultTax	|Float	|成人税费
  childFare	|Float	|儿童单价
  childTax	|Float	|儿童税费
  currency	|String	|货币类型三字码
  data	|String	|会话信息，长度小于1000bytes。需要在调用AirPricing时传给Letsfly
  routeType |Int    |数据来源信息，0:LF，1:tech house
  fromSegments	|Object[]	|去程航段
    carrier	|String	|航司 IATA 二字码,必须与 flightNumber 航司相同
    flightNumber	|String	|航班号,如:CA123。航班号数字前若有多余的数字 0, 必须去掉,如 CZ006 需返回 CZ6
    depAirport	|String	|出发机场 IATA 三字码
    depTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203100300 表示 2012 年 3 月 10 日 3 时 0 分
    arrAirport	|String	|到达机场 IATA 三字码
    arrTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203101305 表示 2012 年 3 月 10 日 13 时 5 分
    stopCities	|String	|经停地，使用’/’分隔城市三字码
    codeShare	|Boolean	|代码共享标识(true 代码共享/false 非代码共享)
    duration	|int	|出发地至到达地飞行时长，单位为分钟
    cabin	|String	|舱位
    cabinClass	|String	|舱位等级
    aircraftCode	|String	|机型
    package      |Object[]     |套餐 
        packageList| Object[]   |套餐组合
            packageCode |String    |套餐具体信息二字码
            amount |Number      |价格
  retSegments	|Object[]	|回程航段
    carrier	|String	|航司 IATA 二字码,必须与 flightNumber 航司相同
    flightNumber	|String	|航班号,如:CA123。航班号数字前若有多余的数字 0, 必须去掉,如 CZ006 需返回 CZ6
    depAirport	|String	|出发机场 IATA 三字码
    depTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203100300 表示 2012 年 3 月 10 日 3 时 0 分
    arrAirport	|String	|到达机场 IATA 三字码
    arrTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203101305 表示 2012 年 3 月 10 日 13 时 5 分
    stopCities	|String	|经停地，使用’/’分隔城市三字码
    codeShare	|Boolean	|代码共享标识(true 代码共享/false 非代码共享)
    cabin	|String	|舱位
    cabinClass	|String	|舱位等级
    aircraftCode	|String	|机型
    package      |Object[]     |套餐
            packageType |Int    |1:行李，2:餐食
            amount |Float      |价格
        

### 1.5 返回结果
```json
{
"status": 0,
"msg": "success",
"routings": [
    {
        "retSegments": [],
        "childTax": 2686.99,
        "fromSegments": [
            {
                "arrAirport": "KUL",
                "operatingFlightno": "",
                "flightNumber": "AK895",
                "stopCities": "",
                "codeShare": "false",
                "carrier": "AK",
                "depAirport": "DMK",
                "stopAirports": "",
                "arrTime": "201709290220",
                "depTime": "201709282310",
                "aircraftCode": "320",
                "cabin": "O",
                "operatingCarrier": "",
                "package": [
                  {
                     "packageList":[
                        {
                         "packageCode": "AA",
                         "amount": 200.00
                        }
                     ]
                  } 
                ] 
            }
        ],
        "childFare": 2027.06,
        "currency": "JPY",
        "adultTax": 2686.99,
        "maxSeats": 3,
        "data": "xxxxxxxxxxxxxxxxxxxxxxxxx",
        "routeType": 1,
        "adultFare": 2027.06
    }
],
"carriers": {
    "AK": 1,
    "OD": -1
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
1040	|流量已超过每天最大使用额
1101	|加密校验失败，signature错误
1102	|商户已禁用，请联系账户管理员
2010	|不支持此航线
2011	|无航班请更换日期

### 1.7 错误状态码
```json
{"status": 1000, "msg": "ERROR MESSAGE" }
``` 
