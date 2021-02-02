# Merchants

Merchants APIs provide interfaces to manage merchants. Merchants, also referred to as billers, can be added to SingularAPI platform for receiving payments. The operations provide the convenience to handle bill payments and receipts of funds in any desired bank account associated with the biller. 

<aside class="notice">
All bank accounts added to a biller profile must be validated by the biller with the bank.
</aside>

<aside class="notice">
Billers are managed on Singular API Platform directly and the uri uses singular class ID 00234000000 for Nigeria.
</aside>

## Create New Biller

Create a new biller profile. This enables a merchant to register as a biller on the platform and create a biller profile.


```Shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"biller_name": "XYZ State Infrastructural Development Agency",
		"phone_number": "08180226678",
		"email": "info-ecommerce@mybusiness.org",
		"website": "",
		"address": "company address location",
		"city": "Abakaliki",
		"state": "Abia"
		"country": "Nigeria",
		"category_id": "001"
		"biller_type": "government",
		"business_type": "Public Utilities",
		"tos_acceptance": "true",
		"contacts": [
			{
				"name": "Philipa Johnson",
				"phone_number": 09000022333,
				"alternate_phone_number": "",
				"email": "philipa.johnson@mybusiness.org"
			},
			{
				"name": "Bendel Akpokpo",
				"phone_number": 01233444988,
				"alternate_phone_number": 06068776867,
				"email": "bendel.akpokpo@mybusiness.org"
			}
		]
  }'
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Biller added successfully",
	"data": {
		"biller_id": "001",
		"biller_name": "XYZ State Infrastructural Development Agency",
		"phone_number": "08180226678",
		"email": "info-ecommerce@mybusiness.org",
		"website": "",
		"address": "company address location",
		"country": "Nigeria",
		"category": {
			"category_id": "001",
			"category_name": "State Payments",
			"category_description": "Pay state allocated bills"
		},
		"biller_type": "government",
		"business_type": "Public Utilities",
		"default_account_id": "",
		"tos_acceptance": {
			"date": null,
			"ip": null
		},
		"contacts": [
			{
				"name": "Philipa Johnson",
				"phone_number": 09000022333,
				"alternate_phone_number": "",
				"email": "philipa.johnson@mybusiness.org"
			},
			{
				"name": "Bendel Akpokpo",
				"phone_number": 01233444988,
				"alternate_phone_number": 06068776867,
				"email": "bendel.akpokpo@mybusiness.org"
			}
		]
	}
}
```

### HTTP Request

`POST /merchants/billers`

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_name | string | Specify Biller Name.
phone_number | string |  Specify Biller contact number.
email | string | Specify Biller contact email address.
website | string | Optional. Specify Biller website url.
address | string | Specify Biller Street Address.
city | string | Specify Biller City.
state | string | Specify Biller State.
country | string | Specify Biller Country. This is a reference data field. Get valid values from [References Countries](/references/countries).
category_id | string | Specify ID of the category biller belongs to. This is a reference data field. Get valid values from [References Biller Categories](/references/categories).
business_type | string | Specify ID of the business type the biller belongs to. This is a reference data field. Get valid values from [References Business Types](/references/business_types).
biller_type | string | Specify Biller Type. Options are "individual", "corporate", "government".
tos_acceptance | boolean | Specify Acceptance of Terms of Service.  Options are "true" (to accept) or "false" (to decline).
contacts | array | Specify one or many contacts object(s) to be added to this biller
contacts:name | string | Specify Name of Biller Contact
contacts:phone_number | string | Specify Phone Number of Biller Contact
contacts:alternate_phone_number | string | Optional. Specify an Alternate Phone Number of Biller Contact
contacts:email | string | Specify Email Address of Biller Contact





## Retrieve Biller Details

This method retrieves biller details

```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers/001"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
 
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Biller details Retrieved successfully",
  "data": {
		"biller_id": "001",
		"biller_name": "Abia State Infrastructural Development Agency",
		"phone_number": "08180226678",
		"email": "infrastructure@engineering.com",
		"address": "company address location",
		"country": "Nigeria",
		"category": {
			"category_id": "001",
			"category_name": "State Payments",
			"category_description": "Pay state allocated bills"
		},
		"default_account_id": "",
		"biller_type": "corporate",
		"accounts": [],
		"products": [],
		"created": "2019-09-12"
		
	}	
 
}
```

### HTTP Request

`GET /merchants/billers/{biller_id}`


### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller Identification Number



## Update a Biller

Update a biller profile. This method allows updating one or more parameters on a biller profile. 


```Shell
curl -x PUT "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers/001"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"biller_name": "XYZ State Infrastructural Development Agency",
		"phone_number": "08180226678",
		"email": "info-ecommerce@mybusiness.org",
		"address": "company address location",
		"city": "Abakaliki",
		"state": "Abia"
		"country": "Nigeria",
		"category_id": "001",
		"default_account_id": "00209099",
		"biller_type": "individual"
	}'
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Biller Updated successfully",
	"data": {
		
		"biller_id": "001",
		"biller_name": "XYZ State Infrastructural Development Agency",
		"phone_number": "08180226678",
		"email": "infrastructure@engineering.com",
		"address": "company address location",
		"country": "Nigeria",
		"default_account_id": "00209099",
		"category": {
			"category_id": "001",
			"category_name": "State Payments",
			"category_description": "Pay state allocated bills"
		},
		"biller_type": "individual"	
	}
}
```

### HTTP Request

`PUT /merchants/billers/{biller_id}`


### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller identification number.


### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_name | string | Specify Biller Name.
phone_number | string |  Specify Biller contact number.
email | string | Specify Biller contact email address.
address | string | Specify Biller Street Address.
city | string | Specify Biller City.
state | string | Specify Biller State.
country | string | Specify Biller Country. This is a reference data field. Get valid values from [References Countries](/references/countries).
category_id | string | Specify Category ID of the category biller belongs to. This is a reference data field. Get valid values from [References Biller Categories](/references/categories).
biller_type | string | Specify Biller Type. Options are "individual", "corporate", "government".
default_account_id | string | Specify the account identification number of a verified account. Only verified accounts, denoted "valid" on status parameter, can be made default account for biller.



## Add Accounts to Biller

Add one or more bank accounts to a biller. This operation associates financial accounts with a biller for the purpose of receiving payments. Any account added must be validated.


```Shell
curl -x PUT "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers/001/accounts"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
	accounts:[
		{
			"scheme_name": "NUBAN",
			"account_name": "XYZ State IDA",
			"account_number": "1234567890",
			"sort_code": "7678999",
			"bank_code": "065",
			"currency": "NGN",
			"country": "Nigeria",
			"account_type": "current",
			"alias": "Alpha Account",
			"priority": 1
			"is_active": true
		}
	]
}'
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Bank Account(s) added successfully",
	"data": {
		"biller_id": "001",
		"biller_name": "XYZ State Infrastructural Development Agency",
		"default_account_id": "",
		"accounts": [
			{
				"account_id": "00209099",
				"scheme_name": "NUBAN",
				"account_name": "XYZ State IDA",
				"account_number": "1234567890",
				"sort_code": "7678999",
				"bank_code": "065",
				"currency" : "NGN",
				"country" : "Nigeria",
				"account_type": "current",
				"alias" : "Alpha Account",
				"priority" : 1,
				"is_active": "true",
				"status": "pending"
			}
		]
	}
}
```

### HTTP Request

`PUT /merchants/billers/{biller_id}/accounts`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller identification number

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
accounts | string | Specify one or many accounts object(s) to be added to this biller.
accounts:scheme_name | string | Specify Banking Account Scheme Name. Options include NUBAN for Nigeria.
accounts:account_name | string | Specify Account Holder Name.
accounts:account_number | string | Specify Account number.
accounts:sort_code | string | Specify Account Sort Code.
accounts:bank_code | string | Specify Bank Code. This is a reference data field. Get valid values from [References Banks](/references/banks).
accounts:currency | string | Specify Account Currency. This is a reference data field. Get valid values from [References Currencies](/references/currencies).
accounts:country | string | Specify Account Country. This is a reference data field. Get valid values from [References Countries](/references/countries).
accounts:alias | string | Optional. Specify Account Alias (or Reference Name).
accounts:priority | integer | Specify Account Priority Number. A lower priority number will be preferred if multiple active accounts exist in the same bank.
accounts:default | string | Specify Account Biller status
accounts:is_active | string | Specify the Account Status. Options are (true, false)





## Update Account on Biller

Update an account on a biller. This method updates an account information on a biller only when it is not yet validated. Once an account is validated (status is "validated") its paramaters can no longer be updated with the exception of two parameters - "priority" and "is_active".


```Shell
curl -x PUT "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers/001/accounts/00209099"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
        "scheme_name": "NUBAN",
        "account_name": "XYZ State IDA",
        "account_number": "1234567890",
        "sort_code": "7678999",
        "bank_code": "065",
        "currency" : "NGN",
        "country" : "Nigeria",
        "account_type": "current",
        "alias" : "Alpha Account",
        "priority" : 1,
        "is_active": "true"
    }'
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Bank Account updated successfully",
	"data": {
		"biller_id": "001",
		"biller_name": "XYZ State Infrastructural Development Agency",
		"accounts": [
			{
				"account_id": "00209099",
				"scheme_name": "NUBAN",
				"account_name": "XYZ State IDA",
				"account_number": "1234567890",
				"sort_code": "7678999",
				"bank_code": "065",
				"currency" : "NGN",
				"country" : "Nigeria",
				"account_type": "current",
				"alias" : "Alpha Account",
				"priority" : 1,
				"is_active": "true",
				"status": "validated"
			}
		]
	}
}
```

### HTTP Request

`PUT /merchants/billers/{biller_id}/accounts/{account_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller identification number.
account_id | string | Specify account reference identification number.

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
scheme_name | string | Optional. Specify Banking Account Scheme Name. Options include NUBAN for Nigeria.
account_name | string | Optional. Specify Account Holder Name.
account_number | string | Optional. Specify Account number.
sort_code | string | Optional. Specify Account Sort Code.
bank_code | string | Optional. Specify Bank Code. This is a reference data field. Get valid values from [References Banks](/references/banks).
currency | string | Optional. Specify Account Currency. This is a reference data field. Get valid values from [References Currencies](/references/currencies).
country | string | Optional. Specify Account Country. This is a reference data field. Get valid values from [References Countries](/references/countries).
alias | string | Optional. Specify Account Alias (or Reference Name).
priority | integer | Optional. Specify Account Priority Number. A lower priority number will be preferred if multiple active accounts exist in the same bank.
is_active | string | Optional. Specify the Account Status. Options are (true, false). Setting the value suspends the use of the account.

<aside class="info">
To suspend the use of a biller account, set the parameter "is_active" to value false.
</aside>






## Retrieve Accounts on Biller

Retrieve details of accounts on a biller. This method fetches all bank accounts on a biller irrespective of the status of the account. A filter may however be added to limit based on "currency", "country", "is_active" or "status".


```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers/001/accounts"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Accounts retrieved successfully",
	"data": {
		"accounts": [
			{
				"biller_account_id": "001",
				"scheme_name": "NUBAN",
				"account_name": "Maya James",
				"account_number": "1100897675",
				"sort_code": "7678999",
				"bank_code": "065",
				"priority" : 1,
				"is_active": "true",
				"status": "validated"	
			},
			{
				"biller_account_reference_id": "002",
				"account_name": "Felix John",
				"scheme_name": "NUBAN",
				"account_number": "1234567890",
				"sort_code": "7678999",
				"bank_code": "065",
				"priority" : 2,
				"is_active": "false",
				"status": "pending"
			}
		]
		
	}
}
```

### HTTP Request

`GET /merchants/billers/{biller_id}/accounts`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller identification number






## Retrieve Billers

Retrieve Billers on the platform. This method retrieves a list of all billers registered on SingularAPI platform for a specific country within the financial domain.

```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
 
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Billers Retrieved successfully",
  "data": [ 
	{
		"biller_id": "001",
		"biller_name": "Abia State Infrastructural Development Agency",
		"phone_number": "08180226678",
		"email": "infrastructure@engineering.com",
		"address": "company address location",
		"country": "Nigeria",
		"category": {
			"category_id": "001",
			"category_name": "State Payments",
			"category_description": "Pay state alocated bills"
		},
		"biller_type": "individual"
	},
	
	{
		"biller_id": "002",
		"biller_name": "MTN",
		"phone_number": "080320000001",
		"email": "itech@mtn.com",
		"address": "company address location",
		"country": "Nigeria",
		"category": {
			"category_id": "004",
			"category_name": "Airtime Vending",
			"category_description": "Pay for your network airtime"
		},
		"biller_type": "corporate"
	},
	
	{
		"biller_id": "003",
		"biller_name": "ikeja Disco",
		"phone_number": "080320033301",
		"email": "product@ikejadisco.com",
		"address": "company address location",
		"country": "Nigeria",
		"category": {
			"category_id": "005",
			"category_name": "Electricity",
			"category_description": "Pay for your electricity units"
		},
		"biller_type": "corporate"
	}
	]
}	

```

### HTTP Request

`GET /merchants/billers`




## Retrieve Biller Categories

This method retrieves all biller categories


```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000000/merchants/biller-categories"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Biller categories retrieved successfully",
	"data": {
		"categories": [
			{
				"category_id": "001",
				"category_name": "State Payments",
				"category_description": "Pay state allocated bills"
			},
			
			{
				"category_id": "002",
				"category_name": "Utility Bills",
				"category_description": "Pay your utility bills here"
			},

			{
				"category_id": "003",
				"category_name": "Cable TV Bills",
				"category_description": "Pay for your cable TV subscriptions here"
			},
			
			{
				"category_id": "004",
				"category_name": "Airtime Vending",
				"category_description": "Pay for your network airtime"
			},
			
			{
				"category_id": "005",
				"category_name": "Electricity",
				"category_description": "Pay for your electricity units"
			}
		]
		
	}
}
```

### HTTP Request

`GET /merchants/biller-categories`






## Retrieve Billers by category

This method retrieves billers by category


```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000000/merchants/billers?categories=004"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Billers Retrieved successfully",
  "data": [ 			
			{
				"biller_id": "002",
				"biller_name": "MTN",
				"phone_number": "080320000001",
				"email": "itech@mtn.com",
				"address": "company address location",
				"country": "Nigeria",
				"category": {
					"category_id": "004",
					"category_name": "Airtime Vending",
					"category_description": "Pay for your network airtime"
				},
				"default_account_id": "",
				"biller_type": "corporate"
			}	
	]
}
```

### HTTP Request

`GET /merchants/billers?category={category_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
category_id | string | Specify category identification







## Add Products to Biller

This method adds a new product to a biller


```Shell
curl -x POST "https://api.singularapi.com/api/v1/finance/00234000000/finance/00234000000/merchants/billers/001/products"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
  -d '{
		"product_name": "Prepaid"
		"products": [
			{ "product_name": "Prepaid" },
			{ "product_name": "Postpaid" },
			{ "product_name": "Token Purchase" }
		]
	}'
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Product added to biller successfully",
	"data": {
		"biller_id": "003",
		"biller_name": "ABC Disco",
		"products":  [
			{
				"product_id": "009",
				"product_name": "Prepaid"
			},
			{
				"product_id": "010",
				"product_name": "Postpaid"
			},
			{
				"product_id": "011",
				"product_name": "Token Purchase"
			}
		
		]
		
	}
}
```

### HTTP Request

`POST /merchants/billers/{biller_id}/products`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller identification number

### Body Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
products | array object | Specify product item(s) to be added
product_name | string | Specify product name









## Retrieve Products on Biller

This method retrieves all products on a biller


```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000000/finance/00234000000/merchants/billers/001/products"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
 
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Products retrieved successfully",
	"data": {
		"biller_id": "003",
		"biller_name": "ikeja Disco",
		"products": [
			{
				"product_id": "010",
				"product_name": "Postpaid"
			},
						
			{
				"product_id": "011",
				"product_name": "Token Purchase"
			}
		]
	
	}
		
}
```

### HTTP Request

`GET /merchants/billers/{biller_id}/products`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller identification number





## Retrieve Product Details

This method retrieves details of a product


```Shell
curl -x GET "https://api.singularapi.com/api/v1/finance/00234000000/finance/00234000000/merchants/billers/003/products/656677"
  -H "Authorization: token-obtained-from-authorization"
  -H 'Content-Type: application/json'
 
```

> The above command returns JSON structured like this:

```json
{
	"status_code": "00",
	"message": "Product details retrieved successfully",
	"data": {
		"biller_id": "003",
		"biller_name": "Kiakia Disco",
		"phone_number": "080320033301",
		"email": "product@kiakiadisco.com",
		"website": "http://www.kiakiadisco.com",
		"address": "company address location",
		"city": "Funtua",
		"state": "Kaduna",
		"country": "Nigeria",
		"category_id": "002",
		"biller_type": "corporate",
		"business_type": "Public Utilities",
		"tos_acceptance": "true",
		"product": {
			"product_id": "656677",
			"product_name": "Token Purchase",
			"product_description": "Generic Token Puchase",
			"product_meta": {}
		}
	}
}
```

### HTTP Request

`GET /merchants/billers/{biller_id}/products/{product_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
biller_id | string | Specify Biller identification number
product_id | string | Specify Product identification number
