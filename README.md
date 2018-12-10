

About API
It provides stable and secure APIs. You can get the latest market data and trade via the APIs. Your trade-bot can run your algorithms to arbitrage or hedge. Now there are hundreds of algorithms in Exchange working safely.
Request Process
Root URL
--------------ENTER URL HERE ------------
Encode char set
UTF-8
Content type of the header (GET method)
application/x-www-form-urlencoded
Content type of the header (POST method)
application/json
Verification
Sign Verification
Exchange API
REST API
API Demo
NodeJs : Enter URL Here
------------------------------------------------------------------------------------------------
Sign Verification
When using trade APIs, api key and api secret is required. Your API ID must have trade permission.
REST API Sample
This is a sample of place order API (POST api.exchange.com/create-order), the parameters are below,
API parameters
symbol=btcusdt, type=buy-limit, price=10000.00, qty=1.0000
API ID parameters
apiid=123456, secret=abcdef
Connect all the parameters with ‘&’，
api_key=123456&price=10000.00&qty=1.0000&secret=ABCDEF&symbol=BTCUSDT&TYPE=BUY
Please use POST method to request the trade APIs.
------------------------------------------------------------------------------------------------

Authentications
Exchange API has two types of authentication, market and trade.
Market API
Users can get latest market data via market APIs. Market APIs are public.
 
Features	API	Details	   
Get Latest Price (Ticker)	GET get-ticker	Details	   
Get Orderbook	GET get-order-book
	Details	   
Get Symbol	GET get-symbol	Details	   
Get Latest Trade Records	GET get-trade	Details	 

Trade API
Users can trade via trade APIs in Exchange. Trade APIs are private. When using trade APIs, you need to sign according to API ID and Secret with trade permission.
 
Features	API	Details	   
Get Account Balance	POST get-balance	Details	   
Place Order	POST create-order	Details	   
Check Order Status	POST order-info	Details	   
Cancel Order	POST cancel-order	Details	   
Check Open Orders	POST open-orders	Details	 

Get Ticker [Market]

GET orderbook
Permission
All API users.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
symbol	string	true	the code of symbol, or al	all = all symbols	 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
ticker	object	true			   
ticker	type	mandatory	value(s)	remarks	   
symbol	string	true			   
last	decimal	true			   
bid	decimal	true		bid1 price	   
ask	decimal	true		ask1 price	   
24hrHigh	decimal	true			   
24hrLow	decimal	true			   
24hrVol	decimal	true			 
Please be noted that parameter names are case sensitive.
Response Sample
GET get-ticker?symbol=BCH_BTC"
{
 	"status":"ok",
	"ticker":[
		{
			"symbol":"BCH_BTC",
			"24hrHigh":0.05,
			"last":0.0001,
			"24hrVol":0.2525,
			"ask":0.0001,
			"24hrLow":0.0001,
			"bid":0.0001
		}
	],
	"timestamp":1537881682945
}

Error Code
Incorrect symbol parameter
{
    "description":"Invalid Symbol.",
    "status":"error",
    "timestamp":1516801104095
}

Get Orderbook [Market]

GET get-order-book
Permission
All API users.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
symbol	string	true			 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
orders	object	true			   
orders	type	mandatory	value(s)	remarks	   
price					   
quantity					   
volume					 
Please be noted that parameter names are case sensitive.
Response Sample
GET get-order-book?symbol=BCH_BTC
{
	"status":"ok",
	"timestamp":1537883682151,
	"orders":[
		{
			"price":0.0001,
			"quantity":10,
			"volume":"0.00100000"
		},
		{
			"price":0.001,
			"quantity":1,
"volume":"0.00100000"
}
]
}


Error Code
Incorrect symbol parameter
{
    "description":"Invalid Symbol.",
    "status":"error"
}

Get Trades [Market]

GET get-trade
Permission
All API users.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
symbol	string	true			   
size	Integer	false	1 to 2000	The number of trade records, sorted by time reverse order. Default = 300	 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true		the timestamp of server side when sending the response	   
trades	object	true			   
trades	type	mandatory	value(s)	remarks	   
tradeId	string	true			   
price	decimal	true			   
quantity	decimal	true			   
take	string	true	buy, sell	the side of take order	   
datetime	string	true		trade time	 

Response Sample
GET get-trade?symbol=BTC_BTC&size=100
{
	"status":"ok",
	"trades":[
		{
			"tradeId":13,
			"take":"SELL",
			"price":0.0001,
			"quantity":10,
			"datetime":1537876687000
		},
	],
	"timestamp":1537882135971
}

Incorrect symbol parameter
{
    "description":"Invalid Symbol.",
    "status":"error"
}

Get Symbols [Market]

GET symbol
Permission
All API users.
Parameters
None
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
symbol	string	true			   
symbol	type	mandatory	value(s)	remarks	   
symbol	string	true			   
24hrHigh	decimal	true			   
last	decimal	true			   
24hrVol	decimal	true			   
ask	decimal	true		Ask price	   
24hrLow	decimal	true			   
bid	decimal	true		Bid price	 
Please be noted that parameter names are case sensitive.
Response Sample
{
    "status": "ok",
    "symbol": [
        {
            "symbol": "ETH_BTC",
            "24hrHigh": 55.00000000,
            "last": 15,
            "24hrVol": 55.00000000,
            "ask": 0.1111,
            "24hrLow": 50.00000000,
            "bid": 15
        }
        ....
    ],
    "timestamp": 1538047135010
}


Check Balance [Trade]

POST get-balance
Permission
Trade APIs are private. When using trade APIs, you need to API ID and Secret has trade permission.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
api_key	string	true		Can apply at exchange	   
currency	string	true			   
secret	string	true		Personal key	 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
balance	string	true			   
balance	type	mandatory	value(s)	remarks	   
available	decimal	true			   
reserved	decimal	true			   
total	decimal	true			 
Please be noted that parameter names are case sensitive.
Response Sample
POST get-balance
{
    "status": "ok",
    "timestamp": 1538048795543,
    "balance": [
        {
            "available": "1000.00000000",
            "reserved": "0.00000000",
            "total": "1000.00000000"
        }
    ]
}
Error Code
Did not use POST method
{
    "description":"Invalid Request Method.",
    "status":"error"
}
Incorrect parameter or parameter missing (Please be noted parameter names are case sensitive, the params should be encode with UTF-8 char set)
{
    "description":"Invalid Param.",
    "status":"error"
}
Incorrect API ID
{
    "description":"Invalid API Details",
    "status":"error"
}

Place Order [Trade]

POST create-order
Permission
Trade APIs are private. When using trade APIs, you need to API ID and Secret has trade permission.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
api_key	string	true			   
price	string	true			   
qty	string	true			   
symbol	string	true			   
type	string	true	BUY / SELL		   
secret	string	true			 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
message	long	true			   
order_id	string	true		order ID	   
type	string	true		BUY / SELL	 
Please be noted that parameter names are case sensitive.
Response Sample
POST create-order
{
	"status":"ok",
	"timestamp":1537882992676,
	"message":"Order has been placed.",
	"order_id":24,
	"type":"BUY"
}


Error Code
Did not use POST method
{
    "description":"Invalid Request Method.",
    "status":"error",
    "timestamp":1516801104095
}
Incorrect parameter or parameter missing
{
    "description":"Invalid Param.",
    "status":"error"
}
Check Balance
{
    "description":"Insufficient Balance.",
    "status":"error"
}
Incorrect symbol parameter
{
    "description":"Invalid Symbol.",
    "status":"error"
}
Incorrect API ID
{
    "description":"Invalid API Credentials.",
    "status":"error"
}

Check Order Status [Trade]

POST order-info
Permission
Trade APIs are private. When using trade APIs, you need to API ID and Secret has trade permission.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
api_key	string	true			   
order_id	string	true			   
type	string	true			   
secret	string	true			 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
orders	object	true			   
order	type	mandatory	value(s)	remarks	   
id	string	true			   
date
	string	true			   
price
	decimal	true			   
total_fee
	decimal	true			   
filled_quantity
	decimal	true			 
Please be noted that parameter names are case sensitive.
Response Sample
POST order-info
{
	"status":"ok",
	"timestamp":1537883934304,
	"orders":[
		{
			"date":1533820052000,
			"id":12,
			"price":15,
			"total_fee":0,
			"filled_quantity":1	
		}
	]
}

Cancel Order [Trade]

POST cancel-order
Permission
Trade APIs are private. When using trade APIs, you need API ID and Secret has trade permission.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
api_key	string	true			   
order_id	string	true			   
type	string	true	BUY / SELL		   
secret	string	true			 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
message	string	true			 
Please be noted that parameter names are case sensitive.
Response Sample
POST cancel-order
{
	"status":"ok",
	"timestamp":1537883532195,
	"message":"Order Cancelled Successfully."
} 

Check Open Orders [Trade]
POST open-orders
Permission
Trade APIs are private. When using trade APIs, you need API ID and Secret has trade permission.
Parameters
 
parameter	type	mandatory	value(s)	remarks	   
api_key	string	true			   
symbol	string	true			   
secret	string	true			 
Response
 
name	type	mandatory	value(s)	remarks	   
status	string	true	ok, error		   
timestamp	long	true			   
orders	object	true			   
orders	type	mandatory	value(s)	remarks	   
timestamp	string	true			   
currency	string	true			   
type	string	true			   
price	decimal	true			   
units_filled	decimal	true			   
units_total	decimal	true			   
estimated_total	decimal	true			 
Please be noted that parameter names are case sensitive.
Response Sample
POST open-orders
{
"status":"ok",
"orders":[
{
"timestamp":1537876616000,
"type":"BUY",
"price":0.0001,
"currency":"BTC",
"units_filled":"5.00000000",
"units_total":"10.00000000",
"estimated_total":"0.00050000"
},
{
"timestamp":1537880675000,
"type":"BUY",
"price":0.0001,
"currency":"BTC",
"units_filled":"0.00000000",
"units_total":"10.00000000",
"estimated_total":"0.00100000"
},
{
"timestamp":1537882992000,
"type":"BUY",
"price":0.001,
"currency":"BTC",
"units_filled":"0.00000000",
"units_total":"1.00000000",
"estimated_total":"0.00100000"
}
],
"timestamp":1537883201960
} 


