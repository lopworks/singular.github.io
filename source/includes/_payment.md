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

Retrieve detailed information on a payment transaction.


```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/66733254776555"
  -H "Authorization: token-obtained-from-authorization"
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

`GET /payments/{payment-id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
payment_id | string | Specify payment identification returned from payment request

### Query Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
account_number | string | Specify source account number


## Retrieve all Payment Transactions
## Validate a Payment Transaction

## Cancel a Payment Transaction

## Retrieve all Beneficiaries

## Add a Beneficiary

Requires [validating beneficiary management](#validate-beneficiary-management)


## Update a Beneficiary

Requires [validating beneficiary management](#validate-beneficiary-management)

## Delete a Beneficiary

Requires [validating beneficiary management](#validate-beneficiary-management)

## Validate Beneficiary Management
## Initiate Payment to a Beneficiary

## Retrieve Billers

## Retrieve Billers' Categories

## Initiate Payment to a Biller

## Retrieve Direct Debit Mandates

## Set Up a Direct Debit Mandate
Requires [validating direct debit mandate](#validate-a-direct-debit-mandate)

## Update a Direct Debit Mandate
Requires [validating direct debit mandate](#validate-a-direct-debit-mandate)

## Cancel a Direct Debit Mandate
Requires [validating direct debit mandate](#validate-a-direct-debit-mandate)

## Validate a Direct Debit Mandate

## Retrieve Standing Order Mandates
## Set Up a Standing Order Mandate
Requires [validating standing order mandate](#validate-a-standing-order-mandate)
## Update a Standing Order Mandate
Requires [validating standing order mandate](#validate-a-standing-order-mandate)
## Cancel a Standing Order  Mandate
Requires [validating standing order mandate](#validate-a-standing-order-mandate)
## Validate a Standing Order Mandate
