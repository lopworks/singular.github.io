# Payments

Payments provide interfaces to manage financial transations and payments. They comprise of the following operations:

- Domestic Payments: 
- International Payments: 



## Domestic Payments

Create Domestic Payment Consents.

```Shell
curl -X POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/domestic-payment-consents"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
	-d '{
  "Data": {
		"read_refund_account": "No",
		"initiation": {
		  "instruction_identification": "string",
		  "end_to_end_identification": "string",
		  "local_instrument": "string",
		  "instructed_amount": {
			"amount": "string",
			"currency": "string"
		  },
		  "debtor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_postal_address": {
			"address_type": "Business",
			"department": "string",
			"sub_department": "string",
			"street_name": "string",
			"building_number": "string",
			"post_code": "string",
			"town_name": "string",
			"country_sub_division": "string",
			"country": "string",
			"address_line": [
			  "string"
			]
		  },
		  "remittance_information": {
			"unstructured": "string",
			"reference": "string"
		  }
		},
		"Authorisation": {
		  "AuthorisationType": "Any",
		  "CompletionDateTime": "2020-12-17T08:26:08.090Z"
		}
	}'
```


> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Account Details retrieved successfully",
  "data": {
	"read_refund_account": "No",
		"initiation": {
		  "instruction_identification": "string",
		  "end_to_end_identification": "string",
		  "local_instrument": "string",
		  "instructed_amount": {
			"amount": "string",
			"currency": "string"
		  },
		  "debtor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_postal_address": {
			"address_type": "Business",
			"department": "string",
			"sub_department": "string",
			"street_name": "string",
			"building_number": "string",
			"post_code": "string",
			"town_name": "string",
			"country_sub_division": "string",
			"country": "string",
			"address_line": [
			  "string"
			]
		  },
		  "remittance_information": {
			"unstructured": "string",
			"reference": "string"
		  }
		},
	"Authorisation": {
	  "AuthorisationType": "Any",
	  "CompletionDateTime": "2020-12-17T08:26:08.090Z"
	}
  }
}
```

### HTTP Request

`POST /payments/domestic-payment-consents`

### Body Parameters

Parameter | Type | Description
--------- | ------- | -----------
consent_id | string | Specify Account Holder Formal title
Creation_date_time | string | Specify Account Holder First Name
status | string | Optional. Specify Account Holder Middle Name
status_update_date_time | string | Specify Account Holder Last Name
read_refund_account | string | Specify Mother's Maiden Name
cut_off_date_time | string | Specify Account Holder Gender



<aside class="notice">
 ...
</aside>





## Get Domestic Payment Consents

Get Domestic Payment Consents.


```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/domestic-payment-consents​/{xxs2134grt}"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```

> The above command returns JSON structured like this:

```json
{
  "status_code": 00,
  "message": "Domestic Payment Consents Read",
  "data":{
		"consent_id": "string",
		"creation_date_time": "2020-12-17T10:50:25.782Z",
		"status": "Authorised",
		"status_update_date_time": "2020-12-17T10:50:25.783Z",
		"read_refund_account": "No",
		"cut_off_date_time": "2020-12-17T10:50:25.783Z",
		"expected_execution_date_time": "2020-12-17T10:50:25.783Z",
		"expected_settlement_date_time": "2020-12-17T10:50:25.783Z",
		"charges": [
		  {
			"charge_bearer": "BorneByCreditor",
			"type": "string",
			"amount": {
			  "amount": "string",
			  "currency": "string"
			}
		  }
		],
		"initiation": {
		  "instruction_identification": "string",
		  "end_to_end_identification": "string",
		  "local_instrument": "string",
		  "instructed_amount": {
			"amount": "string",
			"currency": "string"
		  },
		  "debtor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_postal_address": {
			"address_type": "Business",
			"department": "string",
			"sub_department": "string",
			"street_name": "string",
			"building_number": "string",
			"post_code": "string",
			"town_name": "string",
			"country_sub_division": "string",
			"country": "string",
			"address_line": [
			  "string"
			]
		  },
		  "remittance_information": {
			"unstructured": "string",
			"reference": "string"
		  }
		},
		"authorisation": {
		  "authorisation_type": "Any",
		  "completion_date_time": "2020-12-17T10:50:25.783Z"
		},
		"debtor": {
		  "name": "string"
		}
	  }
 }
```

### HTTP Request

`GET /payments/domestic-payment-consents​/{consent_id}`

### Path Parameter(s)

Parameter | Type | Description
--------- | ------- | -----------
consent_id | string | 






## Get Domestic Payment Consents Funds Confirmation

Get Domestic Payment Consents.


```Shell
curl -X GET "https://api.singularapi.com/api/v1/finance/00234000054/payments/domestic-payment-consents​/{xxs2134grt}/funds-confirmation"
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
```





## Create Domestic Payments

Create Domestic Payments

```Shell
curl -X POST "https://api.singularapi.com/api/v1/finance/00234000054/payments/​domestic-payments
  -H "Authorization: token-obtained-from-authorization"
	-H 'Content-Type: application/json'
	-d '{
  "Data": {
		"consent_id": "string",
		"initiation": {
		  "instruction_identification": "string",
		  "end_to_end_identification": "string",
		  "local_instrument": "string",
		  "instructed_amount": {
			"amount": "string",
			"currency": "string"
		  },
		  "debtor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_account": {
			"scheme_name": "string",
			"identification": "string",
			"name": "string",
			"secondary_identification": "string"
		  },
		  "creditor_postal_address": {
			"address_type": "Business",
			"department": "string",
			"sub_department": "string",
			"street_name": "string",
			"building_number": "string",
			"post_code": "string",
			"town_name": "string",
			"country_sub_division": "string",
			"country": "string",
			"address_line": [
			  "string"
			]
		  },
		  "remittance_information": {
			"unstructured": "string",
			"reference": "string"
		  }
		}
	  }'
```






## Get Domestic Payments




## Get Payment Details




## Get Scheduled Payment Details




## Get Standing Orders​ Payment Details




## Get file Payment Details




## Get International Payment Details




## Get International Scheduled Payment Details




## Get International Standing Orders​ Payment Details

