# Payments

Payment APIs provide interfaces to manage money movement. The interfaces cover the following forms of payments:

- Same Bank (Account-On-Us), Domestic 
- International Payments
- Beneficiary Payments
- Billers and Bill Payments
- Periodical Payments: Standing Order, Direct-Debit, Scheduled Payments


<aside class="notice">
As a standard, the payment process is in two-fold: payment initiation and payment validation. There are a number of payment initiation operations defined under this class but they all use the same payment validation operation. 
</aside>





## Initiate a Payment Transaction

Initiate a payment transaction. This applies to payments within the same bank or to other domestic financial institutions.

```Shell
curl -X POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"payment_type": "NEFT",
		"amount" : 10,000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"meta_data" : {
			"reference": "Transfer Money for Product",
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false"
		}
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Payment request initiated",
  "data": {
		"session_id": "8907654YDFGHJK",
		"payment_id": "66733254776555",
		"status": "completed",
		"creation_date_time": "2017-06-05T15:15:22+00:00",
		"status_update_time": "2017-06-05T18:03:22+00:00",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"reference": "Transfer Money for Product",
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}		
	}
}
```

### HTTP Request

`POST /payments/`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
payment_type | string | Specify type of payment - NEFT, RTGS, Internal
amount | decimal | Specify amount to be transferred
currency | string | Specify an account currency from the list of possible options from the finance house (options ar NGN, USD, EUR, GBP)
source | object | Provide details of the of the originating account
source:account_number | string | Specify source account number
source:account_id | string | (Optional). Specify source account identification
destination | object | Provide details of the beneficiary account
destination:scheme_name | string | Specifiy Banking Account Scheme Name. Options include NUBAN for Nigeria
destination:account_name | string | Specify Account Holder Name
destination:account_number | string | Specify Account number
destination:sort_code | string | Specify Account Sort Code
destination:bank_code | string | Specify Bank Code
meta_data | object | Specify multiple type values information under this object






## Retrieve a Payment Transaction

This API retrieves detailed information on a payment transaction.

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/66733254776555"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
	-d '{"account_number": "1234567890"}'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Payment status retrieved",
  "data": {
		"payment_id": "66733254776555",
		"status": "completed",
		"creation_date_time": "2017-06-05T15:15:22+00:00",
		"status_update_time": "2017-06-05T18:03:22+00:00",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"reference": "Transfer Money for Product",
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}		
	}
}
```

### HTTP Request

`GET /payments/{payment_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
payment_id | string | Specify payment identification returned from payment request

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify source account number



## Retrieve all Payment Transactions

This API retrieves detailed information on a payment transaction.

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments?account_number=1234567890&start_date=2019-05-01&end_date=2020-12-31"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
	
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Payment status retrieved",
  "data": {
		[{ 
		"payment_id": "66733254776555",
		"status": "completed",
		"creation_date_time": "2017-06-05T15:15:22+00:00",
		"status_update_time": "2017-06-05T18:03:22+00:00",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"reference": "Transfer Money for Product",
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}		
	},
	{
		"payment_id": "66733254776566",
		"status": "completed",
		"creation_date_time": "2017-06-05T15:15:22+00:00",
		"status_update_time": "2017-06-05T18:03:22+00:00",
		"amount": 20000.00,
		"currency": "NGN",
		"source": {
			"account_number": "0234567845",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Jane Okoro",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"reference": "Transfer Money for Product",
			"narration": "Payment for Noodles pack",
			"charge_bearer": "BEN",
			"destination_email": "janeokoro@gmail.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}		
	}]}
}
```

### HTTP Request

`GET /payments`


### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
start_date | string | Specify start date in ISO 8601 format 'YYYY-MM-DD'
end_date | string | Specify end date in ISO 8601 format 'YYYY-MM-DD'
account_number | string | Specify customer account number




## Validate a Payment Transaction

This API is used to validate a payment transaction.

```shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/validation"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
  -d '{
		"session_id": "8907654YDFGHJK",
		"amount": 1000000,
        "transaction_id": "string",
        "time_stamp": "Date"
  }'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Payment validation successful",
  "data": {"transaction_id":123456789012456780,
		"paymentAmount":1000000}
}
```

### HTTP Request

`POST /payments/validation

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
session_id | string | 
amount | integer |
transaction_id | string | 
time_stamp | string | 



## Cancel a Payment Transaction

Cancel payment transaction

```Shell
curl -X DELETE "https://api.singularapi.com/api/v1/finance/00234000054/payments/66733254776555"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
	
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Payment transaction cancelled",
  "data": {
		"payment_id": "66733254776555",
		"status": "completed",
		"creation_date_time": "2017-06-05T15:15:22+00:00",
		"status_update_time": "2017-06-05T18:03:22+00:00",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"reference": "Transfer Money for Product",
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}		
	}
}
```

### HTTP Request

`DELETE /payments/{payment_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
payment_id | string | Specify payment identification returned from payment request
session_id | string | Session_id generated during payment initiation




## Retrieve all Beneficiaries

Retrieve beneficiary List.

```shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/beneficiaries?source_account_number=1234567890"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Successful",
  "data": {
	  "beneficiary_list": [
		{
		  "beneficiary_id": "C$0003019202$AU$XX$01000540000001",
		  "beneficiary_name": "Singtel",
		  "beneficiary_nick_name": "Singtel",
		  "payment_type": "LOCAL_CITI",
		  "display_account_number": "XXXXXX2364",
		  "account_id": "3255613852316f2b4d4d796c344e38756339654972776f663745446e6d4c32486f455a4165374a476858343d",
		  "currency_code": "USD",
		  "payment_methods": [
			{
			  "payment_method": "GIRO"
			}
		  ],
		  "beneficiary_status": "ACTIVE",
		  "merchant_number": "10000025142"
		}
	  ]
	}
}
```

### HTTP Request

`GET /payments/beneficiary`

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
source_account_number | string | 







## Add a Beneficiary

This API enables customer to add beneficiary like internal/external bill payment.


```Shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/beneficiaries"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
  -d '{
			"beneficiary_type":"INTERNAL_DOMESTIC",
			"beneficiary_name":"Mark Jacobs",
			"currency_code":"NGN",
			"email":"MarkJ@yahoo.com",
			"phone":"090888906547",
			"beneficiary_notes":"Personal",
			"account_number":9125812364,
			"card_number":"4201125415944521",
			"bank": "ACCESS Bank"
			"country": "NIGERIA"
		
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "beneficiary added successfully",
  "data": {
	  "beneficiary_id": "097640000000000000000000000000023702XX0000015",
	  "beneficiary_status": "ACTIVE"
	}
}
```

### HTTP Request

`POST /payments/beneficiary`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
beneficiary_type | string | type of beneficiary
currency_code | string | currency code
beneficiary_name | string |name of beneficiary
account_number | string |account number
email | string |email address of beneficiary
phone | string |phone number
beneficiary_note | string |narration



## Update a Beneficiary

update a beneficiary details

```Shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/beneficiaries"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
  -d '{			  
	"beneficiary_type":"INTERNAL_DOMESTIC",
	"beneficiary_name":"Mark Jacobs",
	"currency_code":"USD",
	"beneficiary_nick_name":"MarkJ",
	"beneficiary_notes":"Personal",
	"display_account_number": "XXXXXX2364",
	"card_number":"4201125415944521"
	  "currency_code": "USD",
	  "payment_methods": [
		{
		  "payment_method": "GIRO"
		}
	  ]
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "beneficiary details updated successfully",
  "data": {			  
	"beneficiary_type":"INTERNAL_DOMESTIC",
	"beneficiary_name":"Mark Jacobs",
	"currency_code":"USD",
	"beneficiary_nick_name":"MarkJ",
	"beneficiary_notes":"Personal",
	"account_number": "XXXXXX2364",
	"card_number":"4201125415944521",
	"payment_method": "GIRO"
		
	}
}
```

### HTTP Request

`PUT /payments/beneficiary`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
beneficiary_type | string | type of beneficiary
currency_code | string | currency code
beneficiary_name | string |name of beneficiary
account_number | string |account number of beneficiary
card_number | string |card number
payment_method | string |method of payment






## Delete a Beneficiary

This API is used to delete a beneficiary.

```Shell
curl -x DELETE "https://api.singularapi.com/api/v1/finance/00234000054/payments/1234567890"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
 
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "beneficiary deleted successfully",
  "data": {
	  "beneficiary_id": "097640000000000000000000000000023702XX0000015",
	  "beneficiary_status": "Deleted"
	}
}
```

### HTTP Request

`POST /payments/beneficiarys/{beneficiary_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
beneficiary_id | string | unique identifier of beneficiary




## Validate Beneficiary Management

This API validates the details of a beneficiary .

```Shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/beneficiaries/validation"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
  -d '{
		"beneficiary_id": "097640000000000000000000000000023702XX0000015"
		"beneficiary_type":"INTERNAL_DOMESTIC",
		"beneficiary_name":"Mark Jacobs",
		"currency_code":"RUB",
		"beneficiary_nick_name":"MarkJ",
		"beneficiary_notes":"Personal",
		"account_number":9125812364
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "beneficiary validation successful",
  "data": {
	  "beneficiary_id": "097640000000000000000000000000023702XX0000015",
	  "beneficiary_status": "ACTIVE"
	}
}
```

### HTTP Request

`POST /payments/beneficiary/validation`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
beneficiary_id | string |unique identifier of the beneficiary 
beneficiary_type | string | type of beneficiary
beneficiary_name | string | name of beneficiary
currency_code | string |currency code
beneficiary_nick_name | string |alias of beneficiary
beneficiary_notes | string |beneficiary other details
account_number | string | account number of beneficiary



## Initiate Payment to a Beneficiary

This API initiate payment to a beneficiary.

```Shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/1234567890"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
  -H 'Content-Type: application/json'
  -d '{
"source_account_number":  "string"
"payment_method": "INSTANT TRANSFER"
"payment_type": "SALARY"
"beneficiary_details":{
"beneficiary_name": "Taiwo Oyin",
"bank": "FIRST Bank",
"account_name": "Taiwo Oyin",
"account_number":"1234567890",
"email": "taiwooyin@gmail.com",
"phone": "09089999999",
"amount": "500000",
"narration": "salary payment"
}
  
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Payment transfer initiated",
  "data": {"source_account_number":"3255613852316f2b4d4d796c344e38756339654972776f663745446e6d4c32486f455a4165374a476858343d",
  "transaction_amount":4500.25,
  "transfer_currency_indicator":"SOURCE_ACCOUNT_CURRENCY",
  "destination_account_number":"C$0003019202$AU$XX$01000540000001",
  "charge_bearer":"BENEFICIARY",
  "payment_method":"GIRO",
  "transferPurpose":"CASH_DISBURSEMENT"}
}
```

### HTTP Request

`POST /payments/{beneficiary_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
beneficiary_id | string | unique identifier of beneficiary

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
destination_account_number | string |beneficiary account number specified for payment
transaction_debit_amount | string | amount to debit from the drawee
currency | string |currency of payment
transaction_credit_amount | string |amount to credit the beneficiary
source_account_number | string |drawee account number specified for payment



## Retrieve Billers

This method retrieves a list of available billers

```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/billers"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
 
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "billers retrieved successfully",
  "data": {
		"billers": [ 
{ 
  “category_id”: “3”,
  “category_name”: “State Payments”, 
  "biller_id": 23,
  “biller_name”: “Abia State Infrastructural Development Agency”, 
 "product_id": 37, 
 "product_name": "Tax Payment",
 "product_plan": { "Item": "prepaid" } 
 },
 { 
  “category_id”: “2”,
  “category_name”: “Airtime Payments”, 
 "biller_id": 11, 
  “biller_name”: “Mtn”, 
 "product_id": 40,
 "product_name": "Mtn Yello",
 "product_plan": { "Item": "prepaid" } 
 }, 
 {
  “category_id”: “2”,
  “category_name”: “Airtime Payments”, 
 "biller_id": 14, 
  “biller_name”: “9mobile”, 
 "product_id": 41,
 "product_name": "Shine",
 "product_plan": { "Item": "prepaid" } 
 },
 { 
  “category_id”: “2”,
  “category_name”: “Airtime Payments”, 
 "biller_id": 13, 
  “biller_name”: “Glo”, 
 "product_id": 42, 
 "product_name": "Glo Berekete", 
 "product_plan": { "Item": "prepaid" } 
 }, 
 { 
  “category_id”: “2”,
  “category_name”: “Airtime Payments”, 
 "biller_id": 12, 
  “biller_name”: “Airtel”, 
 "product_id": 43, 
 "product_name": "WaZoBia",
 "product_plan": { "Item": "prepaid" } } ]
	}
}
```

### HTTP Request

`GET /payments/billers`



## Get Biller Payment Items

This method retrieves payment information for a biller 


```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/billers/456/paymentitems"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
 
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Biller Payment Items retrieved successfully",
  "data": {
	{"paymentitems": [
			{
				"category_id": "1",
				"biller_id": "905",
				"is_amount_fixed": false,
				"payment_item_id": "01",
				"payment_item_name": "Meter Token",
				"amount": "0",
				"biller_type": "PH",
				"code": "01",
				"currency": "NGN",
				"item_currency_symbol": "",
				"payment_code": "90501",
				"item_fee": "10000"
			}
		]
	}
}
```

### HTTP Request

`GET /payments/billers/{biller_id}/paymentitems`


### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Unique identifier of the biller


## Send Bill Payment Advice

This method is used to notify the biller of the payment


```Shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/billers/advices"
  -H "Authorization: XXXX-YYYYY"
  -H 'Content-Type: application/json'
  -d '{
	"payment_id":"3FTH0001",
	"payment_code":"xxxxyyyyy",
	"customer_id":"0000000001",
	"customer_mobile":"2348056731576",
	"customer_email":"iswtester2@yahoo.com",
	"amount":"360000",
	"account_number": "1234567890"
	}'
 
 
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Bill Payment Advice sent successfully",
  "data": 
	{
	"payment_id":"3FTH0001",
	"customer_id":"0000000001"
	}
}
```

### HTTP Request

`POST /payments/billers/advices`


### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
payment_id | string | Unique reference from payment creation
payment_code | string | Unique payment code retrieved from Get Biller Payment Items call
customer_id | string | Customer’s Unique Identifier
customer_mobile | string | Customer’s Mobile Number
customer_email | string | Customer’s Email Address
amount | string | Amount Paid by customer. Amount should be sent in lower denomination



## Retrieve Billers' Categories

This method retrieves all the biller category types


```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/billers/categories"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
 
```

> The above command returns JSON structured like this:

```json
{
“categories”: 
    [
	{“category_id”: “1”,
    “category_name”: “Utility Bills”, 
    “category_description”: “Pay your utility bills here”
	},
    {“category_id”: “2”,
    “category_name”: “Cable TV Bills”,
    “category_description”: “Pay for your cable TV subscriptions here”
	}
	]
}
```

### HTTP Request

`GET /payments/billers/categories`


### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
categories:category_id | string | 
categories:category_name | string | 
categories:category_description | string | 





## Initiate Payment to a Biller

initiate payment to a biller

```Shell
curl -X POST "https://api.singularapi.com/api/v1/payments/bills/initiate"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
    -H 'Content-Type: application/json'
    -d '{
        "source_account_number": "1234567890",
        "transaction_amount": 10000.34, 
        "transaction_currency_code": "NGN",  
        "transfer_date": "2021-01-13",
        "payment_code":"xxxxyyyyy", 
        "biller_id": 13, 
        “biller_name”: “Glo”, 
        "product_id": 42, 
        "product_name": "Glo Berekete",
        "biller_account_number": "3456754334", 
		"biller_bank_code": "58152052 "
    }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Payment initiated Successfully",
  "data": {
		"payment_id":"3FTH0001",
		"source_account_number": "1234567890",
		"biller_account_number": "3456754334", 
		"biller_bank_code": "58152052 ",
		"transaction":{
			"amount": 10000.34,
			"fee": 25.50,
			"currency_code": "NGN",
			"date": "2021-01-13"
		}
  }
}
```

### HTTP Request

`POST /payments/bills/initiate`
 

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
source_account_number | string | Source account number.
biller_account_number | string | Payee's account number
biller_account_name | string | Payee's account name
biller_bank_code | string | Bank Code of destination account
payment_code | string | Unique payment code retrieved from Get Biller Payment Items call
transaction_amount | string | Transaction amount
transaction_currency_code | string | Transaction currency code in ISO 4217 format.
transfer_date | string | (Optional). Transfer date in ISO 8601 format 'YYYY-MM-DD'
product_id | string | unique identifier of product
product_name | string | name of product



## Initiate International Payment

This API is used to initiate a new International Payment


```Shell
curl -X POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/international_transfers"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
	-H 'Content-Type: application/json'
	-d '{
  "source_account_id":"3255613852316f2b4d4d796c344e38756339654972776f663745446e6d4c32486f455a4165374a476858343d",
  "transaction_amount":4500.25,
  "transfer_currency_indicator":"SOURCE_ACCOUNT_CURRENCY",
  "payee_id":"C$0003019202$AU$XX$01000540000001",
  "charge_bearer":"BENEFICIARY",
  "payment_method":"GIRO",
  "fx_deal_reference_number":"12345678",
  "iban": "xxxxyyyyy",
  "transfer_purpose":"CASH_DISBURSEMENT"
  }'
```


> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": " Transfer successfully initiated",
  "data":{
	  "transaction_reference_id": "6e3774334f724a2b7947663653712f52456f524c41797038516a59347a437549564a77755676376e616a733d",
	  "debit_details": {
		"transaction_debit_amount": 10000.25,
		"currency_code": "AUD",
		"charges": 200
	  },
	  "credit_details": {
		"transaction_credit_amount": 10000.25,
		"currency_code": "USD",
		"charges": 100
	  },
	  "foreign_exchange_rate": 1.5461,
	  "transaction_fee": 25.25,
	  "fee_currency_code": "USD"
	}
}

```

### HTTP Request

`POST /payments/international_transfers`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
source_account_id | string | The source account identifier in encrypted format. 
transaction_amount | string | The transaction amount
transfer_currency_indicator | string | Indicator to specify whether the transfer is in source or destination account currency.
payee_id | string | The payee identifier in encrypted format. 
charge_bearer | string | Field to identify charge bearer.
payment_method | string | The acceptable forms of remittance for a given payments and transfer transaction.
fx_deal_reference_number | string | Fx deal reference number.
transfer_purpose | string | Purpose of transfer.



## Get International Payment Details

This API retrieves details of an International Payment.

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/international_transfers/3234567889y6t5434322/details"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
	-H 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Details of payment successfully read",
  "data":{
    "PaymentStatus": [
      {
        "transaction_reference_id": "string",
        "status": "Accepted",
        "status_update_date_time": "2020-12-22T11:13:45.197Z",
        "status_detail": {
          "local_instrument": "string",
          "status_reason": "Cancelled",
          "status_reason_description": "string"
        }
      }
    ]
	}
 }
```

### HTTP Request

`GET /payments/international_transfers/{transaction_reference_id}/details`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
transaction_reference_id | string | Unique identifier associated with the payment transaction



## Initiate bulk transfers

This API initiates a bulk transfer

```Shell
curl -X POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/bulk_transfers"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
	-H 'Content-Type: application/json'
	-d '{
    "sender_account_number": 22702983,
        "transfers": [
          {
            "amount": 1500,
            "label": "Your optional label",
            "beneficiary_name": "John Doe",
            "receiver_iban": "FR5410096000406142275577Q35",
            "client_reference": "3bc40e21-3ea5-4274-9744-c2f984f7072e"
          },
          {
            "amount": 2500,
            "beneficiary_name": "Cristen Patience",
            "receiver_iban": "FR0210096000404753378717C40",
            "client_reference": "fd5d81c5-4be2-412f-bb4d-5aa1db98dc99",

          },
          {
            "amount": 29999,
            "beneficiary_name": "Kaelyn Ebert",
            "receiver_iban": "FR4214508000507483296188O17",
          }
        ],
        "sender_account_number": 123456789
			}'
```


> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": " Transfer successfully initiated",
  "data":{
	  "bulk_transfer_id": "6e3774334f724a2b7947663653712f52456f524c41797038516a59347a437549564a77755676376e616a733d",
        "transfers": [
          {
            "amount": 1500,
            "label": "Your optional label",
            "beneficiary_name": "John Doe",
            "receiver_iban": "FR5410096000406142275577Q35",
            "client_reference": "3bc40e21-3ea5-4274-9744-c2f984f7072e"
          },
          {
            "amount": 2500,
            "beneficiary_name": "Cristen Patience",
            "receiver_iban": "FR0210096000404753378717C40",
            "client_reference": "fd5d81c5-4be2-412f-bb4d-5aa1db98dc99",

          },
          {
            "amount": 29999,
            "beneficiary_name": "Kaelyn Ebert",
            "receiver_iban": "FR4214508000507483296188O17",
          }
        ]
	}
}

```

### HTTP Request

`POST /payments/bulk_transfers`

Parameter | Type | Description
--------- | ------- | -----------
bulk_transfer_id | string | Unique identifier associated with the bulk payment transaction
sender_account_number | string | Account number of the sender.
transfers:amount | string | amount for a particular transaction in the bulk transfer payment.
transfers:label | string | descriptive information about the payment.
transfers:receiver_iban | string | Receiver information if the beneficiary is an unknown IBAN.
transfers:status | string |  status of a particular transfer process in the bulk transfer.
transfers:beneficiary_name | string | Name of beneficiary of a payment in the bulk transfer.
transfers:client_reference | string | Unique identifier of a beneficiary of a payment in the bulk transfer.
transfers:bank_name | string | Name of beneficiary's bank.
status | string | bulk transfer status.
created_at | string |  Time of bulk payment creation.
updated_at | string |  Time of bulk payment status update.





## Get a single bulk

This API returns the status of every transfer of a single bulk

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/bulk_transfers/5de1c4ef-895d-4a14-86a5-8e19adbf63c4"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
	-H 'Content-Type: application/json'

```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": " Bulk transfer status successfully retrieved",
  "data":{
    "bulk_transfer_id": "5de1c4ef-895d-4a14-86a5-8e19adbf63c4",
    "sender_account_number": 22702983,
    "transfers": [
        {
            "payment_id": "240t76g3-d1ed-46f1-3c15-fa63c339eed6",
            "amount": 29999.20,
          	"label": "This is a test",
			"receiver_iban": "FR90XXXXXXXXXXXXXXXXXXXXB25",
			"beneficiary_name": "John Doe",
			"bank_name": "Société Générale",
            "status": "succeeded",
            "created_at": "2020-08-17T15:56:57.000Z",
            "updated_at": "2020-08-17T15:57:10.000Z"
        },
        {
            "payment_id": "11d97b22-3e71-4578-a44o-2c3aa263bfv4",
            "amount": 1500.50,
            "label": "Label test",
            "receiver_iban": "FR20XXXXXXXXXXXXXXXXXXXXC44", // receiver information if the beneficiary is an unknown IBAN
            "status": "succeeded",
            "beneficiary_name": "Oyin Taiwo",
			"bank_name": "First Bank",
			"created_at": "2020-08-17T15:56:57.000Z",
            "updated_at": "2020-08-17T15:57:10.000Z"
        }
    ],
    "status": "succeeded",
    "created_at": "2020-08-17T15:56:57.000Z",
    "updated_at": "2020-08-17T15:57:10.000Z"
	}
}
```

### HTTP Request

`GET /payments/bulk_transfers/{bulk_transfer_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
bulk_transfer_id | string | Unique identifier associated with the bulk payment transaction

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
bulk_transfer_id | string | Unique identifier associated with the bulk payment transaction
sender_account_number | string | Account number of the sender.
transfers:amount | string | amount for a particular transaction in the bulk transfer payment.
transfers:label | string | descriptive information about the payment.
transfers:receiver_iban | string | Receiver information if the beneficiary is an unknown IBAN.
transfers:status | string |  status of a particular transfer process in the bulk transfer.
transfers:beneficiary_name | string | Name of beneficiary of a payment in the bulk transfer.
transfers:bank_name | string | Name of beneficiary's bank.
status | string | bulk transfer status.
created_at | string |  Time of bulk payment creation.
updated_at | string |  Time of bulk payment status update.







## Get a bulk transfer request

Allows you to get data from a transfer request and know if a transfer has been created from this request

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/bulk_transfers/requests/5de1c4ef-895d-4a14-86a5-8e19adbf63c4"
  -H "Authorization: XXXX-YYYYY-ZZZZZ"
	-H 'Content-Type: application/json'

```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": " bulk transfer request successfully retrieved",
  "data":{
		"id": "5de1c4ef-895d-4a14-86a5-8e19adbf63c4",
		"sender_account_number": 22702983,
	  "transfers": [
		{
		  "amount": 502.0,
		  "receiver_iban": "FR3430003000505147519957P95",
		  "beneficiary_name": "Pierre Dupont"
		  "label": "Refund"
		},
		{
		  "amount": 390.0,
		  "receiver_iban": "FR4730003000307192747741Y56",
		  "beneficiary_name": "Paul Fortin"
		},
		{
		  "amount": 32.88,
		  "receiver_iban": "FR4430003000701618295359B30",
		  "beneficiary_name": "Jacques Vaugard",
		}
	  ],
	  "bulk_transfer_id": "2e64b6d1-a685-4e89-9aed-1f304390fd52", 
	  "created_at": "2020-08-14T09:56:11.000Z",
	  "updated_at": "2020-08-14T09:56:11.000Z"
	}
}
```

### HTTP Request

`GET /payments/bulk_transfers/requests/{bulk_transfer_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
bulk_transfer_id | string | Unique identifier generated during initiation of the bulk transfer
id | string | Unique identifier generated during creation of the bulk transfer


## Retrieve Direct Debit Mandates


Retrieve Direct Debit Mandate(s). A single/multiple record(s) can be generated based on parameters supplied


```Shell
curl -X POST "https://api.singularapi.com/api/v1/payments/direct-debit"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"reference_id": "66733254776555",
		"amount" : 10,000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "1234567890"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}		
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Direct debit mandate on account retrieved successfully",
  "data": [
		{
			"reference_id": "66733254776555",
			"frequency": "Quarterly",
			"start_date": "2017-06-05",
			"end_date": "2017-06-05",
			"amount": 10000.00,
			"currency": "NGN",
			"source": {
				"account_number": "1234567890",
				"account_id": "5544332211"
			}, 
			"destination": {
				"scheme_name": "NUBAN",
				"account_name": "Felix John",
				"account_number": "1234567890",
				"sort_code": "7678999",
				"bank_code": "065",
			}, 
			"supplementary_data" : {
				"narration": "Payment for Ice Packs",
				"charge_bearer": "BEN",
				"destination_email": "fjohn@myemailaddress.com",
				"destination_phone": "090988888766",
				"advise_destination_email": "false",
				"advise_destination_phone": "false",
				"channel": "TP-API"
			}	
		}
	]
}
```

### HTTP Request

`POST /payments/direct-debit`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
reference_id | string | (Optional). Specify the id of a direct debit
amount | decimal | (Optional). Specify amount on mandate
currency | string | (Optional). Specify the payment currency from the list of possible options from the finance house (options ar NGN, USD, EUR, GBP)
source | object | Provide details of the of the originating account
source:account_number | string | Specify source account number
source:account_id | string | (Optional). Specify source account identification
destination | object | Provide details of the beneficiary account
destination:scheme_name | string | (Optional). Specifiy Banking Account Scheme Name. Options include NUBAN for Nigeria
destination:account_name | string | (Optional). Specify Account Holder Name
destination:account_number | string | (Optional). Specify Account number
destination:sort_code | string | (Optional). Specify Account Sort Code
destination:bank_code | string | (Optional). Specify Bank Code






## Set Up a Direct Debit Mandate

Create a direct debit mandate


Requires [validating direct debit mandate](#validate-a-direct-debit-mandate)


```Shell
curl -X POST "https://api.singularapi.com/api/v1/payment/direct-debit/new"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"frequency": "Quarterly",
		"amount" : 10,000.00,
		"start_date" : "2017-06-05",
		"end_date" : "2020-06-05",
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"meta_data" : {
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false"
		}
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Direct debit mandate on account is setup successfully",
  "data": {
		"reference_id": "6673325",
		"frequency": "Quarterly",
		"start_date": "2017-06-05",
		"end_date": "2020-06-05",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}	
	}
}
```

### HTTP Request

`POST /payments/direct-debit/new`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
frequency | string | Specify type of payment - NEFT, RTGS, Internal
start_date | date | Specify the date to initiate the direct debit in ISO 8601 format 'YYYY-MM-DD'
end_date | date | Specify the date to end the direct debit in ISO 8601 format 'YYYY-MM-DD'
amount | decimal | Specify amount to be transferred
currency | string | Specify an account currency from the list of possible options from the finance house (options ar NGN, USD, EUR, GBP)
source | object | Provide details of the of the originating account
source:account_number | string | Specify source account number
source:account_id | string | (Optional). Specify source account identification
destination | object | Provide details of the beneficiary account
destination:scheme_name | string | Specifiy Banking Account Scheme Name. Options include NUBAN for Nigeria
destination:account_name | string | Specify Account Holder Name
destination:account_number | string | Specify Account number
destination:sort_code | string | Specify Account Sort Code
destination:bank_code | string | Specify Bank Code
meta_data | object | Specify multiple type values information under this object


## Update a Direct Debit Mandate

Update direct debit mandate


Requires [validating direct debit mandate](#validate-a-direct-debit-mandate)


```Shell
curl -X PUT "https://api.singularapi.com/api/v1/payment/direct-debit/6673325"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"frequency": "Quarterly",
		"amount" : 10,000.00,
		"end_date" : "2020-06-05",
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"meta_data" : {
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false"
		}
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Direct debit mandate on account is setup successfully",
  "data": {
		"reference_id": "6673325",
		"frequency": "Quarterly",
		"start_date": "2017-06-05",
		"end_date": "2020-06-05",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}	
	}
}
```

### HTTP Request

`PUT /payments/direct-debit/{reference_id}`


### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
reference_id | string | Reference Id of the Direct Debit Mandate.

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
frequency | string | (Optional). Frequency of direct debit mandate
end_date | date | (Optional). Specify the date to end the direct debit in ISO 8601 format 'YYYY-MM-DD'
amount | decimal | (Optional). Specify amount to be transferred
currency | string | (Optional). Specify an account currency from the list of possible options from the finance house (options ar NGN, USD, EUR, GBP)
source | object | Provide details of the of the originating account
source:account_number | string | Specify source account number
source:account_id | string | (Optional). Specify source account identification
destination | object | Provide details of the beneficiary account
destination:scheme_name | string | (Optional). Specifiy Banking Account Scheme Name. Options include NUBAN for Nigeria
destination:account_name | string | (Optional). Specify Account Holder Name
destination:account_number | string | (Optional). Specify Account number
destination:sort_code | string | (Optional). Specify Account Sort Code
destination:bank_code | string | (Optional). Specify Bank Code
meta_data | object | (Optional). Specify multiple type values information under this object


## Validate a Direct Debit Mandate

Validate a direct debit mandate


```Shell
curl -X POST "https://api.singularapi.com/api/v1/payment/direct-debit/6673325/validate"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"frequency": "Quarterly",
		"amount" : 10,000.00,
		"start_date" : "2017-06-05",
		"end_date" : "2020-06-05",
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Direct debit mandate on account is setup successfully",
  "data": {
		"reference_id": "6673325",
		"frequency": "Quarterly",
		"start_date": "2017-06-05",
		"end_date": "2020-06-05",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}	
	}
}
```

### HTTP Request

`POST /payments/direct-debit/{reference_id}/validate`


### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
reference_id | string | Reference Id of the Direct Debit Mandate.

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
frequency | string | (Optional). Frequency of direct debit mandate
start_date | date | Specify the date to initiate the direct debit in ISO 8601 format 'YYYY-MM-DD'
end_date | date | (Optional). Specify the date to end the direct debit in ISO 8601 format 'YYYY-MM-DD'
amount | decimal | (Optional). Specify amount to be transferred
currency | string | (Optional). Specify an account currency from the list of possible options from the finance house (options ar NGN, USD, EUR, GBP)
source | object | Provide details of the of the originating account
source:account_number | string | Specify source account number
source:account_id | string | (Optional). Specify source account identification
destination | object | Provide details of the beneficiary account
destination:scheme_name | string | (Optional). Specifiy Banking Account Scheme Name. Options include NUBAN for Nigeria
destination:account_name | string | (Optional). Specify Account Holder Name
destination:account_number | string | (Optional). Specify Account number
destination:sort_code | string | (Optional). Specify Account Sort Code
destination:bank_code | string | (Optional). Specify Bank Code
meta_data | object | (Optional). Specify multiple type values information under this object


## Cancel a Direct Debit Mandate

Cancel direct debit mandate
Requires [validating direct debit mandate](#validate-a-direct-debit-mandate)


```Shell
curl -X DELETE "https://api.singularapi.com/api/v1/payment/direct-debit/6673325"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}
  }'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Direct debit mandate on account cancelled successfully",
  "data": {
		"reference_id": "6673325",
		"frequency": "Quarterly",
		"start_date": "2017-06-05",
		"end_date": "2020-06-05",
		"amount": 10000.00,
		"currency": "NGN",
		"source": {
			"account_number": "1234567890",
			"account_id": "5544332211"
		}, 
		"destination": {
			"scheme_name": "NUBAN",
			"account_name": "Felix John",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
		}, 
		"supplementary_data" : {
			"narration": "Payment for Ice Packs",
			"charge_bearer": "BEN",
			"destination_email": "fjohn@myemailaddress.com",
			"destination_phone": "090988888766",
			"advise_destination_email": "false",
			"advise_destination_phone": "false",
			"channel": "TP-API"
		}	
	}
}
```

### HTTP Request

`DELETE /payments/direct-debit/{reference_id}`


### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
reference_id | string | Reference Id of the Direct Debit Mandate.

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
source | object | Provide details of the of the originating account
source:account_number | string | Specify source account number
source:account_id | string | (Optional). Specify source account identification



## Retrieve Standing Order Mandates


## Set Up a Standing Order Mandate
Requires [validating standing order mandate](#validate-a-standing-order-mandate)


## Update a Standing Order Mandate
Requires [validating standing order mandate](#validate-a-standing-order-mandate)


## Cancel a Standing Order  Mandate
Requires [validating standing order mandate](#validate-a-standing-order-mandate)


## Validate a Standing Order Mandate
