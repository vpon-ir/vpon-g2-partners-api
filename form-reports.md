# دریافت فهرست کارهای پروژه طبق فرم کارشناسی

مثال : دریافت فهرست 10 ساعت گذشته از فرم 2

https://vpon.ir/bridge/api/v2/project/report/?form=2&h=10

مثال : دریافت فهرست در روز مشخص از فرم 2

https://vpon.ir/bridge/api/v2/project/report/?form=2&day=1405-3-12

شماره فرم با form مشخص میشود (اجباری)

تاریخ شمسی توسط پارامتر day ارسال میشود (اختیاری)

تعداد ساعت ها با h مشخص میشود (اختیاری)

تعداد فیلدهای field_1 field_2 field_x نامشخص است و در هر رکورد ممکن است 4 تا 5 تا یا حتی بیشتر باشد و ثابت نیست


```json
{
   "data": [
      {
         "form_id": "2",
         "files": [
         "https://cdn.vponco.ir/opnform/2/__db1b5a05-4ceb-407b-9be3-bb424c0ebc49.mp4"
         ],
         "field_1": "محمد پرپنجی",
         "field_2": "شهید کمالی",
         "field_3": "6",
         "field_4": "بغل نصب بدون نبشی",
         "field_5": "33",
         "submit_id": "34e1bfc6-8680-4f68-90ed-cc6d97e14b5d",
         "datetime": "1405/3/21 10:53"
      }
    ],
    "message": "فهرست گزارشات فرم",
    "status": "success",
    "status_code": 1
}
```
