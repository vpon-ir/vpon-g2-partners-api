# سند API ویپان نسل 2 برای برندهای همکار

### دریافت فهرست سفارش ها
```
POST https://vpon.ir/bridge/api/v1/orders
```

### کلید API

Include your API key in the request header:

| Header | Value |
|--------|-------|
| `X-API-Key` | `YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ==` |

### پارامترهای درخواست

The request body should be a JSON object with the following fields:

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| `from` | string | No | Start date in Jalali calendar (format: `YYYY-M-D`) |
| `to` | string | No | End date in Jalali calendar (format: `YYYY-M-D`) |

#### Example Request Body

```json
{
  "from": "1405-2-11",
  "to": "1405-2-18"
}
```

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

### Response Fields

| Field | Type | Description |
|-------|------|-------------|
| `message` | string | Persian status message |
| `status` | string | Status of the request (`success`) |
| `status_code` | integer | Status code (`1` = success) |
| `data.from` | string | Start date from request (Jalali) |
| `data.to` | string | End date from request (Jalali) |
| `data.orders` | array | List of orders |

#### Order Object Fields

| Field | Type | Description |
|-------|------|-------------|
| `id` | integer | Unique order identifier |
| `customer` | string | Customer name |
| `address` | string | Full address (may be empty) |
| `province` | string | Province name |
| `city` | string | City name |
| `nbhd` | string | Neighborhood name |
| `lat` | string | Latitude coordinate (may be empty) |
| `lng` | string | Longitude coordinate (may be empty) |
| `order_summery` | string | Comma-separated list of services |
| `bill` | integer | Bill amount in IRR (toman/rial) |
| `schedule_date` | string | Scheduled service date (Jalali) |
| `schedule_time` | string | Scheduled time window |
| `status` | integer | Order status code |
| `status_label` | string | Human-readable status |
| `submited_at` | string | Submission datetime (Jalali) |
| `finished_at` | string | Completion datetime (empty if not finished) |
| `last_note` | string | Most recent note on the order |
| `last_note_at` | string | Last note timestamp (Jalali) |

### Status Codes

| status | status_label | Description |
|--------|--------------|-------------|
| `0` | "در صف رسیدگی" | In queue for processing |
| `1` | "در انتظار انجام" | Awaiting completion |

### Example cURL Request

```bash
curl -X POST https://vpon.ir/bridge/api/v1/orders \
  -H "X-API-Key: YzFhYjRiYjgwMTJmMTg5ZGZTcTYwYjghYjRiY2FjOJmMTg5OTGJmQ==" \
  -H "Content-Type: application/json" \
  -d '{
    "from": "1405-2-11",
    "to": "1405-2-18"
  }'
```

### Notes

- Dates are in the Jalali (Persian) calendar system
- If `from` and `to` are not provided, the API may return all orders (check with provider)
- Empty string values for `address`, `lat`, `lng`, and `finished_at` indicate missing data
- The `bill` amount is in Iranian currency (the example shows 1,430,000 IRR)
