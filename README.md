# سند API ویپان نسل 2 برای برندهای همکار

### دریافت فهرست سفارش ها
```
POST https://vpon.ir/bridge/api/v2/orders?from=1405-2-11&to=1405-2-18
```

### Example cURL Request

```bash
curl -X POST "https://vpon.ir/bridge/api/v2/orders?from=1405-2-11&to=1405-2-18" \
  -H "X-API-Key: YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ=="
```
### کلید API

توسط header کلید api باید ارسال شود

| Header | Value (example) |
|--------|-------|
| `X-API-Key` | `YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ==` |

### پارامترهای درخواست

پارامترها توسط query string ارسال میشوند

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `from` | string | YES | تاریخ جلالی ابتدای بازه (format: `YYYY-M-D`) |
| `to` | string | NO | تاریخ جلالی انتهای بازه (format: `YYYY-M-D`) |

### Response

#### Success Response (200 OK)

```json
{
  "message": "فهرست سفارش ها",
  "data": {
    "from": "1405-2-11",
    "to": "1405-2-18",
    "orders": [
      {
        "id": "36655",
        "customer": "کیهان جنت خواه",
        "phone": "09010352806",
        "partner_note": "",
        "customer_note": "",
        "address": "",
        "province": "تهران",
        "city": "تهران",
        "nbhd": "آجودانیه",
        "lat": "0",
        "lng": "0",
        "services_summery": "نصب یا تعویض موتور کولر آبی",
        "services_count": "1",
        "bill": "2000000",
        "schedule_date": "1405-2-18",
        "schedule_time": "12-14",
        "status": "1",
        "status_label": "در انتظار انجام",
        "submited_at": "1405-2-17 11:21",
        "form": "https://form.vpondev.ir/14db73a0-81a6-4987-832a-ff5dce19863e/5a30ff50-0c56-4b85-b7dc-d40ef62050c0"
      }
    ]
  },
  "status": "success",
  "status_code": 1
}
```

#### Failed Response (Http Code 401)
```json
{
  "message": "Must have a valid X-API-KEY in header.",
  "status": "failed",
  "status_code": 0
}
```

#### Failed Response (Http Code 401)
```json
{
  "message": "Parameter 'from' is required but missing. format YYYY-M-D e.g: 1405-1-18",
  "status": "failed",
  "status_code": 0
}
```

## نکات 
- تاریخ ها به جلالی با فرمت (YYYY-m-d)
- مبالغ همیشه به تومان هست
- در هر دقیقه حداکثر 1 درخواست میتوانید ارسال کنید



### Status Codes

| status | status_label | Description |
|--------|--------------|-------------|
| `0` | "در صف رسیدگی" |  |
| `1` | "در انتظار انجام" | |
| `2` | "انصراف توسط مشتری" |  |
| `3` | "نیاز به بررسی مجدد" |  |
| `4` | "پایان یافته" |  |
| `5` | "نیاز به تعمیر" |  |
| `6` | "لغو شده" |  |
| `7` | "پیش نویس شده" |  |


