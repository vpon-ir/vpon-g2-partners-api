
 # دریافت فهرست کارهای پروژه طبق فرم کارشناسی

مثال : دریافت فهرست 10 ساعت گذشته از فرم 2

https://vpon.ir/bridge/api/v2/project/report/?form=2&h=10

مثال : دریافت فهرست در روز مشخص از فرم 2

https://vpon.ir/bridge/api/v2/project/report/?form=2&day=1405-3-12

درخواست :

شماره فرم با form مشخص میشود (اجباری)

تاریخ شمسی توسط پارامتر day ارسال میشود (اختیاری)

تعداد ساعت ها با h مشخص میشود (اختیاری)

پاسخ :

فیلد video و image ممکن است وجود نداشته باشد 

تعداد فیلدهای field_1 field_2 field_x نامشخص است و در هر رکورد ممکن است 4 و 5 یا بیشتر باشد و ثابت نیست

فیلد های (datetime و form_id و submit_id ) همیشه وجود دارد


```json
{
   "data": [
      {
         "form_id": "2",
         "submit_id": "3e19c4c3-d715-405a-b526-5e6623f05b38",
         "datetime": "1405/3/12 22:12"
         "video": "https://cdn.vponco.ir/opnform/2/__ee74cd30-b3b7-4ba1-872e-9b41da5a23f8.mp4",
         "image": "https://cdn.vponco.ir/opnform/2/__ee74cd2e-9b41d30-b3b7-4ba1-878.jpg",
         "field_1": "امیر عنایتی",
         "field_2": "شهید حجازی",
         "field_3": "6",
         "field_4": "بغل نصب بدون نبشی",
         "field_5": "6",
      }
    ],
    "message": "فهرست گزارشات فرم",
    "status": "success",
    "status_code": 1
}
```

