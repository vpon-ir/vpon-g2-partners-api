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

Include your API key in the request header:

| Header | Value |
|--------|-------|
| `X-API-Key` | `YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ==` |

### پارامترهای درخواست

Parameters should be sent as **query string** parameters:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `from` | string | No | تاریخ جلالی ابتدای بازه (format: `YYYY-M-D`) |
| `to` | string | No | تاریخ جلالی انتهای بازه (format: `YYYY-M-D`) |

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
        "id": "36656",
        "customer": "کیهان جنت خواه",
        "phone": "09010352806",
        "partner_note": "",
        "customer_note": "",
        "address": "",
        "province": "تهران",
        "city": "تهران",
        "nbhd": "آجودانیه",
        "lat": "",
        "lng": "",
        "services_summery": "نصب موتور کولر BLDC بغل نصب",
        "services_count": "3",
        "bill": "9306000",
        "schedule_date": "1405-2-17",
        "schedule_time": "8-10",
        "status": "0",
        "status_label": "در صف رسیدگی",
        "submited_at": "1405-2-17 20:56"
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
  "message": "Your api-key is invalid, send valid 'X-API-KEY' by header.",
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


