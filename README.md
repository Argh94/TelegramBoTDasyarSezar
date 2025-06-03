# 🚀 Telegram Bot Channel Manager (Cloudflare Workers)

**[English](#english) | [فارسی (Persian)](#persian)**

---

## 🇬🇧 English
<a name="english"></a>

[![Language](https://img.shields.io/badge/language-JavaScript-yellow.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![Platform](https://img.shields.io/badge/platform-Cloudflare%20Workers-orange.svg)](https://workers.cloudflare.com/)
[![Dependency](https://img.shields.io/badge/dependency-Telegram%20Bot%20API-blue.svg)](https://core.telegram.org/bots/api)
[![Dependency](https://img.shields.io/badge/storage-Cloudflare%20KV-red.svg)](https://developers.cloudflare.com/workers/runtime-apis/kv/)
[![GitHub Stars](https://img.shields.io/github/stars/SezarSec/telegram-bot-channel-manager?style=social)](https://github.com/SezarSec/telegram-bot-channel-manager/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/SezarSec/telegram-bot-channel-manager?style=social)](https://github.com/SezarSec/telegram-bot-channel-manager/network/members)
[![GitHub Issues](https://img.shields.io/github/issues/SezarSec/telegram-bot-channel-manager)](https://github.com/SezarSec/telegram-bot-channel-manager/issues)
[![License](https://img.shields.io/github/license/SezarSec/telegram-bot-channel-manager)](https://github.com/SezarSec/telegram-bot-channel-manager/blob/main/LICENSE)

> **A blazing-fast, scalable, and serverless Telegram channel management bot powered by Cloudflare Workers!**  
> Effortlessly create, schedule, and control content distribution across multiple Telegram channels with a rich admin panel and automated controls.

---

### ✨ Features at a Glance

- **Guided Multi-step Post Creation:** Capture title, description, image (optional), download limit, and main content (file or text) in an intuitive flow.
- **Multi-Channel Broadcasting:** Send posts to one or multiple Telegram channels, fully configurable.
- **Rich Inline Channel Buttons:**
    - "Get File" deep-link button leading users directly to the bot.
    - Real-time download stats (downloads/limit) at a glance.
- **Auto-Expiring Files:** User-accessed files are deleted from chat after a defined interval (e.g., 15 seconds) for safety and space.
- **Advanced Admin Panel (`/panel`):**
    - One-click post creation, viewing, and deletion (with pagination).
    - Manage and audit target channels.
    - Comprehensive stats (total/banned users).
    - User management (ban/unban, details, pagination).
    - Global message broadcasting.
    - Full forced-join control for growth hacking.
- **Forced Join Enforcement:** Bot auto-checks user membership in required channels before granting access.
- **Cloudflare KV Storage:** All data (posts, users, settings) is securely stored in high-availability, low-latency KV.
- **Serverless, Fast, and Infinitely Scalable:** Deploys as a lightweight Cloudflare Worker.

---

### 🚀 Getting Started

#### Prerequisites

1. **Cloudflare Account:** For deploying Workers and using KV.
2. **Telegram Bot Token:** [Create via BotFather](https://t.me/BotFather).
3. **(Optional) Wrangler CLI:** CLI tool for Cloudflare Workers (recommended).
    ```bash
    npm install -g wrangler
    ```

#### Setup Steps

1. **Clone the Repository:**
    ```bash
    git clone https://github.com/SezarSec/telegram-bot-channel-manager.git
    cd telegram-bot-channel-manager
    ```
    Or copy `index.js` into your Worker project.

2. **Create a KV Namespace:**
    - Cloudflare Dashboard → Workers & Pages → KV → Create Namespace (e.g., `TELEGRAM_BOT_DATA`).
    - Copy the **Namespace ID**.

3. **Configure the Worker:**
    - **Using Wrangler:**
        - Edit `wrangler.toml` as shown:
            ```toml
            name = "telegram-bot-channel-manager"
            main = "src/index.js"
            compatibility_date = "YYYY-MM-DD"
            kv_namespaces = [
              { binding = "BOT_KV", id = "YOUR_KV_NAMESPACE_ID" }
            ]
            ```
        - Set secrets:
            ```bash
            wrangler secret put BOT_TOKEN
            wrangler secret put ADMIN_CHAT_ID
            wrangler secret put BOT_USERNAME
            ```
    - **Via Dashboard:**
        - Create/Edit Worker, paste `index.js` in the editor.
        - Under *Settings → Variables*:
            - Add `BOT_KV` binding to your KV Namespace.
            - Add and encrypt secrets: `BOT_TOKEN`, `ADMIN_CHAT_ID`, `BOT_USERNAME`.
        - Set Compatibility Date.

4. **Deploy:**
    - Wrangler: `wrangler deploy`
    - Dashboard: Save & Deploy

5. **Set Telegram Webhook:**
    - Get your Worker URL (e.g., `https://telegram-bot-channel-manager.your-subdomain.workers.dev`)
    - Open:
        ```
        https://api.telegram.org/bot<YOUR_BOT_TOKEN>/setWebhook?url=<YOUR_WORKER_URL>
        ```
    - Or, visit `/setwebhook` endpoint:
        ```
        https://telegram-bot-channel-manager.your-subdomain.workers.dev/setwebhook
        ```

6. **Initial Bot Setup:**
    - Start a chat with your bot, send `/start`.
    - Use `/panel` to access the admin menu and perform first-time configuration (add target/forced-join channels).
    - Ensure your bot is an admin in all relevant channels with the necessary permissions.

---

### 🛠️ Admin Commands (Chat or Panel)

- `/panel`: Open the full-featured admin panel.
- **Posts:**
    - `/newpost` – Create new post.
    - `/deletepost <ID>` – Delete post by ID.
    - **List & Delete** via panel.
- **Channels:**
    - `/addtargetchannel <ID|Username>`
    - `/removetargetchannel <ID|Username>`
    - `/listtargetchannels`
- **Stats & Users:**
    - `/stats`
    - `/listusers`
    - `/ban <UserID>`
    - `/unban <UserID>`
- **Broadcast:**
    - `/broadcast <Message>`
- **Forced Join:**
    - `/addjoinchannel <ID|Username>`
    - `/removejoinchannel <ID|Username>`
    - `/listjoinchannels`
- **Admins (Main Admin Only):**
    - `/addadmin <UserID>`
    - `/removeadmin <UserID>`
    - `/listadmins`

---

### ⚙️ Required Environment Variables

- `BOT_TOKEN`: Telegram Bot API token
- `ADMIN_CHAT_ID`: Numeric Telegram ID of main admin
- `BOT_USERNAME`: Bot username (without `@`)
- `(Optional) config:channel_username_display`: Channel username to display at post end (e.g., `@MyPublicChannel`)

---

### 🤝 Contributing

Pull requests and issues are welcome! Help make this project better—submit features, report bugs, or start a discussion.

---

### 📞 Contact

- **GitHub:** [https://github.com/Argh94](https://github.com/Argh94)


---

### 📜 License

MIT License

---

---

## 🇮🇷 فارسی (Persian)
<a name="persian"></a>


[![زبان](https://img.shields.io/badge/language-JavaScript-yellow.svg)](https://developer.mozilla.org/en-US/docs/Web/JavaScript)
[![پلتفرم](https://img.shields.io/badge/platform-Cloudflare%20Workers-orange.svg)](https://workers.cloudflare.com/)
[![وابستگی](https://img.shields.io/badge/dependency-Telegram%20Bot%20API-blue.svg)](https://core.telegram.org/bots/api)
[![وابستگی](https://img.shields.io/badge/storage-Cloudflare%20KV-red.svg)](https://developers.cloudflare.com/workers/runtime-apis/kv/)
[![ستاره‌های گیت‌هاب](https://img.shields.io/github/stars/SezarSec/telegram-bot-channel-manager?style=social&label=ستاره)](https://github.com/SezarSec/telegram-bot-channel-manager/stargazers)
[![فورک‌های گیت‌هاب](https://img.shields.io/github/forks/SezarSec/telegram-bot-channel-manager?style=social&label=فورک)](https://github.com/SezarSec/telegram-bot-channel-manager/network/members)
[![مشکلات گیت‌هاب](https://img.shields.io/github/issues/SezarSec/telegram-bot-channel-manager?label=مشکلات)](https://github.com/SezarSec/telegram-bot-channel-manager/issues)
[![مجوز](https://img.shields.io/github/license/SezarSec/telegram-bot-channel-manager?label=مجوز)](https://github.com/SezarSec/telegram-bot-channel-manager/blob/main/LICENSE)

> **ربات مدیریت کانال تلگرام فوق‌سریع و بدون سرور با قدرت Cloudflare Workers!**  
> مدیریت، زمان‌بندی و انتشار هوشمندانه محتوا در چندین کانال تلگرامی با پنل ادمین حرفه‌ای و کنترل‌های خودکار.

---

### ✨ امکانات برجسته

- **ایجاد پست مرحله‌ای:** ثبت تیتر، توضیحات، تصویر (اختیاری)، محدودیت دانلود و محتوای اصلی (فایل یا متن) در چند گام ساده.
- **ارسال به چندین کانال:** هر تعداد کانال تلگرامی که بخواهید، مدیریت کنید.
- **دکمه‌های شیشه‌ای پیشرفته:**  
    - دکمه «دریافت فایل» با لینک مستقیم (Deep Link) به ربات  
    - دکمه آمار دانلود (تعداد دانلود شده از کل محدودیت)
- **حذف خودکار فایل:** فایل‌های ارسالی پس از مدت معین (مثلاً ۱۵ ثانیه) به صورت خودکار از چت حذف می‌شوند.
- **پنل مدیریت پیشرفته (`/panel`):**
    - ایجاد، مشاهده و حذف پست‌ها (با صفحه‌بندی)
    - مدیریت و بررسی کانال‌های هدف
    - مشاهده آمار جامع (تعداد کل/مسدود)
    - مدیریت کاربران (بن/آنبن، جزییات، صفحه‌بندی)
    - ارسال پیام همگانی
    - کنترل کامل عضویت اجباری
- **بررسی عضویت اجباری:** قبل از ارسال فایل، عضویت کاربر در کانال‌های لازم بررسی می‌شود.
- **ذخیره‌سازی Cloudflare KV:** داده‌ها در بستر KV Cloudflare با دسترسی سریع و ایمن ذخیره می‌شود.
- **بدون سرور، سریع و مقیاس‌پذیر:** به صورت Worker روی Cloudflare.

---

### 🚀 راه‌اندازی سریع

#### پیش‌نیازها

1. **حساب Cloudflare** (برای Workers و KV)
2. **توکن ربات تلگرام** (از [BotFather](https://t.me/BotFather))
3. **(اختیاری) Wrangler CLI:** ابزار خط فرمان Cloudflare  
    ```bash
    npm install -g wrangler
    ```

#### مراحل نصب

1. **کلون پروژه:**
    ```bash
    git clone https://github.com/SezarSec/telegram-bot-channel-manager.git
    cd telegram-bot-channel-manager
    ```
    یا فایل `index.js` را کپی کنید.

2. **ایجاد KV Namespace:**
    - داشبورد Cloudflare → Workers & Pages → KV → ایجاد Namespace (مثلاً `TELEGRAM_BOT_DATA`)
    - **ID** را کپی کنید.

3. **پیکربندی ورکر:**
    - **با Wrangler:**
        - ویرایش `wrangler.toml`:
            ```toml
            name = "telegram-bot-channel-manager"
            main = "src/index.js"
            compatibility_date = "YYYY-MM-DD"
            kv_namespaces = [
              { binding = "BOT_KV", id = "YOUR_KV_NAMESPACE_ID" }
            ]
            ```
        - ثبت متغیرهای محرمانه:
            ```bash
            wrangler secret put BOT_TOKEN
            wrangler secret put ADMIN_CHAT_ID
            wrangler secret put BOT_USERNAME
            ```
    - **از طریق داشبورد:**
        - Worker جدید بسازید یا ویرایش کنید و کد را وارد نمایید.
        - در *Settings → Variables*:
            - Binding با نام `BOT_KV` را اضافه کنید.
            - Secrets: `BOT_TOKEN`, `ADMIN_CHAT_ID`, `BOT_USERNAME` را اضافه و رمزنگاری کنید.
        - Compatibility Date را تنظیم کنید.

4. **انتشار:**
    - با Wrangler: `wrangler deploy`
    - یا داشبورد: Save & Deploy

5. **تنظیم Webhook تلگرام:**
    - آدرس ورکر خود را (مثلاً `https://telegram-bot-channel-manager.your-subdomain.workers.dev`) جایگذاری کنید:
        ```
        https://api.telegram.org/bot<YOUR_BOT_TOKEN>/setWebhook?url=<YOUR_WORKER_URL>
        ```
    - یا مسیر `/setwebhook` را در مرورگر باز کنید:
        ```
        https://telegram-bot-channel-manager.your-subdomain.workers.dev/setwebhook
        ```

6. **راه‌اندازی اولیه:**
    - به ربات پیام دهید و `/start` بفرستید.
    - با `/panel` به پنل مدیریت بروید و تنظیمات اولیه را انجام دهید (افزودن کانال و ...).
    - مطمئن شوید ربات در کانال(های) هدف و عضویت اجباری، ادمین است و مجوزها را دارد.

---

### 🛠️ دستورات ادمین (چت یا پنل)

- `/panel`: باز کردن پنل مدیریت
- **پست‌ها:**
    - `/newpost` – ایجاد پست جدید
    - `/deletepost <ID>` – حذف پست با شناسه
    - **لیست و حذف** از پنل
- **کانال‌ها:**
    - `/addtargetchannel <ID|یوزرنیم>`
    - `/removetargetchannel <ID|یوزرنیم>`
    - `/listtargetchannels`
- **آمار و کاربران:**
    - `/stats`
    - `/listusers`
    - `/ban <شناسه>`
    - `/unban <شناسه>`
- **پیام همگانی:**
    - `/broadcast <متن>`
- **عضویت اجباری:**
    - `/addjoinchannel <ID|یوزرنیم>`
    - `/removejoinchannel <ID|یوزرنیم>`
    - `/listjoinchannels`
- **ادمین‌ها (فقط ادمین اصلی):**
    - `/addadmin <شناسه>`
    - `/removeadmin <شناسه>`
    - `/listadmins`

---

### ⚙️ متغیرهای محیطی مورد نیاز

- `BOT_TOKEN`: توکن ربات تلگرام
- `ADMIN_CHAT_ID`: شناسه عددی ادمین اصلی
- `BOT_USERNAME`: نام کاربری ربات (بدون @)
- `(اختیاری) config:channel_username_display`: یوزرنیم کانال انتهای پست

---

### 🤝 مشارکت

پیشنهادها، باگ‌ها و Pull Request های شما موجب پیشرفت پروژه خواهد شد! حتما با ما در ارتباط باشید.

---

### 📞 ارتباط
- **GitHub:** [https://github.com/Argh94](https://github.com/Argh94)

---

### 📜 مجوز

این پروژه تحت مجوز MIT منتشر شده است.

---
