<style>
    .ar{padding-left:20px;}
    .op{margin-left:30px;}
</style>
## 1. Order - SyncOrderStatus

### 1.1 功能描述
>简介： 订单出票状态推送接口

### 1.2 请求说明
> 请求方式：POST<br>
请求URL ：[/](#)

### 1.3 请求参数
Field       |Type       |Description
:------------|:-----------|:-----------
orderNo	|String	|订单号
orderStatus	|String	|订单状态
msg	|String	|订单状态描述
tickets	|Object[]	
  passengerId	|String	|乘客Id
  firstName	|String	|乘客FirstName
  lastName	|String	|乘客LastName
  ticketNo	|String	|票号
  createTime	|String	|出票时间
  flightNumber	|String	|航班号

### 1.3 请求结果
```json
{
  "orderNo": "123456",
  "orderStatus": "TICKETED",
  "msg": "Order has been TICKETED",
  "tickets": {
    "passengerId": "xxxx",
    "firstName": "XU",
    "lastName": "JUNHYUNG",
    "ticketNo": "123123",
    "createTime": "155555555555",
    "flightNumber": "fg123"
  }
}
```
### 1.4 返回参数
Field       |Type       |Description
:------------|:-----------|:-----------
status	|Number	|0,成功;其他,失败
msg	|String	|提示信息,长度小于 64
       
### 1.5 返回结果
```json
{
    "status": 0,
    "msg": "success"
}
```
