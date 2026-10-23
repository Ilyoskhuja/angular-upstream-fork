<docs-decorative-header title="Shablonlar" imgSrc="adev/src/assets/images/templates.svg"> <!-- markdownlint-disable-line -->
Dinamik foydalanuvchi interfeyslarini yaratish uchun Angular shablon sintaksisidan foydalaning.
</docs-decorative-header>

Komponent shablonlari shunchaki statik HTML emas — ular komponent klassingizdagi maʼlumotlardan foydalanishi va foydalanuvchi bilan oʻzaro aloqa uchun ishlov beruvchilarni (handlers) sozlashi mumkin.

## Dinamik matnni koʻrsatish {#showing-dynamic-text}

Angular'da _bogʻlash_ (binding) komponent shabloni va uning maʼlumotlari oʻrtasida dinamik aloqa yaratadi. Bu aloqa komponent maʼlumotlaridagi oʻzgarishlar render qilingan shablonni avtomatik yangilashini taʼminlaydi.

Shablonda dinamik matnni koʻrsatish uchun ikkita jingalak qavs yordamida bogʻlash yaratishingiz mumkin:

```angular-ts
@Component({
  selector: 'user-profile',
  template: `<h1>Profile for {{ userName() }}</h1>`,
})
export class UserProfile {
  userName = signal('pro_programmer_123');
}
```

Angular komponentni render qilganda siz quyidagini koʻrasiz:

```html
<h1>Profile for pro_programmer_123</h1>
```

Signal qiymati oʻzgarganda Angular bogʻlashni avtomatik ravishda yangilab turadi. Yuqoridagi misolni davom ettirib, `userName` signalining qiymatini yangilasak:

```typescript
this.userName.set('cool_coder_789');
```

Render qilingan sahifa yangi qiymatni aks ettirish uchun yangilanadi:

```html
<h1>Profile for cool_coder_789</h1>
```

## Dinamik xususiyatlar va atributlarni oʻrnatish {#setting-dynamic-properties-and-attributes}

Angular kvadrat qavslar yordamida dinamik qiymatlarni DOM xususiyatlariga (properties) bogʻlashni qoʻllab-quvvatlaydi:

```angular-ts
@Component({
  /*...*/
  // Set the `disabled` property of the button based on the value of `isValidUserId`.
  template: `<button [disabled]="!isValidUserId()">Save changes</button>`,
})
export class UserProfile {
  isValidUserId = signal(false);
}
```

Atribut nomi oldiga `attr.` prefiksini qoʻyib, HTML _atributlariga_ ham bogʻlashingiz mumkin:

```angular-html
<!-- Bind the `role` attribute on the `<ul>` element to value of `listRole`. -->
<ul [attr.role]="listRole()"></ul>
```

Bogʻlangan qiymat oʻzgarganda Angular DOM xususiyatlari va atributlarini avtomatik yangilaydi.

## Foydalanuvchi harakatlariga ishlov berish {#handling-user-interaction}

Angular shablondagi elementga oddiy qavslar yordamida hodisa tinglovchilarini (event listeners) qoʻshish imkonini beradi:

```angular-ts
@Component({
  /*...*/
  // Add an 'click' event handler that calls the `cancelSubscription` method.
  template: `<button (click)="cancelSubscription()">Cancel subscription</button>`,
})
export class UserProfile {
  /* ... */

  cancelSubscription() {
    /* Your event handling code goes here. */
  }
}
```

Agar tinglovchingizga [hodisa](https://developer.mozilla.org/docs/Web/API/Event) obyektini uzatish kerak boʻlsa, funksiya chaqiruvi ichida Angular'ning oʻrnatilgan `$event` oʻzgaruvchisidan foydalanishingiz mumkin:

```angular-ts
@Component({
  /*...*/
  // Add an 'click' event handler that calls the `cancelSubscription` method.
  template: `<button (click)="cancelSubscription($event)">Cancel subscription</button>`,
})
export class UserProfile {
  /* ... */

  cancelSubscription(event: Event) {
    /* Your event handling code goes here. */
  }
}
```

## `@if` va `@for` bilan boshqaruv oqimi {#control-flow-with-if-and-for}

Angular'ning `@if` bloki yordamida shablon qismlarini shartli ravishda yashirishingiz va koʻrsatishingiz mumkin:

```angular-html
<h1>User profile</h1>

@if (isAdmin()) {
  <h2>Admin settings</h2>
  <!-- ... -->
}
```

`@if` bloki ixtiyoriy `@else` blokini ham qoʻllab-quvvatlaydi:

```angular-html
<h1>User profile</h1>

@if (isAdmin()) {
  <h2>Admin settings</h2>
  <!-- ... -->
} @else {
  <h2>User settings</h2>
  <!-- ... -->
}
```

Angular'ning `@for` bloki yordamida shablonning bir qismini bir necha marta takrorlashingiz mumkin:

```angular-html
<h1>User profile</h1>

<ul class="user-badge-list">
  @for (badge of badges(); track badge.id) {
    <li class="user-badge">{{ badge.name }}</li>
  }
</ul>
```

Angular yuqoridagi misolda koʻrsatilgan `track` kalit soʻzidan maʼlumotlarni `@for` tomonidan yaratilgan DOM elementlari bilan bogʻlash uchun foydalanadi. Qoʻshimcha maʼlumot uchun [_Nima uchun @for bloklarida track muhim?_](guide/templates/control-flow#why-is-track-in-for-blocks-important) boʻlimiga qarang.

TIP: Angular shablonlari haqida koʻproq bilmoqchimisiz? Toʻliq maʼlumot uchun [Shablonlar boʻyicha chuqur qoʻllanmaga](guide/templates) qarang.

## Keyingi qadam {#next-step}

Ilovada dinamik maʼlumotlar va shablonlar bor, endi maʼlum elementlarni shartli yashirish yoki koʻrsatish, elementlar boʻylab takrorlash va boshqa usullar bilan shablonlarni yaxshilashni oʻrganish vaqti keldi.

<docs-pill-row>
  <docs-pill title="Signallar bilan formalar" href="essentials/signal-forms" />
  <docs-pill title="Shablonlar boʻyicha chuqur qoʻllanma" href="guide/templates" />
</docs-pill-row>
