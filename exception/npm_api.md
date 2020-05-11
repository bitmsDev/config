# API Request

> General data

[Swagger documentation](https://api.transportation.me/v1)

```
# Provider codes

1. ALFA      - Альфа страхование
2. VSK       - ВСК страховой дом
3. VIRTU_RGS - ООО «ВИРТУ СИСТЕМС» / Росгосстрах
4. LIBERTY   - «Совкомбанк страхование» (АО)
5. ZETTA     - ООО «Зетта Страхование»
6. SOGLASIE  - ООО «СК «СОГЛАСИЕ»
7. INGOS     - СПАО «Ингосстрах»

```

**Add new police**
> Request -POST /insurance.set
```json
{
  "provider": [],
  "data" : {
    "user" : {
      "result": "Иванов Василий Петрович",
      "name" : "Василий",
      "patronymic": "Петрович",
      "surname": "Иванов",
      "gender": "M",
      "date_birth": "01.05.1977"
    } 
  }
}
```

> Response
```json
{
  "status": "success",
  "request_id" : "043a4f50-ca02-4571-866c-7a74bf9dc788",
  "data": {
    "providers": [
      {
        "name" : "ALFA",
        "status": "auth",
        "session_id": "dec39048-26b8-45ab-84fa-c39b4a10e3b9"
      },
      {
        "name" : "ZETTA",
        "status": "auth",
        "session_id": "ee3ca7e5-1797-4c82-a671-44ca1686c1f7"
      }
    ]
  }
}
```
