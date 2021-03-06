## Trader Gateway API

/TraderUser/Login POST 
---
> Authenticate the user.

*request*
```
{
  "tu_name": "zhanchen",
  "tu_password": "zhanchen"
}
```

*success response*
```
{
  "tu_id": 20,
  "tu_name": "zhanchen",
  "tu_role": 2,
  "tu_email": "zhanchen@qq.com",
  "t_id": 0,
  "tu_password": "",
  "tu_hash": -170952320
}
``` 
  
*failed response* 
``` 
{
  "message": "Log in Failed"
}
```

> HEADER after login:
```
"TU-Hash" -> 5704312
"TU-Name" -> "zhanchen"
```

/UserOrder POST
---
> A UserOrder is submitted to the trader.

> uo_type: "Stop" "Limit" "Cancel" "Market"  
> uo_status: "Placed" "Cancelled" "PartiallyBought" "PartiallyFinished" "Finished"

*request body*
```
{
  "c_id": 2,
  "uo_type": "Market",
  "uo_vol": 350,
  "uo_year": 2018,
  "uo_month": 10,
  "uo_is_buy": 1,
  "uo_limit_value": "",
  "uo_stop_value": ""
}
``` 
```
{
  "c_id": 2,
  "uo_type": "Limit",
  "uo_vol": 350,
  "uo_year": 2018,
  "uo_month": 10,
  "uo_is_buy": 1,
  "uo_limit_value": "3.7%",
  "uo_stop_value": ""
}
```
```
{
    "c_id": 2,
    "uo_type": "Stop",
    "uo_vol": 350,
    "uo_year": 2018,
    "uo_month": 10,
    "uo_is_buy": 0,
    "uo_limit_value": "",
    "uo_stop_value": "229.6"
}
```

*success response*
```
{
    "uo_id": 321,
    "o_id": -1,
    "c_id": 2,
    "tu_id": 1,
    "uo_price": -1,
    "uo_type": "Limit",
    "uo_vol": 350,
    "uo_status": "Placed",
    "uo_create_time": "2017-05-15 22:21:30",
    "uo_year": 2018,
    "uo_month": 10,
    "uo_is_buy": 1,
    "uo_limit_value": "3.7%",
    "uo_stop_value": ""
}
```

*failed response*
```
401 Unauthorized
```
```
{
  "message": "Add UserOrder Failed"
}
```
/Commodity/All GET
---
> Get all commodities that a trader subscribed 

*success response*
```
{
  "commodities": [
    {
      "bu_id": 1,
      "c_id": 1,
      "c_name": "gold",
      "c_price": 225
    },
    {
      "bu_id": 1,
      "c_id": 2,
      "c_name": "corn",
      "c_price": 15.3
    }
  ]
}
``` 

/Commodity/{c_id}/BrokerUser GET
---
> Get the information of BrokerUser that sells a commodity  
> c_id is the id of a commodity

*success response*
```
{
  "bu_email": "hmcai@sjtu.edu.cn",
  "bu_id": 1,
  "bu_name": "caihongming",
  "bu_password": ""
}
```

/Order/All GET
---
> Get all orders (not trader order)

*success response*
```
{
  "orders": [
    {
      "c_id": 1,
      "o_create_time": "2017-05-30 00:03:13",
      "o_id": 20,
      "o_is_buy": 0,
      "o_limit_value": "",
      "o_month": 6,
      "o_price": -1,
      "o_status": "Placed",
      "o_stop_value": "234.99",
      "o_type": "Limit",
      "o_vol": 192,
      "o_year": 2017,
      "t_id": 1
    },
    {
      "c_id": 1,
      "o_create_time": "2017-05-30 00:03:13",
      "o_id": 21,
      "o_is_buy": 0,
      "o_limit_value": "-1",
      "o_month": 5,
      "o_price": -1,
      "o_status": "Part_Completed",
      "o_stop_value": "-1",
      "o_type": "Market",
      "o_vol": 175,
      "o_year": 2018,
      "t_id": 1
    },
    {
      "c_id": 1,
      "o_create_time": "2017-05-30 00:49:38",
      "o_id": 22,
      "o_is_buy": 1,
      "o_limit_value": "",
      "o_month": 5,
      "o_price": -1,
      "o_status": "Completed",
      "o_stop_value": "",
      "o_type": "Market",
      "o_vol": 10,
      "o_year": 2018,
      "t_id": 1
    }
  ]
}
``` 

/BrokerUser/All GET
---
> Get all brokerUsers in the market

*success response*
```
{
  "brokerUsers": [
    {
      "bu_email": "hmcai@sjtu.edu.cn",
      "bu_id": 1,
      "bu_name": "caihongming",
      "bu_password": "caihongming"
    }
  ]
}
```

/BrokerUser/{bu_id}/Commodities GET
---
> Get all commodities a brokerUser sells  
{bu_id} is the brokerUser id

*success response*
```
{
  "commodities": [
    {
      "bu_id": 1,
      "c_id": 1,
      "c_name": "gold",
      "c_price": 80
    },
    {
      "bu_id": 1,
      "c_id": 2,
      "c_name": "corn",
      "c_price": 15.3
    },
    {
      "bu_id": 1,
      "c_id": 3,
      "c_name": "crude",
      "c_price": 100
    }
  ]
}
```