# Дизайн-спек: UX Upgrade — Подход Б (Средний апгрейд)
Date: 2026-04-16

## Цель
Повысить конверсию и визуальное качество сайта без изменения структуры. Приоритеты: hero → читаемость → карточки → видео в портфолио → hover-эффекты → мобайл.

## Файл
`/Users/shantropa/Desktop/vsCode/index.html` — единственный файл.

---

## 1. Hero

### 1.1 Лейаут — 2 колонки
Добавить `.hero-inner` grid: `grid-template-columns: 1fr 480px`, gap 60px.
Левая колонка — текущий `.hero-content`.
Правая колонка — `.hero-video` с Kinescope iframe (Kabrita).
На мобайле (`max-width: 900px`) — правая колонка скрыта (`display: none`).

```html
<div class="hero-inner">
  <div class="hero-content">...</div>
  <div class="hero-video">
    <iframe src="https://kinescope.io/embed/b9LqTwdSKuvSTM2k3q5TpM"
      width="100%" style="aspect-ratio:16/9"
      allow="autoplay; fullscreen" allowfullscreen frameborder="0"></iframe>
  </div>
</div>
```

```css
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
}
.hero-video iframe { display: block; width: 100%; aspect-ratio: 16/9; border: none; }
@media (max-width: 900px) { .hero-video { display: none; } }
```

### 1.2 Строка клиентов
Добавить между `.hero-sub` и `.hero-ctas`:

```html
<div class="hero-clients">
  <span class="hero-clients-label">Работали с:</span>
  <span>Kabrita</span>
  <span>KGM Automotive</span>
  <span>PROCAR</span>
</div>
```

```css
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

HTML (с явными разделителями):
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

### 1.3 Главная кнопка — solid purple
Добавить `.btn-hero-primary` — solid purple, без `:: ::`, без `btn-primary` класса:

```css
.btn-hero-primary {
  background: var(--purple); color: #fff; border: none;
  padding: 14px 28px; font-size: 15px;
}
.btn-hero-primary:hover { background: #6930cc; transform: translateY(-1px); box-shadow: 0 8px 24px rgba(123,63,228,0.35); }
.btn-hero-primary::before, .btn-hero-primary::after { display: none; }
```

HTML: заменить в hero-ctas:
```html
<a href="#contact" class="btn btn-hero-primary">Обсудить задачу</a>
```

### 1.4 Подзаголовок — короче + контрастнее
Заменить текст `.hero-sub`:
```html
<p class="hero-sub">
  AI-видео и фото вместо студийного продакшна — без аренды локаций и съёмочной группы. Первый черновик за 48 часов.
</p>
```

CSS: `color: rgba(248,248,255,0.72)` (было 0.55).

---

## 2. Читаемость — CSS переменные

Обновить в `:root`:

```css
--text-2: rgba(248,248,255,0.72);    /* было 0.55 */
--text-dark-2: rgba(13,13,20,0.65);  /* было 0.55 */
--text-dark-3: rgba(13,13,20,0.40);  /* было 0.30 */
```

Обновить `.process-step p`:
```css
.process-step p { font-size: 15px; color: var(--text-2); line-height: 1.6; }
```

---

## 3. Карточки услуг

```css
.service-card {
  border-top: 2px solid var(--purple);
  box-shadow: 0 2px 12px rgba(0,0,0,0.06);
}
.service-card:hover {
  box-shadow: 0 16px 40px rgba(0,0,0,0.12);
  transform: translateY(-4px);
}
```

---

## 4. Карточки цен

### 4.1 Featured card — приподнять
```css
.pricing-card.featured {
  transform: translateY(-8px);
  box-shadow: 0 24px 60px rgba(123,63,228,0.14);
}
```

### 4.2 Строка сравнения под заголовком секции
Добавить в `.section-heading` секции pricing:
```html
<p class="pricing-context">Студийная съёмка от 80 000 ₽ за день. AI-продакшн — от 45 000 ₽ за готовый пакет.</p>
```

```css
.pricing-context {
  font-size: 13px; color: var(--text-dark-2); margin-top: 8px;
  font-style: italic;
}
```

---

## 5. Портфолио — видео вместо градиентов

### 5.1 Kabrita карточка
Заменить `.portfolio-cover.p-cover-2` на iframe:
```html
<div class="portfolio-cover portfolio-video">
  <iframe src="https://kinescope.io/embed/b9LqTwdSKuvSTM2k3q5TpM"
    allow="autoplay; fullscreen" allowfullscreen frameborder="0"></iframe>
  <div class="portfolio-cover-inner">
    <div class="p-tag">AI-видео · 🏆 Победитель</div>
    <div class="p-title">Kabrita × VIDMK Hackaton</div>
  </div>
</div>
```

### 5.2 KGM карточка
Заменить `.portfolio-cover.p-cover-6` на iframe:
```html
<div class="portfolio-cover portfolio-video">
  <iframe src="https://kinescope.io/embed/usf3Yks5jhxMjAZpEuSVJF"
    allow="autoplay; fullscreen" allowfullscreen frameborder="0"></iframe>
  <div class="portfolio-cover-inner">
    <div class="p-tag">AI-видео</div>
    <div class="p-title">KGM Automotive</div>
  </div>
</div>
```

### 5.3 CSS для video covers
```css
.portfolio-video {
  position: relative; aspect-ratio: 4/3;
  background: #000; overflow: hidden;
}
.portfolio-video iframe {
  position: absolute; inset: 0; width: 100%; height: 100%; border: none;
  pointer-events: none;  /* клик по карточке, не по iframe */
}
.portfolio-video .portfolio-cover-inner {
  position: absolute; bottom: 0; left: 0; right: 0; z-index: 2;
  background: linear-gradient(to top, rgba(8,8,15,0.9) 0%, transparent 60%);
  padding: 20px;
}
```

### 5.4 Остальные 4 карточки — типографическое превью
Вместо пустых CSS-градиентов добавить внутрь `.portfolio-cover` типографический контент:

PROCAR (p-cover-1, синий градиент):
```html
<div class="p-cover-text">
  <div class="p-cover-brand">PROCAR</div>
  <div class="p-cover-desc">BMW · Mercedes · Lamborghini · Porsche</div>
  <div class="p-cover-desc">Москва-Сити · Кремль · Набережная</div>
</div>
```

Барбер Сэм — Комиксы (p-cover-3, зелёный):
```html
<div class="p-cover-text">
  <div class="p-cover-brand">Барбер Сэм</div>
  <div class="p-cover-desc">Серия AI-комиксов · 6 историй</div>
  <div class="p-cover-desc">Персонаж с фото клиента</div>
</div>
```

Москитные сетки — Брендинг (p-cover-4, оранжевый):
```html
<div class="p-cover-text">
  <div class="p-cover-brand">vse-okna.com</div>
  <div class="p-cover-desc">Брендирование авто · AI-мокап</div>
  <div class="p-cover-desc">Согласован → уже на дороге</div>
</div>
```

Цветочный магазин — Комиксы (p-cover-5, пурпурный):
```html
<div class="p-cover-text">
  <div class="p-cover-brand">Цветочный</div>
  <div class="p-cover-desc">3 сценария · 3 типа покупателей</div>
  <div class="p-cover-desc">«Это прямо про меня» — клиенты</div>
</div>
```

```css
.p-cover-text {
  position: relative; z-index: 1; padding: 24px;
  display: flex; flex-direction: column; justify-content: flex-end; height: 100%;
}
.p-cover-brand {
  font-family: 'Space Grotesk', sans-serif; font-size: 28px; font-weight: 800;
  color: rgba(255,255,255,0.9); letter-spacing: -0.02em; margin-bottom: 6px;
}
.p-cover-desc { font-size: 12px; color: rgba(255,255,255,0.5); line-height: 1.6; }
```

---

## 6. Отзывы — аватары

Заменить `.author-avatar` на уникальные цвета и добавить border:

```css
.author-avatar {
  border: 1px solid rgba(255,255,255,0.12);  /* добавить */
}
```

Цвета по инициалам (через `style="background: ..."`):
| Аватар | Цвет |
|--------|------|
| ПК (PROCAR) | `#1a4a8a` |
| МС (Москитные сетки) | `#2d5a2d` |
| С (Барбер Сэм) | `#8B4500` |
| VK (Hackaton) | `#4a1a8a` |
| ЦМ (Цветочный) | `#7a3a7a` |

---

## Что НЕ меняется
- Структура секций и их порядок
- Русский язык
- `//` badges и `:: ::` кнопки (кроме hero CTA)
- Цвета: `--purple: #7B3FE4`, `--lime: #D7FF00`
- Все тексты и копирайтинг
- FAQ, Contact, Footer — без изменений
