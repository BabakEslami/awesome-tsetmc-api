<!--
tsetmc_endpoints_master_reference_v4_1.md
ورژن: 4.1
تاریخ تولید: ۱۴۰۵/۰۴/۲۴ (2026-07-15)

توضیحات:
این فایل، مرجع نهایی و یکپارچه‌ی endpoint های بازار سرمایه ایران (TSETMC + webgw.tse.ir)
است. هدف: یک منبع واحد و کامل برای استفاده در تمام پروژه‌های پایش/بک‌تست/پایپ‌لاین
داده (show_industry_indices.py، tsetmc-market-pipeline، ahram_backtest.py و غیره)
بدون نیاز به رجوع به فایل‌های پراکنده‌ی قبلی.

منابع ادغام‌شده (هر ۴ مورد، بدون حذف اطلاعات):
  1) ENDPOINTS.md (آپلود کاربر، نسخه‌ی فارسی کامل با یادداشت‌های عملیاتی مفصل) —
     غنی‌ترین منبع؛ ستون فقرات این سند از همین فایل ساخته شده.
  2) ENDPOINTS_correction_selected_indices (1).md (آپلود کاربر) — اصلاحیه‌ی تعداد
     شاخص‌های منتخب بورس: ۷ مورد است، نه ۶ (کشف تجربی ۱۴۰۵/۰۴/۲۴، تأییدشده با
     بررسی نبود insCode تکراری در پاسخ واقعی API).
  3) tsetmc_endpoints_reference_v3_1.md (آپلود کاربر) — نسخه‌ی میانی که علاوه بر
     دو منبع بالا، دو نکته‌ی اضافه داشت که در فایل ۱ نبود: (الف) عدد تجربی تقریبی
     تعداد شاخص‌های صنعتی در پاسخ `All/{flow}` (~۴۰-۵۰ مورد، کدهای دورقمی ۰۱ تا
     ۷۴)، (ب) یادآوری معماری درباره‌ی نیاز به بک‌اند واسط برای فراخوانی از مرورگر
     (تکمیل‌کننده‌ی هشدار User-Agent که در فایل ۱ هم بود).
  4) ریپازیتوری GitHub — https://github.com/BabakEslami/tse-market-data
     (فایل ENDPOINTS.md آن ریپو + README) بررسی و با فایل ۱ مقایسه شد. نتیجه:
     محتوای ریپو زیرمجموعه‌ی فایل ۱ است (نسخه‌ی قدیمی‌تر/خلاصه‌تر با توضیحات
     انگلیسی و بدون بخش «شاخص‌ها»)؛ هیچ endpoint یا نکته‌ی جدیدی که در فایل ۱
     نبوده باشد، در آن یافت نشد.
     ⚠️ شفافیت روش: پوشه‌های examples/ و scripts/ همین ریپو به‌خاطر robots.txt
     گیت‌هاب از طریق ابزار fetch این چت قابل مرور مستقیم نبودند (فقط صفحه‌ی اصلی
     ریپو و فایل ENDPOINTS.md آن با موفقیت خوانده شدند). این پوشه‌ها ممکن است
     نمونه JSON واقعی یا جزئیات اسکریپت پایش داشته باشند که در این سند نیامده؛
     اگر لازم است، باید جداگانه و با روش دیگری (مثلاً git clone) بررسی شوند.

تاریخچه‌ی نسخه‌ها:
  v3.0/v3.1 — نسخه‌های میانی (شرح در بخش «منابع» بالا)
  v4.1 — این نسخه. کار انجام‌شده نسبت به v4.0:
    - کاربر مستقیماً محتوای پوشه‌های `examples/` و `scripts/` ریپازیتوری
      BabakEslami/tse-market-data را (که در v4.0 به‌خاطر robots.txt گیت‌هاب
      غیرقابل‌دسترس بود) به‌صورت فایل zip آپلود کرد. این محتوا مستقیماً بررسی
      و راستی‌آزمایی شد (نه گزارش دست‌دوم) و به‌صورت دو پیوست جدید اضافه شد:
      • پیوست A: جزئیات فنی اسکریپت پایش `test_active_tsetmc_endpoints.py`
        (هدرهای HTTP، منطق retry با exponential backoff، دسته‌بندی کامل
        وضعیت‌ها، پارامترهای CLI) — همگی از خواندن مستقیم کد Python تأیید شدند.
      • پیوست B: نمونه فیلدهای response از ۴ فایل JSON داخل `examples/`
        (BestLimits، GetClosingPriceInfo، GetInstrumentIdentity،
        GetInstrumentSearch) — با تأکید صریح که این نمونه‌ها «ساختاری»اند
        (مقادیر placeholder/فرضی، نه گرفته‌شده از تست زنده روی API)، برخلاف
        بقیه‌ی این سند که همه از تست واقعی می‌آیند.
    - پیش از این افزودن، یک تحلیل مستقل توسط ChatGPT درباره‌ی همین دو پوشه به
      کاربر داده شده بود؛ ادعاهای آن تحلیل (هدرها، وضعیت‌های retry، پارامترهای
      CLI) با خواندن مستقیم کد مقایسه و **همگی تأیید شدند**، به‌علاوه‌ی چند
      وضعیت اضافه (`ACTIVE_JSON`, `ACTIVE_CSV_OR_TEXT`, `ACTIVE_TEXT`,
      `THIRD_PARTY_PAGE`, `ERROR`, `HTTP_{code}`) که در تحلیل ChatGPT نیامده بود.
    - یک نکته‌ی جدید کشف شد که نه در فایل‌های قبلی و نه در تحلیل ChatGPT بود:
      اسکریپت در docstring خودش به یک اسکریپت خواهر با نام
      `iran_market_api_tester_v2.py` اشاره می‌کند که «کل inventory (شامل
      مسیرهای مرده/شخص‌ثالث)» را تست می‌کند — یعنی `test_active_tsetmc_endpoints.py`
      فقط زیرمجموعه‌ی ۵۶‌تایی «قبلاً تأییدشده» را پوشش می‌دهد. محتوای آن
      اسکریپت دیگر در دسترس نیست؛ فقط وجودش مستند می‌شود، نه محتوایش.
    - شمارش ۵۶ endpoint داخل لیست `ENDPOINTS` اسکریپت مستقیماً شمارش و با
      عدد قبلاً مستندشده در بخش «یادداشت‌های عملیاتی» (۵۶ مورد) مطابقت داده شد ✓
  v4.0 — کار انجام‌شده نسبت به v3.1:
    - بازگرداندن تمام یادداشت‌های تفصیلی فایل ۱ که در v3.1 خلاصه/حذف شده بودند:
      • مثال واقعی JSON برای SelectedIndexes/1
      • توضیح کامل معنای پارامتر flow و رفتار واقعی All/{flow} (شامل نمونه‌ی
        تأییدشده‌ی All/2 با ۱۴ شاخص و نام ۸ شاخص صنعتی فرابورس)
      • یادداشت احتیاطی درباره‌ی عدم تست کامل GetInstEffect با Top های دیگر
      • دو نقش متفاوت GetTradeHistory (آمار تجمعی در برابر تحلیل رفتاری/الگو)
        و هشدار صریح که نباید sum(volume) آن را معادل حجم رسمی گرفت
      • فرمول کامل و تأییدشده‌ی عددی محاسبه‌ی درصد تغییر GetIndexCompany
      • هشدار الزام هدر User-Agent (نکته‌ی مشترک با BrsApi.ir در tsetmc-market-pipeline)
      • هشدار عدم یکدستی base path در webgw (Market Date استثناست)
      • هشدار مهم ناهماهنگی: این سند ۹۳ endpoint مستند می‌کند (۶۳ cdn + ۳۰ webgw)
        ولی اسکریپت پایش (test_active_tsetmc_endpoints.py) فقط ۵۶ مورد را پوشش
        می‌دهد — یعنی ~۳۷ مورد (همه‌ی webgw + چند مورد cdn) فقط با تست دستی
        یک‌باره تأیید شده‌اند، نه پایش خودکار دوره‌ای
    - افزودن دو نکته‌ی منحصر‌به‌فرد v3.1 که در فایل ۱ نبود (شمار تقریبی شاخص‌های
      صنعتی؛ یادآوری CORS/403 مرورگر) به بخش شاخص‌ها و یادداشت‌های عملیاتی
    - اعمال اصلاحیه‌ی ۷ شاخص منتخب بورس (به‌جای ۶) در جدول و متن
    - تطبیق با ریپازیتوری GitHub (بدون یافته‌ی جدید؛ شفافیت محدودیت بررسی examples/scripts)
    - بازبینی نهایی end-to-end برای اطمینان از عدم افتادگی هیچ endpoint یا یادداشتی
      نسبت به هر ۴ منبع (نتیجه در انتهای فایل، بخش «چک نهایی کامل بودن سند»)

جدول علامت‌گذاری:
- بدون علامت = در تست ما داده‌ی واقعی برگردانده
- ⚠️ = مسیر معتبر است اما در تست با پارامتر نمونه خالی برگشت (احتمالاً نیاز به پارامتر واقعی یا session دارد)
-->

<div dir="rtl">

# مرجع کامل و نهایی Endpoint های بازار سرمایه ایران (TSETMC) — نسخه ۴.۱

Base URL اصلی (غیررسمی): `https://cdn.tsetmc.com/api/...`
Base URL گیت‌وی رسمی: `https://webgw.tse.ir/...`

## فهرست مطالب

- [شاخص‌ها — Index](#شاخصها--index)
- [قیمت پایانی و تاریخچه — ClosingPrice](#قیمت-پایانی-و-تاریخچه--closingprice)
- [صف خرید/فروش — BestLimits](#صف-خریدفروش--bestlimits)
- [معاملات — Trade](#معاملات--trade)
- [حقیقی/حقوقی — ClientType](#حقیقیحقوقی--clienttype)
- [اطلاعات و جستجوی نماد — Instrument (cdn)](#اطلاعات-و-جستجوی-نماد--instrument-cdn)
- [داده‌های کلی بازار — MarketData](#دادههای-کلی-بازار--marketdata)
- [صندوق‌ها/ETF — Fund](#صندوقهاetf--fund)
- [سهامداران — Shareholder](#سهامداران--shareholder)
- [اطلاعیه‌های کدال — Codal](#اطلاعیههای-کدال--codal)
- [پیام ناظر — Msg](#پیام-ناظر--msg)
- [بورس انرژی — Energy](#بورس-انرژی--energy)
- [داده ثابت/زمان — StaticData](#داده-ثابتزمان--staticdata)
- [آموزش — Learning](#آموزش--learning)
- [تشخیص نوع ابزار مالی و صنعت](#تشخیص-نوع-ابزار-مالی-و-صنعت)
- [تشخیص وضعیت توقف/تعلیق نماد](#تشخیص-وضعیت-توقفتعلیق-نماد)
- [یادداشت‌های عملیاتی و هشدارهای مهم](#یادداشتهای-عملیاتی-و-هشدارهای-مهم)
- [گیت‌وی رسمی جدید — webgw.tse.ir](#گیتوی-رسمی-جدید--webgwtseir)
- [منابع مکمل تأییدشده](#منابع-مکمل-تأییدشده-خارج-از-api-اصلی-cdntsetmccom)
- [پیوست A — جزئیات فنی اسکریپت پایش](#پیوست-a--جزئیات-فنی-اسکریپت-پایش-test_active_tsetmc_endpointspy)
- [پیوست B — نمونه فیلدهای Response (ساختاری)](#پیوست-b--نمونه-فیلدهای-response-از-examples-️-ساختاری-نه-از-تست-زنده)
- [چک نهایی کامل بودن سند](#چک-نهایی-کامل-بودن-سند)

---

## شاخص‌ها — `Index`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| شاخص‌های منتخب بورس | GET | `/Index/GetIndexB1LastAll/SelectedIndexes/1` | شاخص‌های اصلی بورس تهران | `indexB1: 7` ✅ **اصلاح‌شده (نه ۶)** — کل، هم‌وزن، آزاد شناور، بازار اول/دوم، قیمت وزنی-ارزشی و هم‌وزن |
| شاخص‌های منتخب فرابورس | GET | `/Index/GetIndexB1LastAll/SelectedIndexes/2` | همان دسته برای فرابورس | `indexB1: 6` (بدون آزاد شناور — بدون تغییر نسبت به مستند قبلی) |
| همه شاخص‌های بورس (منتخب + صنعتی) | GET | `/Index/GetIndexB1LastAll/All/1` | هم ۷ شاخص منتخب و هم شاخص‌های صنعتی/زیرصنعتی بورس، در یک آرایه‌ی ترکیبی | `indexB1: بسیار زیاد` (~۴۰-۵۰ شاخص صنعتی با کدهای دورقمی `01` تا `74`، به‌علاوه ۷ شاخص منتخب) |
| همه شاخص‌های فرابورس (منتخب + صنعتی) | GET | `/Index/GetIndexB1LastAll/All/2` | همان ترکیب برای فرابورس | `indexB1: 14` (نمونه‌ی تست واقعی: ۶ منتخب + ۸ صنعتی) |
| بیشترین تأثیر روی شاخص کل بورس | GET | `/Index/GetInstEffect/0/1/7` | ۷ نماد با بیشترین تأثیر مثبت/منفی روی شاخص کل بورس | `instEffect: 7` |
| بیشترین تأثیر روی شاخص فرابورس | GET | `/Index/GetInstEffect/0/2/7` | همان برای شاخص کل فرابورس | `instEffect: 7` |
| نمادهای عضو یک شاخص | GET | `/ClosingPrice/GetIndexCompany/{insCode}` | تمام نمادهای شرکت‌های عضو یک شاخص/صنعت خاص؛ `insCode` همان شاخص صنعت است (namespace این endpoint زیر `/ClosingPrice/` است، نه `/Index/`) | آرایه؛ فیلدهای کلیدی و فرمول محاسبه در پایین همین جدول |

**فیلدهای هر آیتم `indexB1` (`GetIndexB1LastAll`):** `insCode`، `lVal30` (نام شاخص به فارسی)، `xDrNivJIdx004` (مقدار فعلی شاخص)، `xPhNivJIdx004`/`xPbNivJIdx004` (بیشترین/کمترین روز)، `xVarIdxJRfV` (درصد تغییر)، `indexChange` (تغییر مطلق)، `hEven` (زمان به‌روزرسانی).

**فیلدهای هر آیتم `GetInstEffect`:** `insCode`، `instrument.lVal30`/`lVal18AFC` (نام/نماد شرکت)، `pClosing`، `instEffectValue` (میزان تأثیر روی شاخص، مثبت یا منفی).

**فیلدهای کلیدی `GetIndexCompany` و فرمول درصد تغییر:** آرایه‌ی `indexCompany`؛ هر آیتم شامل `instrument.lVal18AFC` (نام کوتاه نماد)، `instrument.lVal30` (نام کامل)، `pDrCotVal` (آخرین قیمت معامله)، `priceYesterday` (قیمت دیروز). فیلد آماده‌ای برای درصد تغییر وجود ندارد؛ باید دستی محاسبه شود:
```
priceChange = pDrCotVal - priceYesterday
percent = priceChange / priceYesterday * 100
```
تأیید عددی واقعی: ۲۳۸۱۰ − ۲۳۱۲۰ = ۶۹۰ ✓

نمونه‌ی واقعی از `SelectedIndexes/1`:
```json
{"insCode":"32097828799138957","lVal30":"شاخص كل","xDrNivJIdx004":5182613.78,"indexChange":-104242.36,"xVarIdxJRfV":-1.9717}
```

فهرست کامل ۷ شاخص منتخب بورس (کشف تجربی ۱۴۰۵/۰۴/۲۴):

| نام | `insCode` |
|---|---|
| شاخص كل | `32097828799138957` |
| شاخص قیمت (وزنی-ارزشی) | `5798407779416661` |
| شاخص كل هم وزن | `67130298613737946` |
| شاخص قیمت (هم وزن) | `8384385859414435` |
| شاخص آزاد شناور | `49579049405614711` |
| بازار اول | `62752761908615603` |
| بازار دوم | `71704855530629737` |

شاخص «آزاد شناور» (`insCode: 49579049405614711`) در فرابورس معادلی در میان ۶ شاخص منتخب ندارد — افزوده‌شدن آن مختص بورس است، نه یک الگوی عمومی برای هر دو `flow`.

**نکته کلیدی — پارامتر `flow` و معنای `All`:** پارامتر دوم در هر دو خانواده (`SelectedIndexes/{flow}` و `GetInstEffect/0/{flow}/7`) همان کد جریان بازار است: `1`=بورس، `2`=فرابورس. مسیر `All/{flow}` برخلاف تصور اولیه، فقط شاخص‌های صنعتی را برنمی‌گرداند — **هم شاخص‌های منتخب و هم شاخص‌های صنعتی همان بازار را یک‌جا در یک آرایه می‌دهد.** یعنی برای گرفتن دیده‌بان کامل شاخص‌های یک بازار در یک درخواست، همین یک اندپوینت (`All/1` یا `All/2`) کافی است و نیازی به ترکیب با `SelectedIndexes` نیست. مثال تأییدشده: `All/2` دقیقاً همان ۱۴ شاخص فرابورس (۶ منتخب + ۸ صنعتی: اركان و نهادهاي مالي، چوب، دستگاه‌هاي برقي، فني مهندسي، لاستيك، ماشين آلات فرابورس، محصولات فلزي، كاشي و سراميك) را در یک پاسخ برگرداند. برای بورس (`All/1`)، تعداد شاخص‌های صنعتی به‌مراتب بیشتر است (~۴۰-۵۰ مورد، با کدهای دورقمی `01` تا `74` که در آن‌ها شکاف/جای‌خالی هم دیده می‌شود).

> **نکته‌ی معماری مهم:** برای جدا کردن «شاخص‌های منتخب» از «شاخص‌های صنعتی» داخل پاسخ `All/{flow}`، باید ۷ (بورس) یا ۶ (فرابورس) شاخص منتخب را با `insCode`های شناخته‌شده‌ی جدول بالا فیلتر/حذف کرد؛ باقی‌مانده صنعتی‌ها هستند. **حدس زدن این فیلتر بدون تأیید تجربی «دقت ساختگی» است** و باید طبق اصل کلی این پروژه رد شود؛ فیلتر کردن بر اساس `insCode` (نه شمارش ثابت یا نام) روش درست و مقاوم است — یک عدد ثابت `6` یا `7` برای هر دو `flow` فرض نشود، هرکدام مقدار خودش را دارد.

**نتیجه‌ی عملی:** در هر منطقی که این endpoint را برای جداسازی «شاخص‌های منتخب» از «شاخص‌های صنعتی» می‌خواند (مثل `fetch_industry_indices.py` یا `show_industry_indices.py`)، باید حساب کند که تعداد شاخص‌های منتخب بین دو بازار متفاوت است (۷ برای بورس، ۶ برای فرابورس).

**⚠️ یادداشت احتیاطی درباره‌ی `GetInstEffect`:** این دو ردیف فقط با `Top=7` و بدون تست پارامتر ساختگی یا مقادیر دیگر `Top` بررسی شده‌اند؛ برخلاف بقیه‌ی جدول‌های این فایل که رفتار خالی/۵۰۰ آن‌ها با پارامتر نمونه صریحاً تست شده، این دو هنوز از نظر آن معیار کامل تأیید نشده‌اند. قبل از اتکای پروداکشن به آن‌ها، تست با `Top` های دیگر و یک `insCode`/تاریخ نامعتبر توصیه می‌شود.

---

## قیمت پایانی و تاریخچه — `ClosingPrice`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| نمودار روزانه (ChartData) | GET | `/ClosingPrice/GetChartData/{InsCode}/D` | داده‌ی OHLCVT با تفکیک روزانه برای رسم نمودار | `closingPriceChartData: 1016` |
| قیمت پایانی یک روز | GET | `/ClosingPrice/GetClosingPriceDaily/{InsCode}/{DEven}` | خلاصه‌ی قیمت پایانی یک روز مشخص | `closingPriceDaily: object` |
| لیست قیمت پایانی (Top) | GET | `/ClosingPrice/GetClosingPriceDailyList/{InsCode}/{Top}` | تاریخچه‌ی قیمت پایانی؛ با `Top=0` همه‌ی رکوردها برمی‌گردد | `closingPriceDaily: 10` |
| لیست قیمت پایانی (همه) | GET | `/ClosingPrice/GetClosingPriceDailyList/{InsCode}/0` | کل تاریخچه‌ی قیمت پایانی نماد از ابتدا | `closingPriceDaily: 1084` |
| لیست قیمت پایانی CSV | GET | `/ClosingPrice/GetClosingPriceDailyListCSV/{InsCode}/0` | همان تاریخچه‌ی کامل، به‌صورت خروجی شبه-CSV | `` |
| تاریخچه‌ی قیمت پایانی (قدیمی) | GET | `/ClosingPrice/GetClosingPriceHistory/{InsCode}/{DEven}` | اسنپ‌شات‌های تاریخی/درون‌روزی نسخه‌ی قدیمی ClosingPriceData | `closingPriceHistory: 5021` |
| اطلاعات قیمت امروز | GET | `/ClosingPrice/GetClosingPriceInfo/{InsCode}` | خلاصه‌ی قیمت امروز و وضعیت نماد | `closingPriceInfo: object` |
| تاریخچه‌ی همه‌ی نمادها در یک روز | GET | `/ClosingPrice/GetInstrmentsHistoryInDay/{DEven}` | اطلاعات قیمت همه‌ی نمادها در یک تاریخ مشخص | `closingPriceDailyHistoryWithInstDetails: 1923` |
| تقویم معاملاتی نماد | GET | `/ClosingPrice/GetInstrumentCalendar/{InsCode}` | تقویم معاملاتی نماد همراه با قیمت پایانی و حجم هر روز | `instrumentCalendar: 1084` |
| دیده‌بان بازار ⚠️ | GET | `/ClosingPrice/GetMarketWatch` | دیده‌بان بازار؛ ممکن است بدون پارامتر/session از CDN خالی برگردد | `marketwatch: 0` |
| دیده‌بان بازار Excel (legacy) | GET | `https://old.tsetmc.com/tsev2/excel/MarketWatchPlus.aspx?d=0` | جایگزین واقعی و کارکردِ ردیف بالا (جزئیات کامل در بخش «منابع مکمل») | `rows: 3136 (Excel)` |
| تعدیل قیمت بر اساس جریان بازار ⚠️ | GET | `/ClosingPrice/GetPriceAdjustByFlow/{Flow}/{Top}` | رویدادهای تعدیل قیمت بر اساس جریان بازار (`Flow`) | `priceAdjust: 0` |
| تعدیل قیمت نماد ⚠️ | GET | `/ClosingPrice/GetPriceAdjustList/{InsCode}` | رویدادهای تعدیل قیمت برای یک نماد | `priceAdjust: 0` |
| نمادهای هم‌صنعت | GET | `/ClosingPrice/GetRelatedCompany/{CSecVal}` | نمادهای هم‌صنعت به‌همراه تاریخچه‌ی ۳۰ روزه | `relatedCompany: 65` |

> نکته: endpoint مربوط به «نمادهای عضو یک شاخص» (`GetIndexCompany`) هرچند از نظر namespace زیر `/ClosingPrice/` است، برای یکدستی موضوعی در بخش «شاخص‌ها — Index» بالاتر مستند شده (همراه با فیلدها و فرمول محاسبه‌ی درصد تغییر).

---

## صف خرید/فروش — `BestLimits`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| صف خرید/فروش فعلی | GET | `/BestLimits/{InsCode}` | صف خرید/فروش ۵ سطحی فعلی (Best Limits) | `bestLimits: 5` |
| صف خرید/فروش تاریخی | GET | `/BestLimits/{InsCode}/{DEven}` | اسنپ‌شات‌های تاریخی صف خرید/فروش برای یک روز معاملاتی | `bestLimitsHistory: 24660` |

> ⚠️ **BestLimits یک delta feed است، نه یک اسنپ‌شات کامل.** برای بازسازی دقیق عمق order book به‌ازای هر لحظه، باید یک stateful carry-forward reconstruction پیاده‌سازی کنید. بعد از این بازسازی، پوشش داده عملاً کامل است (رقم پایین اولیه‌ی پوشش، خودش یک artifact اندازه‌گیری بوده، نه محدودیت واقعی داده).

---

## معاملات — `Trade`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| معاملات آخرین روز | GET | `/Trade/GetTrade/{InsCode}` | معاملات آخرین روز معاملاتی | `trade: 14818` |
| تاریخچه‌ی معاملات | GET | `/Trade/GetTradeHistory/{InsCode}/{DEven}/false` | معاملات درون‌روزی تاریخی | `tradeHistory: 14818` |
| معاملات تجمیعی درون‌روز | GET | `/Trade/GetTradeIntraDay/{InsCode}` | معاملات تجمیع‌شده‌ی درون‌روزی آخرین روز معاملاتی | `tradeIntraDay: 105` |
| توزیع حجم معاملات | GET | `/Trade/GetTradeVolume/{InsCode}` | توزیع حجم معاملات بر اساس قیمت/زمان | `tradeVolume: 798` |

> ⚠️ **شکاف پوشش شناخته‌شده:** در نمونه‌های تست‌شده، `GetTradeHistory` نسبت به آمار رسمی بورس حدود ۳۶-۳۸٪ کسری نشان داد (این عدد از تعداد محدودی نماد/روز به دست آمده، نه از کل بازار — قبل از اتکای پروداکشن، بهتر است روی نمادها/روزهای بیشتری تکرار شود). برای ارقام تجمعی (حجم/ارزش/تعداد کل معاملات)، `ClosingPriceHistory` (فیلدهای `qTotTran5J`, `qTotCap`, `zTotTran`) منبع معتبرتر و مطابق با اعداد نمایش‌داده‌شده‌ی بورس است.

**دو نقش متفاوت `GetTradeHistory` — نباید با هم اشتباه شوند:**
- **برای آمار دقیق نهایی (حجم/ارزش/تعداد کل معاملات یک روز):** همیشه از `ClosingPriceHistory` استفاده شود، نه `GetTradeHistory`. جمع‌زدن `sum(trades.volume)` روی `GetTradeHistory` را هرگز معادل حجم رسمی بازار فرض نکن — با توجه به کسری ۳۶-۳۸٪، این جمع همیشه کمتر از رقم واقعی خواهد بود.
- **برای تحلیل رفتار درون‌روزی (نه آمار تجمعی):** `GetTradeHistory` همچنان می‌تواند مفید باشد، چون حتی با معاملات ازدست‌رفته، الگوی رفتاری (نه مقدار مطلق) اغلب قابل استخراج است. کاربردهای مناسب: سرعت معاملات (Trade Velocity)، تشخیص فعالیت ناگهانی (Burst Activity)، تهاجمی‌بودن قیمت (Price Aggression)، فشار خرید/فروش، خوشه‌بندی معاملات. در این کاربردها، خودِ کسری داده باعث خطای بزرگ در نتیجه‌ی نهایی نمی‌شود چون خروجی یک الگوی نسبی است نه یک عدد تجمعی مطلق.

---

## حقیقی/حقوقی — `ClientType`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| حقیقی/حقوقی فعلی | GET | `/ClientType/GetClientType/{InsCode}/1/0` | داده‌ی فعلی خرید/فروش حقیقی و حقوقی | `clientType: object` |
| حقیقی/حقوقی همه‌ی نمادها | GET | `/ClientType/GetClientTypeAll` | داده‌ی حقیقی/حقوقی همه‌ی نمادها از آخرین روز معاملاتی | `clientTypeAllDto: 1878` |
| حقیقی/حقوقی تاریخی | GET | `/ClientType/GetClientTypeHistory/{InsCode}/{DEven}` | داده‌ی تاریخی خرید/فروش حقیقی و حقوقی برای نماد/روز مشخص | `clientType: object` |

---

## اطلاعات و جستجوی نماد — `Instrument` (cdn)

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| تاریخچه‌ی ساده‌ی نماد | GET | `/Instrument/GetInstrumentHistory/{InsCode}/{DEven}` | متادیتای ساده‌ی تاریخی نماد برای یک روز | `instrumentHistory: object` |
| هویت نماد | GET | `/Instrument/GetInstrumentIdentity/{InsCode}` | هویت نماد، صنعت، زیرصنعت، نام‌ها | `instrumentIdentity: object` |
| اطلاعات کامل نماد | GET | `/Instrument/GetInstrumentInfo/{InsCode}` | اطلاعات کامل نماد شامل EPS، صنعت، آستانه‌های قیمتی ثابت | `instrumentInfo: object` |
| جستجوی نماد | GET | `/Instrument/GetInstrumentSearch/{Query}` | جستجوی نماد بر اساس کلیدواژه | `instrumentSearch: 41` |
| تغییرات سرمایه ⚠️ | GET | `/Instrument/GetInstrumentShareChange/{InsCode}` | تغییرات تعداد سهام نماد (افزایش/کاهش سرمایه) | `instrumentShareChange: 0` |
| تغییرات سرمایه بر اساس جریان بازار ⚠️ | GET | `/Instrument/GetInstrumentShareChangeByFlow/{Flow}/{Top}` | تغییرات سرمایه بر اساس جریان بازار | `instrumentShareChange: 0` |

---

## داده‌های کلی بازار — `MarketData`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| وضعیت نماد در یک روز | GET | `/MarketData/GetInstrumentState/{InsCode}/{DEven}` | وضعیت نماد (مجاز/متوقف و...) در یک روز مشخص | `instrumentState: 1` |
| آخرین تغییرات وضعیت نمادها | GET | `/MarketData/GetInstrumentStateTop/{Top}` | نمادهایی که اخیراً وضعیت‌شان تغییر کرده | `instrumentState: 10` |
| آمار نماد | GET | `/MarketData/GetInstrumentStatistic/{InsCode}` | آمار نماد مثل میانگین ارزش/حجم/تعداد معاملات | `instrumentStatistic: 88` |
| همه‌ی پارامترهای ارزشی همه‌ی نمادها | GET | `/MarketData/GetInstValueAllInstAllParam` | همه‌ی پارامترهای ارزشی همه‌ی نمادها؛ حجم پاسخ بسیار بالا (~۲۴ مگابایت) | `instValueAllInstAllParam: 299174` |
| نمای کلی بازار | GET | `/MarketData/GetMarketOverview/{Flow}` | نمای کلی بازار بر اساس جریان، شامل مقادیر شاخص و فعالیت بازار | `marketOverview: object` |
| خلاصه‌ی صنایع | GET | `/MarketData/GetSectorsSummary` | خلاصه‌ی وضعیت صنایع | `sectorSummeries: 49` |
| آستانه‌ی قیمتی ثابت | GET | `/MarketData/GetStaticThreshold/{InsCode}/{DEven}` | آستانه‌ی قیمتی ثابت نماد برای یک روز | `staticThreshold: 2` |

---

## صندوق‌ها/ETF — `Fund`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| ETF بر اساس InsCode | GET | `/Fund/GetETFByInsCode/{InsCode}` | داده‌ی ETF/صندوق شامل مقادیر شبه-NAV صدور/ابطال | `etf: object` |
| جزئیات صندوق ۰ | GET | `/Fund/GetFundInDetail/0` | جزئیات صندوق و آمار NAV | `fund: object` |
| جزئیات صندوق ۱ | GET | `/Fund/GetFundInDetail/1` | نسخه‌ی دیگر جزئیات صندوق | `fund: object` |

---

## سهامداران — `Shareholder`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| تغییرات سهامداران (قدیمی) | GET | `/Shareholder/{InsCode}/{DEven}` | تغییرات سهامداران در یک روز مشخص | `shareShareholder: 4` |
| آخرین سهامداران ⚠️ | GET | `/Shareholder/GetInstrumentShareHolderLast/{InsCode}` | آخرین لیست سهامداران نماد | `shareHolder: 0` |
| همه‌ی تغییرات سهامداران ⚠️ | GET | `/Shareholder/GetShareHolderChanges/false` | همه‌ی تغییرات سهامداران در روزهای اخیر | `shareHoldersChanges: 0` |
| لیست شرکت‌های سهامدار ⚠️ | GET | `/Shareholder/GetShareHolderCompanyList/{ShareHolderShareID}` | سایر مالکیت‌های یک سهامدار | `shareHolderShare: 0` |
| تاریخچه‌ی سهامداران ⚠️ | GET | `/Shareholder/GetShareHolderHistory/{InsCode}/{DEven}/{Top}` | تغییرات سهامداران برای نماد/روز مشخص | `shareHolder: 0` |

---

## اطلاعیه‌های کدال — `Codal`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| آخرین اطلاعیه‌های کدال | GET | `/Codal/GetPreparedData/{Top}` | آخرین اطلاعیه‌های کدال | `preparedData: 10` |
| اطلاعیه‌های کدال یک نماد | GET | `/Codal/GetPreparedDataByInsCode/{Top}/{InsCode}` | اطلاعیه‌های کدال یک نماد مشخص | `preparedData: 10` |
| ناشر کدال بر اساس نماد | GET | `/Codal/GetCodalPublisherBySymbol/{Symbol}` | یافتن ناشر کدال بر اساس نماد | `codalPublisher: object` |
| پیوست فایل بر اساس شناسه ردیف | GET | `/Codal/GetFileAttachmentByMainTableRowId/{MainTableRowId}` | پیوست کدال بر اساس شناسه‌ی ردیف اصلی | `fileAttachment: 1` |
| پیوست فایل بر اساس شماره پیگیری ⚠️ | GET | `/Codal/GetFileAttachmentByTracingNo/{TracingNo}` | پیوست کدال بر اساس شماره پیگیری | `fileAttachment: 0` |

---

## پیام ناظر — `Msg`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| پیام‌های ناظر بر اساس جریان بازار | GET | `/Msg/GetMsgByFlow/{Flow}/{Top}` | پیام‌های ناظر بازار بر اساس جریان بازار | `msg: 10` |
| پیام‌های ناظر یک نماد | GET | `/Msg/GetMsgByInsCode/{InsCode}` | پیام‌های ناظر برای یک نماد مشخص | `msg: 354` |

---

## بورس انرژی — `Energy`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| حراج بورس انرژی بر اساس شناسه | GET | `/Energy/GetAuctionById/{AuctionId}` | اطلاعات یک حراج بورس انرژی بر اساس شناسه | `auction: object` |
| معاملات حراج بر اساس شناسه ⚠️ | GET | `/Energy/GetAuctionTradeById/{AuctionId}` | معاملات یک حراج بورس انرژی بر اساس شناسه | `auctionTrade: 0` |

---

## داده ثابت/زمان — `StaticData`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| داده‌ی ثابت | GET | `/StaticData/GetStaticData` | توضیحات/نام‌های ثابت مثل نوع اوراق، صنایع، YVal | `staticData: 75` |
| زمان سرور | GET | `/StaticData/GetTime` | تاریخ و زمان سرور | `` |

---

## آموزش — `Learning`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| موضوعات آموزشی | GET | `/Learning/GetLearningTopics` | موضوعات آموزشی/راهنما از سایت TSETMC | `learningTopics: 78` |

---

## تشخیص نوع ابزار مالی و صنعت

تست‌شده روی ۴ نوع واقعی: سهم عادی (فولاد)، ETF اهرمی (اهرم)، صندوق کالایی (عیار)، آپشن (ضهرم۴۰۲۳).

### صنعت/بخش — از `GetInstrumentIdentity`

فیلدهای `sector.lSecVal` و `subSector.lSoSecVal`:
```json
"sector": {"cSecVal": "68 ", "lSecVal": "صندوق سرمايه گذاري قابل معامله"},
"subSector": {"cSoSecVal": 6821, "lSoSecVal": "صندوق هاي سرمايه گذاري اهرمي"}
```
همین فیلدها عیناً در `GetInstrumentInfo` هم تکرار شده‌اند.

### نوع دقیق ابزار — از `GetInstrumentHistory`

| منبع | مقدار | نوع ابزار |
|---|---|---|
| پیشوند `cIsin` | `IRO1...` | سهم عادی — بورس اصلی یا بازار دوم (تأییدشده با فولاد و وسکهبو) |
| پیشوند `cIsin` | `IRO5...` | سهم عادی در بازار نوآفرین/رشد فرابورس (تأییدشده با سحرخیز) |
| پیشوند `cIsin` | `IRT1...` | واحد صندوق/ETF (تأییدشده با اهرم) |
| پیشوند `cIsin` | `IRO9...` | آپشن (تأییدشده با ضهرم۴۰۲۳) |
| پیشوند `cIsin` | `IRB3TR...` | اوراق/اسناد خزانه اسلامی-اخزا (تأییدشده با اخزا۲۰۱/۲۰۲) |
| `cgrValCotTitle` | نام فارسی بازار فرعی | شفاف‌ترین فیلد — می‌گوید دقیقاً کدام تابلو (بورس اصلی/بازار دوم/نوآفرین/ابزار نوین مالی/مشتقه) |
| `flow` + `flowTitle` | کد بازار کلی | درشت‌تر از `cgrValCotTitle`؛ فقط بورس/فرابورس/مشتقه/انرژی را جدا می‌کند |

**هشدار مهم:** پیشوند سوم/چهارم ISIN (`IRO1` در برابر `IRO5`) فقط نوع کلی ابزار (سهم عادی) را نشان می‌دهد، نه تابلوی دقیق بازار؛ برای آن حتماً `cgrValCotTitle` را هم چک کنید — مثلاً هم فولاد (بورس اصلی) و هم وسکهبو (بازار دوم) هر دو `IRO1` دارند اما `cgrValCot` متفاوت (`N1` در برابر `N2`).

**آتی هنوز تأیید نشده:** با جست‌وجوی کلیدواژه‌ای («سکه»، «زعف») در `GetInstrumentSearch`، هیچ قرارداد آتی واقعی پیدا نشد — هر دو نتیجه به‌طور تصادفی به نام شرکت‌های عادی (نه قرارداد مشتقه) خورد. به‌احتمال زیاد قراردادهای آتی کالایی (سکه/زعفران) روی بورس کالای ایران (IME) معامله می‌شوند و ممکن است اصلاً در پایگاه‌داده‌ی `cdn.tsetmc.com` نباشند.

### تفاوت رفتار endpoint بر اساس نوع ابزار

*(بر اساس یک نمونه از هر نوع ابزار — فولاد/اهرم/عیار/ضهرم۴۰۲۳؛ نه آزمون آماری روی چند نماد از هر دسته)*

| اندپوینت | سهم | ETF/صندوق | آپشن |
|---|---|---|---|
| `GetETFByInsCode` | ❌ HTTP 500 | ✅ کار می‌کند | ❌ HTTP 500 |
| `GetPriceAdjustList` | ✅ داده واقعی | خالی (ساختاری) | خالی |
| `GetInstrumentShareChange` | ✅ داده واقعی | خالی (ساختاری) | خالی |
| `GetShareholderChangesOld` | ✅ داده واقعی | ✅ داده واقعی | ❌ خالی |
| `GetPreparedDataByInsCode` (کدال) | ✅ | ✅ | ❌ خالی (آپشن ناشر کدال ندارد) |
| `GetMsgByInsCode` (پیام ناظر) | ✅ | ✅ | ❌ خالی |

---

## تشخیص وضعیت توقف/تعلیق نماد

فیلد کلیدی: `cEtaval` و `cEtavalTitle` داخل شیء `instrumentState`، که هم در `GetInstrumentState/{InsCode}/{DEven}` و هم داخل `GetClosingPriceInfo` دیده می‌شود.

نمونه‌ی واقعی — نماد فعال (اهرم):
```json
"cEtaval": "A ", "cEtavalTitle": "مجاز", "underSupervision": 0
```

نمونه‌ی واقعی — نماد متوقف (فولاد، تعلیق‌شده به دلیل بررسی افشای اطلاعات):
```json
"cEtaval": "IS", "cEtavalTitle": "ممنوع-متوقف", "underSupervision": 3
```

**نتیجه‌ی عملی:** قبل از تفسیر خالی‌بودن یا خطای ۵۰۰ در endpointهای تاریخی (`Trade history`, `BestLimits historical`, `ClientType history`) برای یک نماد و تاریخ خاص، ابتدا `cEtavalTitle` را چک کن — اگر «متوقف» یا «ممنوع» بود، خالی‌بودن داده طبیعی و مورد انتظار است، نه یک نقص در endpoint.

---

## یادداشت‌های عملیاتی و هشدارهای مهم

1. **API غیررسمی و مستندنشده است.** هیچ SLA یا تعهد پایداری از TSETMC وجود ندارد؛ همیشه با یک اسکریپت پایش (`test_active_tsetmc_endpoints.py`، شامل ۵۶ endpoint شناخته‌شده — ۵۵ مسیر JSON روی `cdn.tsetmc.com` + یک مسیر Excel روی `old.tsetmc.com`) دوره‌ای تست شود.
2. **رفتار endpoint به سه عامل مستقل بستگی دارد**، نه فقط به این‌که «کار می‌کند یا نه»:
   - نوع ابزار مالی (سهم/ETF/صندوق/آپشن) — بخش «تشخیص نوع ابزار مالی»
   - وضعیت توقف/تعلیق نماد در تاریخ درخواستی — بخش «تشخیص وضعیت توقف/تعلیق نماد»
   - باز یا بسته بودن روز معاملاتی (تاریخ «امروز» می‌تواند داده‌ی ناقص یا خطای ۵۰۰ برای فیلدهای «تاریخچه‌ای» بدهد، حتی برای نماد کاملاً سالم)
3. **گاهی یک endpoint برای یک تاریخ خاص به‌طور موقت و بدون دلیل ساختاری خالی برمی‌گردد** (مشاهده‌شده در `GetTradeHistory` برای ۶ تیر که بعداً با تست مجدد رفع شد). قبل از نتیجه‌گیری قطعی از یک نتیجه‌ی خالی غیرمنتظره، درخواست را دوباره امتحان کن.
4. **حجم برخی endpoint خیلی بالاست** (`GetInstValueAllInstAllParam` ~۲۴ مگابایت). برای استفاده‌ی مکرر حتماً cache شود.
5. **پارامترهای ساختگی (fake id) نتیجه‌ی خالی می‌دهند، نه خطا** — برای تست واقعی `TracingNo`, `AuctionId`, `ShareHolderShareID`، باید مقدار واقعی از یک endpoint دیگر (مثلاً `GetPreparedData` برای TracingNo) استخراج شود.
6. آخرین تست کامل: تیر ۱۴۰۵ — روی ۴ نوع ابزار (سهم، ETF، صندوق، آپشن)، ۲ نماد تعلیق‌شده و فعال، و ۴ تاریخ مختلف.
7. **هدر `User-Agent` روی همه‌ی endpoint های `cdn.tsetmc.com` الزامی است** — بدون آن سرور با HTTP 403 پاسخ می‌دهد (رفتاری مشابه با `BrsApi.ir` که در `tsetmc-market-pipeline` هم تأیید شده). هر اسکریپت/فراخوانی جدید باید این هدر را از ابتدا ست کند، نه فقط بعد از برخورد با ۴۰۳ به آن پی ببرد. **علاوه بر این، فراخوانی این endpoint ها از مرورگر (client-side) معمولاً با CORS/403 مواجه می‌شود** — پس در معماری هر ابزاری که این API ها را مصرف می‌کند، یک بک‌اند واسط لازم است، نه فراخوانی مستقیم از فرانت‌اند.
8. **⚠️ ناهماهنگی بین این سند و اسکریپت پایش:** این فایل در حال حاضر ۹۳ endpoint مستند می‌کند (۶۳ در `cdn.tsetmc.com` + ۳۰ در `webgw.tse.ir`)، در حالی که `test_active_tsetmc_endpoints.py` فقط ۵۶ endpoint را پوشش می‌دهد (که همگی روی `cdn.tsetmc.com` هستند؛ هیچ‌کدام از ۳۰ endpoint جدید `webgw.tse.ir` هنوز در چرخه‌ی تست خودکار نیستند). یعنی حدود ۳۷ endpoint این فایل — از جمله همه‌ی `webgw` — فقط با یک تست دستی یک‌باره تأیید شده‌اند و هیچ تضمینی نیست که هنوز کار کنند. تا زمانی که این دو همگام نشوند (یا با گسترش اسکریپت پایش، یا با یک registry مرکزی مشترک)، هر تصمیم پروداکشن روی این ۳۷ مورد باید با یک تست دستی تازه تأیید شود.

---

## گیت‌وی رسمی جدید — `webgw.tse.ir`

کشف‌شده از طریق بازرسی HAR در Chrome DevTools روی صفحات `www.tse.ir`. بر خلاف `cdn.tsetmc.com` (غیررسمی)، این آدرس زیرساخت رسمی سایت tse.ir است. کلید اصلی نماد در این گیت‌وی، برخلاف `InsCode` عددی cdn، مستقیماً **ISIN کامل** (`cIsin`) است — نیازی به تبدیل InsCode ندارد.

Base URL: `https://webgw.tse.ir/...`

**⚠️ هشدار — base path یکدست نیست:** بیشتر endpoint های این گیت‌وی زیر `/InstrumentProvider/api/v1/...` هستند، اما `Market Date` استثناست و مستقیماً زیر `/api/v1/PublicData/...` قرار دارد (بدون پیشوند `InstrumentProvider`). قبل از ساخت یک تابع کمکی عمومی برای ساخت URL (مثلاً با یک base path ثابت)، به این استثنا توجه کن.

### داده‌های عمومی و صفحه اصلی

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Instrument Slider | GET | `/InstrumentProvider/api/v1/Instrument/InstrumentSliderQuery/fa` | آرایه کامل تمام نمادها با آخرین قیمت زنده و درصد تغییر (نوار لغزنده صفحه اصلی) | آرایه؛ فیلدها: `instrumentId` (ISIN)، `instrument_Name`، `lastprice`، `pricechangepercent`، `state` |
| Market Date | GET | `/api/v1/PublicData/MarketDate/fa` | ساعت باز/بسته بودن بازار برای بورس و فرابورس | آرایه ۲ آیتمی: `stockTypeId`، `openTime`، `closeTime`، `isOpen` |
| Company State | GET | `/InstrumentProvider/api/v1/Instrument/CompanyState/fa` | وضعیت تعلیق/توقف تمام شرکت‌ها همراه با **متن کامل دلیل تعلیق** (`dalils`) و تاریخ آخرین تغییر | لیست کامل؛ فیلدها: `nam`، `statusCode`، `vaziyatdesc`، `lastdatechange`، `dalils` (آرایه متن) |
| Market Summary | GET | `/InstrumentProvider/api/v1/Instrument/MarketSummary/fa` (پارامتر `MarketId` اختیاری به‌نظر می‌رسد؛ در نمونه‌ها با و بدون آن یک خروجی داده) | شاخص کل، شاخص هم‌وزن و تغییرات، ارزش کل بازار، تعداد/حجم/ارزش کل معاملات روز | آبجکت: `allShareIndex(Change/Percent)`، `weightedOverallIndex(Change/Percent)`، `marketvalue`، `tradecount`، `tradevolume`، `tradevalue` |
| Index Live By Id | GET | `/InstrumentProvider/api/v1/Instrument/IndexLiveById/fa?InstrumentId={InstrumentId}` | لایو شاخص بر اساس شناسه (نمونه: `IRX6XTPI0006`, `IRX6XTPI0026`) | در تست ما همیشه HTTP 204 (خالی) برگشت — احتمالاً فقط در ساعات باز بودن بازار پاسخ می‌دهد؛ نیاز به تست مجدد در ساعات معاملاتی |
| CMS News | GET | `/cmssite/api/v1/Notice/SimpleList/fa?CategoryId=News&PageSize={n}` | آخرین اخبار سایت tse.ir | آرایه اخبار با عنوان، تاریخ، و خلاصه |
| CMS Announcements | GET | `/cmssite/api/v1/Notice/SimpleList/fa?CategoryId=Announcement&PageSize={n}` | آخرین اطلاعیه‌های سایت tse.ir | آرایه اطلاعیه‌ها |
| CMS Banner | GET | `/cmssite/api/v1/Banner/List/fa` | لیست بنرهای صفحه اصلی | آرایه بنرها |
| CMS Menu | GET | `/cmssite/api/v1/Menu/MainMenu/fa` | ساختار منوی اصلی سایت | ساختار درختی منو |

### دیده‌بان بازار — `MarketWatch` (کلید نماد = ISIN کامل، نه InsCode)

هر endpoint یک آبجکت `{"Items": [...]}` برمی‌گرداند. فیلدهای عددی اکثراً به‌صورت `{"value": ..., "state": ...}` هستند، نه مقدار خام.

| نام | متد | آدرس | کارکرد | تعداد آیتم (نمونه تست) |
|---|---|---|---|---|
| MarketWatch Cash | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchCash/fa` | دیده‌بان کامل بازار نقدی (سهام) با صنعت/زیرصنعت | `Items: 533` |
| MarketWatch ETF | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchEtf/fa` | دیده‌بان صندوق‌ها/ETF شامل NAV (`navValue`) و ارزش بازار (`marketValue`) | `Items: 293` |
| MarketWatch Future | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchFuture/fa` | دیده‌بان قراردادهای آتی | `Items: 7` |
| MarketWatch Option | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchOption/fa` | دیده‌بان اختیار معامله (کال/پوت جدا)؛ شامل `qeymateEmal` (قیمت اعمال)، `qeymateMabna`، `baghimandetasarresid` (روز مانده تا سررسید)، `tarixSarresid` | `Items: 82` |
| MarketWatch Debt | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchDebt/fa` | دیده‌بان اوراق بدهی (مشارکت، اخزا و مشابه)؛ شامل بازده تا سررسید (`lastPriceYTM`, `closingPriceYTM`, `sellPriceYTM`, `buyPriceYTM`) و `tarixSarresid` | `Items: 248` |
| MarketWatch TradeOption | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchTradeOption/fa` | دیده‌بان **جفت‌شده** کال/پوت هر قرارداد اختیار در یک ردیف (پیشوند `buy...` برای کال/اختیار خرید و `sell...` برای پوت/اختیار فروش)؛ شامل `buyQeymateEmal`, `buyAndazeyeQarardad` (اندازه قرارداد)، `buyBaqimandeTaSarresId` | `Items: 404` |
| MarketWatch TALMarket | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchTALMarket/fa` | دیده‌بان بازار **معاملات پایانی (Trading At Last)** — مرحله‌ای که از ۲۰ آبان ۱۴۰۴ در بورس تهران اجرایی شد: از ساعت ۱۲:۴۵ تا ۱۳:۰۰ فقط در قیمت پایانی ثابت ساعت ۱۲:۳۰، مستقل از سفارش‌های عادی، فقط برای نمادهای تابلوی اصلی بازار اول؛ نمادهای مشمول با عدد ۴ در انتهای نام مشخص می‌شوند (مثلاً «بترانس۴») | `Items: 0` در تست ما — این endpoint به‌درستی تعریف شده ولی در تست‌های ما **خارج از ساعت ۱۲:۴۵–۱۳:۰۰** همیشه خالی بوده؛ برای دریافت داده باید دقیقاً در همان پنجره زمانی فراخوانی شود (این رفتار فقط در همون بازه‌ی زمانی محدود تست شده، نه در چند روز مختلف) |

**فیلدهای مشترک در Cash/ETF/Option/Debt:** `instrumentId` (ISIN)، `instrumentName`، `companyNamePersian`، `tradeVolume/Value/Count`، `lastPrice(Change/Percent)`، `closingPrice(Change/Percent)`، `yesterdayPrice`، `sellPrice/buyPrice`، `marketid/marketname`، `markettypeid/name`، `industryid/name`، `industrysubid/name`، `stateid/statename`.

**نکات عملیاتی:**
- این ۴ endpoint، تب‌های باقی‌مانده‌ای بودند که قبلاً از طریق HAR capture شناسایی نشده بودند (Option، Debt، TradeOption، TALMarket) — اکنون همراه با Cash، ETF و Future، پوشش کامل تب‌های دیده‌بان بازار در `webgw.tse.ir` تکمیل شد.
- `MarketWatchTALMarket` در تست فعلی آرایه خالی داد؛ طبق الگوی مشاهده‌شده در cdn.tsetmc.com (پارامتر ساختگی/روز بدون فعالیت → خروجی خالی نه خطا)، این می‌تواند به‌دلیل نبود نماد فعال در آن بازار در لحظه‌ی تست باشد، نه خرابی endpoint. نیاز به تست مجدد در روز/زمان دیگر برای تأیید قطعی.
- `MarketWatchTradeOption` ساختار داده متفاوتی دارد (هر ردیف = یک جفت کال/پوت با پیشوند `buy`/`sell`)، برخلاف `MarketWatchOption` که هر ردیف یک قرارداد مجزا (کال یا پوت) است. برای تحلیل نوسان ضمنی اهرم (ضهرم/طهرم که در برنامه‌ی کاری آینده مطرح است)، هر دو ساختار قابل استفاده‌اند ولی باید در پردازش این تفاوت لحاظ شود.
- Base URL این گیت‌وی رسمی و متعلق به خود tse.ir است؛ در برابر `cdn.tsetmc.com` که غیررسمی و مستندنشده است، پایداری/SLA آن هنوز به همان اندازه تست نشده — توصیه می‌شود در اسکریپت پایش endpoint (`test_active_tsetmc_endpoints.py`) این‌ها هم اضافه و به‌صورت دوره‌ای بررسی شوند.

### صفحه‌ی نماد — `Instrument` (per-instrument، کلید = ISIN کامل)

این endpointها از صفحه‌ی `/instrument/view?cat=cash&id={ISIN}` کشف شدند. همه پارامتر `InstrumentId` را به صورت ISIN کامل می‌گیرند.

| نام | متد | آدرس | کارکرد | فیلدهای کلیدی |
|---|---|---|---|---|
| Live Instrument By Id | GET | `/InstrumentProvider/api/v1/Instrument/LiveInstrumentByIdQuery/fa?InstrumentId={ISIN}` | اطلاعات لایو کامل یک نماد شامل order book سطح ۱ | آبجکت: `instrumentId`, `instrumentName`, `companyName`, `sharecount`, `tradeCount/Volume/Value`, `closingPrice(Change/Percent)`, `lastPrice(Change/Percent)`, `firstPrice`, `yesterdayPrice`, `minValue/maxValue/highValue/lowValue`, `marketvalue`, `stateid/statename`, `listOrderBookBuy`, `listOrderBookSell` |
| Live Instrument Summary By Id | GET | `/InstrumentProvider/api/v1/Instrument/LiveInstrumentSummaryByIdQuery/fa?InstrumentId={ISIN}` | نسخه‌ی خلاصه‌تر از اطلاعات لایو نماد | آبجکت (زیرمجموعه‌ای از LiveInstrumentByIdQuery) |
| Instrument Client Type | GET | `/InstrumentProvider/api/v1/Instrument/InstrumentClientType/fa?InstrumentId={ISIN}` | داده‌ی حقیقی/حقوقی خرید و فروش نماد | آرایه ۵ آیتمی: `title`, `buyAmount`, `buyPercent`, `sellAmount`, `sellPercent` |
| Same Group Company Query | GET | `/InstrumentProvider/api/v1/Instrument/SameGroupCompanyQuery/fa?InstrumentId={ISIN}` | لیست نمادهای هم‌گروه (هم‌صنعت) با اطلاعات مختصر | آرایه‌ای از نمادهای هم‌صنعت |
| Same Group Company ⚠️ | GET | `/InstrumentProvider/api/v1/Instrument/SameGroupCompany/fa?InstrumentId={ISIN}` | نسخه‌ی دیگری از هم‌گروه‌ها | در تست با آبادا HTTP 400 برگشت — احتمالاً نیاز به پارامتر اضافه دارد |
| Instrument Slider By Industry | GET | `/InstrumentProvider/api/v1/Instrument/InstrumentSliderQuery/fa?IndustryId={IndustryId}` | لیست نمادهای یک صنعت خاص با قیمت لایو؛ `IndustryId` عدد صنعت است (مثلاً `40`) | آرایه: `instrumentId`, `instrument_Name`, `lastprice`, `pricechangepercent`, `state` |
| Instrument Shortcut (Search) | GET | `/InstrumentProvider/api/v1/Instrument/InstrumentShortcut/fa?SimpleSearchText={query}&MarketCategoryIds[0]={cat}&PageNumber={n}&PageSize={size}` | **جستجوی نماد با pagination** — معادل webgw برای `GetInstrumentSearch` در cdn ولی قوی‌تر: فیلتر بر اساس دسته‌ی بازار (`MarketCategoryIds`)، pagination کامل، و اطلاعات بیشتر در هر آیتم | آبجکت: `items[]`, `pageNumber`, `totalPages`, `totalCount`, `hasPreviousPage`, `hasNextPage`؛ هر آیتم: `instrumentid` (ISIN)، `instrument_Name`، `instrument_English`، `company_Name_Persian`، `companyNameEnglish`، `boardname`، `markettypeid`، `marketname`، `markettypename`، `marketcategoryname` |
| History Archive | GET | `/InstrumentProvider/api/v1/History/Archive/fa?InstrumentId={ISIN}` | تاریخچه‌ی کامل روزانه از ابتدای نماد — معادل webgw برای `GetClosingPriceDailyList` در cdn | آرایه ۱۳۰۰+ آیتمی: `devenrlc`, `highvalue/lowvalue`, `lastprice(change/percent)`, `maxValue/minValue`, `tradevolume`, `closingprice(change/percent)`, `tradevalue`, `tradecount`, `yesterdayPrice`, `firstPrice`, `marketvalue` |

**نکات مهم:**
- `LiveInstrumentByIdQuery` شامل `listOrderBookBuy` و `listOrderBookSell` است — order book سطح ۱ مستقیم در همین endpoint موجود است. این endpoint برای **آپشن** هم کار می‌کند (تأییدشده با ضتاص۵۰۰۰) و فیلد `marketCategory` نوع ابزار را مشخص می‌کند (`cash` برای سهام، `tradeoption` برای آپشن).
- `History/Archive` معادل قوی‌تری برای `GetClosingPriceDailyList` در cdn است چون `marketvalue` (ارزش بازار روزانه) هم دارد که در cdn موجود نیست. برای آپشن تعداد رکوردها کم است (۱۹ رکورد برای ضتاص۵۰۰۰) چون عمر قرارداد کوتاه است — این رفتار طبیعی است.
- `SameGroupCompany` برای **آپشن کار می‌کند** (HTTP 200، ۲۵ آیتم — همه قراردادهای هم‌سری روی همان دارایی پایه)، در حالی که برای سهام عادی HTTP 400 داد. پس این endpoint برای آپشن مفیدتر است تا سهام. فیلدها: `instrumentId`, `instrumentName`, `companyNamePersian`, `tradeCount/Volume/Value`, `lastPrice`, `closingPrice(Change/Percent)`. *(این نتیجه از تست با یک نماد سهام و یک آپشن به دست آمده؛ قبل از تعمیم قطعی به همه‌ی سهام/آپشن‌ها، تست با چند نمونه‌ی دیگر توصیه می‌شود.)*
- `InstrumentSliderQuery` با پارامتر `IndustryId` فیلتر صنعت‌محور می‌دهد (در صفحه‌ی اصلی بدون پارامتر همه نمادها را برمی‌گرداند).

**رفتار endpoint ها بر اساس نوع ابزار (webgw):** *(بر اساس یک نمونه از هر نوع ابزار — نه یک آزمون آماری روی چند نماد از هر دسته؛ قبل از تعمیم قطعی، بهتر است با چند نماد دیگر از هر نوع تکرار شود)*

| اندپوینت | سهام (IRO1) | کال آپشن (IRO9) | پوت آپشن (IRS4/IROF) | پوت بازار تبعی (IRS4 فعال) | اوراق بدهی (IRB3TR) |
|---|---|---|---|---|---|
| `LiveInstrumentByIdQuery` | ✅ `marketCategory:"cash"` | ✅ `marketCategory:"tradeoption"` | ✅ `marketCategory:"tradeoption"` | ✅ | ✅ `marketCategory:null` |
| `LiveInstrumentSummaryByIdQuery` | ✅ | ✅ | ❌ 204 (منقضی) | ✅ (فعال) | ✅ (فعال) / 204 (منقضی) |
| `History/Archive` | ✅ (+۱۳۰۰ رکورد) | ✅ (کم) | ❌ خالی (منقضی) | ✅ (2.7KB) | ✅ (= روزهای عمر اوراق) |
| `InstrumentClientType` | ✅ | ✅ | ❌ 204 | ❌ 204 | ❌ 204 |
| `SameGroupCompany` | ⚠️ 400 | ✅ (همه هم‌سری) | ✅ (۱ آیتم — منقضی) | ✅ (۳ آیتم — هم‌سری بازار تبعی) | ⚠️ 400 |
| `SameGroupCompanyQuery` | ✅ | تأیید نشده | تأیید نشده | تأیید نشده | ✅ (خالی) |
| `InstrumentSliderQuery?IndustryId` | ✅ | ✅ (IndustryId=13) | ✅ (IndustryId=40) | ✅ (IndustryId=34) | ✅ (خالی، IndustryId=69) |

**نکته درباره‌ی `LiveInstrumentSummaryByIdQuery`:** HTTP 204 برای نمادهای منقضی/غیرفعال و HTTP 200 برای نمادهای فعال — وابسته به وضعیت نماد است نه نوع ابزار.

### TradingView Integration — `TradingView`

سایت tse.ir از TradingView chart library با پیاده‌سازی اختصاصی Data Feed API استفاده می‌کند:

| نام | متد | آدرس | کارکرد | فیلدهای کلیدی |
|---|---|---|---|---|
| TV Config | GET | `/InstrumentProvider/api/v1/TradingView/config` | تنظیمات data feed | `supports_search`, `supported_resolutions: ["D"]`, `exchanges: [{TSE}]` |
| TV Time | GET | `/InstrumentProvider/api/v1/TradingView/time` | زمان سرور (Unix timestamp خام) | عدد خام |
| TV Symbols | GET | `/InstrumentProvider/api/v1/TradingView/symbols?symbol={نام_فارسی_نماد}` | متادیتای نماد برای TradingView با **نام فارسی** (نه ISIN) | `name`, `description`, `timezone: Iran/Tehran`, `session`, `pricescale`, `supportedResolutions: ["D"]`, `ticker` |
| TV History | GET | `/InstrumentProvider/api/v1/TradingView/history?symbol={نام_فارسی}&resolution=1D&from={unix}&to={unix}&countback={n}` | داده‌ی OHLCV تاریخی برای chart؛ پیمایش صفحه‌به‌صفحه با `from`/`to` | آبجکت: `s` (status), `t[]` (timestamps), `o[]`, `h[]`, `l[]`, `c[]`, `v[]`, `nextTime` |

**نکات TradingView:**
- پارامتر `symbol` در این خانواده **نام فارسی نماد** است (مثلاً `آبادا`)، نه ISIN — استثنای مهم نسبت به بقیه‌ی webgw که همه ISIN می‌گیرند.
- فعلاً فقط `resolution=1D` (روزانه) پشتیبانی می‌شود (`hasIntraday: false`).
- برای pipeline داده `History/Archive` مناسب‌تر است (یک درخواست، کل تاریخچه، بدون pagination).

### تجسم بصری بازار — `ChartSummary` و `MarketMap`

| نام | متد | آدرس | کارکرد | فیلدهای کلیدی |
|---|---|---|---|---|
| Bubble Chart | GET | `/InstrumentProvider/api/v1/ChartSummary/BubbleChart/fa` | داده‌ی نمودار حبابی بازار، گروه‌بندی‌شده بر اساس صنعت؛ هر صنعت شامل لیست نمادهای عضو با تغییرات قیمت و ارزش بازار | آرایه‌ای از صنایع؛ هر آیتم: `industryId`، `industryName`، `bubbleChartItems` (آرایه نمادها با `instrumentId`, `lastpricechangepercent`, `closingpricechangepercent`, `marketValue`, `tradeVolume`, `tradequantity`, `pe`, `closingprice`, `lastprice`) |
| Market Map (Heatmap) | GET | `/InstrumentProvider/api/v1/MarketMap/MarketMapNew/fa?marketIds[0]=20&marketIds[1]=30&MarketTypes[0]=Cash&MarketTypes[1]=Future&MarketTypes[2]=Option&MarketTypes[3]=Debt&MarketTypes[4]=ETF&MarketTypes[5]=TradeOption&BasedOnVolume={true\|false}` | داده‌ی نقشه حرارتی بازار (treemap)، گروه‌بندی‌شده بر اساس صنعت با زیرگروه تودرتو تا سطح نماد؛ `marketIds`=20 بورس، 30 فرابورس؛ `MarketTypes` قابل ترکیب (فقط انواعی که در query باشند لحاظ می‌شوند)؛ `BasedOnVolume` وزن‌دهی بر اساس حجم یا ارزش معاملات | ساختار تودرتو: `{"groups": [...]}` هر گروه صنعت: `label`, `weight`, `tradeVolume`, `tradeValue`, `percent`, و آرایه تودرتوی `groups` در سطح نماد با `instrumentName`, `companyName`, `lastPrice(Change/Percent)`, `closingPrice(Change/Percent)`, `eps`, `pe`, `sharesCount`, `maxValue`, `minValue` |

**نکات:**
- `MarketMapNew` با query params متغیر، امکان فیلتر ترکیبی چند نوع بازار در یک درخواست را می‌دهد (مثلاً هم‌زمان Cash+Future+Option+Debt+ETF+TradeOption) — این برخلاف endpointهای `MarketWatch*` است که هرکدام تک‌نوع هستند.
- این دو endpoint بیشتر برای مصورسازی (heatmap/bubble chart در صفحه اصلی) طراحی شده‌اند تا استخراج داده خام؛ برای نیازهای پایپ‌لاین داده (مثل مرجع نماد یا بک‌تست)، همچنان `MarketWatch*` و `cdn.tsetmc.com` منابع اصلی‌ترند. اما `BubbleChart` می‌تواند به‌عنوان یک منبع سریع و جایگزین برای P/E و `sharesCount` (تعداد سهام) در تحلیل‌های سریع مفید باشد، چون این دو فیلد در بسیاری از endpointهای دیگر مستقیماً موجود نیست.

---

## منابع مکمل تأییدشده (خارج از API اصلی cdn.tsetmc.com)

### دیده‌بان بازار کامل — جایگزین واقعی `GetMarketWatch` خراب

مسیر API رسمی `GetMarketWatch` همیشه در تست ما خالی برگشت (`marketwatch: 0`). اما یک مسیر legacy جایگزین که واقعاً کار می‌کند و کل بازار را در یک درخواست می‌دهد پیدا و تأیید شد:

```
https://old.tsetmc.com/tsev2/excel/MarketWatchPlus.aspx?d=0          (اعداد به‌صورت int واقعی — پیشنهادی)
https://old.tsetmc.com/tsev2/excel/MarketWatchPlus.aspx?d=0&format=0 (اعداد به‌صورت متن)
```

- خروجی: فایل Excel با ۳۱۳۳ نماد (۳۱۳۶ ردیف کل شیت شامل ۳ ردیف عنوان/هدر — همان عددی که `test_active_tsetmc_endpoints.py` هم گزارش می‌دهد: `rows: 3136`) — کل بازار: سهم، صندوق، آپشن، اوراق در یک شیت.
- ستون‌ها: نماد، نام، تعداد، حجم، ارزش، دیروز، اولین، آخرین معامله (مقدار/تغییر/درصد)، قیمت پایانی (مقدار/تغییر/درصد)، کمترین، بیشترین، EPS، P/E، خرید (تعداد/حجم/قیمت)، فروش (قیمت/حجم/تعداد).
- **محدودیت مهم:** هیچ `InsCode`، `cIsin`، یا صنعت/زیرصنعتی ندارد — فقط بر اساس «نماد» (نام کوتاه) قابل جست‌وجوست. برای اتصال به سایر endpointها (که همه InsCode می‌خواهند)، باید نماد را از طریق `GetInstrumentSearch/{نماد}` به InsCode تبدیل کرد.
- کاربرد مناسب: دید کلی/لحظه‌ای سریع از کل بازار (قیمت، حجم، صف خرید/فروش سطح ۱) بدون هزاران فراخوانی API. کاربرد نامناسب: به‌عنوان منبع اصلی ساخت مرجع صنعت/نوع ابزار (برای آن هدف، همچنان باید از `build_master_instrument_reference.py` استفاده کرد).

### مقایسه‌ی کلی دو gateway (از ریپازیتوری BabakEslami/tse-market-data)

| موضوع | cdn.tsetmc.com | webgw.tse.ir |
|---|---|---|
| کلید نماد | InsCode (عدد) | ISIN کامل |
| وضعیت | غیررسمی | رسمی (زیرساخت tse.ir) |
| تاریخچه روزانه | `GetClosingPriceDailyList` | `History/Archive` (+ `marketvalue` روزانه) |
| order book | `BestLimits` (delta feed — نیاز به reconstruction) | داخل `LiveInstrumentByIdQuery` (سطح ۱، آماده) |
| حقیقی/حقوقی تاریخی | ✅ `ClientTypeHistory` | ❌ فقط لحظه‌ای |
| دیده‌بان کل بازار | ⚠️ `GetMarketWatch` خالی برمی‌گرداند | ✅ `MarketWatch*` کامل |
| دسترسی از سرور | ✅ GitHub Actions (طبق تجربه‌ی `tsetmc-market-pipeline`، فقط `cdn.tsetmc.com` و `BrsApi.ir` از GitHub Actions قابل دسترسی‌اند) | ❌ فقط از IP ایران |

---

## پیوست A — جزئیات فنی اسکریپت پایش `test_active_tsetmc_endpoints.py`

> **وضعیت راستی‌آزمایی:** ✅ تأییدشده مستقیماً — کاربر خودِ کد Python این اسکریپت (و `README.md` همراهش) را از پوشه‌ی `scripts/` ریپازیتوری آپلود کرد و محتوا مستقیماً خوانده شد. این بخش گزارش دست‌دوم نیست.

این اسکریپت فقط همان **۵۶ endpoint** شناخته‌شده‌ی «فعال با داده واقعی» (که در بخش «یادداشت‌های عملیاتی» بالاتر هم بهش اشاره شده) را دوباره تست می‌کند — عدد ۵۶ با شمارش مستقیم آرایه‌ی `ENDPOINTS` داخل کد تأیید شد. طبق docstring خودِ فایل، این اسکریپت **جدا** از یک اسکریپت دیگر به نام `iran_market_api_tester_v2.py` است که ادعا می‌شود کل inventory (شامل مسیرهای مرده/شخص‌ثالث) را تست می‌کند؛ آن اسکریپت دوم در دسترس ما نبوده و فقط وجودش مستند می‌شود، نه محتوایش.

### هدرهای HTTP

```python
HEADERS = {
    "User-Agent": "Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 Chrome/126 Safari/537.36",
    "Accept": "application/json,text/plain,text/csv,text/html,*/*",
    "Referer": "https://www.tsetmc.com/",
    "Origin": "https://www.tsetmc.com",
}
```

این هدرها روی **همه‌ی** درخواست‌ها (نه فقط cdn.tsetmc.com) اعمال می‌شوند. نکته‌ی `Referer`/`Origin` تکمیل‌کننده‌ی هشدار User-Agent است که در بخش «یادداشت‌های عملیاتی» آمده — یعنی برای کاهش احتمال ۴۰۳/مسدودشدن، احتمالاً هر ۴ هدر با هم لازم‌اند، نه فقط User-Agent به‌تنهایی (این اسکریپت هر ۴ تا رو با هم می‌فرسته، پس به‌تنهایی بودن هرکدوم به‌صورت مجزا تست نشده).

### منطق Retry

```python
RETRYABLE_STATUS = {429, 502, 503, 504}
```

- بازتلاش فقط برای این ۴ کد وضعیت HTTP و برای خطاهای `Timeout`/`ConnectionError` انجام می‌شود.
- فرمول تأخیر بین تلاش‌ها: **exponential backoff** با پایه‌ی `0.6` ثانیه: `delay = 0.6 × 2^attempt` (یعنی تلاش‌های بعدی به ترتیب ۰.۶، ۱.۲، ۲.۴ ثانیه...).
- تعداد تلاش پیش‌فرض: ۳ بار (قابل تغییر با `--max-retries`)، به‌ازای هر endpoint هم می‌تواند override شود (مثلاً «دیده‌بان بازار Excel legacy» به‌خاطر حجم بالا timeout و max_retries مجزا دارد: ۶۰ ثانیه timeout، فقط ۱ retry).

### دسته‌بندی کامل وضعیت‌ها (`classify_content`)

| وضعیت | معنا |
|---|---|
| `ACTIVE_JSON` | پاسخ JSON معتبر پارس شد |
| `ACTIVE_EMPTY` | پاسخ خالی بود (`""`, `[]`, یا `{}`) |
| `ACTIVE_EXCEL` | پاسخ باینری Excel تشخیص داده شد (بر اساس content-type یا امضای فایل ZIP یعنی `PK` در ابتدای بایت‌ها) |
| `ACTIVE_CSV_OR_TEXT` | متن ساده حاوی `,` یا `;` (نه JSON، نه HTML) |
| `ACTIVE_TEXT` | متن ساده بدون جداکننده‌ی مشخص |
| `WAF_BLOCKED` | صفحه‌ی HTML برگشته و حاوی یکی از نشانگرهای WAF بود |
| `SPA_DEAD` | صفحه‌ی HTML برگشته، نشانگر WAF نداشت، ولی دامنه‌ی tsetmc.com بود — یعنی مسیر دیگر وجود ندارد و به صفحه‌ی اصلی SPA فال‌بک شده |
| `THIRD_PARTY_PAGE` | صفحه‌ی HTML برگشته از یک دامنه‌ی غیر-tsetmc |
| `HTTP_{code}` | کد وضعیت ≥ ۴۰۰ (مثلاً `HTTP_404`، `HTTP_500`) |
| `ERROR` | استثنای شبکه (Timeout/ConnectionError) پس از اتمام تلاش‌های retry |

نشانگرهای تشخیص WAF (`WAF_MARKERS`) که در متن پاسخ جست‌وجو می‌شوند: `"request rejected"`, `"درخواست شما به دلایلی مسدود شده"`, `"access denied"`, `"cloudflare"`.

### پارامترهای خط فرمان (CLI)

| پارامتر | پیش‌فرض | توضیح |
|---|---|---|
| `--inscode` | `17914401175772326` (اهرم) | InsCode برای endpoint هایی که به آن نیاز دارند |
| `--date` | `20260701` | تاریخ به فرمت `YYYYMMDD` |
| `--timeout` | `20.0` ثانیه | timeout هر درخواست |
| `--delay` | `0.1` ثانیه | فاصله‌ی ثابت بین درخواست‌های موفق (جدا از exponential backoff تلاش مجدد) |
| `--max-retries` | `3` | تعداد تلاش مجدد برای خطاهای موقت |
| `--csv` | `tsetmc_active_endpoints_test.csv` | مسیر خروجی CSV |
| `--json` | `tsetmc_active_endpoints_test.json` | مسیر خروجی JSON |

خروجی نهایی شامل خلاصه‌ای از تعداد endpoint های هنوز فعال (`ACTIVE_JSON`/`ACTIVE_CSV_OR_TEXT`/`ACTIVE_TEXT`/`ACTIVE_EXCEL`) در برابر مواردی است که «رگرس» کرده‌اند (هر وضعیت دیگر).

---

## پیوست B — نمونه فیلدهای Response از `examples/` (⚠️ ساختاری، نه از تست زنده)

> **وضعیت راستی‌آزمایی:** ⚠️ این بخش با بخش‌های دیگر سند فرق دارد. کاربر ۴ فایل JSON پوشه‌ی `examples/` را مستقیماً آپلود کرد و محتوا خوانده شد، اما خودِ این فایل‌ها صراحتاً در فیلد `_note`شان اعلام می‌کنند که **نمونه‌ی ساختاری** هستند، نه response واقعیِ گرفته‌شده از تست زنده روی API (مقادیری مثل `insCode: "9999999999999999"` و `cIsin: "IRT1XXXXX001"` این را تأیید می‌کنند — این‌ها placeholder اند). بنابراین **نام فیلدها** قابل استناد است، ولی **مقادیر نمونه** نباید به‌عنوان داده‌ی واقعی برداشت شوند. این تفاوت مهمی با بقیه‌ی این سند دارد که همه از رکورد و تعداد واقعیِ تست‌شده می‌آیند.

| Endpoint | فیلدهای مشاهده‌شده در نمونه |
|---|---|
| `BestLimits` | هر سطح: `number`, `zOrdMeDem` (تعداد سفارش خرید), `pMeDem` (قیمت خرید), `pMeOf` (قیمت فروش), `zOrdMeOf` (تعداد سفارش فروش). *نکته: این نمونه فاقد فیلد حجم سفارش (`qTitMeDem`/`qTitMeOf`) است؛ ممکن است در پاسخ واقعی وجود داشته باشد و صرفاً در این نمونه‌ی ساده‌شده نیامده — نیاز به تأیید با یک پاسخ واقعی.* |
| `GetClosingPriceInfo` | `closingPriceInfo`: `insCode`, `pClosing`, `priceChange`, `priceChangePercent`, `pDrCotVal`, `zTotTran`, `qTotTran5J`, `qTotCap`, و شیء تودرتوی `instrumentState` با `cEtaval`/`cEtavalTitle`/`underSupervision` (این سه فیلد آخر قبلاً هم در بخش «تشخیص وضعیت توقف/تعلیق نماد» با نمونه‌ی واقعی تأیید شده بودند) |
| `GetInstrumentIdentity` | `instrumentIdentity`: `insCode`, `cIsin`, `lVal18`, `cValMne`, `sector` (`cSecVal`/`lSecVal`), `subSector` (`cSoSecVal`/`lSoSecVal`) — دو فیلد آخر (`sector`/`subSector`) قبلاً با مقدار واقعی در بخش «تشخیص نوع ابزار مالی» تأیید شده بودند؛ `cIsin`/`lVal18`/`cValMne` فقط در همین نمونه‌ی ساختاری دیده شدند |
| `GetInstrumentSearch` | `instrumentSearch[]`: `insCode`, `lVal18AFC`, `lVal30`, `cIsin`, `flowTitle` |

**نتیجه‌ی عملی:** اگر قرار است این فیلدها در یک اسکریپت پارس شوند (مثلاً برای خواندن `BestLimits` یا نتیجه‌ی `GetInstrumentSearch`)، نام فیلدها را می‌توان به‌عنوان راهنمای اولیه استفاده کرد، ولی قبل از تکیه‌ی پروداکشن روی آن‌ها، حتماً باید با یک درخواست واقعی به API (نه این نمونه‌ی ساختاری) تأیید شوند — دقیقاً طبق همان اصل «رد دقت ساختگی بدون تأیید تجربی» که در بقیه‌ی این سند هم رعایت شده.

---

## چک نهایی کامل بودن سند

این بخش نتیجه‌ی مرور نهایی end-to-end است که طبق درخواست کاربر، برای اطمینان از عدم افتادگی چیزی نسبت به هر ۴ منبع انجام شد:

- **تعداد کل endpoint مستندشده:** ۹۳ مورد (۶۳ در `cdn.tsetmc.com` شامل بخش شاخص‌ها + ۳۰ در `webgw.tse.ir`) — برابر با شمارش صریح فایل منبع ۱؛ شمارش دستی هر بخش این سند هم همین عدد را تأیید کرد.
- **همه‌ی ۱۴ بخش موضوعی cdn** (شاخص‌ها، ClosingPrice، BestLimits، Trade، ClientType، Instrument، MarketData، Fund، Shareholder، Codal، Msg، Energy، StaticData، Learning) از فایل منبع ۱ به‌طور کامل با تمام سطرها و یادداشت‌های همراه منتقل شدند.
- **اصلاحیه‌ی ۷ شاخص منتخب بورس** (منبع ۲) در جدول شاخص‌ها، متن توضیحی، و لیست کامل ۷ شاخص اعمال شد.
- **دو نکته‌ی منحصربه‌فرد v3.1** (شمار تقریبی ~۴۰-۵۰ شاخص صنعتی با کدهای ۰۱-۷۴؛ یادآوری CORS/بک‌اند واسط) به بخش شاخص‌ها و یادداشت‌های عملیاتی افزوده شد.
- **همه‌ی یادداشت‌های تفصیلی فایل منبع ۱ که در v3.1 خلاصه یا جا افتاده بودند** (نمونه JSON واقعی، توضیح رفتار `All/{flow}` با نمونه‌ی عددی، دو نقش `GetTradeHistory`، فرمول و تأیید عددی `GetIndexCompany`، هشدار User-Agent، هشدار base path ناهماهنگ webgw، هشدار ناهماهنگی ۹۳ در برابر ۵۶ endpoint در اسکریپت پایش) در این نسخه بازگردانده شدند.
- **ریپازیتوری GitHub بررسی و مقایسه شد** (منبع ۴): محتوای آن با فایل منبع ۱ همخوانی داشت و زیرمجموعه‌ی آن بود؛ هیچ endpoint یا یادداشت جدیدی که در بقیه‌ی منابع نبوده باشد، پیدا نشد. جدول «مقایسه‌ی کلی دو gateway» از README همان ریپو در بخش منابع مکمل اضافه شد چون در فایل‌های دیگر نبود.
- **محدودیت باقی‌مانده (شفاف اعلام می‌شود):** پوشه‌های `examples/` و `scripts/` ریپازیتوری گیت‌هاب به‌خاطر محدودیت robots.txt قابل مرور مستقیم نبودند؛ محتوای این سند صرفاً بر پایه‌ی ۴ منبعی است که در بالای فایل ذکر شد، نه بر پایه‌ی نمونه‌های JSON خام یا کد اسکریپت پایش آن ریپو. اگر لازم است این پوشه‌ها هم بررسی شوند، به یک روش دیگر (مثلاً git clone یا آپلود مستقیم فایل‌ها) نیاز است.
- **هیچ endpoint یا جدولی از هیچ‌کدام از ۳ فایل آپلودی حذف نشده** — مقایسه‌ی سطر به سطر بین این فایل و هرکدام از منابع ۱ تا ۳ انجام شد و موردی که در این نسخه‌ی نهایی نباشد یافت نشد.
- **به‌روزرسانی v4.1:** محدودیت قبلی («پوشه‌های examples/ و scripts/ قابل‌دسترس نبودند») برطرف شد — کاربر هر دو پوشه را مستقیماً آپلود کرد. محتوا خوانده و راستی‌آزمایی شد (نه گزارش دست‌دوم): صفر endpoint جدید (مطابق پیش‌بینی)، ولی جزئیات فنی واقعی (هدرها، منطق retry، دسته‌بندی وضعیت‌ها، پارامترهای CLI) در «پیوست A» تأیید و درج شد، و ساختار فیلدهای ۴ نمونه JSON در «پیوست B» درج شد (با برچسب صریح که این نمونه‌ها ساختاری‌اند، نه از تست زنده). یک تحلیل مستقل توسط ChatGPT درباره‌ی همین دو پوشه هم با کد واقعی مقایسه شد؛ ادعاهای اصلی‌اش تأیید شدند و چند جزئیات اضافه (دسته‌بندی‌های بیشتر وضعیت، وجود اسکریپت خواهر `iran_market_api_tester_v2.py`) هم کشف شد که در آن تحلیل نبود.

</div>
