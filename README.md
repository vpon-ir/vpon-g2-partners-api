# سند API ویپان نسل 2 برای برندهای همکار

### دریافت فهرست سفارش ها
```
POST https://vpon.ir/bridge/api/v2/orders?from=1405-2-11&to=1405-2-18
```

### نمونه cURL

```bash
curl -X POST "https://vpon.ir/bridge/api/v2/orders?from=1405-2-11&to=1405-2-18" \
  -H "X-API-Key: YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ=="
```

### نمونه کد php
```php
<?php
function fetchOrders() {
    $url = 'https://vpon.ir/bridge/api/v2/orders?from=1405-2-11&to=1405-2-18';
    $apiKey = 'YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ==';
    
    $ch = curl_init();
    
    curl_setopt($ch, CURLOPT_URL, $url);
    curl_setopt($ch, CURLOPT_POST, true);
    curl_setopt($ch, CURLOPT_RETURNTRANSFER, true);
    curl_setopt($ch, CURLOPT_HTTPHEADER, [
        'X-API-Key: ' . $apiKey,
        'Content-Type: application/json'
    ]);
    
    $response = curl_exec($ch);
    $httpCode = curl_getinfo($ch, CURLINFO_HTTP_CODE);
    
    if (curl_errno($ch)) {
        $error = curl_error($ch);
        curl_close($ch);
        throw new Exception('cURL Error: ' . $error);
    }
    
    curl_close($ch);
    
    if ($httpCode >= 400) {
        throw new Exception('HTTP Error: ' . $httpCode . ' - ' . $response);
    }
    
    return json_decode($response, true);
}
```

### نمونه کد JS
```js
function fetchOrders() {
    const url = 'https://vpon.ir/bridge/api/v2/orders?from=1405-2-11&to=1405-2-18';
    const apiKey = 'YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ==';
    
    try {
        const response = await fetch(url, {
            method: 'POST',
            headers: {
                'X-API-Key': apiKey,
                'Content-Type': 'application/json'
            }
        });
        
        if (!response.ok) {
            throw new Error(`HTTP error! status: ${response.status}`);
        }
        
        const data = await response.json();
        console.log('Success:', data);
        return data;
        
    } catch (error) {
        console.error('Error:', error);
        throw error;
    }
}
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

### پاسخ ها

####  عملیات موفق (Http Code 200)

```json
{
  "message": "فهرست سفارش ها",
  "data": {
    "from": "1405-2-11",
    "to": "1405-2-18",
    "orders": [
      {
        "id": "36658",
        "customer": "کیهان جنت خواه",
        "phone": "09010352806",
        "partner_note": "",
        "customer_note": "لطفا قبل از اینکه تشریف بیارید یک تماس با من بگیرید",
        "address": "",
        "province": "تهران",
        "city": "تهران",
        "nbhd": "آرژانتین",
        "lat": "",
        "lng": "",
        "services_summery": "نصب موتور کولر BLDC وسط نصب",
        "services_count": "1", 
        "services": [
          {
            "group_id": "1",
            "title": "خدمات کولر آبی",
            "note": "نصب یا تعویض موتور کولر آبی  test",
            "count": "1",
            "products_price": "0",
            "skills_price": "1000000",
            "price": "1000000"
          }
        ],
        "bill": "4004000",
        "schedule_date": "1405-2-19",
        "schedule_time": "18-20",
        "status": "0",
        "status_label": "در صف رسیدگی",
        "last_report": "",
        "submited_at": "1405-2-18 16:09",
        "form": "https://form.vpondev.ir/5a779ad2-54b5-4a89-bc8d-b9f7aa314fcf/e5508c11-edfd-440f-be4c-0294b44f19c2",
        "form_admin": "https://formadmin.vpondev.ir/5a779ad2-54b5-4a89-bc8d-b9f7aa314fcf/e5508c11-edfd-440f-be4c-0294b44f19c2",
        "form_uuid": "5a779ad2-54b5-4a89-bc8d-b9f7aa314fcf",
        "order_uuid": "e5508c11-edfd-440f-be4c-0294b44f19c2",
        "customer_feedback": {
          "skills": "5",
          "dress": "5",
          "behaviour": "5",
          "match": "1",
          "callcenter": "5",
          "referral_chance": "5",
          "updated_at": "2026-05-18 12:35:45"
        }
      }
    ]
  },
  "status": "success",
  "status_code": 1
}
```

امکان دارد مقدار services  و یا customer_feedback خالی بصورت null باشد
در صورت لغو فبلد last_report دربگیرنده اخرین گزارش و علت لغو است



####  خطا نوع اول (Http Code 401)
```json
{
  "message": "Must have a valid X-API-KEY in header.",
  "status": "failed",
  "status_code": 0
}
```

#### خطای نوع دوم (Http Code 400)
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
- در هر دقیقه حداکثر 2 درخواست تکراری میتوانید ارسال کنید
- کد 200 در http یعنی درخواست معتبر است و پردازش شده در غیر این صورت خیر


### کدهای وضعیت سفارش

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


