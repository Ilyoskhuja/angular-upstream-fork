<docs-decorative-header title="Oʻrnatish" imgSrc="adev/src/assets/images/what_is_angular.svg"> <!-- markdownlint-disable-line -->
</docs-decorative-header>

Angular bilan onlayn starterlar orqali yoki terminalingizda lokal tarzda tezda boshlang.

## Onlayn sinab koʻring {#play-online}

Agar loyiha sozlamasdan turib Angular'ni brauzeringizda shunchaki sinab koʻrmoqchi boʻlsangiz, onlayn sandbox'imizdan foydalanishingiz mumkin:

<docs-card title="Playground" href="/playground" link="Playground'da ochish" iconImgSrc="adev/src/assets/icons/playground.svg" titleInline>
Angular ilovasi bilan oʻynashning eng tez usuli. Hech qanday sozlash talab qilinmaydi.
</docs-card>

## Yangi loyihani lokal tarzda sozlash {#set-up-a-new-project-locally}

Agar yangi loyiha boshlayotgan boʻlsangiz, Git kabi vositalardan foydalana olish uchun lokal loyiha yaratishni xohlasangiz kerak.

### Talablar {#prerequisites}

- **Node.js** - [v22.22.3 yoki undan yangi](/reference/versions)
- **Matn muharriri** - Biz [Visual Studio Code](https://code.visualstudio.com/)'ni tavsiya qilamiz
- **Terminal** - [Angular CLI](/tools/cli) buyruqlarini bajarish uchun zarur
- **Ishlab chiqish vositasi** - Ish jarayoningizni yaxshilash uchun [Angular Language Service](/tools/language-service)'ni tavsiya qilamiz

### Koʻrsatmalar {#instructions}

Quyidagi qoʻllanma lokal Angular loyihasini sozlash boʻyicha sizga yoʻl koʻrsatadi.

#### Angular CLI'ni oʻrnating {#install-angular-cli}

Terminalni oching (agar [Visual Studio Code](https://code.visualstudio.com/)'dan foydalanayotgan boʻlsangiz, [oʻrnatilgan terminalni](https://code.visualstudio.com/docs/editor/integrated-terminal) ochishingiz mumkin) va quyidagi buyruqni bajaring:

<docs-code-multifile>
  <docs-code
    header="npm"
    language="shell"
    >
    npm install -g @angular/cli
    </docs-code>
  <docs-code
    header="pnpm"
    language="shell"
    >
    pnpm install -g @angular/cli
    </docs-code>
  <docs-code
    header="yarn"
    language="shell"
    >
    yarn global add @angular/cli
    </docs-code>
  <docs-code
    header="bun"
    language="shell"
    >
    bun install -g @angular/cli
    </docs-code>
</docs-code-multifile>

Agar bu buyruqni Windows yoki Unix'da bajarishda muammolarga duch kelsangiz, qoʻshimcha maʼlumot uchun [CLI hujjatlariga](/tools/cli/setup-local#install-the-angular-cli) qarang.

#### Yangi loyiha yarating {#create-a-new-project}

Terminalingizda [`ng new`](cli/new) CLI buyrugʻini kerakli loyiha nomi bilan bajaring. Quyidagi misollarda biz `my-first-angular-app` nomli namunaviy loyihadan foydalanamiz.

```shell
ng new <project-name>
```

Sizga loyihangiz uchun bir nechta konfiguratsiya variantlari taklif qilinadi. Kerakli variantlarni tanlash uchun strelka va enter tugmalaridan foydalaning.

Agar maxsus talablaringiz boʻlmasa, sukut boʻyicha variantlarni qabul qilish va sozlashni davom ettirish uchun shunchaki enter tugmasini bosing.

Konfiguratsiya variantlarini tanlaganingizdan va CLI sozlashni yakunlaganidan soʻng quyidagi xabarni koʻrishingiz kerak:

```text
✔ Packages installed successfully.
    Successfully initialized git.
```

Endi loyihangizni lokal tarzda ishga tushirishga tayyorsiz!

#### Yangi loyihangizni lokal tarzda ishga tushirish {#running-your-new-project-locally}

Terminalingizda yangi Angular loyihangiz papkasiga oʻting.

```shell
cd my-first-angular-app
```

Bu bosqichda barcha bogʻliqliklaringiz oʻrnatilgan boʻlishi kerak (buni loyihangizda `node_modules` papkasi mavjudligini tekshirish orqali bilib olishingiz mumkin), shuning uchun loyihangizni quyidagi buyruq bilan ishga tushirishingiz mumkin:

```shell
npm start
```

Agar hammasi muvaffaqiyatli boʻlsa, terminalingizda shunga oʻxshash tasdiq xabarini koʻrishingiz kerak:

```text
Watch mode enabled. Watching for file changes...
NOTE: Raw file sizes do not reflect development server per-request transformations.
  ➜  Local:   http://localhost:4200/
  ➜  press h + enter to show help
```

Endi ilovangizni koʻrish uchun `Local` qatoridagi manzilga (masalan, `http://localhost:4200`) kirishingiz mumkin. Omadli kodlash! 🎉

### Ishlab chiqishda AI'dan foydalanish {#using-ai-for-development}

Oʻzingiz yoqtirgan AI bilan jihozlangan IDE'da qurishni boshlash uchun [Angular prompt qoidalari va eng yaxshi amaliyotlari bilan tanishing](/ai/develop-with-ai).

## Keyingi qadamlar {#next-steps}

Angular loyihangizni yaratganingizdan soʻng, [Asoslar qoʻllanmasida](/essentials) Angular haqida koʻproq bilib olishingiz yoki chuqur qoʻllanmalarimizdan biror mavzuni tanlashingiz mumkin!
