# Autocomplete payment page

> Create pay

**Request payment**

```-POST /v1/payment.set```

```json
{
  "uri" : "https://example.com/53623373-d87c-45c3-9023-fa1789357432",
  "number" : "1100110011001100",
  "mouth" : "12",
  "year" : "24",
  "holder": "Ivan Ivanov",
  "cvc" : "000"
}
```

**Response payment**
```json
{
  "status" : "success",
  "request_id" : "f0e9e3bb-d9b9-463b-8fd1-483396a4bc6a"
}
```

> Get SMS-code

**Request**

```-POST {EXTERNAL URI}```

```json
{
  "request_id" : "f0e9e3bb-d9b9-463b-8fd1-483396a4bc6a",
  "price": "2000.00",
  "description": "",
  "card": "*1100"
}
```

**Response**

```json
{
  "request_id" : "f0e9e3bb-d9b9-463b-8fd1-483396a4bc6a",
  "code": "0202"
}
```

> Get Log

```-GET /v1/payment.get/{requestId}```

```json
{
  "request_id" : "b3b83dfd-91b4-4b06-b0a6-b0f7cd39bbb9",
  "price": "2000.00",
  "screen": {
    "payment": "https://ftp.tapme.shop/screen/fcd6a3d4.webp",
    "blank" : "https://ftp.tapme.shop/screen/3ef23694.webp"
  }
}
```
