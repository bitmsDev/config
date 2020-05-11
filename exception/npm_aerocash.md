# NPM 

**Example response object**
````json
{
  "code": 200,
  "status": "success",
  "response": {}
}
````


> Request status

**Status: error**

| | | | | |
|----------|----------|----------|-----------|-----------|
| # | code | event | message | action |
| 1 | ``404`` | ``Create Payment`` | ``Provider not found!`` | **Add new the provider** | 
| 2 | ``403`` | ``Input payment data`` | ``Payment method not access!`` | **Read error log** | 
| 3 | ``500`` | ``Parse payment data`` | ``Invalid {parameter}!`` | **Read error log and request parameters** | 
| 4 | ``504`` | ```` | ``Invalid {parameter}!`` | **Read error log and request parameters** | 

> Action

**Add new the provider**
```http
curl --location --request POST 'https://api.bitms.ru/v1/provider' \
--header 'Content-Type: application/json' \
--data-raw '{
	"uri": "https://api.example.com",
	"name" : "example",
	"config": {
		"text_selector": {
			"price": "selector name",
			"description": "selector name"
		},
		"form_serletor": {
			"card" : {
				"number": "input selector",
				"mouth": "input/select selector",
				"year": "input/select selector",
				"cvc": "input selector"
			},
			"user": {
				"name": "input selector",
				"surname": "input selector"
			},
			"checkbox": {
				"notify": "checkbox selector"
			}
			
		}
	}
}'
```
