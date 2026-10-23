<docs-decorative-header title="Signallar bilan formalar" imgSrc="adev/src/assets/images/signals.svg"> </docs-decorative-header>

Signal Forms forma holatini Angular signallari yordamida boshqaradi va maʼlumotlar modelingiz bilan UI oʻrtasida avtomatik sinxronlashni taʼminlaydi.

Ushbu qoʻllanma Signal Forms bilan formalar yaratishning asosiy tushunchalari boʻylab sizga yoʻl koʻrsatadi. U quyidagicha ishlaydi:

## Birinchi formangizni yaratish

### 1. `signal()` bilan forma modelini yarating

Har bir forma formangizning maʼlumotlar modelini saqlaydigan signal yaratishdan boshlanadi:

```ts
interface LoginData {
  email: string;
  password: string;
}

const loginModel = signal<LoginData>({
  email: '',
  password: '',
});
```

### 2. `FieldTree` yaratish uchun forma modelini `form()`'ga uzating

Keyin, forma modelingizni `form()` funksiyasiga uzatib **maydonlar daraxtini** (field tree) yaratasiz — bu modelingiz tuzilmasini aks ettiruvchi obyekt boʻlib, maydonlarga nuqta belgisi orqali murojaat qilish imkonini beradi.

Ildiz forma obyekti ham, uning ichki xususiyatlari ham `FieldTree` tugunlaridir:

```ts
const loginForm = form(loginModel);

loginForm; // is a FieldTree
loginForm.email; // is also a FieldTree
```

### 3. HTML input'larni `[formField]` direktivi bilan bogʻlang

Keyin, HTML input'laringizni `[formField]` direktivi yordamida formaga bogʻlaysiz; bu ular oʻrtasida ikki tomonlama bogʻlash yaratadi:

```html
<input type="email" [formField]="loginForm.email" />
<input type="password" [formField]="loginForm.password" />
```

Natijada foydalanuvchi oʻzgarishlari (masalan, maydonga matn kiritish) formani avtomatik yangilaydi.

NOTE: `[formField]` direktivi shuningdek, kerak boʻlganda `required`, `disabled` va `readonly` kabi atributlar uchun maydon holatini ham sinxronlaydi.

### 4. `FieldTree` signallari bilan holatni oʻqing

Daraxtning istalgan qismi holatiga `FieldTree` tugunini funksiya sifatida chaqirish orqali murojaat qilishingiz mumkin. Bu qiymat, validatsiya holati va oʻzaro aloqa holati uchun reaktiv signallarni oʻz ichiga olgan holat obyektini qaytaradi:

```ts
loginForm(); // Returns state for the whole form
loginForm.email(); // Returns state for the email field
```

Joriy qiymatni oʻqish uchun `value()` signaliga murojaat qiling:

```html
<!-- Render values that update automatically as user types -->
<p>Form value: {{ loginForm().value() | json }}</p>
<p>Email: {{ loginForm.email().value() }}</p>
```

```ts
// Get the current value
const currentEmail = loginForm.email().value();
```

### 5. `set()` bilan qiymatlarni yangilang

Istalgan tugundagi `value.set()` metodi yordamida qiymatlarni dasturiy ravishda yangilashingiz mumkin. Bu `FieldTree`'ni ham, asosiy model signalini ham yangilaydi:

```ts
// Update the value programmatically
loginForm.email().value.set('alice@wonderland.com');
```

Natijada maydon qiymati ham, model signali ham avtomatik yangilanadi:

```ts
// The model signal is also updated
console.log(loginModel().email); // 'alice@wonderland.com'
```

### Toʻliq misol

<docs-code-multifile preview path="adev/src/content/examples/signal-forms/src/login-simple/app/app.ts">
  <docs-code header="app.ts" path="adev/src/content/examples/signal-forms/src/login-simple/app/app.ts"/>
  <docs-code header="app.html" path="adev/src/content/examples/signal-forms/src/login-simple/app/app.html"/>
  <docs-code header="app.css" path="adev/src/content/examples/signal-forms/src/login-simple/app/app.css"/>
</docs-code-multifile>

## Asosiy foydalanish

`[formField]` direktivi barcha standart HTML input turlari bilan ishlaydi. Eng keng tarqalgan namunalar:

### Matnli input'lar

Matnli input'lar turli `type` atributlari va textarea'lar bilan ishlaydi:

```html
<!-- Text and email -->
<input type="text" [formField]="form.name" />
<input type="email" [formField]="form.email" />
```

#### Sonlar

Sonli input'lar satr va sonlar oʻrtasida avtomatik konvertatsiya qiladi:

```html
<!-- Number - automatically converts to number type -->
<input type="number" [formField]="form.age" />
```

#### Sana va vaqt

Sana input'lari qiymatlarni `YYYY-MM-DD` satrlari sifatida, vaqt input'lari esa `HH:mm` formatida saqlaydi:

```html
<!-- Date and time - stores as ISO format strings -->
<input type="date" [formField]="form.eventDate" />
<input type="time" [formField]="form.eventTime" />
```

Agar sana satrlarini Date obyektlariga aylantirish kerak boʻlsa, maydon qiymatini `Date()`'ga uzatish orqali buni qilishingiz mumkin:

```ts
const dateObject = new Date(form.eventDate().value());
```

#### Koʻp qatorli matn

Textarea'lar matnli input'lar bilan bir xil ishlaydi:

```html
<!-- Textarea -->
<textarea [formField]="form.message" rows="4"></textarea>
```

### Belgilash katakchalari (checkbox)

Belgilash katakchalari boolean qiymatlarga bogʻlanadi:

```html
<!-- Single checkbox -->
<label>
  <input type="checkbox" [formField]="form.agreeToTerms" />
  I agree to the terms
</label>
```

#### Bir nechta belgilash katakchalari

Bir nechta variant uchun har biriga alohida boolean `formField` yarating:

```html
<label>
  <input type="checkbox" [formField]="form.emailNotifications" />
  Email notifications
</label>
<label>
  <input type="checkbox" [formField]="form.smsNotifications" />
  SMS notifications
</label>
```

### Radio tugmalar

Radio tugmalar belgilash katakchalariga oʻxshab ishlaydi. Radio tugmalar bir xil `[formField]` qiymatidan foydalansa, Signal Forms ularning barchasiga avtomatik ravishda bir xil `name` atributini bogʻlaydi:

```html
<label>
  <input type="radio" value="free" [formField]="form.plan" />
  Free
</label>
<label>
  <input type="radio" value="premium" [formField]="form.plan" />
  Premium
</label>
```

Foydalanuvchi radio tugmani tanlaganda, forma `formField`'i oʻsha radio tugmaning `value` atributidagi qiymatni saqlaydi. Masalan, "Premium" tanlansa, `form.plan().value()` qiymati `"premium"` boʻladi.

### Tanlov roʻyxatlari (select)

Select elementlari statik va dinamik variantlar bilan ishlaydi:

```angular-html
<!-- Static options -->
<select [formField]="form.country">
  <option value="">Select a country</option>
  <option value="us">United States</option>
  <option value="ca">Canada</option>
</select>

<!-- Dynamic options with @for -->
<select [formField]="form.productId">
  <option value="">Select a product</option>
  @for (product of products; track product.id) {
    <option [value]="product.id">{{ product.name }}</option>
  }
</select>
```

NOTE: Koʻp tanlovli select (`<select multiple>`) hozircha `[formField]` direktivi tomonidan qoʻllab-quvvatlanmaydi.

## Validatsiya va holat

Signal Forms forma maydonlaringizga qoʻllashingiz mumkin boʻlgan oʻrnatilgan validatorlarni taqdim etadi. Validatsiya qoʻshish uchun `form()`'ga ikkinchi argument sifatida sxema funksiyasini uzating:

```ts
const loginForm = form(loginModel, (schemaPath) => {
  debounce(schemaPath.email, 500);
  required(schemaPath.email);
  email(schemaPath.email);
});
```

Sxema funksiyasi validatsiya qoidalarini sozlash uchun maydonlaringizga yoʻllarni taqdim etuvchi **sxema yoʻli** (schema path) parametrini qabul qiladi.

Keng tarqalgan validatorlar:

- **`required()`** - Maydonda qiymat borligini taʼminlaydi
- **`email()`** - Email formatini tekshiradi
- **`min()`** / **`max()`** - Son diapazonlarini tekshiradi
- **`minLength()`** / **`maxLength()`** - Satr yoki toʻplam uzunligini tekshiradi
- **`pattern()`** - Regex namunasiga mosligini tekshiradi

Validatorga ikkinchi argument sifatida parametrlar obyektini uzatib, xato xabarlarini ham moslashtirishingiz mumkin:

```ts
required(schemaPath.email, {message: 'Email is required'});
email(schemaPath.email, {message: 'Please enter a valid email address'});
```

`FieldTree`'dagi har bir tugun oʻzining validatsiya va oʻzaro aloqa holatini reaktiv signallar orqali ochib beradi.

### FieldTree holat signallari

Daraxtdagi har bir tugun, shu jumladan ildiz forma obyekti ham, holatini kuzatish uchun bir xil signallarni taqdim etadi. Har bir tugun `FieldTree` boʻlgani uchun validlik va oʻzaro aloqani kuzatish API'si har bir darajada bir xil.

| Holat        | Tavsif                                                                                    |
| ------------ | ----------------------------------------------------------------------------------------- |
| `valid()`    | Tugun barcha validatsiya qoidalaridan oʻtsa `true` qaytaradi                              |
| `invalid()`  | Validatsiya xatolari boʻlsa `true` qaytaradi                                              |
| `pending()`  | Asinxron validatsiya davom etayotgan boʻlsa `true` qaytaradi                              |
| `touched()`  | Foydalanuvchi maydonga yoki uning biror ichki maydoniga fokus berib, chiqqan boʻlsa `true` qaytaradi |
| `dirty()`    | Qiymat foydalanuvchi tomonidan oʻzgartirilgan boʻlsa `true` qaytaradi                     |
| `disabled()` | Tugun oʻchirilgan boʻlsa `true` qaytaradi                                                 |
| `readonly()` | Tugun faqat oʻqish uchun boʻlsa `true` qaytaradi                                          |
| `errors()`   | `kind` va `message` xususiyatlariga ega validatsiya xatolari massivini qaytaradi          |

### Toʻliq misol {#complete-example-validation}

<docs-code-multifile preview path="adev/src/content/examples/signal-forms/src/login-validation/app/app.ts">
  <docs-code header="app.ts" path="adev/src/content/examples/signal-forms/src/login-validation/app/app.ts"/>
  <docs-code header="app.html" path="adev/src/content/examples/signal-forms/src/login-validation/app/app.html"/>
  <docs-code header="app.css" path="adev/src/content/examples/signal-forms/src/login-validation/app/app.css"/>
</docs-code-multifile>

## Keyingi qadamlar

Signal Forms va uning qanday ishlashi haqida koʻproq bilish uchun chuqur qoʻllanmalarga qarang:

- [Umumiy koʻrinish](guide/forms/signals/overview) - Signal Forms bilan tanishuv va ulardan qachon foydalanish
- [Forma modellari](guide/forms/signals/models) - Signallar bilan forma maʼlumotlarini yaratish va boshqarish
- [Maydon holatini boshqarish](guide/forms/signals/field-state-management) - Validatsiya holati, oʻzaro aloqani kuzatish va maydon koʻrinishi bilan ishlash
- [Validatsiya](guide/forms/signals/validation) - Oʻrnatilgan validatorlar, maxsus validatsiya qoidalari va asinxron validatsiya

<docs-pill-row>
  <docs-pill title="Bogʻliqliklarni inyeksiya qilish bilan modulli dizayn" href="essentials/dependency-injection" />
</docs-pill-row>
