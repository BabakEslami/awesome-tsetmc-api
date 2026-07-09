<div dir="rtl">

# Iran Capital Market API Reference 📊

مرجع غیررسمی و آزمایش‌شده‌ی endpoint های API بازار سرمایه ایران — برای توسعه‌دهنده‌هایی که می‌خوان بدون ساعت‌ها probe کردن، مستقیم سراغ ساخت ابزار برن.

> ⚠️ **این پروژه هیچ ارتباط رسمی با شرکت مدیریت فناوری بورس تهران یا شرکت بورس اوراق بهادار تهران ندارد.** این یک مستندسازی جامعه‌محور از API هایی است که از طریق مشاهده‌ی ترافیک شبکه و تست عملی به دست آمده. هیچ SLA یا تعهد پایداری‌ای پشت این endpoint ها نیست و ممکن است در هر لحظه بدون اطلاع قبلی تغییر کنند.

## این ریپو چیه؟

دو منبع داده‌ی مکمل مستند شده‌اند:

**۱. `cdn.tsetmc.com`** — ~۵۶ endpoint غیررسمی و مستندنشده که به‌صورت عملی تست شده‌اند. کلید نماد در این API، `InsCode` عددی است.

**۲. `webgw.tse.ir`** — gateway رسمی سایت `tse.ir` که از طریق بازرسی HAR در Chrome DevTools کشف شد. کلید نماد در این API، **ISIN کامل** است (نه InsCode). این gateway شامل endpoint هایی است که در cdn موجود نیستند: دیده‌بان کامل بازار با تمام تب‌ها، تاریخچه‌ی روزانه با ارزش بازار، order book سطح ۱ زنده، و جستجوی نماد با pagination.

هدف: کسی که می‌خواد روی داده‌های بازار سرمایه ایران ابزار بسازه (پایپ‌لاین قیمت، بک‌تست، دیده‌بان، ربات تلگرام و...) بتونه از این نقطه شروع کنه، نه از صفر.

## محتوای ریپو

| فایل | محتوا |
|---|---|
| [`ENDPOINTS.md`](./ENDPOINTS.md) | مرجع کامل endpoint ها برای هر دو gateway، دسته‌بندی‌شده، همراه با جدول رفتار بر اساس نوع ابزار (سهام/آپشن/اوراق)، تشخیص نوع ابزار مالی، و هشدارهای عملیاتی |
| [`examples/`](./examples) | نمونه response واقعی JSON برای مهم‌ترین endpoint ها |
| [`scripts/`](./scripts) | اسکریپت پایش برای تست دوره‌ای زنده‌بودن endpoint ها |

## شروع سریع

### cdn.tsetmc.com

```
https://cdn.tsetmc.com/api/...
```

کلید: `InsCode` (شناسه‌ی عددی داخلی)

```bash
# تاریخچه‌ی قیمت پایانی
curl "https://cdn.tsetmc.com/api/ClosingPrice/GetClosingPriceDailyList/{InsCode}/0"

# پیدا کردن InsCode از روی نام نماد
curl "https://cdn.tsetmc.com/api/Instrument/GetInstrumentSearch/{Query}"
```

### webgw.tse.ir

```
https://webgw.tse.ir/InstrumentProvider/api/v1/...
```

کلید: `ISIN کامل` (مثلاً `IRO1NBAB0001`)

```bash
# دیده‌بان کامل بازار نقدی
curl "https://webgw.tse.ir/InstrumentProvider/api/v1/MarketWatch/MarketWatchCash/fa"

# اطلاعات لایو + order book یک نماد
curl "https://webgw.tse.ir/InstrumentProvider/api/v1/Instrument/LiveInstrumentByIdQuery/fa?InstrumentId={ISIN}"

# تاریخچه‌ی کامل روزانه (شامل ارزش بازار)
curl "https://webgw.tse.ir/InstrumentProvider/api/v1/History/Archive/fa?InstrumentId={ISIN}"
```

برای لیست کامل endpoint ها، جزئیات رفتاری، و هشدارهای مهم، به [`ENDPOINTS.md`](./ENDPOINTS.md) مراجعه کنید.

## تفاوت کلیدی دو gateway

| موضوع | cdn.tsetmc.com | webgw.tse.ir |
|---|---|---|
| کلید نماد | InsCode (عدد) | ISIN کامل |
| وضعیت | غیررسمی | رسمی (زیرساخت tse.ir) |
| تاریخچه روزانه | `GetClosingPriceDailyList` | `History/Archive` (+ marketvalue روزانه) |
| order book | `BestLimits` (delta feed — نیاز به reconstruction) | داخل `LiveInstrumentByIdQuery` (سطح ۱، آماده) |
| حقیقی/حقوقی تاریخی | ✅ `ClientTypeHistory` | ❌ فقط لحظه‌ای |
| دیده‌بان کل بازار | ⚠️ `GetMarketWatch` خالی برمی‌گرداند | ✅ `MarketWatch*` کامل |
| دسترسی از سرور | ✅ GitHub Actions | ❌ فقط از IP ایران |

## مشارکت

اگر endpoint جدیدی پیدا کردید یا رفتار متفاوتی مشاهده کردید، خوشحال می‌شویم PR بدهید. برای هر ادعای رفتاری، نمونه‌ی واقعی تست (نه فرضی) ضمیمه کنید — ترجیحاً با HAR export یا خروجی curl.

## مجوز

MIT — استفاده، تغییر و توزیع آزاد، بدون هیچ تضمینی از صحت یا پایداری داده‌ها.

</div>
