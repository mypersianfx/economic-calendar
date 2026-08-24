# PersianFX Economic Calendar API

## 📊 PersianFX Economic Calendar API

یک API ساده و کاربردی برای دریافت اطلاعات **تقویم اقتصادی بازارهای مالی**.

این API اطلاعات رویدادهای اقتصادی روز را در قالب `JSON` ارائه می‌دهد و شامل اطلاعاتی مانند نام رویداد، نام فارسی، ارز مرتبط، زمان انتشار، میزان اهمیت، مقادیر Actual، Forecast و Previous و همچنین توضیحات مربوط به اهمیت خبر در بازار است.

مناسب برای:

* وب‌سایت‌های فارکس و بازارهای مالی
* اپلیکیشن‌های اقتصادی
* ربات‌های تلگرام و دیسکورد
* داشبوردهای معاملاتی
* ابزارهای تحلیل تکنیکال و فاندامنتال
* سیستم‌های هشدار اخبار اقتصادی
* پروژه‌های شخصی و تجاری

---

## 🌐 API Endpoint

برای دریافت تقویم اقتصادی روز:

```text
https://api.persianfx.com/api.php
```

نوع درخواست:

```text
GET
```

---

# 🚀 Quick Start

### JavaScript

```javascript
fetch("https://api.persianfx.com/api.php")
  .then(response => response.json())
  .then(data => {
    console.log(data);
  })
  .catch(error => {
    console.error("API Error:", error);
  });
```

### Async / Await

```javascript
async function getEconomicCalendar() {
  try {
    const response = await fetch(
      "https://api.persianfx.com/api.php"
    );

    const data = await response.json();

    console.log(data);

    data.events.forEach(event => {
      console.log(
        `${event.time} - ${event.currency} - ${event.event_name}`
      );
    });

  } catch (error) {
    console.error("Error:", error);
  }
}

getEconomicCalendar();
```

---

## 🐍 Python Example

```python
import requests

url = "https://api.persianfx.com/api.php"

response = requests.get(url)

data = response.json()

print("Status:", data["status"])
print("Date:", data["date"])
print("Events:", data["count"])

for event in data["events"]:
    print(
        event["time"],
        event["currency"],
        event["event_name"]
    )
```

---

## 🐘 PHP Example

```php
<?php

$url = "https://api.persianfx.com/api.php";

$response = file_get_contents($url);

$data = json_decode($response, true);

echo "Status: " . $data["status"] . PHP_EOL;

echo "Date: " . $data["date"] . PHP_EOL;

echo "Events Count: " . $data["count"] . PHP_EOL;

foreach ($data["events"] as $event) {

    echo $event["time"] . " - ";

    echo $event["currency"] . " - ";

    echo $event["event_name"] . PHP_EOL;

}

?>
```

---

# 📦 Response Structure

نمونه ساختار پاسخ API:

```json
{
  "status": "success",
  "date": "2026-08-25",
  "count": 10,
  "events": [
    {
      "id": 154,
      "external_id": 17616,
      "event_name": "Monetary Policy Meeting Minutes",
      "event_name_fa": "صورتجلسه نشست سیاست پولی",
      "currency": "AUD",
      "date": "2026-08-25",
      "time": "05:00:00",
      "impact": "low",
      "actual": null,
      "forecast": null,
      "previous": null,
      "revised": null,
      "description": null,
      "usual_effect": "هر چه از حد انتظار انقباضی تر باشد، به نفع ارزش پول خواهد بود؛",
      "why_trader_cares": "توضیح اهمیت این رویداد برای معامله‌گران",
      "crypto_effect": null,
      "metal_effect": "low",
      "energy_effect": null,
      "source_name": "بانک مرکزی استرالیا",
      "source_link": "https://www.rba.gov.au/",
      "next_release": "2026-08-25",
      "status": "waiting"
    }
  ]
}
```

---

# 🔍 Response Fields

## اطلاعات اصلی پاسخ

| Field    | Description                       |
| -------- | --------------------------------- |
| `status` | وضعیت پاسخ API                    |
| `date`   | تاریخ تقویم اقتصادی               |
| `count`  | تعداد کل رویدادهای دریافت‌شده     |
| `events` | آرایه شامل لیست رویدادهای اقتصادی |

---

# 📅 Event Object

هر آیتم در آرایه `events` یک رویداد اقتصادی است.

## شناسه‌ها

| Field         | Description        |
| ------------- | ------------------ |
| `id`          | شناسه داخلی رویداد |
| `external_id` | شناسه خارجی رویداد |

---

## 📰 اطلاعات رویداد

| Field           | Description                 |
| --------------- | --------------------------- |
| `event_name`    | نام رویداد به زبان انگلیسی  |
| `event_name_fa` | نام رویداد به زبان فارسی    |
| `currency`      | ارز یا کشور مرتبط با رویداد |
| `date`          | تاریخ انتشار رویداد         |
| `time`          | ساعت انتشار رویداد          |

نمونه:

```json
{
  "event_name": "US CB Consumer Confidence",
  "event_name_fa": "شاخص اعتماد مصرف کننده کنفرانس‌بورد",
  "currency": "USD",
  "date": "2026-08-25",
  "time": "17:30:00"
}
```

---

# 🔥 Impact

فیلد `impact` میزان اهمیت رویداد اقتصادی را مشخص می‌کند.

مقادیر احتمالی:

| Value  | معنی        |
| ------ | ----------- |
| `low`  | اهمیت پایین |
| `mid`  | اهمیت متوسط |
| `high` | اهمیت بالا  |

مثال:

```json
"impact": "mid"
```

---

# 📈 Economic Data

هر رویداد می‌تواند شامل مقادیر اقتصادی زیر باشد:

| Field      | Description           |
| ---------- | --------------------- |
| `actual`   | مقدار واقعی اعلام‌شده |
| `forecast` | مقدار پیش‌بینی‌شده    |
| `previous` | مقدار قبلی            |
| `revised`  | مقدار اصلاح‌شده قبلی  |

مثال:

```json
{
  "actual": null,
  "forecast": "90.3",
  "previous": "90.8",
  "revised": null
}
```

ممکن است قبل از انتشار خبر، مقدار `actual` برابر با `null` باشد.

---

# 🧠 اطلاعات تحلیلی رویداد

این API علاوه بر داده‌های خام اقتصادی، اطلاعات مفیدی درباره اهمیت رویداد نیز ارائه می‌دهد.

| Field              | Description                          |
| ------------------ | ------------------------------------ |
| `description`      | توضیحات مربوط به رویداد              |
| `usual_effect`     | تأثیر معمول نتیجه رویداد بر ارزش ارز |
| `why_trader_cares` | دلیل اهمیت رویداد برای معامله‌گران   |

نمونه:

```json
{
  "usual_effect": "اگر مقدار فعلی از پیش‌بینی بیشتر باشد تاثیر مثبت بر ارزش ارز دارد؛",
  "why_trader_cares": "این شاخص می‌تواند اطلاعات مهمی درباره وضعیت اقتصاد ارائه دهد؛"
}
```

---

# ₿ تأثیر بر بازارهای مختلف

هر رویداد می‌تواند دارای اطلاعاتی درباره تأثیر احتمالی بر بازارهای مختلف باشد.

| Field           | Market               |
| --------------- | -------------------- |
| `crypto_effect` | بازار ارزهای دیجیتال |
| `metal_effect`  | بازار فلزات          |
| `energy_effect` | بازار انرژی          |

مقادیر احتمالی:

```text
low
mid
high
null
```

مثال:

```json
{
  "crypto_effect": "low",
  "metal_effect": "mid",
  "energy_effect": "low"
}
```

---

# 🏛️ منبع خبر

اطلاعات منبع انتشار رویداد:

| Field         | Description                   |
| ------------- | ----------------------------- |
| `source_name` | نام منبع یا سازمان منتشرکننده |
| `source_link` | لینک رسمی منبع                |

مثال:

```json
{
  "source_name": "بانک مرکزی ژاپن",
  "source_link": "https://www.boj.or.jp/"
}
```

---

# 🔄 انتشار بعدی

| Field          | Description              |
| -------------- | ------------------------ |
| `next_release` | تاریخ انتشار بعدی رویداد |

مثال:

```json
"next_release": "2026-09-09"
```

---

# ⏳ Event Status

فیلد `status` وضعیت فعلی رویداد را مشخص می‌کند.

مثال:

```json
"status": "waiting"
```

برای مثال، مقدار `waiting` نشان می‌دهد که رویداد هنوز منتشر نشده و در انتظار انتشار است.

---

# 💻 نمایش ساده تقویم

### JavaScript

```javascript
async function showCalendar() {

  const response = await fetch(
    "https://api.persianfx.com/api.php"
  );

  const data = await response.json();

  data.events.forEach(event => {

    console.log(`
      ${event.time}
      ${event.currency}
      ${event.event_name_fa}
      Impact: ${event.impact}
    `);

  });

}

showCalendar();
```

---

# 🔔 پیدا کردن اخبار مهم

می‌توانید رویدادها را بر اساس میزان اهمیت فیلتر کنید.

```javascript
async function getHighImpactEvents() {

  const response = await fetch(
    "https://api.persianfx.com/api.php"
  );

  const data = await response.json();

  const importantEvents = data.events.filter(
    event => event.impact === "high"
  );

  console.log(importantEvents);

}

getHighImpactEvents();
```

---

# 🇺🇸 فیلتر رویدادها بر اساس ارز

مثلاً دریافت تمام اخبار مربوط به دلار آمریکا:

```javascript
const usdEvents = data.events.filter(
  event => event.currency === "USD"
);
```

مثال کامل:

```javascript
async function getUSDEvents() {

  const response = await fetch(
    "https://api.persianfx.com/api.php"
  );

  const data = await response.json();

  const usdEvents = data.events.filter(
    event => event.currency === "USD"
  );

  console.log(usdEvents);

}

getUSDEvents();
```

---

# ⚠️ نکات مهم

* پاسخ API در قالب `JSON` ارائه می‌شود.
* برخی فیلدها ممکن است مقدار `null` داشته باشند.
* مقدار `actual` معمولاً قبل از انتشار خبر `null` است.
* زمان رویداد در فیلد `time` قرار دارد.
* میزان اهمیت خبر در فیلد `impact` مشخص می‌شود.
* اطلاعات مربوط به تأثیر احتمالی بر بازار کریپتو، فلزات و انرژی در فیلدهای مربوطه ارائه می‌شود.
* بهتر است برای کاهش درخواست‌های غیرضروری، داده‌ها را برای مدت کوتاهی Cache کنید.

---

# 🌐 API URL

```text
https://api.persianfx.com/api.php
```

---

# 🏢 PersianFX

داده‌های این API توسط PersianFX ارائه می‌شود.

وب‌سایت:

[PersianFX](https://persianfx.com?utm_source=chatgpt.com)

API Endpoint:

[Economic Calendar API](https://api.persianfx.com/api.php?utm_source=chatgpt.com)

---

# 📄 License

لطفاً قبل از استفاده تجاری یا گسترده از API، شرایط و قوانین استفاده از سرویس PersianFX را بررسی کنید.

---

## ⭐ Support

اگر این API برای پروژه شما مفید بود، خوشحال می‌شویم Repository را ⭐ Star کنید.

**PersianFX Economic Calendar API**

Economic Calendar Data for Traders, Developers and Financial Applications.
