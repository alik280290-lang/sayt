# UX Upgrade — Средний апгрейд

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Повысить конверсию и визуальное качество сайта: hero с видео и сильным CTA, лучший контраст текста, выразительные карточки, реальные видео в портфолио, живые аватары отзывов.

**Architecture:** Все изменения в одном файле `index.html`. CSS-правила добавляются в `<style>` блок в `<head>`. HTML изменяется точечно по секциям. Нет сборки, нет зависимостей.

**Tech Stack:** Vanilla HTML/CSS, Kinescope (видеохостинг, iframe embed)

---

### Task 1: Читаемость — CSS переменные и размер текста

**Files:**
- Modify: `index.html` — блок `:root` и правило `.process-step p`

- [ ] **Шаг 1: Обновить три CSS переменные в `:root`**

Найти блок `:root { ... }` (в начале `<style>`) и изменить три строки:

```css
/* Было: */
--text-2: rgba(248,248,255,0.55);
--text-dark-2: rgba(13,13,20,0.55);
--text-dark-3: rgba(13,13,20,0.30);

/* Стало: */
--text-2: rgba(248,248,255,0.72);
--text-dark-2: rgba(13,13,20,0.65);
--text-dark-3: rgba(13,13,20,0.40);
```

- [ ] **Шаг 2: Обновить размер текста в Process**

Найти `.process-step p { ... }` и изменить `font-size`:

```css
/* Было: */
.process-step p { font-size: 14px; color: var(--text-2); line-height: 1.6; }

/* Стало: */
.process-step p { font-size: 15px; color: var(--text-2); line-height: 1.6; }
```

- [ ] **Шаг 3: Проверить в браузере**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: Весь вторичный текст на сайте стал заметно контрастнее. Описания карточек, подзаголовки секций, мета-лейблы в кейсах — все читаются без напряжения.

---

### Task 2: Hero — CTA кнопка, подзаголовок, строка клиентов

**Files:**
- Modify: `index.html` — CSS кнопки, HTML hero-секции

- [ ] **Шаг 1: Добавить CSS класс `.btn-hero-primary`**

В `<style>` блоке, после блока `/* ─── BUTTONS ─── */`, добавить:

```css
/* Кнопка hero — solid purple, без :: :: */
.btn-hero-primary {
  background: var(--purple); color: #fff; border: none;
  padding: 14px 28px; font-size: 15px;
}
.btn-hero-primary:hover {
  background: #6930cc;
  transform: translateY(-1px);
  box-shadow: 0 8px 24px rgba(123,63,228,0.35);
}
.btn-hero-primary::before,
.btn-hero-primary::after { display: none; }
```

- [ ] **Шаг 2: Добавить CSS для строки клиентов**

В `<style>` блоке, после `.hero-award-icon { ... }`, добавить:

```css
/* Строка клиентов в hero */
.hero-clients {
  display: flex; align-items: center; gap: 8px; flex-wrap: wrap;
  margin-bottom: 32px; font-size: 13px;
}
.hero-clients-label { color: var(--text-3); font-weight: 500; margin-right: 4px; }
.hero-clients-name {
  color: var(--text-2); font-family: 'Space Grotesk', sans-serif; font-weight: 600;
}
.hero-clients-dot { color: var(--text-3); }
```

- [ ] **Шаг 3: Заменить кнопку CTA в hero**

Найти в HTML hero-секции:
```html
<a href="#contact" class="btn btn-primary">Обсудить задачу</a>
```
Заменить на:
```html
<a href="#contact" class="btn btn-hero-primary">Обсудить задачу</a>
```

- [ ] **Шаг 4: Заменить текст `.hero-sub`**

Найти:
```html
<p class="hero-sub">
  AI-видео и фото для рекламы, брендинга и соцсетей. Заменяет студийный продакшн: без аренды локаций, без съёмочной группы, без долгих согласований. Первый черновик — за 24–48 часов.
</p>
```
Заменить на:
```html
<p class="hero-sub">
  AI-видео и фото вместо студийного продакшна — без аренды локаций и съёмочной группы. Первый черновик за 48 часов.
</p>
```

- [ ] **Шаг 5: Обновить CSS `.hero-sub` — уменьшить отступ**

После Task 1 `--text-2` уже будет `0.72`, поэтому менять только `margin-bottom`.

Найти `.hero-sub { ... }` и изменить только `margin-bottom`:

```css
/* Было: */
.hero-sub {
  font-size: 18px; color: var(--text-2); max-width: 560px;
  margin-bottom: 40px; line-height: 1.7;
}

/* Стало: */
.hero-sub {
  font-size: 18px; color: var(--text-2); max-width: 560px;
  margin-bottom: 32px; line-height: 1.7;
}
```

- [ ] **Шаг 6: Добавить строку клиентов в HTML hero**

Найти в hero HTML:
```html
      <div class="hero-ctas">
```
Вставить перед этой строкой:
```html
      <div class="hero-clients">
        <span class="hero-clients-label">Работали с:</span>
        <span class="hero-clients-name">Kabrita</span>
        <span class="hero-clients-dot">·</span>
        <span class="hero-clients-name">KGM Automotive</span>
        <span class="hero-clients-dot">·</span>
        <span class="hero-clients-name">PROCAR</span>
      </div>
```

- [ ] **Шаг 7: Проверить в браузере**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: Hero — кнопка "Обсудить задачу" стала ярко-фиолетовой и сразу бросается в глаза. Подзаголовок короче. Под подзаголовком — строка "Работали с: Kabrita · KGM Automotive · PROCAR".

---

### Task 3: Hero — 2-колонки с видео Kabrita справа

**Files:**
- Modify: `index.html` — CSS hero layout, HTML hero-секции

- [ ] **Шаг 1: Добавить CSS для 2-колоночного лейаута**

В `<style>` блоке, после `.hero-content { ... }`, добавить:

```css
/* Hero 2-колонки */
.hero-inner {
  display: grid;
  grid-template-columns: 1fr 460px;
  gap: 60px;
  align-items: center;
}
.hero-video {
  border-radius: 12px;
  overflow: hidden;
  border: 1px solid rgba(123,63,228,0.25);
  box-shadow: 0 32px 80px rgba(0,0,0,0.5);
  position: relative; z-index: 1;
}
.hero-video iframe {
  display: block; width: 100%; aspect-ratio: 16/9; border: none;
}
```

- [ ] **Шаг 2: Добавить медиазапрос для скрытия видео на мобайле**

В блоке `@media (max-width: 1024px)` добавить:
```css
.hero-inner { grid-template-columns: 1fr; }
.hero-video { display: none; }
```

- [ ] **Шаг 3: Обернуть hero-content в hero-inner и добавить видео**

Найти в HTML:
```html
  <div class="container">
    <div class="hero-content fade-up">
```
Заменить на:
```html
  <div class="container">
    <div class="hero-inner">
    <div class="hero-content fade-up">
```

Затем найти закрывающий тег `.hero-content`:
```html
    </div>
  </div>
  <div class="scroll-indicator">
```
Заменить на:
```html
    </div>
    <div class="hero-video">
      <iframe
        src="https://kinescope.io/embed/b9LqTwdSKuvSTM2k3q5TpM"
        allow="autoplay; fullscreen"
        allowfullscreen
        frameborder="0"></iframe>
    </div>
    </div>
  </div>
  <div class="scroll-indicator">
```

- [ ] **Шаг 4: Убрать `max-width: 800px` у `.hero-content`**

Найти `.hero-content { ... }` и удалить или закомментировать `max-width: 800px` — внутри grid-колонки он не нужен:

```css
/* Было: */
.hero-content { position: relative; z-index: 1; max-width: 800px; }

/* Стало: */
.hero-content { position: relative; z-index: 1; }
```

- [ ] **Шаг 5: Проверить в браузере**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: Hero — слева текст + кнопки, справа видеоплеер Kabrita с фиолетовой рамкой и глубокой тенью. На экране уже сразу видно качество работы. На мобайле (DevTools → 375px) видео не показывается, текст занимает всю ширину.

---

### Task 4: Карточки услуг и цен

**Files:**
- Modify: `index.html` — CSS `.service-card`, `.pricing-card.featured`, HTML pricing section-heading

- [ ] **Шаг 1: Добавить border-top и тень к service-card**

Найти `.service-card { ... }` и добавить две строки:

```css
/* Было: */
.service-card {
  padding: 28px; border-radius: 8px;
  background: #fff; border: 1px solid rgba(0,0,0,0.08);
  transition: all 0.3s ease; cursor: default;
}

/* Стало: */
.service-card {
  padding: 28px; border-radius: 8px;
  background: #fff; border: 1px solid rgba(0,0,0,0.08);
  border-top: 2px solid var(--purple);
  box-shadow: 0 2px 12px rgba(0,0,0,0.06);
  transition: all 0.3s ease; cursor: default;
}
```

- [ ] **Шаг 2: Усилить hover эффект service-card**

Найти `.service-card:hover { ... }` и обновить:

```css
/* Было: */
.service-card:hover {
  border-color: rgba(123,63,228,0.3);
  transform: translateY(-3px);
  box-shadow: 0 12px 32px rgba(0,0,0,0.08);
}

/* Стало: */
.service-card:hover {
  border-color: rgba(123,63,228,0.3);
  transform: translateY(-4px);
  box-shadow: 0 16px 40px rgba(0,0,0,0.12);
}
```

- [ ] **Шаг 3: Приподнять featured pricing card**

Найти `.pricing-card.featured { ... }` и добавить `transform`:

```css
/* Было: */
.pricing-card.featured {
  border-color: rgba(123,63,228,0.4);
  background: #fff;
  box-shadow: 0 0 32px rgba(123,63,228,0.08);
}

/* Стало: */
.pricing-card.featured {
  border-color: rgba(123,63,228,0.4);
  background: #fff;
  box-shadow: 0 24px 60px rgba(123,63,228,0.14);
  transform: translateY(-8px);
}
```

- [ ] **Шаг 4: Добавить CSS `.pricing-context`**

В `<style>` блоке, после `.pricing-note { ... }`, добавить:

```css
.pricing-context {
  font-size: 13px; color: var(--text-dark-2);
  margin-top: 8px; font-style: italic;
}
```

- [ ] **Шаг 5: Добавить строку сравнения в HTML pricing секции**

Найти в HTML секции pricing:
```html
      <p>Начать можно с разового проекта. Большинство клиентов переходят на ретейн после первого результата.</p>
    </div>
```
Вставить после этой строки (перед закрывающим `</div>`):
```html
      <p class="pricing-context">Студийная съёмка от 80 000 ₽ за день. AI-продакшн — от 45 000 ₽ за готовый пакет.</p>
```

- [ ] **Шаг 6: Проверить в браузере**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: Карточки услуг имеют фиолетовую полоску сверху и заметную тень. Hover поднимает карточку выше. Средняя ценовая карточка приподнята над остальными. Под описанием в pricing — курсивная строка сравнения.

---

### Task 5: Портфолио — видео Kinescope для Kabrita и KGM

**Files:**
- Modify: `index.html` — CSS portfolio-video, HTML двух portfolio-card

- [ ] **Шаг 1: Добавить CSS для `.portfolio-video`**

В `<style>` блоке, в разделе `/* ═══ PORTFOLIO ═══ */`, после `.portfolio-cover::after { ... }`, добавить:

```css
/* Portfolio: видео карточки */
.portfolio-video {
  position: relative; aspect-ratio: 4/3;
  background: #000; overflow: hidden;
}
.portfolio-video iframe {
  position: absolute; inset: 0;
  width: 100%; height: 100%; border: none;
  pointer-events: none;
}
.portfolio-video .portfolio-cover-inner {
  position: absolute; bottom: 0; left: 0; right: 0; z-index: 2;
  background: linear-gradient(to top, rgba(8,8,15,0.9) 0%, transparent 60%);
  padding: 20px;
}
```

- [ ] **Шаг 2: Заменить Kabrita portfolio-cover на видео**

Найти HTML карточки Kabrita (содержит `p-cover-2` и `Kabrita × VIDMK`):
```html
        <div class="portfolio-cover p-cover-2">
          <div class="portfolio-cover-inner">
            <div class="p-tag">AI-видео · 🏆 Победитель</div>
            <div class="p-title">Kabrita × VIDMK Hackaton</div>
          </div>
        </div>
```
Заменить на:
```html
        <div class="portfolio-cover portfolio-video">
          <iframe
            src="https://kinescope.io/embed/b9LqTwdSKuvSTM2k3q5TpM"
            allow="autoplay; fullscreen"
            allowfullscreen
            frameborder="0"></iframe>
          <div class="portfolio-cover-inner">
            <div class="p-tag">AI-видео · 🏆 Победитель</div>
            <div class="p-title">Kabrita × VIDMK Hackaton</div>
          </div>
        </div>
```

- [ ] **Шаг 3: Заменить KGM portfolio-cover на видео**

Найти HTML карточки KGM (содержит `p-cover-6` и `KGM Automotive`):
```html
        <div class="portfolio-cover p-cover-6">
          <div class="portfolio-cover-inner">
            <div class="p-tag">AI-видео</div>
            <div class="p-title">KGM Automotive</div>
          </div>
        </div>
```
Заменить на:
```html
        <div class="portfolio-cover portfolio-video">
          <iframe
            src="https://kinescope.io/embed/usf3Yks5jhxMjAZpEuSVJF"
            allow="autoplay; fullscreen"
            allowfullscreen
            frameborder="0"></iframe>
          <div class="portfolio-cover-inner">
            <div class="p-tag">AI-видео</div>
            <div class="p-title">KGM Automotive</div>
          </div>
        </div>
```

- [ ] **Шаг 4: Проверить в браузере (требуется интернет)**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: Два portfolio-card показывают реальные видеоролики — Kabrita и KGM. Видео загружается через iframe. Тег и название карточки видны поверх видео (gradient overlay). Клик по карточке работает (pointer-events: none на iframe).

---

### Task 6: Портфолио — типографические превью + аватары отзывов

**Files:**
- Modify: `index.html` — HTML 4 оставшихся portfolio-cover, CSS `.p-cover-text`, HTML testimonial аватары, CSS `.author-avatar`

- [ ] **Шаг 1: Добавить CSS для типографических превью**

В `<style>` блоке, после `.portfolio-video { ... }` (добавленного в Task 5), добавить:

```css
/* Portfolio: типографические превью */
/* position: absolute чтобы не ломать flex-layout .portfolio-cover */
.p-cover-text {
  position: absolute;
  bottom: 64px; left: 20px; right: 20px;
  z-index: 1;
}
.p-cover-brand {
  font-family: 'Space Grotesk', sans-serif; font-size: 26px; font-weight: 800;
  color: rgba(255,255,255,0.9); letter-spacing: -0.02em; margin-bottom: 4px;
}
.p-cover-desc { font-size: 11px; color: rgba(255,255,255,0.55); line-height: 1.5; }
```

- [ ] **Шаг 2: Добавить типографический контент в карточку PROCAR**

Найти HTML карточки PROCAR (содержит `p-cover-1` и `PROCAR — Автопарк люкс`):
```html
        <div class="portfolio-cover p-cover-1">
          <div class="portfolio-cover-inner">
            <div class="p-tag">AI-фото</div>
            <div class="p-title">PROCAR — Автопарк люкс</div>
          </div>
        </div>
```
Заменить на:
```html
        <div class="portfolio-cover p-cover-1">
          <div class="p-cover-text">
            <div class="p-cover-brand">PROCAR</div>
            <div class="p-cover-desc">BMW · Mercedes · Lamborghini · Porsche</div>
            <div class="p-cover-desc">Москва-Сити · Кремль · Набережная</div>
          </div>
          <div class="portfolio-cover-inner">
            <div class="p-tag">AI-фото</div>
            <div class="p-title">PROCAR — Автопарк люкс</div>
          </div>
        </div>
```

- [ ] **Шаг 3: Добавить типографический контент в карточку Барбер Сэм**

Найти HTML карточки Барбер Сэм (содержит `p-cover-3`):
```html
        <div class="portfolio-cover p-cover-3">
          <div class="portfolio-cover-inner">
            <div class="p-tag">Комиксы</div>
            <div class="p-title">Барбер Сэм — серия</div>
          </div>
        </div>
```
Заменить на:
```html
        <div class="portfolio-cover p-cover-3">
          <div class="p-cover-text">
            <div class="p-cover-brand">Барбер Сэм</div>
            <div class="p-cover-desc">Серия AI-комиксов · 6 историй</div>
            <div class="p-cover-desc">Персонаж с фото клиента</div>
          </div>
          <div class="portfolio-cover-inner">
            <div class="p-tag">Комиксы</div>
            <div class="p-title">Барбер Сэм — серия</div>
          </div>
        </div>
```

- [ ] **Шаг 4: Добавить типографический контент в карточку Москитные сетки**

Найти HTML карточки Москитные сетки (содержит `p-cover-4`):
```html
        <div class="portfolio-cover p-cover-4">
          <div class="portfolio-cover-inner">
            <div class="p-tag">Брендинг</div>
            <div class="p-title">Москитные сетки — авто</div>
          </div>
        </div>
```
Заменить на:
```html
        <div class="portfolio-cover p-cover-4">
          <div class="p-cover-text">
            <div class="p-cover-brand">vse-okna.com</div>
            <div class="p-cover-desc">Брендирование авто · AI-мокап</div>
            <div class="p-cover-desc">Согласован → уже на дороге</div>
          </div>
          <div class="portfolio-cover-inner">
            <div class="p-tag">Брендинг</div>
            <div class="p-title">Москитные сетки — авто</div>
          </div>
        </div>
```

- [ ] **Шаг 5: Добавить типографический контент в карточку Цветочный магазин**

Найти HTML карточки Цветочный магазин (содержит `p-cover-5`):
```html
        <div class="portfolio-cover p-cover-5">
          <div class="portfolio-cover-inner">
            <div class="p-tag">Комиксы</div>
            <div class="p-title">Цветочный магазин — серия</div>
          </div>
        </div>
```
Заменить на:
```html
        <div class="portfolio-cover p-cover-5">
          <div class="p-cover-text">
            <div class="p-cover-brand">Цветочный</div>
            <div class="p-cover-desc">3 сценария · 3 типа покупателей</div>
            <div class="p-cover-desc">«Это прямо про меня» — клиенты</div>
          </div>
          <div class="portfolio-cover-inner">
            <div class="p-tag">Комиксы</div>
            <div class="p-title">Цветочный магазин — серия</div>
          </div>
        </div>
```

- [ ] **Шаг 6: Обновить CSS `.author-avatar` — добавить border**

Найти `.author-avatar { ... }` и добавить border:

```css
/* Найти существующее правило и добавить border: */
.author-avatar {
  /* существующие свойства */
  border: 1px solid rgba(255,255,255,0.12);
}
```

- [ ] **Шаг 7: Заменить цвета аватаров в HTML (оба набора — Set 1 и Set 2)**

В HTML секции testimonials есть два Set (оригинал и дубль для бесконечной прокрутки). Нужно обновить `style="background: ..."` в обоих.

PROCAR (инициалы "ПК"):
- Найти `<div class="author-avatar">ПК</div>` (оба экземпляра)
- Заменить на `<div class="author-avatar" style="background:#1a4a8a">ПК</div>`

Москитные сетки (инициалы "МС"):
- Найти `<div class="author-avatar">МС</div>` (оба)
- Заменить на `<div class="author-avatar" style="background:#2d5a2d">МС</div>`

Барбер Сэм (инициал "С"):
- Найти `<div class="author-avatar">С</div>` (оба)
- Заменить на `<div class="author-avatar" style="background:#8B4500">С</div>`

Hackaton VK (инициалы "VK"):
- Найти `<div class="author-avatar">VK</div>` (оба)
- Заменить на `<div class="author-avatar" style="background:#4a1a8a">VK</div>`

Цветочный (инициалы "ЦМ"):
- Найти `<div class="author-avatar">ЦМ</div>` (оба)
- Заменить на `<div class="author-avatar" style="background:#7a3a7a">ЦМ</div>`

- [ ] **Шаг 8: Финальная проверка всего сайта**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Прокрутить весь сайт сверху вниз. Ожидание:
- Hero: фиолетовая кнопка слева, видеоплеер справа, строка клиентов
- Секция услуг: карточки с фиолетовой полоской сверху, заметны на светлом фоне
- Pricing: средняя карточка приподнята, курсивная строка сравнения под описанием
- Portfolio: Kabrita и KGM показывают видео, остальные 4 — типографические превью с названиями
- Testimonials: у каждого автора свой цвет аватара
