<docs-decorative-header title="Signallar" imgSrc="adev/src/assets/images/signals.svg"> <!-- markdownlint-disable-line -->
Dinamik maʼlumotlarni yarating va boshqaring.
</docs-decorative-header>

Angular'da holatni (state) yaratish va boshqarish uchun _signallardan_ foydalanasiz. Signal — qiymat atrofidagi yengil oʻram.

Lokal holatni saqlash uchun signal yaratishda `signal` funksiyasidan foydalaning:

```typescript
import {signal} from '@angular/core';

// Create a signal with the `signal` function.
const firstName = signal('Morgan');

// Read a signal value by calling it— signals are functions.
console.log(firstName());

// Change the value of this signal by calling its `set` method with a new value.
firstName.set('Jaime');

// You can also use the `update` method to change the value
// based on the previous value.
firstName.update((name) => name.toUpperCase());
```

Angular signallar qayerda oʻqilishini va qachon yangilanishini kuzatib boradi. Freymvork bu maʼlumotdan DOM'ni yangi holat bilan yangilash kabi qoʻshimcha ishlarni bajarish uchun foydalanadi. Vaqt oʻtishi bilan oʻzgaruvchi signal qiymatlariga javob berish qobiliyati _reaktivlik_ deb ataladi.

## Hisoblangan ifodalar (computed)

`computed` — qiymatini boshqa signallar asosida hosil qiluvchi signal.

```typescript
import {signal, computed} from '@angular/core';

const firstName = signal('Morgan');
const firstNameCapitalized = computed(() => firstName().toUpperCase());

console.log(firstNameCapitalized()); // MORGAN
```

`computed` signali faqat oʻqish uchun; unda `set` yoki `update` metodlari yoʻq. Buning oʻrniga, `computed` signalining qiymati u oʻqiyotgan signallardan birortasi oʻzgarganda avtomatik ravishda oʻzgaradi:

```typescript
import {signal, computed} from '@angular/core';

const firstName = signal('Morgan');
const firstNameCapitalized = computed(() => firstName().toUpperCase());
console.log(firstNameCapitalized()); // MORGAN

firstName.set('Jaime');
console.log(firstNameCapitalized()); // JAIME
```

## Komponentlarda signallardan foydalanish

Holatni yaratish va boshqarish uchun komponentlaringiz ichida `signal` va `computed`'dan foydalaning:

```ts
@Component({
  /* ... */
})
export class UserProfile {
  isTrial = signal(false);
  isTrialExpired = signal(false);
  showTrialDuration = computed(() => this.isTrial() && !this.isTrialExpired());

  activateTrial() {
    this.isTrial.set(true);
  }
}
```

TIP: Angular signallari haqida koʻproq bilmoqchimisiz? Toʻliq maʼlumot uchun [Signallar boʻyicha chuqur qoʻllanmaga](guide/signals) qarang.

## Keyingi qadam

Dinamik maʼlumotlarni eʼlon qilish va boshqarishni oʻrganib oldingiz, endi bu maʼlumotlardan shablonlar ichida qanday foydalanishni oʻrganish vaqti keldi.

<docs-pill-row>
  <docs-pill title="Shablonlar bilan dinamik interfeyslar" href="essentials/templates" />
  <docs-pill title="Signallar boʻyicha chuqur qoʻllanma" href="guide/signals" />
</docs-pill-row>
