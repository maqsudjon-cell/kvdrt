# KVADRAT — panjara m² hisoblagich

**kvdrt.maqsudjon.com**

Payvand va montaj ishlari uchun kvadrat metr hisoblagich. O'lchamlarni yozasiz —
jami m² darhol chiqadi, PDF yoki Telegram xabari qilib beriladi.

Bitta `index.html` fayl. Server yo'q, build yo'q, o'rnatish yo'q.
Ma'lumot faqat brauzerdagi `localStorage`-da saqlanadi.

---

## Raqamlar tartibi

Har bir qator — bitta detal. Tartib **doim** bir xil:

```
eni  bo'yi  vistup
120  130    30
```

| Raqam | Nomi   | Ma'nosi                              |
|-------|--------|--------------------------------------|
| 1-chi | eni    | kengligi, chapdan o'ngga             |
| 2-chi | bo'yi  | balandligi, pastdan tepaga           |
| 3-chi | vistup | oldinga qancha chiqadi (chuqurligi)  |

Vistup yozilmasa — tekis panjara deb olinadi (`120 130`).

## Formula

**Vistupli** (3 ta raqam) — old yuza + to'rtta yon yuza:

```
S = eni × bo'yi + 2 × vistup × (eni + bo'yi)

120 130 30 →  1.20 × 1.30 + 2 × 0.30 × (1.20 + 1.30)
           =  1.56 + 1.50
           =  3.06 m²
```

**Tekis** (2 ta raqam):

```
S = eni × bo'yi        →  287 179  =  5.1373 m²
```

## Qator yozish qoidalari

| Nima              | Qanday yoziladi                                        |
|-------------------|--------------------------------------------------------|
| Dona soni         | `2 dona` · `2sht` · `2шт` · `x2` · `(2)`               |
| Kasr              | `145,5` yoki `145.5`                                   |
| Detal nomi        | raqamlardan oldin/keyin so'z: `oshxona 120 130 30`     |
| Izoh (hisoblanmaydi) | qator `#` yoki `//` bilan boshlansa                 |
| Ajratgich         | bo'sh joy, `x`, `×`, `х`, `*` — bari ishlaydi          |

`x` harfi faqat alohida turganda ajratgich sanaladi, shuning uchun
`oshxona`, `taxta` kabi so'zlar buzilmaydi.

## Imkoniyatlar

- **Qisqa tanishtiruv** — birinchi kirishda 4 ta slayd (nima qiladi, raqamlar
  tartibi, qator qoidalari, natija). Bir marta ko'rsatiladi
  (`localStorage: kvadrat.intro.v1`), keyin yordam oynasidan qayta ochiladi.
- **Ikki xil kiritish** — bittalab (maydonlar bo'yicha) yoki ro'yxat/nusxa
  (bir necha o'nlab qatorni birdan qo'yish).
- **Jonli chizma** — eni / bo'yi / vistup qaysi tomon ekanini ko'rsatadi,
  yozilayotgan raqamlarga qarab o'zgaradi.
- **SM / MM** — o'lchov birligi tanlanadi, natija baribir m² da.
- **Narx** — 1 m² narxi kiritilsa umumiy summa ham hisoblanadi.
- **Doimiy pastki panel** — jami m², summa va **PDF** / **Telegram** tugmalari
  ekrandan ketmaydi. Ro'yxat qancha uzun bo'lmasin, natijaga scroll qilib
  borish shart emas. Yonida «tepaga» tugmasi.
- **Uzun ro'yxat yig'iladi** — 15 qatordan ko'pi «Yana N ta qatorni ko'rsatish»
  ostiga yashiriladi. Jami va eksport doim to'liq ro'yxat bo'yicha.
- **Eksport** — PDF va Telegram uchun nusxa. PDF da kirill/o'zbek harflari
  lotinga o'giriladi (`гор` → `gor`), shuning uchun hech qachon buzilmaydi.
- **Yorug' / qorong'i mavzu**, avtomatik saqlash, mobilga to'liq moslashgan.

## Ishga tushirish

```bash
open index.html
```

Boshqa hech narsa kerak emas. Yagona tashqi bog'liqlik — PDF uchun jsPDF (CDN)
va Google Fonts; ular yuklanmasa ham hisoblash ishlayveradi.

## Deploy

GitHub Pages, `main` bo'lim ildizidan. Domen `CNAME` faylida:
`kvdrt.maqsudjon.com`.
