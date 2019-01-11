<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Booking - SetPassengers

### 1.1 功能描述
>简介：向目标行程添加乘客信息，此接口在预定流程为必需。<br>
    注意事项：调用此接口前必须调用AirPricing接口，并依赖于AirPricing接口的结果。

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/flight/booking](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
action	|String	|SetPassengers
key	|String	|商户在平台申请的 key.
signature	|String |使用授权密钥对指定格式进行AES 256 CBC加密的数据，如果您的API密钥数据为：<br> key: ctPJAIdxUA3ptaWCsecret: 024sYXZXMlFKaiAa65IYuMCB0hE2CgaP 则需要加密数据的格式为：'key&timestamp'，例如：'ctPJAIdxUA3ptaWC&1500375695.65'，那么使用上述密钥加密后数据为： '15hhHQ8C6F9OxD/BNyztUPUJyiRlGPRafEkcI6q2E5Y='
timestamp	|String	|时间戳信息，用于加密和验证
version	|String	|API 版本信息，2.0.1
request	|Object	
  sessionId	|String	|sessionId，由AirPricing接口应答产生
  routeType |Int    |数据来源信息，0:LF，1:tech house
  passengers	|Object[]	|乘机人信息
    passengerId	|String	|passengerid,从0开始增加，不允许重复
    firstName	|String	|firstName，如果有middleName,格式为firstName middleName
    lastName	|String	|lastName
    ageType	|Number	|乘客类型,0:成人 1:儿童 -1:留学生
    birthday	|String	|生日,格式:YYYYMMDD
    gender	|String	|乘客性别,M:男 F:女
    cardNum	|String	|证件号码,最大 15 个字符
    cardType	|String	|证件类型,PP:护照 GA:港澳通行证 TW:台湾通行证 TB:台胞证 HX:回乡证 HY:国际海员证
    cardIssuePlace	|String	|证件发行国家,国家二字码
    cardExpired	|String	|证件有效时间,格式:YYYYMMDD
    nationality	|String	|乘客国籍,国家二字码
  contact	|Object	|联系人信息,参考下面的 Contact Element
    firstName	|String	|firstName，如果有middleName,格式为firstName middleName
    lastName	|String	|lastName
    address	|String	|详细地址
    postcode	|Number	|邮编
    email	|String	|联系人邮箱
    mobile	|String	|联系人手机号,需要国家码+手机号
### 1.3 请求结果
```json
{
    "timestamp": "1508142479.56",
    "request": {
        "passengers": [
            {
                "cardExpired": "20190506",
                "cardType": "PP",
                "birthday": "19830418",
                "nationality": "CN",
                "cardIssuePlace": "CN",
                "passengerId": "0",
                "firstName": "YANG",
                "ageType": 0,
                "gender": "F",
                "cardNum": "G35388575",
                "lastName": "Liu"
            },
            {
                "cardExpired": "20190510",
                "cardType": "PP",
                "birthday": "19830315",
                "nationality": "CN",
                "cardIssuePlace": "CN",
                "passengerId": "1",
                "firstName": "WANTAO",
                "ageType": 0,
                "gender": "M",
                "cardNum": "G35392875",
                "lastName": "LI"
            }
        ],
        "sessionId": "dd0a785f24f4f70e9816969044df3605",
        "routeType": 1,
        "contact": {
            "firstName": "qwe",
            "mobile": "13774293883",
            "lastName": "qwe",
            "postcode": "200335",
            "address": "Ctrip Building, No.99 Fuquan Road, Shanghai, China",
            "email": "GPYYXGXPZ@ctrip.com"
        }
    },
    "version": "2.0.1",
    "key": "xxxxxxxxxxxxxxxx",
    "signature": "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
    "action": "SetPassengers"
}
```
### 1.4 返回参数
Field       |Type       |Description
:------------|:-----------|:-----------
status	|Number	|0,成功;其他,失败
msg	|String	|提示信息,长度小于 64
totalCost	|Float	|总计需要金额
currency	|String	|货币类型三字码
        

### 1.5 返回结果
```json  
{
    "status": 0,
    "totalCost": 20513.74,
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
2007	|SetPassenger请求格式错误：乘客类型错误
2008	|SetPassenger只允许设置一次，重复设置错误
2009	|PassengerID不存在，通常SellSSR或AssignSeat之前需要调用SetPassenger
2014	|儿童人数不能大于成人人数,并且不能只有单独儿童人数
### 1.7 错误状态码
```json
{"status": 1000, "msg": "ERROR MESSAGE" }

