<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Booking - AirPricing

### 1.1 功能描述
>简介：通过AirPricing接口，可以对相应航班信息进行价格，仓位校验。<br>
注意事项1: 最大响应时间为30秒，价格变动或仓位变动都会引起校验失败。<br>
注意事项2: 调用AirPricing接口前必须调用LowFareSearch接口，并且AirPricing接口调用结果依赖于LowFareSearch接口调用结果

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/booking](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|AirPricing
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y='
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
    routing	|String	|LowFareSearch接口中返回的routing信息
    currency |String |请求币种，如USD
    adultNumber（optional）	|String	|成人人数，小于9
    childNumber（optional）	|String	|儿童人数，小于9
    timeout（optional）	|String	|接口访问的超时时间，单位：秒
### 1.3 请求结果
```json
{
    "action": "AirPricing",
    "key": "xxxxxxxxxxxxxxxx",
    "timestamp": "1466134420.74",
    "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "version": "2.0.3",
    "request": {
        "tripType": "1",
        "routing": {
            "data": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
            "fromSegments": [
                {
                    "carrier": "AA",
                    "depAirport": "PEK",
                    "depTime": "201203140140",
                    "arrAirport": "HKG",
                    "arrTime": "201203150530",
                    "stopCities": "",
                    "codeShare": false,
                    "cabin": "E",
                    "aircraftCode": "Boeing 777",
                    "flightNumber": "AA89"
                },
                {
                    "carrier": "CA",
                    "depAirport": "HKG",
                    "depTime": "201204151400",
                    "arrAirport": "TPE",
                    "arrTime": "201204151715",
                    "stopCities": "",
                    "codeShare": false,
                    "cabin": "E",
                    "aircraftCode": "Boeing 737",
                    "flightNumber": "CA189"
                }
            ],
            "retSegments": []
        }
    }
}
```
### 1.4 返回参数
Field       |Type       |Description
:------------|:-----------|:-----------
status	|Number	|0,成功;其他,失败
isPriceChanged	|Boolean	|价格变动 (True代表价格变动了)
msg	|String	|提示信息,长度小于 64
sessionId	|String	|会话标识:标记服务接口调用的唯一标识,相应的调用结果中会原值返回。
maxSeats	|Number	|可预订的座位数,最大为 9
routing	|Object	|报价信息
  adultFare	|Float	|成人单价
  adultTax	|Float	|成人税费
  childFare	|Float	|儿童单价
  childTax	|Float	|儿童税费
  currency	|String	|货币类型三字码
  fromSegments	|Object[]	
    carrier	|String	|航司 IATA 二字码,必须与 flightNumber 航司相同
    flightNumber	|String	|航班号,如:CA123。航班号数字前若有多余的数字 0, 必须去掉,如 CZ006 需返回 CZ6
    depAirport	|String	|出发机场 IATA 三字码
    depTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203100300 表示 2012 年 3 月 10 日 3 时 0 分
    arrAirport	|String	|到达机场 IATA 三字码
    arrTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203101305 表示 2012 年 3 月 10 日 13 时 5 分
    stopCities	|String	|经停地，使用’/’分隔城市三字码
    cabin	|String	|舱位
    cabinClass	|String	|舱位等级
    aircraftCode	|String	|机型
    codeShare	|Boolean	|代码共享标识(true 代码共享/false 非代码共享)
    package      |Object[]     |套餐
            packageType |Int    |1:行李，2:餐食
            amount |Float      |价格
  retSegments	|Object[]	
    carrier	|String	|航司 IATA 二字码,必须与 flightNumber 航司相同
    flightNumber	|String	|航班号,如:CA123。航班号数字前若有多余的数字 0, 必须去掉,如 CZ006 需返回 CZ6
    depAirport	|String	|出发机场 IATA 三字码
    depTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203100300 表示 2012 年 3 月 10 日 3 时 0 分
    arrAirport	|String	|到达机场 IATA 三字码
    arrTime	|String	|起飞日期时间,格式:YYYYMMDDHHMM 例: 201203101305 表示 2012 年 3 月 10 日 13 时 5 分
    stopCities	|String	|经停地，使用’/’分隔城市三字码
    cabin	|String	|舱位
    cabinClass	|String	|舱位等级
    aircraftCode	|String	|机型
    codeShare	|Boolean	|代码共享标识(true 代码共享/false 非代码共享)
    duration	|Int	|出发地至到达地飞行时长，单位为分钟
    package      |Object[]     |套餐
            packageType |Int    |1:行李，2:餐食
            amount |Float      |价格
rule	|Object	|退改签信息,参考 Rule Element
  changesInfoList	|Object[]	
    Element	|Object	
      changesType	|Int	|改期类型 0：客票全部未使用；1：客票部分使用【即去程已使用，在往返行程中使用，代表回程的退票信息】【单程时0；往返时0、1都要有】
      changesStatus	|String	|改期标识 T：不可改期 H：有条件改期 F：免费改期 E：按航司客规【公布运价专用】
      changesFee	|Decimal	|改期费 1）当changesStatus =H,必须赋值；2）若changesStatus =T/F,此字段可不赋值。
      currency	|String	|改期费币种 当refundStatus =H，必须赋值。
      passengerType	|Int	|乘客类型，0 成人/1 儿童 1）对于对乘客类型的查询、验价，必须按乘客类型返回；如成人+儿童的查询，成人和儿童的退改签都要有。
      revNoshow	|String	|是否允许NoShow改期 T：不可改； H：有条件改；F：免费改；E：按航司客规为准【公布运价专用】
      revNoShowCondition	|Int	|改期时航班起飞前多久算NoShow，单位：小时 1）若无法确认此时间，请默认赋0。
      revNoshowFee	|Decimal	|NoShow改期费用 1）当revNoshow =H，必须赋值；2）展示给客人的noshow改期费= changesFee + revNoshowFee。
      enRevRemark	|String	|(option) 中文改期备注
      cnRevRemark	|String	|(option) 英文改期备注
  refundInfoList	|Object[]	
    Element	|Object	
      refundType	|Int	|退票类型 0：客票全部未使用；1：客票部分使用【即去程已使用，在往返行程中使用，代表回程的退票信息】【单程时0；往返时0、1都要有】
      refundStatus	|String	|退票标识 T：不可退 H：有条件退 F：免费退 E：按航司客规【公布运价专用】
      refundFee	|Decimal	|退票费 1）当refundStatus =H,必须赋值；2）若refundStatus =T/F,此字段可不赋值。
      currency	|String	|退票费币种 当refundStatus =H，必须赋值。
      passengerType	|Int	|乘客类型，0 成人/1 儿童 1）对于多乘客类型的查询、验价，必须按乘客类型返回；如成人+儿童的查询，成人和儿童的退改签都要有。
      refNoshow	|String	|是否允许NoShow退票 T：不可退； H：有条件退；F：免费退；E：按航司客规为准【公布运价专用】
      refNoShowCondition	|Int	|退票时航班起飞前多久算NoShow，单位：小时 1）若无法确认此时间，请默认赋0。
      refNoshowFee	|Decimal	|NoShow退票费用 1）当IsRefNoshow =H，必须赋值；2）展示给客人的noshow退票费= refundFee+ refNoshowFee。
      enRevRemark	|Decimal	|(option) 中文退票备注
      cnRevRemark	|Decimal	|(option) 英文退票备注
  baggageInfoList	|Object[]	
    Element	|Object	
      segmentNo	|Int	|航段序号，从1开始 1）注意是按航段赋值，而不是按去程/回程赋值
      passengerType	|Int	|乘客类型，0 成人/1 儿童 1）对于多乘客类型的查询、验价，必须按乘客类型返回；如成人+儿童的查询，成人和儿童的行李额都要有。
      baggagePiece	|Int	|行李额件数，单位PC，枚举值如下：0无免费托运行李，此时baggageWeight需赋值为-1；-1表示计重制，对应的baggageWeight表示每人可携带的总重量(此时baggageWeight必须赋正值，否则过滤）；>0表示计件制，对应的baggageWeight表示每件行李重量（若计件制时不知每件行李额的重量，baggageWeight必须赋值为-1）。
      baggageWeight	|Int	|行李额重量，单位KG，必须赋值，跟BaggagePiece配合使用
      cnBaggage	|Object	|中文行李额备注
      enBaggage	|Object	|英文行李额备注

### 1.5 返回结果
```json  
{
    "status": 0,
    "isPriceChanged": false,
    "rule": {
        "changesInfoList": [
            {
                "enRemark": "",
                "revNoShowCondition": 0,
                "revNoshowFee": 0,
                "changesStatus": "T",
                "changesFee": 0,
                "currency": "CNY",
                "enRevRemark": "",
                "revNoshow": "T",
                "cnRevRemark": "",
                "changesType": 0,
                "passengerType": 0,
                "cnRemark": ""
            },
            {
                "enRemark": "",
                "revNoShowCondition": 0,
                "revNoshowFee": 0,
                "changesStatus": "T",
                "changesFee": 0,
                "currency": "CNY",
                "enRevRemark": "",
                "revNoshow": "T",
                "cnRevRemark": "",
                "changesType": 1,
                "passengerType": 0,
                "cnRemark": ""
            },
            {
                "enRemark": "",
                "revNoShowCondition": 0,
                "revNoshowFee": 0,
                "changesStatus": "T",
                "changesFee": 0,
                "currency": "CNY",
                "enRevRemark": "",
                "revNoshow": "T",
                "cnRevRemark": "",
                "changesType": 0,
                "passengerType": 1,
                "cnRemark": ""
            },
            {
                "enRemark": "",
                "revNoShowCondition": 0,
                "revNoshowFee": 0,
                "changesStatus": "T",
                "changesFee": 0,
                "currency": "CNY",
                "enRevRemark": "",
                "revNoshow": "T",
                "cnRevRemark": "",
                "changesType": 1,
                "passengerType": 1,
                "cnRemark": ""
            }
        ],
        "refundInfoList": [
            {
                "enRemark": "",
                "enRefRemark": "",
                "refNoshow": "T",
                "cnRefRemark": "",
                "refundFee": 0,
                "refundStatus": "T",
                "currency": "CNY",
                "refNoShowCondition": 0,
                "cnRemark": "",
                "refNoshowFee": 0,
                "refundType": 0,
                "passengerType": 0
            },
            {
                "enRemark": "",
                "enRefRemark": "",
                "refNoshow": "T",
                "cnRefRemark": "",
                "refundFee": 0,
                "refundStatus": "T",
                "currency": "CNY",
                "refNoShowCondition": 0,
                "cnRemark": "",
                "refNoshowFee": 0,
                "refundType": 1,
                "passengerType": 0
            },
            {
                "enRemark": "",
                "enRefRemark": "",
                "refNoshow": "T",
                "cnRefRemark": "",
                "refundFee": 0,
                "refundStatus": "T",
                "currency": "CNY",
                "refNoShowCondition": 0,
                "cnRemark": "",
                "refNoshowFee": 0,
                "refundType": 0,
                "passengerType": 1
            },
            {
                "enRemark": "",
                "enRefRemark": "",
                "refNoshow": "T",
                "cnRefRemark": "",
                "refundFee": 0,
                "refundStatus": "T",
                "currency": "CNY",
                "refNoShowCondition": 0,
                "cnRemark": "",
                "refNoshowFee": 0,
                "refundType": 1,
                "passengerType": 1
            }
        ],
        "baggageInfoList": [
            {
                "baggageWeight": 0,
                "baggagePiece": 0,
                "enBaggage": "",
                "cnBaggage": "",
                "segmentNo": 1,
                "passengerType": 0
            },
            {
                "baggageWeight": 0,
                "baggagePiece": 0,
                "enBaggage": "",
                "cnBaggage": "",
                "segmentNo": 1,
                "passengerType": 1
            }
        ]
    },
    "maxSeats": 3,
    "sessionId": "fa54e852093ba64efee0b0273310a63b",
    "routing": {
        "retSegments": [],
        "childTax": 2686.99,
        "fromSegments": [
            {
                "arrAirport": "KUL",
                "operatingFlightno": "",
                "flightNumber": "AK881",
                "stopCities": "",
                "codeShare": "false",
                "carrier": "AK",
                "depAirport": "DMK",
                "stopAirports": "",
                "arrTime": "201709281315",
                "depTime": "201709281000",
                "aircraftCode": "320",
                "cabin": "I",
                "operatingCarrier": ""
            }
        ],
        "childFare": 6777.66,
        "currency": "CNY",
        "adultTax": 2686.99,
        "data": "xxxxxxx",
        "adultFare": 6777.66
    },
    "msg": "success",
    "timeflag": 1504792769.236955
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
2012	|此航班已售罄

### 1.7 错误状态码
```json
{
    "status": 1000,
    "msg": "Letslfy flight inernal error"
}
``` 
