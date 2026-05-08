# سند API ویپان نسل 2 برای برندهای همکار

### دریافت فهرست سفارش ها
```
POST https://vpon.ir/bridge/api/v2/orders?from=1405-2-11&to=1405-2-18
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
| `from` | string | No | Start date in Jalali calendar (format: `YYYY-M-D`) |
| `to` | string | No | End date in Jalali calendar (format: `YYYY-M-D`) |

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
        "id": 36651,
        "customer": "مرتضی",
        "address": "",
        "province": "تهران",
        "city": "تهران",
        "nbhd": "آبشار",
        "lat": "",
        "lng": "",
        "order_summery": "خدمات کولر آبی,نصب یا تعویض موتور کولر آبی,برای نوع متداول موتورهای سیم‌پیچی,",
        "bill": 1430000,
        "schedule_date": "1405-2-16",
        "schedule_time": "8-10",
        "status": 0,
        "status_label": "در صف رسیدگی",
        "submited_at": "1405-2-16 13:43",
        "finished_at": "",
        "last_note": "این درخواست توسط شریک تجاری ثبت شد",
        "last_note_at": "1405-2-16 13:43"
      }
    ]
  },
  "status": "success",
  "status_code": 1
}
```

#### Failed Response (Http Code 401)
{
  "message": "Your api-key is invalid, send valid 'X-API-KEY' by header.",
  "status": "failed",
  "status_code": 0
}

## نکات 
- تاریخ ها به جلالی با فرمت () مثال ()
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
### Example cURL Request

```bash
curl -X POST "https://vpon.ir/bridge/api/v1/orders?from=1405-2-11&to=1405-2-18" \
  -H "X-API-Key: YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ=="
```

