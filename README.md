# cafe-menu-data

Repository نگهداری داده‌های منوی کافه آنلاین (Online Cafe Menu).

این Repository **فقط Data** است و شامل هیچ کد Frontend (React / Vite / Tailwind / Admin Panel) نیست.
اطلاعات داخل آن Fake و برای تست و توسعه است.

قرار است توسط یک Frontend ساخته‌شده با **React + Vite** مصرف شود؛ Frontend این فایل‌های JSON را خوانده و منو را نمایش می‌دهد.

## Repository Structure

```
cafe-menu-data/
│
├── data/
│   ├── products.json
│   ├── categories.json
│   └── cafe.json
│
├── images/
│   └── products/
│
├── README.md
└── .gitignore
```

## Data Model

### Category

```json
{
  "id": 1,
  "name": "قهوه",
  "slug": "coffee"
}
```

- `id`: شناسه یکتا
- `name`: نام نمایشی
- `slug`: نام لاتین یکتا (برای URL)

### Product

```json
{
  "id": 1,
  "cafeId": 1,
  "name": "لاته",
  "slug": "latte",
  "description": "قهوه اسپرسو همراه با شیر بخار داده شده",
  "categoryId": 1,
  "image": "images/products/1.webp",
  "variants": [
    { "id": 101, "name": "کوچک", "price": 150000 },
    { "id": 102, "name": "متوسط", "price": 180000 },
    { "id": 103, "name": "بزرگ", "price": 220000 }
  ],
  "isAvailable": true
}
```

- `id`, `cafeId`, `categoryId`: شناسه‌ها
- `name`, `slug`, `description`: اطلاعات محصول
- `image`: مسیر تصویر (نسبی به ریشه Repository)
- `variants`: لیست گزینه‌های قیمت محصول (حداقل یک Variant دارد)
- `isAvailable`: وضعیت موجود بودن (برای تست وضعیت ناموجود)

### Variant

هر محصول حداقل یک Variant دارد. سناریوهای پشتیبانی‌شده:

- **یک قیمت**: یک Variant با نامی مثل `تکی`
- **چند سایز**: `کوچک` / `متوسط` / `بزرگ`
- **حجم‌بندی**: `250ml` / `350ml` / `500ml`

Variant IDها در کل Repository یکتا هستند.

## Price

قیمت‌ها به صورت **Integer** و بر اساس **تومان** هستند (بدون جداکننده و بدون واحد):

```json
"price": 180000
```

## Image Naming Convention

نام فایل تصویر با Product ID هماهنگ است (فرمت WebP):

```
Product ID = 25  →  images/products/25.webp
```

این قرارداد باعث می‌شود هنگام حذف یک Product، تصویر مربوطه نیز قابل پیدا کردن و حذف باشد.

## Future Compatibility

ساختار فعلی ساده نگه داشته شده تا در آینده بتوان افزود:

- چند کافه
- افزودنی‌ها (Add-ons)
- تخفیف (Discount)
- موجودی (Inventory)
- محصول ویژه (Featured)
- برچسب‌ها (Tags)
- گزینه‌های محصول (Options)
- ذخیره‌سازی جداگانه تصاویر (Object Storage مثل R2)
