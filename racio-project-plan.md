# 🚀 RACIO.UA — Повний план проєкту на 15 днів
> Next.js 14 + TypeScript + Tailwind + Sanity CMS + Vercel  
> Команда: Розробник (DEV) · Дизайнер (DS) · PM  
> Бюджет: 100 000 ₴ · Термін: 3 тижні (15 робочих днів)

---

## ЛЕГЕНДА
- 🔴 MUST — критично, без цього не рухатись далі
- 🟡 ВАЖЛИВО — виконати в цей день
- 🟢 БОНУС — якщо залишився час
- 💬 ПРОМПТ — вставляти у Cursor або Claude
- 🐙 GIT — команди для термінала
- ✅ ЧЕКПОІНТ — що перевірити в кінці дня

---

# ═══════════════════════════════════
# ТИЖДЕНЬ 1 — ФУНДАМЕНТ
# ═══════════════════════════════════

---

## ДЕНЬ 1 — Налаштування проєкту

### 📋 PM — День 1

#### Ранок (9:00–11:00)
**🔴 Налаштування GitHub**
1. Зайди на github.com → New organization → назви `racio-agency`
2. New repository → `racio-site` → Private → Initialize with README
3. Settings → Branches → Add rule:
   - Branch name pattern: `main`
   - ✅ Require pull request before merging
   - ✅ Require approvals: 1
   - ✅ Dismiss stale pull request approvals
4. Запроси розробника і дизайнера: Settings → Members → Invite

**🐙 GIT — Створи гілку dev**
```bash
git clone https://github.com/racio-agency/racio-site.git
cd racio-site
git checkout -b dev
git push origin dev
```

**🔴 Налаштування Vercel**
1. vercel.com → New Project → Import `racio-site`
2. Framework: Next.js
3. Production Branch: `main`
4. Збережи — Vercel автоматично зробить preview для кожної гілки

#### День (11:00–14:00)
**🔴 Збір URL зі старого сайту racio.ua**

Спосіб 1 — через WordPress адмінку:
1. Зайди в wp-admin → Plugins → Add New → встанови "Export All URLs"
2. Tools → Export All URLs → Download CSV

Спосіб 2 — онлайн безкоштовно:
1. Зайди на screaming-frog.co.uk/seo-spider → Download (безкоштовно до 500 URL)
2. Enter URL: racio.ua → Start
3. Export → All → CSV

**🔴 Таблиця 301-редіректів у Google Sheets**

Створи таблицю з колонками:
| Старий URL | Новий URL | Тип | Статус | Примітка |
|-----------|-----------|-----|--------|---------|
| /ru/uslugi/buhgalterskij-uchet | /poslugy/buhgalterskiy-oblik | 301 | TODO | |
| /ru/blog | /blog | 301 | TODO | |
| /ru/o-nas | /pro-nas | 301 | TODO | |
| /ru/kontakty | /kontakty | 301 | TODO | |
| /?p=123 | /blog/slug | 301 | TODO | WordPress ID |

#### Обід (14:00–15:00)

#### День (15:00–17:00)
**🔴 Уточнення у клієнта**

💬 ПРОМПТ (Claude.ai):
```
Я PM на проєкті розробки корпоративного сайту racio.ua.
Замінюємо WordPress на Next.js + Sanity CMS.

Склади фінальний список питань до клієнта які мені потрібно
уточнити СЬОГОДНІ перед стартом розробки. Категорії:
1. Технічні (форма, домен, хостинг)
2. Контентні (хто редагує, які матеріали є)
3. Бізнесові (дедлайн, пріоритети сторінок)
4. SEO (чи є поточні позиції які треба зберегти)

Для кожного питання напиши чому воно критичне для команди.
Формат: питання + чому важливо + що буде якщо не уточнити.
```

**🔴 Перший меседж клієнту**

💬 ПРОМПТ (Claude.ai):
```
Напиши офіційний email клієнту — компанії Racio (racio.ua).
Контекст: сьогодні перший день роботи над їх новим сайтом.
Замінюємо WordPress на Next.js + Sanity CMS.
Команда: розробник, дизайнер, я (PM). Термін: 3 тижні.
50% передоплата отримана.

Email має містити:
- Підтвердження старту
- Короткий план по тижнях
- Список питань які потрібно уточнити (куди слати заявки
  з форми, хто редагуватиме контент, чи є жорсткий дедлайн)
- Формат звітності (раз на 2-3 дні коротке оновлення)
- Посилання на GitHub репо (вставлю сам)

Тон: професійний але живий, не корпоративний шаблон.
```

✅ **ЧЕКПОІНТ PM День 1:**
- [ ] GitHub репо створено, команда запрошена
- [ ] Gілка dev створена і запушена
- [ ] Vercel підключено до репо
- [ ] Список URL зі старого сайту готовий (мінімум 20 URL)
- [ ] Таблиця редіректів створена в Google Sheets
- [ ] Email клієнту відправлено

---

### 👨‍💻 DEV — День 1

#### Ранок (9:00–12:00)
**🔴 Крок 1 — Клонуй репо і створи проєкт**

```bash
git clone https://github.com/racio-agency/racio-site.git
cd racio-site
git checkout dev
git checkout -b feat/project-init
```

💬 ПРОМПТ 1 (Cursor IDE — Ctrl+L):
```
Ти Senior Next.js розробник. Я починаю проєкт корпоративного
сайту racio.ua. Мені потрібно налаштувати проєкт з нуля.

СТЕК: Next.js 14 App Router, TypeScript (strict), Tailwind CSS,
Sanity CMS, Vercel deploy.

ВИМОГИ: Lighthouse ≥ 90, LCP < 2.5s, CLS < 0.1,
адаптив 375/768/1280px, SEO-оптимізація.

ЗАВДАННЯ — згенеруй команди для термінала:

1. Ініціалізація Next.js 14:
npx create-next-app@latest . --typescript --tailwind --eslint
--app --src-dir --import-alias "@/*"

2. Встановити залежності:
npm install @sanity/client next-sanity @portabletext/react
@sanity/image-url react-hook-form @hookform/resolvers zod
resend framer-motion @radix-ui/react-accordion

3. Створи структуру папок у src/:
app/ components/ui/ components/sections/ components/layout/
lib/ types/ styles/

4. Створи .env.local з змінними:
NEXT_PUBLIC_SANITY_PROJECT_ID=
NEXT_PUBLIC_SANITY_DATASET=production
SANITY_API_TOKEN=
RESEND_API_KEY=
NEXT_PUBLIC_GA_ID=
NEXT_PUBLIC_GTM_ID=

5. Налаштуй tsconfig.json на strict mode

Виведи всі команди. Після кожного блоку поясни що зробили.
```

**🔴 Крок 2 — Ініціалізація Sanity**

```bash
npm create sanity@latest -- --project racio-cms --dataset production --template clean
```

💬 ПРОМПТ 2 (Cursor):
```
Налаштуй Sanity CMS для проєкту racio.ua.

Створи файл sanity.config.ts у корені проєкту:
- Studio route: /studio
- Project ID з env NEXT_PUBLIC_SANITY_PROJECT_ID
- Dataset: production
- Підключи всі схеми

Створи папку sanity/schemas/ і такі файли:

1. article.ts — поля: title (string, required), slug (slug,
source: title, required), category (string, options: ['новини',
'поради', 'кейси']), author (reference до teamMember),
mainImage (image з полем alt), body (array block — rich text),
publishedAt (datetime), seo (object: metaTitle, metaDescription,
ogImage)

2. service.ts — поля: title, slug, shortDescription (text, max
200 символів), fullDescription (text), checklist (array of
strings — що входить), process (array of objects: stepNumber
number, title string, description text), faq (array of objects:
question string, answer text), illustration (image з alt),
seo (як у article)

3. teamMember.ts — поля: name (required), position (required),
photo (image з alt), bio (text), order (number — для сортування)

4. review.ts — поля: clientName (required), company, text
(required, text), rating (number, min 1 max 5), isVisible
(boolean, default true)

5. settings.ts — тип: 'settings', singleton. Поля: phone,
email, address, socials (object: facebook, instagram, linkedin,
telegram), statistics (array of objects: label string,
value string — наприклад '500+ клієнтів')

6. index.ts — експортує всі схеми як масив

Всі поля мають бути з українськими title для редактора CMS.
TypeScript з повними типами. Validation де потрібно.
```

#### Обід (12:00–13:00)

#### День (13:00–17:00)

💬 ПРОМПТ 3 (Cursor):
```
Створи файли для роботи з Sanity API у Next.js 14 App Router.

ФАЙЛ 1: src/lib/sanityClient.ts
- Публічний клієнт (useCdn: true) для читання
- Серверний клієнт з токеном (без CDN) для preview
- Функція urlFor(source) через @sanity/image-url
- Правильні TypeScript типи

ФАЙЛ 2: src/lib/queries.ts
Async функції з GROQ запитами:
- getAllServices(): повертає Service[] (title, slug, shortDescription, illustration)
- getServiceBySlug(slug: string): повна Service
- getAllArticles(): Article[] (title, slug, category, mainImage, publishedAt, author name)
- getArticleBySlug(slug: string): повна Article з body
- getTeamMembers(): TeamMember[] відсортовані по order asc
- getVisibleReviews(): Review[] де isVisible == true
- getSiteSettings(): Settings singleton

Кожна функція має cache() з React для дедуплікації.
Обробка помилок через try/catch.

ФАЙЛ 3: src/types/index.ts
TypeScript інтерфейси для всіх типів:
Article, Service, ServiceProcess, ServiceFAQ, TeamMember,
Review, Settings, SiteStatistic, Slug, SanityImage, SEOMeta

ФАЙЛ 4: src/lib/utils.ts
- formatDate(date: string): string — форматує дату українською
- generateSlug(text: string): string
- truncateText(text: string, maxLength: number): string
```

**🐙 GIT — кінець дня**
```bash
git add .
git commit -m "feat: initial project setup, sanity schemas, types and queries"
git push origin feat/project-init
```
Потім відкрий Pull Request на GitHub: feat/project-init → dev

✅ **ЧЕКПОІНТ DEV День 1:**
- [ ] Next.js запускається на localhost:3000
- [ ] Sanity Studio відкривається на localhost:3000/studio
- [ ] Всі 5 схем створені і видно у Studio
- [ ] sanityClient.ts підключається без помилок
- [ ] queries.ts написані і типізовані
- [ ] PR відкритий у GitHub
- [ ] .env.local заповнений (взяв projectId з sanity.io)

---

### 🎨 DS — День 1

#### Ранок (9:00–11:00)
**🔴 Клонуй репо**
```bash
git clone https://github.com/racio-agency/racio-site.git
cd racio-site
git checkout dev
git pull origin dev
```
Попроси розробника скинути .env.local значення в особисте повідомлення.

**🔴 Аудит Figma**

💬 ПРОМПТ (Claude.ai):
```
Я дизайнер. Верстаю корпоративний сайт racio.ua на
Next.js 14 + Tailwind CSS. Є Figma-макет.

Дай мені чекліст аудиту Figma який я маю пройти СЬОГОДНІ
перед тим як почати верстати. Що конкретно перевірити:

1. Кольори — що зафіксувати
2. Типографіка — які параметри записати для кожного брейкпоінту
3. Spacing — як визначити систему відступів
4. Компоненти — які виокремити щоб не переробляти пізніше
5. Адаптив — як перевірити наявність всіх трьох версій (375/768/1280)
6. Зображення — на що звернути увагу для Lighthouse ≥ 90

Результат: таблиця токенів яку я заповню і передам розробнику
для tailwind.config.ts
```

#### День (11:00–17:00)
**🔴 Заповни таблицю токенів з Figma:**

| Токен | Значення |
|-------|---------|
| color-primary | # |
| color-secondary | # |
| color-accent | # |
| color-text-primary | # |
| color-text-secondary | # |
| color-background | # |
| color-background-card | # |
| color-border | # |
| font-family | |
| font-size-h1-desktop | px |
| font-size-h1-mobile | px |
| font-size-body | px |
| border-radius-card | px |
| border-radius-button | px |
| section-padding-desktop | px |
| section-padding-mobile | px |

**🔴 Після заповнення — передай розробнику і запусти промпт:**

💬 ПРОМПТ (Cursor):
```
Заповни tailwind.config.ts моїми токенами з Figma:

color-primary: #______
color-secondary: #______
color-accent: #______
color-text-primary: #______
color-text-secondary: #______
color-background: #______
color-card: #______
color-border: #______
font-family: ______
border-radius-card: ______px
border-radius-button: ______px

Згенеруй:
1. Повний tailwind.config.ts з extend: { colors, fontFamily,
   borderRadius, screens: {sm:'375px', md:'768px', lg:'1280px'},
   fontSize з h1-h4 і body варіантами }

2. src/styles/globals.css з:
   - @tailwind base/components/utilities
   - CSS змінні для всіх кольорів
   - Базові стилі body, h1-h6, a, p
   - Клас .container: max-w-[1280px] mx-auto px-4 md:px-8

3. Компонент src/components/ui/Button.tsx:
   Props: variant (primary|secondary|outline), size (sm|md|lg),
   children, href?, onClick?, disabled?
   - Якщо href — рендерить як next/link
   - Hover, focus, disabled стани
   - TypeScript з повними типами
```

**🐙 GIT — кінець дня**
```bash
git checkout -b feat/design-tokens-setup
git add .
git commit -m "design: add tailwind config tokens and globals css"
git push origin feat/design-tokens-setup
```
Відкрий PR: feat/design-tokens-setup → dev

✅ **ЧЕКПОІНТ DS День 1:**
- [ ] Репо клонований, запускається локально
- [ ] Всі токени виписані з Figma
- [ ] tailwind.config.ts готовий
- [ ] globals.css готовий
- [ ] Button компонент створений
- [ ] PR відкритий

---

## ДЕНЬ 2 — Layout + UI компоненти

### 📋 PM — День 2

**🟡 Ранок (9:00–10:00)**
- Перевір PR від розробника і дизайнера
- Якщо все ок — апруй і злий в dev
- Напиши в чат команди що в dev є оновлення, треба зробити git pull

**🟡 День (10:00–17:00) — Контент зі старого сайту**

💬 ПРОМПТ (Claude.ai):
```
Я PM. Мені потрібно скопіювати контент зі старого сайту
racio.ua (WordPress) для нового сайту на Sanity CMS.

Допоможи організувати процес:

1. Для кожного типу контенту (Послуги, Статті блогу,
   Команда, Відгуки) — що конкретно копіювати і в якому
   форматі зберігати в Google Docs.

2. Пріоритет копіювання — що потрібно першим щоб розробник
   міг тестувати CMS вже на 3-4 день.

3. Структура Google Doc для кожного типу контенту щоб
   потім зручно вносити в Sanity Studio.

4. Які зображення треба зберегти і де їх взяти зі старого сайту.
```

Заповнюй Google Docs по кожному типу контенту:
- `racio-content-services.doc` — всі послуги
- `racio-content-articles.doc` — статті блогу
- `racio-content-team.doc` — члени команди з фото
- `racio-content-reviews.doc` — відгуки клієнтів

✅ **ЧЕКПОІНТ PM День 2:**
- [ ] PR від дня 1 заапрувані і злиті в dev
- [ ] Контент послуг скопійований (мінімум 3 послуги)
- [ ] Контент команди скопійований
- [ ] Відповідь від клієнта на email з питаннями

---

### 👨‍💻 DEV — День 2

**🔴 Ранок — синк з dev**
```bash
git checkout dev
git pull origin dev
git checkout -b feat/layout-and-client
```

💬 ПРОМПТ 1 (Cursor):
```
Створи RootLayout для проєкту racio.ua на Next.js 14 App Router.

ФАЙЛ: src/app/layout.tsx
- Шрифт Inter з next/font/google, subsets: ['latin', 'cyrillic']
- Metadata об'єкт:
  metadataBase: new URL('https://racio.ua')
  title: { template: '%s | Racio', default: 'Racio — Бухгалтерські послуги' }
  description: 'Racio — професійна бухгалтерія для бізнесу'
  openGraph: { type: 'website', locale: 'uk_UA', siteName: 'Racio' }
- Рендерить <Header /> та <Footer /> навколо {children}
- Підключає globals.css

ФАЙЛ: src/components/layout/Header.tsx (серверний компонент)
- Тягне getSiteSettings() для телефону
- Лого зліва (текст "Racio" + іконка placeholder)
- Навігація: Послуги (/poslugy), Блог (/blog),
  Про нас (/pro-nas), Пакети (/pakety), Контакти (/kontakty)
- Кнопка "Зв'язатись" → /kontakty (використай Button компонент)
- Мобільне меню: окремий клієнтський компонент MobileMenu.tsx
  з useState для open/close, анімація slide-down

ФАЙЛ: src/components/layout/Footer.tsx (серверний компонент)
- Тягне getSiteSettings()
- Лого і короткий опис компанії
- Навігаційні лінки (ті самі що в Header)
- Контакти: телефон, email, адреса
- Соціальні мережі з іконками (SVG inline)
- Copyright рядок з поточним роком

ФАЙЛ: next.config.js
- images.domains: ['cdn.sanity.io']
- redirects: async () => [] (заповнимо пізніше)
- Усі TypeScript помилки мають бути виправлені
```

💬 ПРОМПТ 2 (Cursor):
```
Створи src/app/page.tsx — головна сторінка racio.ua.

Це серверний компонент який:
1. Тягне дані через: getVisibleReviews(), getAllServices(),
   getSiteSettings() паралельно через Promise.all
2. Має metadata export з OG тегами

Структура сторінки — заглушки для секцій (заповнимо пізніше):
- <HeroSection /> — приймає settings пропс
- <ServicesPreview services={services} /> — 3-4 послуги
- <StatsSection stats={settings.statistics} />
- <ReviewsSection reviews={reviews} />
- <CTASection /> — заклик до дії з формою

Для кожної секції створи окремий файл у src/components/sections/
з мінімальною реалізацією (буде доповнюватись дизайнером).
Всі компоненти TypeScript з правильними пропсами.
```

**🐙 GIT — кінець дня**
```bash
git add .
git commit -m "feat: add root layout, header, footer, and homepage structure"
git push origin feat/layout-and-client
```
PR: feat/layout-and-client → dev

✅ **ЧЕКПОІНТ DEV День 2:**
- [ ] Layout рендериться без помилок
- [ ] Header з навігацією і мобільним меню
- [ ] Footer з контактами
- [ ] Головна сторінка з секціями-заглушками
- [ ] Дані з Sanity підтягуються (перевір в Studio — додай тестовий відгук)

---

### 🎨 DS — День 2

**🔴 Синк**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/design-ui-components
```

💬 ПРОМПТ (Cursor):
```
Створи всі базові UI компоненти для сайту racio.ua.
Tailwind CSS, TypeScript, Next.js 14, mobile-first адаптив.

КОМПОНЕНТ: src/components/ui/ServiceCard.tsx
Props: title: string, slug: string, shortDescription: string,
illustration?: SanityImage
- Картка з зображенням (next/image + urlFor)
- Заголовок, короткий опис (макс 2 рядки)
- Кнопка "Детальніше" → /poslugy/{slug}
- Hover: підняття картки (translateY -4px, shadow)
- Адаптив: mobile — повна ширина, tablet — 2 колонки,
  desktop — 3 колонки (через батьківський грід)

КОМПОНЕНТ: src/components/ui/BlogCard.tsx
Props: title, slug, category, mainImage: SanityImage,
publishedAt: string, author: { name: string }
- Зображення 16:9 зверху
- Бейдж категорії (кольоровий)
- Дата (форматована)
- Заголовок (2 рядки макс)
- Ім'я автора
- Вся картка клікабельна → /blog/{slug}

КОМПОНЕНТ: src/components/ui/ReviewCard.tsx
Props: clientName, company?: string, text, rating: number
- Зірки рейтингу (заповнені/незаповнені SVG)
- Текст відгуку (4 рядки макс з truncate)
- Ім'я і компанія внизу

КОМПОНЕНТ: src/components/ui/TeamCard.tsx
Props: name, position, photo: SanityImage, bio?: string
- Квадратне фото (next/image, aspect-square)
- Ім'я жирним
- Посада кольором secondary

КОМПОНЕНТ: src/components/ui/SectionHeader.tsx
Props: title: string, subtitle?: string, centered?: boolean
- Використовується на кожній секції
- H2 заголовок + підзаголовок
- centered проп для вирівнювання по центру

Всі компоненти: TypeScript, next/image для фото,
aria-label для доступності.
```

**🐙 GIT — кінець дня**
```bash
git add .
git commit -m "design: add ServiceCard, BlogCard, ReviewCard, TeamCard, SectionHeader components"
git push origin feat/design-ui-components
```

✅ **ЧЕКПОІНТ DS День 2:**
- [ ] Всі 5 компонентів створені
- [ ] Перевірені на localhost на 375px
- [ ] Hover стани працюють
- [ ] PR відкритий

---

## ДЕНЬ 3–4 — Головна сторінка

### 👨‍💻 DEV — Дні 3–4

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/homepage-logic
```

💬 ПРОМПТ (Cursor):
```
Допрацюй головну сторінку racio.ua.

src/app/page.tsx вже має заглушки секцій.
Мені потрібно підключити реальні компоненти і дані.

1. HeroSection (src/components/sections/HeroSection.tsx)
   Props: phone: string, stats: SiteStatistic[]
   - Великий заголовок з акцентом
   - Підзаголовок про послуги
   - Дві кнопки: "Отримати консультацію" і "Наші послуги"
   - Статистика з settings.statistics (підтягується з Sanity)
   - next/image для hero зображення

2. ServicesPreview (src/components/sections/ServicesPreview.tsx)
   Props: services: Service[]
   - SectionHeader з заголовком
   - Грід ServiceCard (3 колонки на desktop)
   - Кнопка "Всі послуги" → /poslugy

3. ReviewsSection (src/components/sections/ReviewsSection.tsx)
   Props: reviews: Review[]
   - Горизонтальний скролл або слайдер (простий — без
     зовнішніх бібліотек, через overflow-x-auto)
   - ReviewCard для кожного відгуку

4. CTASection (src/components/sections/CTASection.tsx)
   - Блок із закликом: "Залиштіть заявку"
   - Проста форма: ім'я + телефон + кнопка
   - Form action вказує на /api/contact (зробимо пізніше)

Всі секції — серверні компоненти крім CTASection
(там буде useState для форми).
```

💬 ПРОМПТ — Metadata і SEO (Cursor):
```
Додай повноцінний SEO для головної сторінки racio.ua.

src/app/page.tsx:
1. Розширений metadata export:
   - title, description
   - keywords
   - openGraph: title, description, images (og image URL),
     type: 'website', locale: 'uk_UA'
   - twitter: card, title, description, images
   - robots: { index: true, follow: true }
   - alternates: { canonical: 'https://racio.ua' }

2. JSON-LD компонент src/components/seo/JsonLd.tsx:
   Props: data: Record<string, unknown>
   Рендерить <script type="application/ld+json">

3. Organization JSON-LD для головної:
   @type: Organization, name: Racio,
   url, logo, contactPoint (phone, email),
   sameAs (масив соцмереж з settings)

4. app/robots.ts — генерує robots.txt:
   User-agent: *, Allow: /,
   Disallow: /studio/,
   Sitemap: https://racio.ua/sitemap.xml
```

**🐙 GIT**
```bash
git add .
git commit -m "feat: homepage sections with sanity data, seo metadata, json-ld"
git push origin feat/homepage-logic
```

✅ **ЧЕКПОІНТ DEV Дні 3–4:**
- [ ] Головна відображає дані з Sanity
- [ ] Hero з кнопками
- [ ] Секція послуг (додай 2-3 тестові у Studio)
- [ ] Секція відгуків
- [ ] JSON-LD в source коді сторінки
- [ ] robots.txt відкривається

---

### 🎨 DS — Дні 3–4

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/design-homepage
```

💬 ПРОМПТ (Cursor):
```
Зверстай Hero секцію для сайту racio.ua точно по Figma макету.

Компонент: src/components/sections/HeroSection.tsx
Отримує пропси: phone: string, stats: SiteStatistic[]

ВИМОГИ:
- Mobile-first: 375px → 768px → 1280px
- next/image для hero зображення з:
  priority={true} (LCP зображення — важливо для Lighthouse)
  sizes="(max-width: 768px) 100vw, 50vw"
  placeholder="blur"
- Анімація появи через framer-motion:
  import { motion } from 'framer-motion'
  const fadeUp = { initial:{opacity:0,y:24}, animate:{opacity:1,y:0}, transition:{duration:0.5} }
  Кожен елемент — окрема motion.div з затримкою (delay: 0, 0.1, 0.2)
- CLS = 0 — всі зображення з фіксованими розмірами
- Статистика виводиться динамічно з пропсу stats[]

Після Hero секції зверстай AnmationWrapper компонент:
src/components/ui/AnimationWrapper.tsx
- Обгортка для будь-якого блоку
- Анімація fadeInUp при появі у viewport
- whileInView, viewport: {once: true} — анімується тільки раз
- Використовується у кожній секції сторінки
```

💬 ПРОМПТ — Анімації (Cursor):
```
Додай анімації при скролі до секцій головної сторінки racio.ua.

Використовуй AnimationWrapper компонент.
Обгорни ним кожну секцію і кожну картку.

ВАЖЛИВО для Lighthouse CLS < 0.1:
1. Ніколи не анімуй width або height — тільки opacity і transform
2. Всі motion.div мають мати визначені розміри або min-height
3. Картки в гріді — однакова висота через grid-rows: auto

Перевір що:
- Жодне зображення не зсуває сусідні елементи при завантаженні
- Кожне зображення має явний width і height або aspect-ratio
- Шрифти підключені через next/font (вже є в layout)
```

**🐙 GIT**
```bash
git add .
git commit -m "design: homepage hero section, animations, all breakpoints"
git push origin feat/design-homepage
```

✅ **ЧЕКПОІНТ DS Дні 3–4:**
- [ ] Hero виглядає як у Figma на 375/768/1280px
- [ ] Анімації при скролі працюють
- [ ] Немає горизонтального скролу на мобільному
- [ ] Lighthouse CLS < 0.1 (перевір в Chrome DevTools)

---

## ДЕНЬ 5 — Синк команди + перший preview клієнту

### 📋 PM — День 5

**🔴 Вранці — злити все в dev і відправити клієнту**

1. Перевір всі відкриті PR → апруй → злий в dev
2. Vercel автоматично задеплоїть dev preview URL
3. Перевір preview на телефоні і на desktop

💬 ПРОМПТ — Оновлення клієнту (Claude.ai):
```
Напиши коротке оновлення клієнту Racio після першого тижня
роботи. Тон: впевнений, конкретний, без зайвих слів.

Що зроблено:
- Налаштований проєкт (Next.js + Sanity CMS)
- Головна сторінка з анімаціями
- Всі базові компоненти
- CMS готова — можна вже додавати контент

Що потрібно від клієнта:
- Підтвердити напрямок по preview URL (вставлю сам)
- Фінальні тексти для Hero секції
- Фото команди у форматі JPG/PNG (мінімум 800x800px)

Що буде наступного тижня:
- Всі внутрішні сторінки
- Блог, послуги, команда
- Форма зворотного зв'язку

Формат: Telegram повідомлення, коротко, з emoji.
```

---

# ═══════════════════════════════════
# ТИЖДЕНЬ 2 — ВНУТРІШНІ СТОРІНКИ
# ═══════════════════════════════════

---

## ДЕНЬ 6–7 — Сторінки послуг і блогу

### 👨‍💻 DEV — Дні 6–7

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/services-and-blog-pages
```

💬 ПРОМПТ 1 (Cursor):
```
Створи сторінки послуг для racio.ua на Next.js 14 App Router.

ФАЙЛ 1: src/app/poslugy/page.tsx — список послуг
- Серверний компонент
- Тягне getAllServices()
- metadata: title 'Послуги | Racio', опис, OG теги
- BreadcrumbList JSON-LD: Головна > Послуги
- Рендерить ServiceCard для кожної послуги в гріді

ФАЙЛ 2: src/app/poslugy/[slug]/page.tsx — сторінка послуги
- generateStaticParams() — для кожного slug з Sanity
- generateMetadata() — динамічний title, description, OG
  з seo полів Sanity. Fallback на title якщо seo порожньо
- export const revalidate = 3600
- Тягне getServiceBySlug(slug)
- notFound() якщо slug не знайдено
- Service JSON-LD:
  @type: Service, name, description, provider: Organization

КОМПОНЕНТИ для сторінки послуги:
src/components/sections/ServiceDetail.tsx
Props: service: Service
Секції:
1. Hero з назвою і описом
2. Checklist — що входить у послугу (іконки ✓)
3. Process — кроки роботи (нумерований список)
4. FAQ — акордеон (використай @radix-ui/react-accordion)
5. CTA — форма або кнопка "Замовити"
```

💬 ПРОМПТ 2 (Cursor):
```
Створи сторінки блогу для racio.ua.

ФАЙЛ 1: src/app/blog/page.tsx — список статей
- getAllArticles() з Sanity
- metadata з OG тегами
- BreadcrumbList JSON-LD
- Фільтр по категорії (клієнтський компонент з useState)
- Грід BlogCard
- Якщо статей немає — красива заглушка

ФАЙЛ 2: src/app/blog/[slug]/page.tsx — стаття
- generateStaticParams() і generateMetadata()
- export const revalidate = 3600
- Article JSON-LD:
  @type: Article, headline, datePublished, author,
  image, publisher
- BreadcrumbList: Головна > Блог > Назва статті

КОМПОНЕНТ: src/components/sections/ArticleBody.tsx
Props: body: PortableTextBlock[]
- @portabletext/react для rich text
- Кастомні стилі для: h2, h3, ul, ol, blockquote,
  code (inline і block), зображення (next/image)
- Всі заголовки мають id для anchor links
```

**🐙 GIT**
```bash
git add .
git commit -m "feat: services listing and detail pages with ISR and JSON-LD"
git add .
git commit -m "feat: blog listing and article pages with rich text renderer"
git push origin feat/services-and-blog-pages
```

---

### 🎨 DS — Дні 6–7

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/design-inner-pages
```

💬 ПРОМПТ (Cursor):
```
Зверстай сторінку послуги для racio.ua по Figma макету.

src/components/sections/ServiceDetail.tsx вже має структуру.
Мені потрібно зробити красивий UI для кожної секції.

1. Service Hero:
   - Велике зображення або градієнт фон
   - Назва послуги h1
   - Короткий опис
   - Breadcrumb навігація

2. Checklist секція:
   - Кожен пункт: іконка галочки (SVG, зелений) + текст
   - Грід 2 колонки на desktop, 1 на mobile
   - AnimationWrapper для появи

3. Process секція (кроки):
   - Нумеровані кроки з великою цифрою
   - З'єднуюча лінія між кроками на desktop
   - На mobile — вертикальний список

4. FAQ акордеон:
   - Кожне питання — рядок з іконкою + (плюс/мінус)
   - Плавна анімація розкриття
   - Рамка навколо відкритого пункту

5. CTA блок внизу:
   - Фон контрастний (primary color)
   - Заголовок + кнопка "Замовити консультацію"

Адаптив для всіх секцій: 375 / 768 / 1280px.
Використовуй AnimationWrapper на кожній секції.
```

**🐙 GIT**
```bash
git add .
git commit -m "design: service detail page all sections responsive"
git commit -m "design: blog listing and article page styles"
git push origin feat/design-inner-pages
```

---

## ДЕНЬ 8 — Про нас, Пакети, Контакти

### 👨‍💻 DEV — День 8

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/remaining-pages-and-form
```

💬 ПРОМПТ 1 (Cursor):
```
Створи сторінки /pro-nas, /pakety, /kontakty для racio.ua.

СТОРІНКА: src/app/pro-nas/page.tsx
- getTeamMembers() з Sanity
- metadata і BreadcrumbList JSON-LD
- Секція команди: грід TeamCard
- Секція сертифікатів: зображення з settings
- AboutStats: статистика компанії (роки, клієнти)

СТОРІНКА: src/app/pakety/page.tsx
- Статичний контент (або з Sanity якщо є схема)
- Таблиця або картки пакетів
- Відмінності між пакетами (✓/✗ features)
- CTA кнопка для кожного пакету

СТОРІНКА: src/app/kontakty/page.tsx
- Статична сторінка + форма
- Контактна інформація з settings
- Компонент ContactForm (клієнтський)
- metadata і BreadcrumbList
```

💬 ПРОМПТ 2 (Cursor):
```
Створи форму зворотного зв'язку для racio.ua.

КОМПОНЕНТ: src/components/sections/ContactForm.tsx
'use client'
- react-hook-form + zod валідація
- Поля: name (required, min 2), phone (required, ua формат),
  email (required, valid email), message (optional, max 500)
- Стани: idle → loading → success → error
- При success: "Дякуємо! Ми зв'яжемось з вами найближчим часом"
- При error: "Сталась помилка. Спробуйте ще раз або зателефонуйте"

API ROUTE: src/app/api/contact/route.ts
- POST метод
- Приймає: name, phone, email, message
- Валідація на сервері через zod (ті самі правила)
- Відправка через Resend:
  from: 'noreply@racio.ua'
  to: EMAIL_TO (з env змінної CONTACT_EMAIL)
  subject: 'Нова заявка з сайту — {name}'
  html: красивий шаблон з усіма даними
- Rate limiting: не більше 5 заявок з однієї IP за годину
  (просто через Map в пам'яті — для MVP достатньо)
- Повертає: { success: true } або { error: 'message' }

Додай CONTACT_EMAIL до .env.local
```

**🐙 GIT**
```bash
git add .
git commit -m "feat: pro-nas, pakety, kontakty pages"
git commit -m "feat: contact form with react-hook-form, zod, resend email"
git push origin feat/remaining-pages-and-form
```

✅ **ЧЕКПОІНТ DEV День 8:**
- [ ] Всі 7 сторінок відкриваються без 404
- [ ] Форма відправляє — email приходить
- [ ] Валідація форми показує помилки

---

### 📋 PM — День 8

**🔴 Наповнення Sanity Studio**

Зайди на localhost:3000/studio і заповни:

1. **Settings** (перший — від нього залежать Header і Footer):
   - Телефон, email, адреса
   - Соцмережі (посилання)
   - Статистика (наприклад: "500+ клієнтів", "10 років досвіду")

2. **Team Members** (3-5 людей):
   - Ім'я, посада, фото, короткий опис
   - Order: 1, 2, 3... для правильного порядку

3. **Services** (мінімум 3):
   - Всі поля включно з FAQ і Process
   - Slug автогенерується з назви

4. **Reviews** (мінімум 4):
   - isVisible: true
   - Рейтинг 4-5 зірок

💬 ПРОМПТ (Claude.ai):
```
Я PM. Заповнюю Sanity CMS для сайту бухгалтерської компанії
racio.ua. Допоможи написати контент.

1. Напиши 5 пунктів checklist для послуги "Бухгалтерський облік"
   (що входить у послугу)

2. Напиши 4 кроки процесу роботи (Process) для тієї ж послуги:
   крок 1 → крок 4 з назвою і описом кожного

3. Напиши 5 FAQ питань і відповідей для бухгалтерських послуг

4. Напиши 4 реалістичних відгуки від клієнтів компанії

Тон: діловий, конкретний, без шаблонних фраз.
Мова: українська.
```

---

## ДЕНЬ 9 — SEO інфраструктура

### 👨‍💻 DEV — День 9

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/seo-infrastructure
```

💬 ПРОМПТ 1 (Cursor):
```
Додай повну SEO інфраструктуру для racio.ua на Next.js 14.

ФАЙЛ 1: src/app/sitemap.ts
export default async function sitemap() {
  Тягне з Sanity: всі slug послуг, всі slug статей
  Повертає масив з:
  - Статичні URL: /, /poslugy, /blog, /pro-nas, /kontakty, /pakety
  - Динамічні: /poslugy/{slug} для кожної послуги
  - Динамічні: /blog/{slug} для кожної статті
  Кожен URL: { url, lastModified: new Date(), changeFrequency, priority }
  Головна priority: 1.0, послуги: 0.9, блог: 0.8, інші: 0.7

ФАЙЛ 2: src/app/robots.ts (вже є, перевір і допрацюй)
User-agent: * → Allow: /
Disallow: /studio/, /api/
Sitemap: https://racio.ua/sitemap.xml

ФАЙЛ 3: src/components/seo/BreadcrumbJsonLd.tsx
Props: items: { name: string, url: string }[]
Генерує BreadcrumbList JSON-LD
Використовується на кожній внутрішній сторінці

ФАЙЛ 4: Додай 301-редіректи у next.config.js
Я передам список від PM у форматі:
[{ source: '/old', destination: '/new', permanent: true }]
Залиш порожній масив і TypeScript тип.
```

💬 ПРОМПТ 2 (Cursor):
```
Додай Open Graph зображення для кожного типу сторінок racio.ua.
Використай next/og (ImageResponse).

ФАЙЛ 1: src/app/opengraph-image.tsx
Дефолтне OG зображення для головної:
- Фон у кольорі primary бренду
- Лого "Racio" великим шрифтом
- Підзаголовок "Бухгалтерські послуги"
- Розмір 1200x630px

ФАЙЛ 2: src/app/poslugy/[slug]/opengraph-image.tsx
- Динамічне OG для кожної послуги
- Тягне назву послуги з Sanity по slug
- Назва послуги + "| Racio"

ФАЙЛ 3: src/app/blog/[slug]/opengraph-image.tsx
- Тягне заголовок статті
- Ім'я автора
- Дата публікації

Всі OG зображення: 1200x630px, шрифт Inter.
```

**🐙 GIT**
```bash
git add .
git commit -m "seo: sitemap, robots, breadcrumb json-ld, og images"
git push origin feat/seo-infrastructure
```

---

### 📋 PM — День 9

**🔴 301 редіректи — фінальний список**

Відкрий Google Sheets таблицю → відфільтруй тільки ті де є відповідний новий URL.

💬 ПРОМПТ (Claude.ai):
```
У мене є список URL зі старого сайту racio.ua (WordPress).
Мені потрібно скласти 301 редіректи для next.config.js.

Старі URL (приклад):
/ru/uslugi/buhgalterskij-uchet-predpriyatij
/ru/uslugi/nalogovaya-otchetnost
/ru/blog/article-name
/ru/o-nas
/ru/kontakty

Нова структура:
/poslugy/[slug]
/blog/[slug]
/pro-nas
/kontakty

Згенеруй масив для next.config.js у форматі:
[
  { source: '/старий-url', destination: '/новий-url', permanent: true },
]

Також врахуй:
- URL з /ru/ префіксом → без префіксу
- WordPress /?p=123 → 301 на головну якщо не знаємо slug
- /feed, /wp-login.php, /wp-admin → /
```

Відправ готовий масив розробнику у GitHub issue або в чат.

---

## ДЕНЬ 10 — QA і Lighthouse

### 📋 PM — День 10

**🔴 Повне QA тестування**

Відкрий dev preview URL і перевір кожну сторінку:

```
ЧЕКЛІСТ КОЖНОЇ СТОРІНКИ:
□ Відкривається без помилок (console.log чистий)
□ Mobile 375px — немає горизонтального скролу
□ Tablet 768px — коректний layout
□ Desktop 1280px — виглядає як у Figma
□ Всі зображення завантажуються
□ Посилання в навігації ведуть правильно
□ Нема зламаних посилань (404)
□ Текст читається (контраст, розмір)

ФОРМА /kontakty:
□ Валідація показує помилки (submit порожньої форми)
□ Валідний submit — email приходить
□ Success повідомлення з'являється

CMS КОНТЕНТ:
□ Відгуки відображаються на головній
□ Послуги відображаються на /poslugy
□ Статті відображаються на /blog
□ Команда відображається на /pro-nas
□ Settings (телефон, email) у Header і Footer
```

Всі знайдені баги — заводь як GitHub Issues:
Title: `[BUG] Опис проблеми`
Label: `bug`
Assign: відповідній людині

---

### 👨‍💻 DEV — День 10

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b fix/lighthouse-optimization
```

💬 ПРОМПТ (Cursor):
```
Мені потрібно оптимізувати racio.ua для Lighthouse ≥ 90.

Проведи аудит коду і виправ типові проблеми:

1. LCP < 2.5s — перевір:
   - Hero зображення має priority={true} в next/image
   - Шрифт Inter підключений через next/font (не @import)
   - Нема render-blocking ресурсів

2. CLS < 0.1 — перевір:
   - Кожне next/image має явний width і height або fill з
     контейнером фіксованого розміру
   - Шрифти не зсувають текст при завантаженні
     (next/font автоматично вирішує це)
   - Framer Motion не анімує layout properties

3. Performance — перевір:
   - Компоненти які не потрібні при першому рендері —
     dynamic import з ssr: false
   - Іконки — inline SVG або next/image, не img теги
   - Нема великих npm пакетів (перевір bundle через
     @next/bundle-analyzer)

4. Accessibility:
   - Всі img і next/image мають alt
   - Кнопки і посилання мають aria-label де немає тексту
   - Форма має label для кожного input

Виведи список конкретних змін які треба зробити.
```

**🐙 GIT**
```bash
git add .
git commit -m "fix: lighthouse performance optimizations - LCP, CLS, accessibility"
git push origin fix/lighthouse-optimization
```

---

# ═══════════════════════════════════
# ТИЖДЕНЬ 3 — ФІНАЛ І ЗДАЧА
# ═══════════════════════════════════

---

## ДЕНЬ 11 — GTM, GA4, Cookie Consent

### 👨‍💻 DEV — День 11

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b feat/analytics-and-cookies
```

💬 ПРОМПТ (Cursor):
```
Додай аналітику і cookie consent до racio.ua.

1. Google Tag Manager:
   - Компонент src/components/analytics/GTM.tsx
   - Вставляє GTM script у <head> і noscript у <body>
   - GTM ID береться з env NEXT_PUBLIC_GTM_ID
   - Підключи у src/app/layout.tsx

2. Cookie Consent банер:
   - Компонент src/components/ui/CookieBanner.tsx
   - 'use client', зберігає згоду у localStorage
   - При згоді — завантажує GTM
   - При відмові — GTM не завантажується
   - UI: банер знизу сторінки, кнопки "Прийняти" і "Відхилити"
   - Після вибору — банер зникає і більше не з'являється

3. Підключи CookieBanner у layout.tsx після Footer

ВАЖЛИВО: GTM не повинен завантажуватись до згоди користувача.
Використовуй conditional rendering або dynamic import.
```

**🔴 PM — Налаштуй GA4 і GTM**

1. analytics.google.com → New Property → racio.ua → Web
2. Скопіюй Measurement ID (G-XXXXXXXXXX)
3. tagmanager.google.com → New Account → Container: racio.ua
4. Workspace → Tags → New:
   - Tag Type: Google Analytics GA4 Configuration
   - Measurement ID: G-XXXXXXXXXX
   - Trigger: All Pages
5. Submit → Publish → Version Name: "Initial setup"
6. Скопіюй GTM ID (GTM-XXXXXXX) → передай розробнику для .env

---

## ДЕНЬ 12 — Фінальний Lighthouse + виправлення

### 👨‍💻 DEV — День 12

**🐙 GIT**
```bash
git checkout dev && git pull origin dev
git checkout -b fix/final-fixes
```

**🔴 Запуск Lighthouse**
1. Chrome → відкрий dev preview URL
2. DevTools (F12) → Lighthouse
3. Categories: всі ✓ → Device: Mobile → Analyze
4. Зафіксуй цифри: Performance, Accessibility, Best Practices, SEO

💬 ПРОМПТ (Cursor — вставляй конкретні помилки):
```
Lighthouse показав такі помилки на racio.ua:

[ВСТАВИТИ СПИСОК ПОМИЛОК З LIGHTHOUSE]

Для кожної помилки:
1. Поясни чому вона виникла
2. Дай конкретне виправлення з кодом
3. Скажи скільки очків це додасть

Пріоритет: спочатку виправлення які найбільше впливають
на Performance score.
```

**🐙 GIT**
```bash
git add .
git commit -m "fix: lighthouse score improvements based on audit"
git push origin fix/final-fixes
```

**🔴 Мета дня: Lighthouse ≥ 90 на Mobile**

Якщо не виходить досягти 90 — мінімально прийнятно:
- Performance ≥ 85
- Accessibility ≥ 95
- Best Practices ≥ 90
- SEO = 100

---

## ДЕНЬ 13 — Деплой на продакшн

### 👨‍💻 DEV — День 13

**🐙 GIT — Milestone merge: dev → main**

Повідом PM що готово до злиття в main.
PM створює PR: dev → main, перевіряє, зливає.
Vercel автоматично деплоїть на racio.ua.

**🔴 Прив'язка домену racio.ua**
```
Vercel → Project → Settings → Domains → Add Domain
Введи: racio.ua
Додай також: www.racio.ua → redirect to racio.ua

Vercel покаже DNS записи які треба додати:
A record: @ → 76.76.21.21
CNAME: www → cname.vercel-dns.com

Зайди до реєстратора домену → DNS → додай ці записи
Перевір через: https://dnschecker.org
Зазвичай активується за 5-30 хвилин.
```

**🔴 Перевір після деплою:**
```bash
# Перевір sitemap
curl https://racio.ua/sitemap.xml

# Перевір robots
curl https://racio.ua/robots.txt

# Перевір 301 редіректи
curl -I https://racio.ua/ru/o-nas
# Має повернути: HTTP/2 301, Location: https://racio.ua/pro-nas
```

💬 ПРОМПТ — Фінальна перевірка (Claude.ai):
```
Я розробник. Сайт racio.ua задеплоєний на Vercel.
Дай мені фінальний чекліст перевірки перед здачею клієнту.

Категорії:
1. Технічні перевірки (домен, SSL, редіректи)
2. SEO перевірки (sitemap, robots, meta теги, JSON-LD)
3. Функціональні (форма, навігація, CMS)
4. Performance (Lighthouse, Core Web Vitals)
5. Безпека (env змінні, api routes)

Для кожного пункту: що перевірити і як саме.
```

---

## ДЕНЬ 14 — Налаштування Sanity для клієнта

### 📋 PM — День 14

**🔴 Налаштуй доступ клієнта до Sanity Studio**
1. sanity.io → твій проєкт → Members → Invite
2. Введи email клієнта → роль: Editor
3. Клієнт отримає email з запрошенням

**🔴 Напиши інструкцію редактора**

💬 ПРОМПТ (Claude.ai):
```
Напиши детальну інструкцію для нетехнічного редактора сайту
racio.ua. Редактор буде використовувати Sanity Studio на
адресі racio.ua/studio.

Напиши покрокові інструкції з описом кожного кроку
(як ніби пояснюєш людині яка перший раз бачить CMS):

РОЗДІЛ 1: Як увійти в систему
РОЗДІЛ 2: Як додати нову статтю в блог
  (заголовок, текст, зображення, категорія, дата, SEO поля)
РОЗДІЛ 3: Як додати відгук клієнта
РОЗДІЛ 4: Як додати члена команди
РОЗДІЛ 5: Як відредагувати існуючий контент
РОЗДІЛ 6: Як опублікувати зміни (Publish кнопка)
РОЗДІЛ 7: Що НЕ чіпати (технічні поля)

Формат: нумеровані кроки, без технічних термінів.
Збережи у форматі Google Doc або Markdown.
```

Зроби скріншоти кожного кроку в Studio і встав в документ.

---

### 🎨 DS — День 14

**🔴 Відео-огляд (Loom)**
1. Завантаж Loom: loom.com
2. Запиш відео 5-7 хвилин:
   - Відкрий racio.ua — проведи по всіх сторінках
   - Покажи адаптив (DevTools → Toggle Device)
   - Зайди в racio.ua/studio — покажи як додати статтю
   - Покажи Lighthouse скріншот
3. Скопіюй посилання → передай PM

**🔴 Pixel-perfect фінальна перевірка**
1. Встанови розширення PerfectPixel для Chrome
2. Зроби скріншоти з Figma для кожної сторінки
3. Накладай і перевіряй відступи, розміри
4. Список невідповідностей → GitHub issue для виправлення

---

## ДЕНЬ 15 — ЗДАЧА

### 📋 PM — День 15

**🔴 Фінальний чекліст здачі:**
```
ТЕХНІЧНЕ:
□ racio.ua відкривається через HTTPS
□ www.racio.ua → redirect на racio.ua
□ SSL сертифікат активний (зелений замок)
□ GitHub репо — чистий, є README з описом проєкту
□ Vercel project налаштований, домен прив'язаний

СТОРІНКИ:
□ / — головна з даними з CMS
□ /poslugy — список послуг
□ /poslugy/[slug] — мінімум 3 послуги
□ /blog — список статей
□ /blog/[slug] — мінімум 2 статті
□ /pro-nas — команда з фото
□ /kontakty — форма працює
□ /pakety — пакети відображаються

SEO:
□ racio.ua/sitemap.xml відкривається
□ racio.ua/robots.txt відкривається
□ JSON-LD є у source code кожної сторінки
□ OG теги є (перевір через opengraph.xyz)
□ 301-редіректи зі старого WordPress

CMS:
□ Sanity Studio → racio.ua/studio
□ Клієнт запрошений з роллю Editor
□ Мінімум 3 послуги, 2 статті, 4 відгуки, 3 члени команди

АНАЛІТИКА:
□ GA4 отримує дані (Real-time → є сесії)
□ GTM контейнер опублікований
□ Cookie banner відображається на новому пристрої

ФОРМА:
□ /kontakty → заповни форму → email приходить клієнту

PERFORMANCE:
□ Lighthouse Mobile Performance ≥ 85 (ціль ≥ 90)
□ Скріншот Lighthouse збережений

МАТЕРІАЛИ ЗДАЧІ:
□ Посилання на GitHub репо
□ Посилання на racio.ua
□ Посилання на Sanity Studio
□ Відео-огляд (Loom посилання)
□ Інструкція редактора (Google Doc)
□ Скріншот Lighthouse
□ Таблиця 301-редіректів (для SEO-аудиту)
```

**🔴 Фінальний меседж клієнту**

💬 ПРОМПТ (Claude.ai):
```
Напиши фінальний email клієнту про здачу сайту racio.ua.

Що передаємо:
- Посилання на сайт (вставлю)
- Посилання на GitHub (вставлю)
- Відео-огляд Loom (вставлю)
- Інструкцію редактора (додаток)
- Lighthouse скріншот (додаток)

Email має:
- Подякувати за співпрацю
- Коротко перерахувати що зроблено (список)
- Пояснити що далі: як увійти в Studio, як редагувати
- Запропонувати підтримку (окремий retainer)
- Попросити підтвердити прийом роботи

В кінці: м'яко нагадати про другу частину оплати (50%).

Тон: тепло-діловий, з гордістю за зроблену роботу.
```

---

## ПІДСУМКОВИЙ РОЗПОДІЛ ЗАДАЧ

| День | DEV | DS | PM |
|------|-----|----|----|
| 1 | Проєкт + Sanity схеми | Токени + Button | GitHub + URL збір |
| 2 | Layout + Homepage структура | UI компоненти | Контент зі старого сайту |
| 3–4 | Homepage логіка + SEO meta | Homepage верстка + анімації | Preview клієнту |
| 5 | — | — | Синк + milestone review |
| 6–7 | Services + Blog сторінки | Inner pages верстка | QA + Sanity наповнення |
| 8 | Про нас + Форма | Стилі форми і команди | Sanity наповнення |
| 9 | SEO інфраструктура | OG зображення | 301 редіректи |
| 10 | Lighthouse fixes | Pixel-perfect QA | Повне QA тестування |
| 11 | GTM + Cookie consent | — | GA4 налаштування |
| 12 | Фінальний Lighthouse | — | Баги із QA |
| 13 | Деплой + домен | — | dev → main merge |
| 14 | Readme + cleanup | Відео-огляд | Інструкція редактора |
| 15 | — | — | Здача + рахунок |

---

## ПРАВИЛА КОМАНДИ

### GitHub — залізні правила:
1. Ніколи не пушити напряму в `main` або `dev`
2. Один PR = одна задача
3. Кожен ранок: `git checkout dev && git pull origin dev`
4. Коміт формат: `feat:` `fix:` `design:` `cms:` `seo:` `config:`
5. PM апрувить і зливає — розробники не зливають самі

### Комунікація:
- Щоранку: хто що робить сьогодні (1-2 речення в чат)
- При блокері: одразу в чат, не чекати до вечора
- PM надсилає клієнту оновлення кожні 2-3 дні

### Якщо щось пішло не так:
- Не ламай `dev` — виправляй у своїй гілці
- Якщо зламав — одразу пиши команді
- Важкий баг — попроси розробника, не витрачай 3 години сам

```
racio-site/
├── src/
│   ├── app/
│   │   ├── api/
│   │   │   └── contact/
│   │   │       └── route.ts         # форма (обробка)
│   │   ├── blog/
│   │   │   ├── [slug]/
│   │   │   │   └── page.tsx
│   │   │   └── page.tsx
│   │   ├── kontakty/
│   │   │   └── page.tsx
│   │   ├── pakety/
│   │   │   └── page.tsx
│   │   ├── poslugy/
│   │   │   ├── [slug]/
│   │   │   │   └── page.tsx
│   │   │   └── page.tsx
│   │   ├── pro-nas/
│   │   │   └── page.tsx
│   │   ├── layout.tsx               # root layout
│   │   ├── page.tsx                 # головна сторінка
│   │   ├── robots.ts
│   │   └── sitemap.ts
│   ├── components/
│   │   ├── layout/                  # Header, Footer
│   │   ├── sections/                # Hero, Services і т.д.
│   │   └── ui/                      # Button, Card і т.д.
│   ├── lib/
│   │   ├── sanity/
│   │   │   └── schemas/             # всі CMS схеми
│   │   ├── queries.ts
│   │   ├── sanityClient.ts
│   │   └── utils.ts
│   └── types/
│       └── index.ts
├── .env.local
├── next.config.js
├── tailwind.config.ts
└── racio-project-plan.md
```
---

*Документ: racio-project-plan.md*
*Версія: 1.0 — складено для команди з 3 людей*
*Проєкт: racio.ua редизайн 2024*
