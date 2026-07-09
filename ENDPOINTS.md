<div dir="rtl">

# مرجع کامل Endpoint های بازار سرمایه ایران (TSETMC)

Base URL: `https://cdn.tsetmc.com/api/...`

جدول علامت‌گذاری:
- بدون علامت = در تست ما داده‌ی واقعی برگردانده
- ⚠️ = مسیر معتبر است اما در تست با پارامتر نمونه خالی برگشت (احتمالاً نیاز به پارامتر واقعی یا session دارد)

## فهرست مطالب

- [قیمت پایانی و تاریخچه](#قیمت-پایانی-و-تاریخچه--closingprice)
- [صف خرید/فروش](#صف-خریدفروش--bestlimits)
- [معاملات](#معاملات--trade)
- [حقیقی/حقوقی](#حقیقیحقوقی--clienttype)
- [اطلاعات و جستجوی نماد](#اطلاعات-و-جستجوی-نماد--instrument)
- [داده‌های کلی بازار](#داده‌های-کلی-بازار--marketdata)
- [صندوق‌ها/ETF](#صندوق‌هاetf--fund)
- [سهامداران](#سهامداران--shareholder)
- [اطلاعیه‌های کدال](#اطلاعیه‌های-کدال--codal)
- [پیام ناظر](#پیام-ناظر--msg)
- [بورس انرژی](#بورس-انرژی--energy)
- [داده ثابت/زمان](#داده-ثابتزمان--staticdata)
- [آموزش](#آموزش--learning)
- [تشخیص نوع ابزار مالی و صنعت](#تشخیص-نوع-ابزار-مالی-و-صنعت)
- [تشخیص وضعیت توقف/تعلیق نماد](#تشخیص-وضعیت-توقفتعلیق-نماد)
- [یادداشت‌های عملیاتی و هشدارهای مهم](#یادداشت‌های-عملیاتی-و-هشدارهای-مهم)
- [گیت‌وی رسمی جدید — webgw.tse.ir](#گیت‌وی-رسمی-جدید--webgwtseir)
- [منابع مکمل تأییدشده](#منابع-مکمل-تأییدشده-خارج-از-api-اصلی-cdntsetmccom)

## قیمت پایانی و تاریخچه — `ClosingPrice`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| ChartData daily | GET | `/ClosingPrice/GetChartData/{InsCode}/D` | OHLCVT chart data, daily resolution | `closingPriceChartData: 1016` |
| ClosingPrice daily | GET | `/ClosingPrice/GetClosingPriceDaily/{InsCode}/{DEven}` | Single day closing price summary | `closingPriceDaily: object` |
| ClosingPrice daily list top | GET | `/ClosingPrice/GetClosingPriceDailyList/{InsCode}/{Top}` | Historical closing prices; Top=0 returns all | `closingPriceDaily: 10` |
| ClosingPrice daily list all | GET | `/ClosingPrice/GetClosingPriceDailyList/{InsCode}/0` | All historical closing prices | `closingPriceDaily: 1084` |
| ClosingPrice daily list CSV | GET | `/ClosingPrice/GetClosingPriceDailyListCSV/{InsCode}/0` | All historical closing prices as CSV-like output | `` |
| ClosingPrice history | GET | `/ClosingPrice/GetClosingPriceHistory/{InsCode}/{DEven}` | Old ClosingPriceData intraday/history snapshots | `closingPriceHistory: 5021` |
| ClosingPrice info today | GET | `/ClosingPrice/GetClosingPriceInfo/{InsCode}` | Today price summary and instrument state | `closingPriceInfo: object` |
| Instruments history in day | GET | `/ClosingPrice/GetInstrmentsHistoryInDay/{DEven}` | Price info of all instruments on a specific date | `closingPriceDailyHistoryWithInstDetails: 1923` |
| Instrument calendar | GET | `/ClosingPrice/GetInstrumentCalendar/{InsCode}` | Instrument trading calendar with closing prices and volumes | `instrumentCalendar: 1084` |
| Market watch ⚠️ | GET | `/ClosingPrice/GetMarketWatch` | Market watch data; may return empty from CDN without params/session | `marketwatch: 0` |
| Market watch Excel (legacy) | GET | `https://old.tsetmc.com/tsev2/excel/MarketWatchPlus.aspx?d=0` | Legacy full market watch export; جایگزین واقعی ردیف بالا (جزئیات کامل در بخش «منابع مکمل») | `rows: 3136 (Excel)` |
| Price adjust by flow ⚠️ | GET | `/ClosingPrice/GetPriceAdjustByFlow/{Flow}/{Top}` | Price adjustment events by market flow | `priceAdjust: 0` |
| Price adjust list ⚠️ | GET | `/ClosingPrice/GetPriceAdjustList/{InsCode}` | Price adjustment events for instrument | `priceAdjust: 0` |
| Related company | GET | `/ClosingPrice/GetRelatedCompany/{CSecVal}` | Instruments and 30-day history in industry sector | `relatedCompany: 65` |

## صف خرید/فروش — `BestLimits`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| BestLimits now | GET | `/BestLimits/{InsCode}` | Current 5-level order book / best limits | `bestLimits: 5` |
| BestLimits historical | GET | `/BestLimits/{InsCode}/{DEven}` | Historical order book snapshots for one trading day | `bestLimitsHistory: 24660` |

> ⚠️ **BestLimits یک delta feed است، نه یک اسنپ‌شات کامل.** برای بازسازی دقیق عمق order book به‌ازای هر لحظه، باید یک stateful carry-forward reconstruction پیاده‌سازی کنید. بعد از این بازسازی، پوشش داده عملاً کامل است.

## معاملات — `Trade`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Trade now | GET | `/Trade/GetTrade/{InsCode}` | Trades for last trading day | `trade: 14818` |
| Trade history | GET | `/Trade/GetTradeHistory/{InsCode}/{DEven}/false` | Historical intraday trades | `tradeHistory: 14818` |
| Trade intraday | GET | `/Trade/GetTradeIntraDay/{InsCode}` | Intraday aggregated trades for last trading day | `tradeIntraDay: 105` |
| Trade volume | GET | `/Trade/GetTradeVolume/{InsCode}` | Trade volume distribution by price/time | `tradeVolume: 798` |

> ⚠️ **شکاف پوشش شناخته‌شده:** `GetTradeHistory` نسبت به آمار رسمی بورس حدود ۳۶-۳۸٪ کسری دارد. برای ارقام تجمعی (حجم/ارزش/تعداد کل معاملات)، `ClosingPriceHistory` منبع معتبر است.

## حقیقی/حقوقی — `ClientType`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| ClientType now | GET | `/ClientType/GetClientType/{InsCode}/1/0` | Current real/legal buyer-seller data | `clientType: object` |
| ClientType all | GET | `/ClientType/GetClientTypeAll` | Client type data for all instruments from last trading day | `clientTypeAllDto: 1878` |
| ClientType history | GET | `/ClientType/GetClientTypeHistory/{InsCode}/{DEven}` | Historical real/legal buyer-seller data for instrument/day | `clientType: object` |

## اطلاعات و جستجوی نماد — `Instrument`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Instrument history | GET | `/Instrument/GetInstrumentHistory/{InsCode}/{DEven}` | Historical simple instrument metadata for a day | `instrumentHistory: object` |
| Instrument identity | GET | `/Instrument/GetInstrumentIdentity/{InsCode}` | Instrument identity, sector, sub-sector, names | `instrumentIdentity: object` |
| Instrument info | GET | `/Instrument/GetInstrumentInfo/{InsCode}` | Instrument full information, EPS, sector, static thresholds | `instrumentInfo: object` |
| Instrument search | GET | `/Instrument/GetInstrumentSearch/{Query}` | Instrument search by keyword | `instrumentSearch: 41` |
| Share change ⚠️ | GET | `/Instrument/GetInstrumentShareChange/{InsCode}` | Share changes for instrument | `instrumentShareChange: 0` |
| Share change by flow ⚠️ | GET | `/Instrument/GetInstrumentShareChangeByFlow/{Flow}/{Top}` | Share changes by market flow | `instrumentShareChange: 0` |

## داده‌های کلی بازار — `MarketData`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Instrument state | GET | `/MarketData/GetInstrumentState/{InsCode}/{DEven}` | Instrument state for day | `instrumentState: 1` |
| Instrument state top | GET | `/MarketData/GetInstrumentStateTop/{Top}` | Recently changed instrument states | `instrumentState: 10` |
| Instrument statistic | GET | `/MarketData/GetInstrumentStatistic/{InsCode}` | Instrument statistics such as average value/volume/trades | `instrumentStatistic: 88` |
| Inst value all params | GET | `/MarketData/GetInstValueAllInstAllParam` | All instrument value parameters for all instruments; very large | `instValueAllInstAllParam: 299174` |
| Market overview | GET | `/MarketData/GetMarketOverview/{Flow}` | Market overview by flow with index values and activity | `marketOverview: object` |
| Sectors summary | GET | `/MarketData/GetSectorsSummary` | Sectors summary | `sectorSummeries: 49` |
| Static threshold | GET | `/MarketData/GetStaticThreshold/{InsCode}/{DEven}` | Static price thresholds for day | `staticThreshold: 2` |

## صندوق‌ها/ETF — `Fund`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| ETF by inscode | GET | `/Fund/GetETFByInsCode/{InsCode}` | ETF/fund data including redemption/subscription NAV-like values | `etf: object` |
| Fund detail 0 | GET | `/Fund/GetFundInDetail/0` | Fund details and NAV stats | `fund: object` |
| Fund detail 1 | GET | `/Fund/GetFundInDetail/1` | Fund details variant | `fund: object` |

## سهامداران — `Shareholder`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Shareholder changes old | GET | `/Shareholder/{InsCode}/{DEven}` | Shareholder changes at day | `shareShareholder: 4` |
| Shareholder last ⚠️ | GET | `/Shareholder/GetInstrumentShareHolderLast/{InsCode}` | Latest shareholders for instrument | `shareHolder: 0` |
| Shareholder changes all ⚠️ | GET | `/Shareholder/GetShareHolderChanges/false` | All shareholder changes in recent days | `shareHoldersChanges: 0` |
| Shareholder company list ⚠️ | GET | `/Shareholder/GetShareHolderCompanyList/{ShareHolderShareID}` | Other holdings of shareholder | `shareHolderShare: 0` |
| Shareholder history ⚠️ | GET | `/Shareholder/GetShareHolderHistory/{InsCode}/{DEven}/{Top}` | Shareholder changes for instrument/day | `shareHolder: 0` |

## اطلاعیه‌های کدال — `Codal`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Prepared data top | GET | `/Codal/GetPreparedData/{Top}` | Recent codal notifications | `preparedData: 10` |
| Prepared data by inscode | GET | `/Codal/GetPreparedDataByInsCode/{Top}/{InsCode}` | Codal notifications for instrument | `preparedData: 10` |
| Codal publisher by symbol | GET | `/Codal/GetCodalPublisherBySymbol/{Symbol}` | Codal publisher lookup by symbol | `codalPublisher: object` |
| File attachment by row id | GET | `/Codal/GetFileAttachmentByMainTableRowId/{MainTableRowId}` | Codal attachment by main table row id | `fileAttachment: 1` |
| File attachment by tracing ⚠️ | GET | `/Codal/GetFileAttachmentByTracingNo/{TracingNo}` | Codal attachment by tracing no | `fileAttachment: 0` |

## پیام ناظر — `Msg`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Messages by flow | GET | `/Msg/GetMsgByFlow/{Flow}/{Top}` | Supervisor messages by flow | `msg: 10` |
| Messages by inscode | GET | `/Msg/GetMsgByInsCode/{InsCode}` | Supervisor messages for instrument | `msg: 354` |

## بورس انرژی — `Energy`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Energy auction by id | GET | `/Energy/GetAuctionById/{AuctionId}` | Energy exchange auction by id | `auction: object` |
| Energy auction trade by id ⚠️ | GET | `/Energy/GetAuctionTradeById/{AuctionId}` | Energy auction trades by id | `auctionTrade: 0` |

## داده ثابت/زمان — `StaticData`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Static data | GET | `/StaticData/GetStaticData` | Static descriptions/names such as paper type, sectors, YVal | `staticData: 75` |
| Time | GET | `/StaticData/GetTime` | Server date and time | `` |

## آموزش — `Learning`

| نام | متد | آدرس | کارکرد | رکورد/کلید |
|---|---|---|---|---|
| Learning topics | GET | `/Learning/GetLearningTopics` | Learning/help topics from TSETMC site | `learningTopics: 78` |

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
| Endpoint | سهم | ETF/صندوق | آپشن |
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
   - نوع ابزار مالی (سهم/ETF/صندوق/آپشن) — بخش بالا
   - وضعیت توقف/تعلیق نماد در تاریخ درخواستی — بخش بالا
   - باز یا بسته بودن روز معاملاتی (تاریخ «امروز» می‌تواند داده‌ی ناقص یا خطای ۵۰۰ برای فیلدهای «تاریخچه‌ای» بدهد، حتی برای نماد کاملاً سالم)
3. **گاهی یک endpoint برای یک تاریخ خاص به‌طور موقت و بدون دلیل ساختاری خالی برمی‌گردد** (مشاهده‌شده در `GetTradeHistory` برای ۶ تیر که بعداً با تست مجدد رفع شد). قبل از نتیجه‌گیری قطعی از یک نتیجه‌ی خالی غیرمنتظره، درخواست را دوباره امتحان کن.
4. **حجم برخی endpoint خیلی بالاست** (`GetInstValueAllInstAllParam` ~۲۴ مگابایت). برای استفاده‌ی مکرر حتماً cache شود.
5. **پارامترهای ساختگی (fake id) نتیجه‌ی خالی می‌دهند، نه خطا** — برای تست واقعی `TracingNo`, `AuctionId`, `ShareHolderShareID`، باید مقدار واقعی از یک endpoint دیگر (مثلاً `GetPreparedData` برای TracingNo) استخراج شود.
6. آخرین تست کامل: تیر ۱۴۰۵ — روی ۴ نوع ابزار (سهم، ETF، صندوق، آپشن)، ۲ نماد تعلیق‌شده و فعال، و ۴ تاریخ مختلف.

---

## گیت‌وی رسمی جدید — `webgw.tse.ir`

کشف‌شده از طریق بازرسی HAR در Chrome DevTools روی صفحات `www.tse.ir`. بر خلاف `cdn.tsetmc.com` (غیررسمی)، این آدرس زیرساخت رسمی سایت tse.ir است. کلید اصلی نماد در این گیت‌وی، برخلاف `InsCode` عددی cdn، مستقیماً **ISIN کامل** (`cIsin`) است — نیازی به تبدیل InsCode ندارد.

Base URL: `https://webgw.tse.ir/...`

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
| MarketWatch TALMarket | GET | `/InstrumentProvider/api/v1/MarketWatch/MarketWatchTALMarket/fa` | دیده‌بان بازار **معاملات پایانی (Trading At Last)** — مرحله‌ای که از ۲۰ آبان ۱۴۰۴ در بورس تهران اجرایی شد: از ساعت ۱۲:۴۵ تا ۱۳:۰۰ فقط در قیمت پایانی ثابت ساعت ۱۲:۳۰، مستقل از سفارش‌های عادی، فقط برای نمادهای تابلوی اصلی بازار اول؛ نمادهای مشمول با عدد ۴ در انتهای نام مشخص می‌شوند (مثلاً «بترانس۴») | `Items: 0` در تست ما — این endpoint به‌درستی تعریف شده ولی **خارج از ساعت ۱۲:۴۵–۱۳:۰۰** همیشه خالی است؛ برای دریافت داده باید دقیقاً در همان پنجره زمانی فراخوانی شود |

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
- `SameGroupCompany` برای **آپشن کار می‌کند** (HTTP 200، ۲۵ آیتم — همه قراردادهای هم‌سری روی همان دارایی پایه)، در حالی که برای سهام عادی HTTP 400 داد. پس این endpoint برای آپشن مفیدتر است تا سهام. فیلدها: `instrumentId`, `instrumentName`, `companyNamePersian`, `tradeCount/Volume/Value`, `lastPrice`, `closingPrice(Change/Percent)`.
- `InstrumentSliderQuery` با پارامتر `IndustryId` فیلتر صنعت‌محور می‌دهد (در صفحه‌ی اصلی بدون پارامتر همه نمادها را برمی‌گرداند).

**رفتار endpoint ها بر اساس نوع ابزار (webgw):**
| Endpoint | سهام (IRO1) | کال آپشن (IRO9) | پوت آپشن (IRS4/IROF) | پوت بازار تبعی (IRS4 فعال) | اوراق بدهی (IRB3TR) |
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

| نام | متد | آدرس | کارکرد | ساختار خروجی |
|---|---|---|---|---|
| Bubble Chart | GET | `/InstrumentProvider/api/v1/ChartSummary/BubbleChart/fa` | داده‌ی نمودار حبابی بازار، گروه‌بندی‌شده بر اساس صنعت؛ هر صنعت شامل لیست نمادهای عضو با تغییرات قیمت و ارزش بازار | آرایه‌ای از صنایع؛ هر آیتم: `industryId`، `industryName`، `bubbleChartItems` (آرایه نمادها با `instrumentId`, `lastpricechangepercent`, `closingpricechangepercent`, `marketValue`, `tradeVolume`, `tradequantity`, `pe`, `closingprice`, `lastprice`) |
| Market Map (Heatmap) | GET | `/InstrumentProvider/api/v1/MarketMap/MarketMapNew/fa?marketIds[0]=20&marketIds[1]=30&MarketTypes[0]=Cash&MarketTypes[1]=Future&MarketTypes[2]=Option&MarketTypes[3]=Debt&MarketTypes[4]=ETF&MarketTypes[5]=TradeOption&BasedOnVolume={true\|false}` | داده‌ی نقشه حرارتی بازار (treemap)، گروه‌بندی‌شده بر اساس صنعت با زیرگروه تودرتو تا سطح نماد؛ `marketIds`=20 بورس، 30 فرابورس؛ `MarketTypes` قابل ترکیب (فقط انواعی که در query باشند لحاظ می‌شوند)؛ `BasedOnVolume` وزن‌دهی بر اساس حجم یا ارزش معاملات | ساختار تودرتو: `{"groups": [...]}` هر گروه صنعت: `label`, `weight`, `tradeVolume`, `tradeValue`, `percent`, و آرایه تودرتوی `groups` در سطح نماد با `instrumentName`, `companyName`, `lastPrice(Change/Percent)`, `closingPrice(Change/Percent)`, `eps`, `pe`, `sharesCount`, `maxValue`, `minValue` |

**نکات:**
- `MarketMapNew` با query params متغیر، امکان فیلتر ترکیبی چند نوع بازار در یک درخواست را می‌دهد (مثلاً هم‌زمان Cash+Future+Option+Debt+ETF+TradeOption) — این برخلاف endpointهای `MarketWatch*` است که هرکدام تک‌نوع هستند.
- این دو endpoint بیشتر برای مصورسازی (heatmap/bubble chart در صفحه اصلی) طراحی شده‌اند تا استخراج داده خام؛ برای نیازهای پایپ‌لاین داده (مثل مرجع نماد یا بک‌تست)، همچنان `MarketWatch*` و `cdn.tsetmc.com` منابع اصلی‌ترند. اما `BubbleChart` می‌تواند به‌عنوان یک منبع سریع و جایگزین برای P/E و `sharesCount` (تعداد سهام) در تحلیل‌های سریع مفید باشد، چون این دو فیلد در بسیاری از endpointهای دیگر مستقیماً موجود نیست.

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

</div>
