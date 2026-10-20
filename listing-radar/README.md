# Listing Radar — MVP

داشبورد فارسی برای پایش اولیه توکن‌های DEX در شبکه‌های EVM و Solana با اعلان تلگرام و تأیید دستی. این نسخه خرید انجام نمی‌دهد؛ تأیید تلگرامی فقط تصمیم دستی را ثبت می‌کند.

## قابلیت‌ها
- داشبورد فارسی و راست‌چین
- دریافت پروفایل‌های جدید از DexScreener و بررسی جفت‌معاملاتی
- امتیازدهی اولیه با نقدینگی، حجم و سن جفت
- اعلان تلگرام با دکمه‌های تأیید دستی، رد و بررسی مجدد
- ذخیره وضعیت در Cloudflare KV و اسکن دوره‌ای با Cron

## محدودیت‌ها
- پایش اطلاعیه‌های صرافی‌های متمرکز (CEX) هنوز پیاده‌سازی نشده است.
- امتیازدهی، ممیزی قرارداد یا تضمین سود نیست؛ honeypot، مالکیت متمرکز و قابلیت mint/freeze کامل بررسی نمی‌شوند.
- تأیید تلگرام معامله اجرا نمی‌کند.
- کلید خصوصی یا seed phrase را هرگز در این پروژه وارد نکنید.

## استقرار در Cloudflare Workers
1. یک KV namespace بسازید و شناسه آن را در wrangler.toml جایگزین REPLACE_WITH_KV_NAMESPACE_ID کنید.
2. Secrets زیر را در تنظیمات Worker تعریف کنید: TELEGRAM_BOT_TOKEN، TELEGRAM_CHAT_ID و TELEGRAM_ALLOWED_USER_ID.
3. Worker را deploy کنید و webhook تلگرام را به https://YOUR-WORKER-DOMAIN/telegram وصل کنید.
4. مسیر /api/scan اسکن دستی و /api/status وضعیت سرویس را می‌دهد.

TELEGRAM_CHAT_ID مقصد اعلان‌هاست؛ TELEGRAM_ALLOWED_USER_ID شناسه عددی کاربر مجاز برای تأیید و رد است و لزوماً یکی نیستند. توکن را در کد یا مخزن قرار ندهید.

## مسیرها
- / داشبورد
- /api/status وضعیت
- /api/opportunities فرصت‌های ذخیره‌شده
- /api/scan اجرای اسکن با POST
- /telegram دریافت callback تلگرام

تنظیمات اختیاری: MIN_LIQUIDITY_USD (پیش‌فرض 25000)، MIN_VOLUME_24H_USD (پیش‌فرض 10000)، MAX_PROFILE_SCAN (پیش‌فرض 25). این پروژه MVP است، نه سامانه آماده معامله خودکار.