# Kvadrat Hisoblash

Katta hajmdagi o'lcham ma'lumotlaridan **kvadrat metr (m²)** ni avtomatik
hisoblovchi professional, mobilga moslashgan veb-dastur. Bir martada 100–500+
qatorli ma'lumotni qabul qiladi, parchalaydi, hisoblaydi va Telegram, CSV, TXT
yoki JSON formatida eksport qiladi.

100% ofline ishlaydi — barcha ma'lumotlar brauzeringizdagi `localStorage`-da
saqlanadi. Hech qanday server, hech qanday bog'liqlik, hech qanday `npm install`
talab etilmaydi: bu bitta `index.html` faylidir.

---

## ✨ Asosiy imkoniyatlar

- **Uchta kirish usuli** — qo'lda matn, fayl yuklash (`.txt` / `.csv`), bufer
  klipidan joylash.
- **Aqlli parser** — Cyrillic va Latin miqdor belgilarini, vergulli kasr
  raqamlarini, har xil ajratuvchilarni va yorliqlarni tushunadi.
- **Ikki formula** —
  - **Kvadrat** (3 ta o'lcham): 3D quti yuzasini hisoblash.
  - **Flat** (2 ta o'lcham): oddiy to'g'ri to'rtburchak yuzasi.
- **Tezkor natija jadvali** — qator turi bo'yicha ranglangan, kengaytiriladigan
  qatorlar, hujayradagi tahrirlash, nusxa olish va o'chirish tugmalari.
- **Filtr · Qidirish · Saralash** — natijalar yuzasidan tezda kerakli qatorlarni
  topish.
- **Eksport** — Telegram uchun nusxa olish, CSV/TXT/JSON yuklash, chop etish.
- **Tarix (sessiyalar)** — har bir hisobni saqlash, tartiblash, qayta yuklash
  (50 tagacha).
- **Avto-saqlash** — har 30 soniyada matn maydoni avtomatik saqlanadi.
- **Sozlamalar** — kasr xonalari, o'lchov birligi (cm/mm), til, mavzu
  (yorug'/qorong'i/avto), Telegram shabloni.
- **Klaviatura yorliqlari** — Ctrl+Enter (hisoblash), Ctrl+S (saqlash) va h.k.

---

## 🚀 Foydalanish

### 1. Fayllarni yuklab olish

Hech qanday o'rnatish kerak emas. Faylni ochib, brauzerda ishlating:

```bash
git clone https://github.com/<sizning-username>/kvadrat-hisoblash.git
cd kvadrat-hisoblash
open index.html        # macOS
xdg-open index.html    # Linux
start index.html       # Windows
```

Yoki `index.html` faylini brauzerga to'g'ridan-to'g'ri sudrab tashlang.

### 2. Birinchi hisob

1. Bosh sahifada **`📋 Misol`** tugmasini bosing — namuna ma'lumotlar
   kirish maydoniga yuklanadi.
2. **`⚡ Hisoblash`** tugmasini bosing (yoki `Ctrl+Enter`).
3. O'ng tarafda (yoki mobilda pastda) **JAMI: m²** xulosasi paydo bo'ladi.
4. **`📋 Telegram uchun`** tugmasini bossangiz, formatlangan natija buferga
   nusxalanadi — bevosita Telegramga joylab yuborish mumkin.

### 3. Faylni yuklash

`Fayl` yorlig'iga o'ting va `.txt` yoki `.csv` faylni quying. Maksimal hajm —
**5 MB**. CSV uchun avtomatik tarzda sarlavha aniqlanadi va birinchi qator
o'tkazib yuboriladi.

---

## 📐 Format qoidalari

### Format 1: Kvadrat (3 ta raqam — A B C)

3D quti tashqi yuzasi formulasi:

```
C₂ = C × 2
result = ((B + C₂) / 100) × (A / 100) + (B / 100) × (C₂ / 100)
```

**Misol:** `137 150 15` → `2.9160 m²`

### Format 2: Flat (2 ta raqam — A B)

Oddiy to'g'ri to'rtburchak:

```
result = (A / 100) × (B / 100)
```

**Misol:** `287 179` → `5.1373 m²`

### Miqdor (qty) belgilari

Qator oxirida miqdor ko'rsatilsa, natija shu raqamga ko'paytiriladi:

| Belgi               | Misol             | Tushuncha          |
|---------------------|-------------------|--------------------|
| `шт`, `штук`, `штука` | `137 150 15 2шт`  | Cyrillic, qty=2    |
| `штN` (шт raqam)     | `220 180 22 шт5`  | Cyrillic, qty=5    |
| `sht`, `pcs`, `dona` | `200 100 25 3sht` | Latin, qty=3       |
| `xN` yoki `*N`        | `75 60 x2`        | Multiplikator, qty=2 |
| `(N)` yoki `[N]`      | `500 300 50 (4)`  | Qavslarda, qty=4   |

### Yorliqlar (label)

Raqamlar orasidagi yoki yonidagi matnli so'zlar e'tiborga olinmaydi, lekin
kirish satrida saqlanadi. Tipik yorliqlar:

`без каз`, `анкер`, `гор`, `шк`, `вер`, `низ`, `боковой`, `задний`

### Ajratuvchilar

Raqamlarni quyidagilar bilan ajratish mumkin:

```
bo'sh joy   x   X   х   Х   ×   *   ,   ;   /
```

Misollar:

```
137 150 15
137x150x15
137 х 150 х 15
137*150*15
145,5 170,5 30      ← vergul (,) kasr sifatida ham ishlaydi
```

### Komment va bo'sh qatorlar

`#` yoki `//` bilan boshlanuvchi qatorlar e'tiborga olinmaydi. Bo'sh qatorlar
ham o'tkazib yuboriladi.

```
# bu komment
//yoki bunaqa
                ← bo'sh qator ham e'tiborga olinmaydi
```

### Maxsus holatlar

| Vaziyat               | Natija                                   |
|-----------------------|------------------------------------------|
| 4+ raqam              | Birinchi 3 tasi ishlatiladi (ogohlantirish) |
| 1 ta raqam            | Xato: "Kamida 2 ta raqam kerak"          |
| Hech raqam yo'q       | Xato: "Format tushunilmadi"              |
| Manfiy raqam          | Xato: "Manfiy raqamlar ruxsat etilmaydi" |
| 0 yoki >10000         | Hisoblanadi, lekin ogohlantirish ko'rsatiladi |

---

## ⌨ Klaviatura yorliqlari

| Yorliq                  | Amal               |
|-------------------------|--------------------|
| `Ctrl/Cmd + Enter`      | Hisoblash          |
| `Ctrl/Cmd + S`          | Sessiya saqlash    |
| `Ctrl/Cmd + K`          | Qidiruv qutisiga o'tish |
| `Ctrl/Cmd + N`          | Yangi sessiya boshlash |
| `Esc`                   | Modalni yopish     |

---

## ⚙ Sozlamalar

Yuqori o'ng burchakdagi **`⚙`** tugmasi orqali quyidagilar boshqariladi:

- **Aniqlik (kasr xonalari)** — 2 dan 6 gacha (sukut: 4).
- **O'lchov birligi** — `cm → m²` (sukut) yoki `mm → m²`. O'zgartirilganda
  natijalar avtomatik qayta hisoblanadi.
- **Til** — O'zbek (sukut), Русский, English.
- **Mavzu** — Yorug', Qorong'i yoki Avto (tizim sozlamasi bo'yicha).
- **Avto-saqlash** — har 30 soniyadagi avtomatik saqlash (sukut: yoqilgan).
- **Telegram shabloni** — eksport sarlavhasini moslashtirish.
- **🗑 Hammasini tozalash** — barcha sozlamalar va saqlangan sessiyalarni
  o'chirish.

---

## 📦 Eksport formatlari

### A) Telegram uchun matn
Bir tugma bosish bilan formatlangan matn buferga nusxalanadi:

```
📐 Kvadrat hisobi (08.05.2026)

1. 137 150 15 2шт = 5.8320
2. 135 150 15 без каз = 2.8800
3. 287 179 (flat) = 5.1373
...
─────────────
✓ Jami: 23 ta
📦 Donalar: 35
🟰 JAMI: 131.5917 m²
```

### B) CSV
Excel yoki Google Sheetsda ochish uchun. Ustunlar:

`#`, `Kirish`, `Tur`, `A`, `B`, `C`, `Miqdor`, `Birlik_qiymat`, `Jami_qiymat`

Fayl nomi: `kvadrat-hisob-YYYY-MM-DD.csv`.

### C) Plain TXT
Telegram bilan o'xshash, lekin emojisiz. Chop qilish yoki arxivlash uchun.

### D) JSON
To'liq metama'lumotli arxiv: barcha qatorlar, sozlamalar, xulosa.

### E) 🖨 Chop etish
Brauzer chop qilish dialogini ochadi. Print uchun maxsus styling qo'llaniladi:
sarlavha, jadval va xulosalar — kerak emas tugmalarsiz.

---

## 🌐 GitHub Pages'ga joylash

1. Repozitoriyani yarating: `kvadrat-hisoblash`.
2. `index.html`, `sample.txt`, `README.md`, `.gitignore` fayllarini push qiling:

   ```bash
   git init
   git add index.html sample.txt README.md .gitignore
   git commit -m "Initial release"
   git branch -M main
   git remote add origin https://github.com/<USER>/kvadrat-hisoblash.git
   git push -u origin main
   ```

3. GitHub repozitoriyangizda **Settings → Pages** ga kiring.
4. **Source** sifatida `Deploy from a branch` ni tanlang, branch — `main`,
   folder — `/ (root)`.
5. **Save** ni bosing. Bir-ikki daqiqa kuting.
6. URL ko'rinadi: `https://<USER>.github.io/kvadrat-hisoblash/`.

Agar custom domeningiz bo'lsa, `Settings → Pages → Custom domain` orqali
qo'shing.

### Lokal ravishda sinash

```bash
# Python 3 (har bir tizimda mavjud)
python3 -m http.server 8000
# yoki
npx serve .
```

So'ng brauzerda `http://localhost:8000` ni oching.

---

## 📁 Fayl strukturasi

```
.
├── index.html      ← Bitta faylga jamlangan: HTML + CSS + JS
├── README.md       ← Hujjat (siz hozir o'qiyapsiz)
├── sample.txt      ← Sinov uchun namuna ma'lumotlar
└── .gitignore
```

Hech qanday `node_modules`, `package.json`, `build/` yo'q. Bu shunchaki bir
qancha statik fayl.

---

## 🛠 Texnik xususiyatlar

| Xususiyat               | Qiymat                                        |
|-------------------------|------------------------------------------------|
| Texnologiya             | Vanilla HTML5 + CSS3 + ES2020 JavaScript       |
| Bog'liqliklar           | **Hech yo'q** (CDN, framework, build step ham) |
| Hosting                 | GitHub Pages, Netlify, har qanday static host  |
| Saqlash                 | `localStorage` (klient brauzerida)             |
| Mobil moslik            | Mukammal — sticky bottom action bar bilan      |
| Brauzer talablari       | Chrome, Firefox, Safari, Edge — so'nggi versiyalar |
| Maks. hajm              | 500+ qatorni 500ms da hisoblaydi               |

---

## 🐛 Muammo bo'lsa

- **Buferdan joylashtirish ishlamayapti** — brauzer xavfsizlik sababli
  bufer ruxsatini so'raydi. Ruxsat berishingiz kerak.
- **Fayl yuklamayapti** — fayl `.txt` yoki `.csv` ekanligini va 5 MB dan
  oshmaganligini tekshiring.
- **Saqlangan sessiyalar yo'q bo'lib ketdi** — brauzerda incognito/private
  rejimda yoki "Clear browsing data" qilingan bo'lsa, `localStorage`
  tozalanadi.

---

## 📝 Litsenziya

MIT — istalgan maqsadda foydalanishingiz mumkin.

---

**Maxsulot foydali bo'lishini tilayman! 📐**
