<docs-decorative-header title="Bogʻliqliklarni inyeksiya qilish" imgSrc="adev/src/assets/images/dependency_injection.svg"> <!-- markdownlint-disable-line -->
Kodni qayta ishlating va ilovangiz hamda testlaringiz boʻylab xatti-harakatlarni boshqaring.
</docs-decorative-header>

Komponentlar oʻrtasida mantiqni ulashish kerak boʻlganda, Angular [bogʻliqliklarni inyeksiya qilish (dependency injection)](guide/di) dizayn namunasidan foydalanadi. U sizga "servis" yaratish imkonini beradi — servis kodni komponentlarga inyeksiya qilish va uni yagona haqiqat manbasidan boshqarish imkonini beradi.

## Servislar nima?

Servislar — inyeksiya qilinishi mumkin boʻlgan qayta ishlatiladigan kod boʻlaklari.

Komponentni aniqlashga oʻxshab, servislar quyidagilardan iborat:

- Klassni `@Service` orqali Angular servisi sifatida eʼlon qiluvchi va ilovangizning istalgan joyidan foydalanish mumkin boʻlgan servisni aniqlash imkonini beruvchi **TypeScript dekoratori**.
- Servis inyeksiya qilinganda foydalanish mumkin boʻlgan kerakli kodni aniqlovchi **TypeScript klassi**

Quyida `Calculator` servisiga misol keltirilgan.

```angular-ts
import {Service} from '@angular/core';

@Service()
export class Calculator {
  add(x: number, y: number) {
    return x + y;
  }
}
```

## Servisdan qanday foydalanish

Komponentda servisdan foydalanmoqchi boʻlsangiz, quyidagilarni bajarishingiz kerak:

1. Servisni import qiling
2. Servis inyeksiya qilinadigan klass maydonini eʼlon qiling. Klass maydoniga servisni yaratuvchi oʻrnatilgan [`inject`](/api/core/inject) funksiyasini chaqirish natijasini tayinlang

`Receipt` komponentida bu quyidagicha koʻrinishi mumkin:

```angular-ts
import {Component, inject} from '@angular/core';
import {Calculator} from './calculator';

@Component({
  selector: 'app-receipt',
  template: `<h1>The total is {{ totalCost }}</h1>`,
})
export class Receipt {
  private calculator = inject(Calculator);
  totalCost = this.calculator.add(50, 25);
}
```

Bu misolda `Calculator` Angular'ning [`inject`](/api/core/inject) funksiyasini chaqirish va unga servisni uzatish orqali ishlatilmoqda.

## Keyingi qadam

<docs-pill-row>
  <docs-pill title="Asoslardan keyingi qadamlar" href="essentials/next-steps" />
  <docs-pill title="Bogʻliqliklarni inyeksiya qilish boʻyicha chuqur qoʻllanma" href="guide/di" />
</docs-pill-row>
