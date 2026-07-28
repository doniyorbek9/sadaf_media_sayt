# Sadaf Media — sayt

To'y, xatna, banket va boshqa marosimlar uchun videografiya xizmati sayti.
AI-yordamchi (Groq), buyurtma formasi (Telegramga + Excel'ga saqlanadi).

## Loyihada nima bor

- `app.py` — Flask backend
- `templates/index.html` — sayt (real logo, video, jamoa, narxlar)
- `static/logo.png`, `static/hero-preview.mp4` — sizning fayllaringizdan
- `data/orders.xlsx` — buyurtmalar shu yerga avtomatik saqlanadi (birinchi buyurtmada yaratiladi)

## 1. Railway'ga joylash

1. Bu papkani GitHub'ga yuklang (yangi repo yarating, push qiling). **`.env` faylini hech qachon GitHub'ga yubormang** — u sizning maxfiy kalitlaringizni saqlaydi, `.gitignore` uni avtomatik chiqarib tashlaydi.
2. [railway.app](https://railway.app) da "New Project" → "Deploy from GitHub repo" → shu repo'ni tanlang.
3. Railway loyihasida **Variables** bo'limiga o'ting va quyidagilarni qo'shing:

   | Nomi | Qiymati |
   |---|---|
   | `TELEGRAM_BOT_TOKEN` | sizning bot tokeningiz |
   | `ADMIN_CHAT_ID` | pastdagi 2-qadamga qarang |
   | `GROQ_API_KEY` | sizning Groq kalitingiz |
   | `ADMIN_DOWNLOAD_KEY` | o'zingiz o'ylab toping (masalan `sadaf-admin-2026`) — buyurtmalar faylini yuklab olish uchun parol |

4. Railway avtomatik `Procfile`ni ko'rib, saytni ishga tushiradi. Bir necha daqiqadan so'ng sizga domen beriladi (masalan `sadaf-media.up.railway.app`). Keyinchalik o'z domeningizni ham ulashingiz mumkin (Railway → Settings → Domains).

## 2. Telegram Chat ID'ni qanday topish (buyurtma xabarlari shu yerga tushadi)

1. Telegram'da botingizni toping va unga istalgan xabar yozing (masalan "salom").
2. Brauzerda quyidagi manzilni oching (TOKEN o'rniga o'z tokeningizni qo'ying):
   `https://api.telegram.org/botTOKEN/getUpdates`
3. Natijada `"chat":{"id": 123456789, ...}` ko'rinishida raqam chiqadi — shu raqam sizning `ADMIN_CHAT_ID`.
4. Shu raqamni Railway'dagi `ADMIN_CHAT_ID` o'zgaruvchisiga qo'ying.

> Eslatma: bir nechta admin xabar olishini xohlasangiz, keyinroq buni guruh chatiga yuborishga o'zgartirib beraman.

## 3. Buyurtmalarni Excel formatda olish

Quyidagi manzilga kirsangiz, barcha buyurtmalar bo'lgan `.xlsx` fayl yuklab olinadi:

```
https://SIZNING-DOMENINGIZ/admin/orders?key=SIZ_TANLAGAN_ADMIN_DOWNLOAD_KEY
```

Bu link botda "ochib ketmaydi" — doim shu manzilga kirib, eng yangi Excel faylni olasiz.

## 4. Narxlar va matnlarni o'zgartirish

- Narxlar/paketlar: `app.py` ichidagi `PACKAGES` lug'atini tahrirlang.
- Xizmatlar ro'yxati: `app.py` ichidagi `SERVICES`.
- Jamoa: `app.py` ichidagi `TEAM`.
- Bularning barchasi saytga ham, AI-yordamchining bilim bazasiga ham avtomatik tushadi — ikkalasini alohida yozish shart emas.

## 5. Hali hal qilinmagan narsalar

- **"3 kunlik" paket nomi** — hozircha "Cinema Grand" deb qo'yildi, narxi ham hali yo'q ("so'rov bo'yicha" deb yozilgan). Nom/narx aytsangiz, bir zumda yangilab beraman.
- **To'lov** — hozircha faqat "xizmatdan keyin to'lov" deb yozilgan, onlayn to'lov (Click/Payme) yo'q. Kerak bo'lsa keyin qo'shamiz.
- Showreel video sifatida hozircha yuborgan videongizdan 12 soniyalik parcha ishlatildi (fon uchun). To'liq portfolio bo'limi keyingi bosqichda qo'shiladi — bir nechta qisqa video/rasm namunalar yuborsangiz, joylab beraman.

## Lokal test qilish (ixtiyoriy)

```
pip install -r requirements.txt
python3 app.py
```

`.env` faylidagi maxfiy kalitlar avtomatik o'qiladi (faqat lokal uchun; Railway'da Variables ishlatiladi).
