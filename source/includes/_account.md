# Accounts

Accounts APIs provide interfaces to manage customer accounts. They comprise of the following operations:

- Account Setup: Manage the lifecycle of an account: create, reactivate or close
- Account Information: Obtain information on details, transfers and other activites
- Account Instruction: Set up instructions or initiate requests on an account



## Create new account

Create a new financial account.

```Shell
curl -X POST "https://api.singularapi.com/api/v1/finance/00234000054/accounts/"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
	-d '{
		"title": "Mr", 
		"first_name": "John", 
		"middle_name": "Felix", 
		"last_name": "Thompson", 
		"gender": "male", 
		"date_of_birth": "1992-03-17", 
		"address": "3 Silver Court Plaza, Agungi Estate", 
		"city": "Lekki", 
		"country": "Nigeria", 
		"nationality": "Nigerian", 
		"email": "king_felix@me.com", 
		"account_type": "savings", 
		"currency": "NGN", 
		"bvn": "1234567890"
	}'
```


> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Account created successfully",
  "data": {
	  "account_number": "0123456784",
	  "account_id": "0123456784",
	  "name": "Abisola Fadekemi Adeyemi"
  }
}
```

### HTTP Request

`POST /accounts`

### Body Parameters

Parameter | Type | Description
--------- | ------- | -----------
title | string | Specify Account Holder Formal title
first_name | string | Specify Account Holder First Name
middle_name | string | Optional. Specify Account Holder Middle Name
last_name | string | Specify Account Holder Last Name
gender | string | Specify Account Holder Gender
date_of_birth | string | Specify Account Holder Date of Birth
address | string | Specify Account Holder Street Address
city | string | Specify Account Holder City
country | string | Specify Account Holder Country
nationality | string | Specify Account Holder Nationality
email| string | Specify Account Holder Email Address
phone_number| string | Specify Account Holder Phone Number
account_type| string | Specify Account Holder Type of Account
currency | string | Choose an account currecny from the list of possible options from the finance house (options ar NGN, USD, EUR, GBP)
BVN | string | Bank verification number Required mainly for account opening in Nigeria



<aside class="notice">
To open a quick account with limited facilities in Nigeria, send only a customer BVN in the body parameter.
</aside>



## Reactivate an account

Reactivate an existing account.

```Shell
curl -X PUT "https://api.singularapi.com/api/v1/finance/00234000054/accounts/0099332211/reactivate"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
	-d '{
		"kyc_session_id": "8767764439", 
		"account_id": "939388374747", 
	}'
```


> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Account reactivated successfully",
  "data": {
		"account_number": "0099332211",
		"account_id": "939388374747",
		"account_status": "active"
  }
}
```

### HTTP Request

`PUT /accounts/{account_number}/reactivate`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
kyc_session_id | string | (Optional). Specify a session ID for a KYC Submission. Implementation is dependent on the financial instittution
account_id | string | (Optional). Specify Account Holder Account ID



## Retrieve account details

Retrieve details of an account.


```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/accounts/1010119934"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Account Details retrieved successfully",
  "data": {
	  "account_number": "1010119934",
	  "account_id": "878788909876",
		"name": "Ado John Sule",
		"currency": "NGN",
	  "current_balance": 1232321.98,
		"book_balance": 1332321.98,
		"account_opening_date": "2017-01-13",
		"last_transaction_date": "2019-03-15T07:05:59.524Z",
		"account_type": "Savings",
		"phone_number": "09091234567",
		"email": "ado.john@example.com",
		"account_status": "Active",
		"customer_id": "123222132"
	}
 }
```

### HTTP Request

`GET /accounts/{account_number}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account Number

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_id | string | (Optional). Specify Account Holder Account ID



## Retrieve summary of all accounts

Retrieves all accounts belonging to a customer.

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/accounts/0099332211/summary"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "All account(s) retrieved successfully",
  "data": {
	"name": "Ado John Sule",
	"phone_number": "09091234567",
	"email": "ado.john@example.com",
	"customer_id": "123222132",
	"accounts":[
		{
			"account_number": "1010119934",
			"account_id": "878788909876",
			"currency": "NGN",
			"current_balance": 1232321.98,
			"book_balance": 1332321.98,
			"last_transaction_date": "2019-03-15T07:05:59.524Z",
			"account_type": "Savings",
			"account_status": "Active",
		},
		{
			"account_number": "3455556721",
			"account_id": "",
			"currency": "EUR",
			"current_balance": 543.00,
			"book_balance": 543.00,
			"last_transaction_date": "2016-02-05T18:21:05.619Z",
			"account_type": "Savings",
			"account_status": "Inactive",
		}
	]
  }
}
```

### HTTP Request

`GET /accounts/{account_number}/summary`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_id | string | (Optional). Specify Account Holder account number



## Retrieve transaction history

Retrieve transaction history of a given account as an array of transactions. Depending on implementation and request parameters sent, you may get different response details.

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/accounts/1234567890/transactions"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Successfully Retrieve Transactions",
  "data": {
		"transactions": [
		  {
			"transaction_id": "1653372928889",
			"transaction_date": "2017-09-03",
			"transaction_amount": 8900.45,
			"currency": "NGN",
			"transaction_type": "debit",
			"transaction_status": "Approved",
			"transaction_description": "Payment for UTIL/879811AA",
			"transaction_reference": "Paid for Electricity"
		  },
		  {
			"transaction_id": "8d82f1c6-c772-454b-bf11-4a7790cac887",
			"transaction_date": "2018-09-10",
			"amount": 3000.00,
			"currency": "NGN",
			"transaction_type": "debit",
			"transaction_status": "Failed",
			"transaction_description": "LAG/1546 - Fee for Exit Toll",
			"transaction_reference": "LAG/1546 - Fee for Exit Toll"
		  }
		]
  }
}
```

### HTTP Request

`GET /accounts/{account_number}/transactions`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
transaction_from_date | string | Starting range date for transactions in ISO 8601 format 'YYYY-MM-DD'
transaction_to_date | string | Ending range date for transactions in ISO 8601 format 'YYYY-MM-DD'
last_number_of_transactions | string | (Optional) Specify last number of transactions

<aside class="notice">
Most financial institutions have different request requirements
- some require either transaction_from_date or both transaction_from_date and transaction_to_date
</aside>





## Get account activity statement

Retrieve the activity statement on an account

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/accounts/1234567890/statement"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```


> The above command returns JSON structured like this:

```json
{
  "statusCode": 00,
  "message": "Account Statement Retrieved",
  "data": {
		"account_number": "1234567890",
		"available_balance": 1000900.45,
		"book_balance": 1000900.45,
		"currency": "NGN",
		"transactions": [
		  {
			"posted_date": "2017-09-03",
			"transaction_id": "5GH788HG89K",
			"transaction_date": "2017-09-03",
			"transaction_description": "PAYT FROM XYZ INDIVIDUAL",
			"transaction_type": "debit",
			"amount": 8900.45,
			"balance": 1000900.45,
			"currency": "NGN"
		  },
		  {
			"posted_date": "2017-09-03",
			"transaction_id": "345556012334",
			"transaction_date": "2017-09-03",
			"transaction_description": "PAYT FROM XYZ INDIVIDUAL",
			"transaction_type": "credit",
			"amount": 3000.00,
			"balance": 1003900.45,
			"currency": "NGN"
		  }
		]
  }
}
```

### HTTP Request

`GET /accounts/{account_number}/statement`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
from_date | string | Required. Starting range date for statement in ISO 8601 format 'YYYY-MM-DD'
to_date | string | Required. Ending range date for statement in ISO 8601 format 'YYYY-MM-DD'
transaction_type | string | Optional. Specify type of transactions to be included - debit, credit or both (default)
delivery_format | string | Optional. Specify format of the response received. Options are json (default), csv
delivery_channel | string | Optional. Specify channel for delivery. Options are online (default), email (requires supplying delivery_email as a parameter)
delivery_email | string | Required if delivery_channel is email. Specify Email Address to receive statement.



## Get account balance

Retrieve balance of a specified account.

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/accounts/1234567890/balance"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Account balance retrieved successfully",
  "data": {
		"account_number": "1234567890",
		"account_id": "",
		"currency": "NGN",
		"available_balance": 800000.00,
		"book_balance": 800000.00
  }
}
```

### HTTP Request

`GET /accounts/{account_number}/balance`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number



## Get account beneficiaries details

Retrieve saved beneficiaries on an account.

```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/accounts/1234567890/beneficiaries"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```


> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Beneficiary details retrieved successfully",
  "data": [
		{
			"account_id": "",
			"beneficiary_id": "",
			"reference": "",
			"beneficiary_name": "Afus Jide",
			"bank_name": "",
			"bank_code": "",
			"sort_code": "",
			"account_number": "1234567890",
			"iban": "",
			"routing_number": "",
			"bank_address": "",
			"bank_city": "",
			"bank_state": "",
			"bank_country": "Nigeria",
			"beneficiary_address": "",
			"beneficiary_city": "",
			"beneficiary_state": "",
			"beneficiary_country": "",
			"supplementary_data": ""
		},
		{
			"account_id": "",
			"beneficiary_id": "",
			"reference": "Club Payments Monthly",
			"beneficiary_name": "Bimbola Ahmed",
			"bank_name": "XYZ Bank",
			"bank_code": "098",
			"sort_code": "349087",
			"account_number": "0987654321",
			"iban": "",
			"routing_number": "",
			"bank_address": "",
			"bank_city": "",
			"bank_state": "",
			"bank_country": "Nigeria",
			"beneficiary_address": "",
			"beneficiary_city": "",
			"beneficiary_state": "",
			"beneficiary_country": "",
			"supplementary_data": ""
		}
  ]
  
}
```

### HTTP Request

`GET /accounts/{account_number}/beneficiaries`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_id | string | (Conditional). Some financial institutions require specifying Account Holder account number



## Initiate an account instruction

Give an instruction on an account.

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/1234567890/instruction"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Standing instruction created successfully",
  "data": {
		"account_number": "1234567890",
		"account_id": "1234567890",
		"instruction_number": "6789029286354"
  }
}
```

### HTTP Request

`POST /accounts/{account_number}/instruction`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number

### Body Parameters

Parameter | Type | Description
--------- | ------- | -----------
amount | string | Specify Amount
startDate | string | Specify effective start date
endDate | string | Specify termination date of instruction
remit_account_id | string | Specify Account to be credited

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>





## Manage account standing order

Manage account standing order

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/1234567890/sorder"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Standing order created successfully",
  "data": {
		"account_number": "1234567890",
		"account_id": "1234567890",
		"reference_id": "6789029286354"
  }
}
```

### HTTP Request

`POST /accounts/{account_number}/sorder`

### Path Parameters

Parameter | Type | Description
--------- | ------- | -----------
account_number  | string | Specify Account Holder First Name

### Body Parameters

Parameter | Type | Description
--------- | ------- | -----------
amount | string | Specify Amount
start_date | string | Specify effective start date
end_date | string | Specify termination date of a standing order
frequency | string | (Optional). frequency of payment between the start and end dates 
narration | string | (Optional). Purpose for the standing order
beneficiary_name | string | Name of the beneficiary to the standing order
beneficiary_account | string | Account Id/number of the beneficiary to the standing order

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>




## Obtain account rates

Retrieve the rate on an account.

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/1234567890/rate"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Account rate retrieved successfully",
  "data": {
		"account_number": "1234567890",
		"account_id": "1234567890",
		"account_type": "Savings",
		"rate": 0.75
  }
}
```

### HTTP Request

`GET /accounts/{account_number}/rate`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_id | string | (Optional). Specify the account number 


<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>







## Get account product details

Get account product details

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/1234567890/product"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
	"account_number": "1010119934",
	"account_id": "1010119934",
	"products":[
		{
		  "account_type": "Eazy Savings",
		  "currency": "NGN",
		  "status": "Active"
		},
		{
		  "account_type": "Visa Account",
		  "currency": "NGN",
		  "status": "Expire"
		}
	]
}
```

### HTTP Request

`GET /accounts/{account_number}/product`

### Path Parameters

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify the account number

### Query Parameters

Parameter | Type | Description
--------- | ------- | -----------
account_id | string | (Optional). Specify the account number 

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>





## Retrieve account's transaction history Details

Retrieve transaction details data associated with a transactionReferenceId

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/v1/accounts/{account_number}/transactions/{transactionReferenceId}"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Successful",
  "data": {
		
		  "account_number": "XXXXXX2364",
		  "bank_name": "HSBC Bank",
		  "transaction_type": "TRANSFER",
		  "transaction_description": "INTEREST PAYMENT",
		  "amount": 50.55,
		  "currency": "NGN",
		  "transaction_date": "2017-12-21",
		  "transaction_fee_type": "INTEREST",
		  "transaction_fee": 15.15,
		  "transaction_status": "NEW",
		  "transaction_posting_date": "2017-26-12",
		  "transaction_reference_number": "889409390NM8300",
		  "customer_name": John Smith,
		  
		  "beneficiary_bank_details": {
			"full_name": "Albert Neigh",
			"account_number": "XXXXXX2391",
			"bank_name": "HSBC Bank"
		  }		  
		
  }
}
```

### HTTP Request

`GET /accounts/{account_number}/transactions/{transactionReferenceId}

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify Account Holder account number
transaction_reference_id | string | Reference Id to uniquely identify the transaction.This is applicable for successful transactions.

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_id | string | (Optional). Specify Account Holder account number

<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>



## Retrieve issued devices details

Retrieve details about issued devices or inventory .

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/issuedDevice/IDIR795386"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Issued device details retrieved successfully",
  "data": {
		  "issuedDeviceInstanceRecord": {
			"issuedDeviceType": "string",
			"issuedDeviceDescription": "string",
			"issuedDeviceProperty": {
			  "issuedDevicePropertyType": {
				"issuedDevicePropertyValue": "string"
			  },
			  "issuedDeviceStatus": "string"
			}
		  }
		}
 }
```

### HTTP Request

`GET /accounts/issuedDevice/{reference_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
issuedDeviceInstanceReference | string |Reference to the Issued Device instance


<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>



## Initiate service fees 

Initiate service fees on an account product

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/account/servicefees/initiation"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Service fee initiated successfully",
  "data": {
			"date": "09-22-2018"
			  "reference_id": "SFIR735161",
			  "serviceFeesInstanceReference": "SFIAR706075",
			  "serviceFeesInstanceStatus": "string",
			  "serviceFeesInstanceRecord": {
				"feeConfigurationProfile": {
				  "feeDefinition": "string"
				}
			  }
			}
  

 }
```


### HTTP Request

`POST /accounts/account/servicefees/initiation`

### Body Parameters

Parameter | Type | Description
--------- | ------- | -----------
product_reference | string | productInstanceReference
savingsAccountNumber | string | savingsAccountNumber
accountType | string | accountType
accountCurrency | string | accountCurrency
taxReference | string | taxReference
date | string | date
linkedAccounts.linkType | string | date
linkedAccounts.accountDetails | string | date



<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>



## Retrieve account lien details.

Retrieve details about an active account lien .

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/123456/lien​/4567"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json


{
  "status_code": 00,
  "description": "Successful",
  "message": "Account lien details retrieved successfully",
  "data": {
    "lien_type": "string",
    "lien_definition": "string",
    "lienRecord": {
      "lien_originator": "string",
      "lien_purpose": "string",
      "lien_amount": "USD 250",
      "lien_start_date": "09-22-2018",
      "lien_expiry_date": "09-22-2018",
      "lien_status": "string"
    }
  }
 }
```


### HTTP Request

`GET /accounts/{account_number}/lien​/{lien_id}`



<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>




## Request device changes or replacement

Request changes or replacement devices or inventory.

```ruby
require 'kittn'

api = Kittn::APIClient.authorize!('meowmeowmeow')
api.kittens.get(2)
```

```python
import kittn

api = kittn.authorize('meowmeowmeow')
api.kittens.get(2)
```

```shell
curl "http://example.com/accounts/issuedDevice​/requisition"
  -H "Authorization: meowmeowmeow"
```

```javascript
const kittn = require('kittn');

let api = kittn.authorize('meowmeowmeow');
let max = api.kittens.get(2);
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "description": "Successful",
  "message": "Issued device details retrieved successfully",
  "data": {
  "issuedDeviceInstanceRecord": {
    "issuedDeviceDescription": "string",
    "issuedDeviceProperty": {
      "issuedDevicePropertyType": {
        "issuedDevicePropertyValue": "string"
      },
      "issuedDeviceStatus": "string"
    }
  },
  "requestResponseRecord": {}
}

```

### HTTP Request

`PUT /accounts/issuedDevice​/requisition`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
issuedDeviceInstanceReference | string |Reference to the Issued Device instance
issuedDeviceType | string |Reference to the Issued Device instance
issuedDeviceStatus | string |Reference to the Issued Device instance


<aside class="success">
Remember — a happy kitten is an authenticated kitten!
</aside>




