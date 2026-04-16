# Style Redesign Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Переработать визуальный стиль index.html — редакционная типографика (// :: символы), чередование тёмных/светлых секций, лайм #D7FF00 на двух элементах.

**Architecture:** Все изменения в одном файле `index.html`. CSS-переменные обновляются в `:root`, затем каждая секция переводится на нужный фон с соответствующими цветами текста. Новые стили badge и button добавляются, старые — заменяются.

**Tech Stack:** Vanilla HTML/CSS, Google Fonts (Space Grotesk + Inter)

---

### Task 1: Обновить CSS-переменные и базовые стили

**Files:**
- Modify: `index.html` — блок `:root` и `.badge`, `.btn`

- [ ] **Шаг 1: Обновить `:root` — добавить новые переменные, убрать cyan**

Найти блок `:root { ... }` и заменить полностью:

```css
:root {
  --bg: #08080F;
  --bg-light: #F5F4F0;
  --bg-2: #0F0F1A;
  --card: rgba(255,255,255,0.04);
  --card-light: rgba(255,255,255,0.85);
  --border: rgba(255,255,255,0.08);
  --border-md: rgba(255,255,255,0.12);
  --border-accent: rgba(123,63,228,0.4);
  --border-light: rgba(0,0,0,0.08);
  --text: #F8F8FF;
  --text-2: rgba(248,248,255,0.55);
  --text-3: rgba(248,248,255,0.30);
  --text-dark: #0D0D14;
  --text-dark-2: rgba(13,13,20,0.55);
  --text-dark-3: rgba(13,13,20,0.30);
  --purple: #7B3FE4;
  --lime: #D7FF00;
  --radius-sm: 6px;
  --radius-md: 10px;
  --radius-lg: 10px;
  --radius-full: 100px;
}
```

- [ ] **Шаг 2: Заменить стиль `.badge` на редакционный `//` формат**

Найти блок `/* ─── BADGE ─── */` и заменить:

```css
/* ─── BADGE ─── */
.badge {
  display: inline-flex; align-items: center; gap: 0;
  color: var(--purple);
  font-size: 11px; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase;
  margin-bottom: 20px;
  font-family: 'Space Grotesk', sans-serif;
}
.badge::before { content: '// '; color: var(--purple); opacity: 0.7; }

/* Badge на светлом фоне */
.badge-light {
  display: inline-flex; align-items: center;
  color: var(--purple);
  font-size: 11px; font-weight: 700; letter-spacing: 0.1em; text-transform: uppercase;
  margin-bottom: 20px;
  font-family: 'Space Grotesk', sans-serif;
}
.badge-light::before { content: '// '; color: var(--purple); opacity: 0.6; }
```

- [ ] **Шаг 3: Обновить стили кнопок**

Найти `/* ─── BUTTONS ─── */` и заменить:

```css
/* ─── BUTTONS ─── */
.btn {
  display: inline-flex; align-items: center; gap: 8px;
  padding: 12px 24px; border-radius: 4px;
  font-family: 'Space Grotesk', sans-serif; font-size: 14px; font-weight: 700;
  cursor: pointer; transition: all 0.2s ease; border: none;
  letter-spacing: 0.02em;
}
/* Кнопка на тёмном: :: текст :: */
.btn-primary {
  background: transparent; color: var(--text);
  border: 1px solid rgba(123,63,228,0.5);
  position: relative;
}
.btn-primary::before { content: ':: '; color: var(--purple); opacity: 0.8; }
.btn-primary::after  { content: ' ::'; color: var(--purple); opacity: 0.8; }
.btn-primary:hover { background: rgba(123,63,228,0.12); border-color: rgba(123,63,228,0.8); }

/* Кнопка на светлом: сплошная фиолетовая */
.btn-primary-light {
  background: var(--purple); color: #fff;
  border-radius: 4px;
}
.btn-primary-light:hover { background: #6930cc; }

.btn-secondary {
  background: transparent; color: var(--text);
  border: 1px solid var(--border-md);
  border-radius: 4px;
}
.btn-secondary:hover { border-color: rgba(255,255,255,0.3); background: rgba(255,255,255,0.05); }

/* Вторичная на светлом */
.btn-secondary-light {
  background: transparent; color: var(--text-dark);
  border: 1px solid rgba(0,0,0,0.15);
  border-radius: 4px;
  font-family: 'Space Grotesk', sans-serif; font-size: 14px; font-weight: 600;
  padding: 12px 24px; cursor: pointer; transition: all 0.2s; display: inline-flex;
}
.btn-secondary-light:hover { border-color: rgba(0,0,0,0.3); }
```

- [ ] **Шаг 4: Обновить `.card` — радиус и убрать cyan из hover**

```css
.card {
  background: var(--card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  transition: border-color 0.3s ease, box-shadow 0.3s ease;
}
.card:hover { border-color: var(--border-accent); box-shadow: 0 0 24px rgba(123,63,228,0.08); }
```

- [ ] **Шаг 5: Проверить в браузере — открыть index.html**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: страница загружается, нет console errors.

---

### Task 2: Секция Hero — тёмная, бейдж лайм для хакатона, новые кнопки

**Files:**
- Modify: `index.html` — секция `<!-- ═══════════ HERO ═══════════ -->`

- [ ] **Шаг 1: Обновить badge в hero**

Найти:
```html
<div class="badge">AI-продакшн для бизнеса</div>
```
Заменить:
```html
<div class="badge">AI-продакшн для бизнеса</div>
```
*(badge уже обновлён стилями в Task 1 — визуально изменится автоматически)*

- [ ] **Шаг 2: Обновить кнопки hero**

Найти:
```html
<a href="#contact" class="btn btn-primary">Обсудить задачу</a>
<a href="#portfolio" class="btn btn-secondary">Смотреть примеры →</a>
```
Заменить:
```html
<a href="#contact" class="btn btn-primary">Обсудить задачу</a>
<a href="#portfolio" class="btn btn-secondary">Смотреть примеры</a>
```

- [ ] **Шаг 3: Заменить hero-award на лайм-бейдж**

Найти весь блок `.hero-award`:
```html
<div class="hero-award">
  <div class="hero-award-icon">🏆</div>
  Победитель VIDMK Hackaton · Номинация AI Realism
</div>
```
Заменить:
```html
<div class="hero-award">
  <div class="hero-award-icon">🏆</div>
  Победитель VIDMK Hackaton · Номинация AI Realism
</div>
```

- [ ] **Шаг 4: Обновить CSS `.hero-award` на лайм**

Найти блок `.hero-award { ... }` и `.hero-award-icon { ... }` и заменить:

```css
.hero-award {
  display: inline-flex; align-items: center; gap: 12px;
  background: rgba(215,255,0,0.07);
  border: 1px solid rgba(215,255,0,0.2);
  border-radius: 6px;
  padding: 10px 16px; font-size: 13px; color: var(--lime);
  font-family: 'Space Grotesk', sans-serif; font-weight: 600;
}
.hero-award-icon {
  width: 28px; height: 28px; border-radius: 4px;
  background: rgba(215,255,0,0.15);
  display: flex; align-items: center; justify-content: center; font-size: 14px;
  flex-shrink: 0;
}
```

- [ ] **Шаг 5: Проверить hero в браузере**

Ожидание: badge показывает `// AI-продакшн для бизнеса`, кнопка обёрнута `::`, award-бейдж лаймовый.

---

### Task 3: Светлые секции — Stats и Services

**Files:**
- Modify: `index.html` — секции stats и services, добавить CSS для светлых секций

- [ ] **Шаг 1: Добавить CSS для светлых секций**

После блока `/* ══════════════════════════════ STATS */` добавить в `<style>`:

```css
/* ─── LIGHT SECTION BASE ─── */
.section-light { background: var(--bg-light); }
.section-light .badge,
.section-light .badge-light { color: var(--purple); }
.section-light .badge::before,
.section-light .badge-light::before { color: var(--purple); }
.section-light .section-heading h2 { color: var(--text-dark); }
.section-light .section-heading p { color: var(--text-dark-2); }
```

- [ ] **Шаг 2: Перевести Stats на светлый фон**

Найти:
```html
<div class="stats" id="stats">
```
Заменить:
```html
<div class="stats section-light" id="stats">
```

- [ ] **Шаг 3: Обновить CSS `.stats` и `.stat-number`**

Найти блок `/* ══════════════════════════════ STATS */` и добавить/обновить:

```css
.stats {
  border-top: 1px solid rgba(0,0,0,0.08);
  border-bottom: 1px solid rgba(0,0,0,0.08);
  padding: 40px 0;
}
.stat-item {
  text-align: center; padding: 20px;
  border-right: 1px solid rgba(0,0,0,0.08);
}
.stat-item:last-child { border-right: none; }
.stat-number {
  font-family: 'Space Grotesk', sans-serif;
  font-size: clamp(36px, 4vw, 52px); font-weight: 700;
  color: var(--text-dark);
  line-height: 1;
  background: none; -webkit-background-clip: unset; -webkit-text-fill-color: unset; background-clip: unset;
}
.stat-label { font-size: 13px; color: var(--text-dark-2); margin-top: 8px; }
```

- [ ] **Шаг 4: Перевести Services на светлый фон**

Найти:
```html
<section class="section" id="services">
```
Заменить:
```html
<section class="section section-light" id="services">
```

- [ ] **Шаг 5: Обновить CSS карточек услуг для светлого фона**

Найти блок `/* ══════════════════════════════ SERVICES */` и обновить `.service-card`:

```css
.service-card {
  padding: 28px; border-radius: 8px;
  background: #fff; border: 1px solid rgba(0,0,0,0.08);
  transition: all 0.3s ease; cursor: default;
}
.service-card:hover {
  border-color: rgba(123,63,228,0.3);
  transform: translateY(-3px);
  box-shadow: 0 12px 32px rgba(0,0,0,0.08);
}
.service-card.wide { grid-column: span 2; }
.service-icon {
  width: 44px; height: 44px; border-radius: 8px;
  background: rgba(123,63,228,0.08); border: 1px solid rgba(123,63,228,0.15);
  display: flex; align-items: center; justify-content: center;
  font-size: 20px; margin-bottom: 18px;
}
.service-card h3 { font-size: 17px; font-weight: 700; margin-bottom: 8px; color: var(--text-dark); }
.service-card p { font-size: 14px; color: var(--text-dark-2); line-height: 1.6; }
.service-tag {
  display: inline-block; margin-top: 14px;
  font-size: 10px; font-weight: 700; letter-spacing: 0.08em; text-transform: uppercase;
  color: var(--purple); opacity: 0.7;
}
```

- [ ] **Шаг 6: Проверить в браузере**

Ожидание: Stats и Services — светло-бежевый фон, тёмный текст, карточки белые.

---

### Task 4: Тёмные секции — Process и Portfolio (без изменений фона, обновить детали)

**Files:**
- Modify: `index.html` — CSS процесса и портфолио

- [ ] **Шаг 1: Обновить `.process` — убрать bg-2, использовать основной тёмный**

Найти:
```css
.process { background: var(--bg-2); }
```
Заменить:
```css
.process { background: var(--bg); }
```

- [ ] **Шаг 2: Обновить `.step-number` — убрать gradient border**

Найти блок `.step-number { ... }` и заменить:

```css
.step-number {
  width: 52px; height: 52px; border-radius: 50%;
  background: var(--bg); border: 1px solid rgba(123,63,228,0.35);
  display: flex; align-items: center; justify-content: center;
  font-family: 'Space Grotesk', sans-serif; font-size: 16px; font-weight: 800;
  color: var(--lime); margin: 0 auto 24px; position: relative; z-index: 1;
}
```

- [ ] **Шаг 3: Обновить `.stat-number` — counter animation совместимость**

В JavaScript найти строку:
```js
el.textContent = Math.floor(ease * target) + (progress === 1 ? suffix : '');
```
Оставить как есть — counter работает с textContent, цвет управляется CSS.

- [ ] **Шаг 4: Проверить в браузере**

Ожидание: Process — тёмный фон, номера шагов лаймовые. Portfolio — без изменений.

---

### Task 5: Светлые секции — Cases и Pricing

**Files:**
- Modify: `index.html` — секции cases и pricing

- [ ] **Шаг 1: Перевести Cases на светлый фон**

Найти:
```html
<section class="section cases" id="cases">
```
Заменить:
```html
<section class="section section-light" id="cases">
```

- [ ] **Шаг 2: Обновить CSS кейсов для светлого фона**

Найти блок `/* ══════════════════════════════ CASE STUDIES */` и обновить:

```css
.cases { }
.case-card {
  display: grid; grid-template-columns: 320px 1fr;
  border-radius: 8px; overflow: hidden;
  border: 1px solid rgba(0,0,0,0.08);
  transition: all 0.3s ease;
}
.case-card:hover { border-color: rgba(123,63,228,0.3); box-shadow: 0 16px 40px rgba(0,0,0,0.1); }
.case-body { padding: 36px; background: #fff; }
.case-meta-item span { display: block; color: var(--text-dark-3); margin-bottom: 2px; }
.case-meta-item strong { color: var(--text-dark); font-weight: 600; }
.case-body h3 { font-size: 21px; margin-bottom: 12px; color: var(--text-dark); }
.case-body p { font-size: 14px; color: var(--text-dark-2); line-height: 1.7; margin-bottom: 24px; }
.case-stat strong {
  font-family: 'Space Grotesk', sans-serif; font-size: 22px; font-weight: 700;
  color: var(--purple); display: block;
}
.case-stat span { font-size: 12px; color: var(--text-dark-3); }
.case-link { font-size: 14px; font-weight: 700; color: var(--purple); display: inline-flex; align-items: center; gap: 6px; transition: gap 0.2s; }
.case-link:hover { gap: 10px; }
```

- [ ] **Шаг 3: Перевести Pricing на светлый фон**

Найти:
```html
<section class="section" id="pricing" style="background: var(--bg-2);">
```
Заменить:
```html
<section class="section section-light" id="pricing">
```

- [ ] **Шаг 4: Обновить CSS ценовых карточек для светлого фона**

Найти `/* ══════════════════════════════ PRICING */` и обновить:

```css
.pricing-card {
  padding: 32px; border-radius: 8px;
  background: #fff; border: 1px solid rgba(0,0,0,0.08);
  position: relative;
}
.pricing-card.featured {
  border-color: rgba(123,63,228,0.4);
  background: #fff;
  box-shadow: 0 0 32px rgba(123,63,228,0.08);
}
.pricing-name { font-family: 'Space Grotesk', sans-serif; font-size: 12px; font-weight: 700; color: var(--text-dark-2); margin-bottom: 8px; text-transform: uppercase; letter-spacing: 0.06em; }
.pricing-price { font-family: 'Space Grotesk', sans-serif; font-size: 36px; font-weight: 800; color: var(--text-dark); margin-bottom: 4px; line-height: 1; }
.pricing-price span { font-size: 15px; font-weight: 500; color: var(--text-dark-2); }
.pricing-period { font-size: 13px; color: var(--text-dark-3); margin-bottom: 12px; }
.pricing-for-whom { font-size: 13px; color: var(--text-dark-2); margin-bottom: 20px; line-height: 1.5; border-left: 2px solid rgba(123,63,228,0.3); padding-left: 12px; }
.pricing-divider { border: none; border-top: 1px solid rgba(0,0,0,0.08); margin-bottom: 20px; }
.pricing-features li { font-size: 14px; color: var(--text-dark-2); display: flex; align-items: flex-start; gap: 10px; }
.pricing-features li::before { content: '✓'; color: var(--purple); font-weight: 700; flex-shrink: 0; }
.pricing-note { text-align: center; margin-top: 28px; font-size: 13px; color: var(--text-dark-3); }
```

- [ ] **Шаг 5: Заменить `.pricing-popular` на лайм**

Найти:
```css
.pricing-popular {
  position: absolute; top: -14px; left: 50%; transform: translateX(-50%);
  background: var(--gradient); color: #fff;
  font-size: 12px; font-weight: 700; padding: 4px 16px; border-radius: var(--radius-full);
  white-space: nowrap;
}
```
Заменить:
```css
.pricing-popular {
  position: absolute; top: -13px; left: 50%; transform: translateX(-50%);
  background: var(--lime); color: #0D0D14;
  font-size: 11px; font-weight: 800; padding: 4px 14px; border-radius: 3px;
  white-space: nowrap; letter-spacing: 0.04em;
  font-family: 'Space Grotesk', sans-serif;
}
```

- [ ] **Шаг 6: Обновить кнопки в pricing на светлые версии**

Найти в HTML секции pricing все кнопки и обновить классы:

```html
<!-- Tier 1 -->
<a href="#contact" class="btn btn-secondary-light pricing-btn">Начать с проекта</a>

<!-- Tier 2 (featured) -->
<a href="#contact" class="btn btn-primary-light pricing-btn">Обсудить ретейн</a>

<!-- Tier 3 -->
<a href="#contact" class="btn btn-secondary-light pricing-btn">Обсудить сотрудничество</a>
```

- [ ] **Шаг 7: Проверить Cases и Pricing в браузере**

Ожидание: Cases — светлый фон, белые карточки кейсов; Pricing — светлый фон, белые карточки, лайм-тег "Основной формат".

---

### Task 6: FAQ и Contact — обновить детали на тёмном

**Files:**
- Modify: `index.html` — CSS FAQ и Contact

- [ ] **Шаг 1: Убрать gradient из Contact background**

Найти:
```css
.contact {
  background: linear-gradient(135deg, rgba(123,63,228,0.08) 0%, rgba(0,212,255,0.05) 100%);
  border-top: 1px solid var(--border);
}
```
Заменить:
```css
.contact {
  background: var(--bg);
  border-top: 1px solid var(--border);
}
```

- [ ] **Шаг 2: Убрать gradient из кнопки формы**

Проверить кнопку в Contact форме — она уже использует `btn btn-primary`, что теперь редакционный `:: ::` стиль на тёмном.

- [ ] **Шаг 3: Обновить `.nav-btn` — убрать gradient**

Найти в HTML:
```html
<a href="#contact" class="btn btn-primary nav-btn">Обсудить задачу</a>
```
CSS `.nav-btn` уже наследует `btn-primary`. Но в навигации нужна немного другая кнопка — добавить отдельный стиль:

```css
.nav-btn {
  padding: 8px 18px; font-size: 13px;
  background: var(--purple) !important; color: #fff !important;
  border: none !important;
}
.nav-btn::before, .nav-btn::after { display: none !important; }
.nav-btn:hover { background: #6930cc !important; }
```

- [ ] **Шаг 4: Финальная проверка — прокрутить весь сайт**

Ожидание:
- Тёмные секции: Hero, Process, Portfolio, Testimonials, FAQ, Contact, Footer
- Светлые секции: Stats, Services, Cases, Pricing
- Лайм: award-бейдж в hero, тег "Основной формат" в ценах
- Нигде нет cyan `#00D4FF`
- Нигде нет purple→cyan градиента
- Кнопки на тёмном: `:: текст ::`
- Кнопки на светлом: сплошные фиолетовые или обводка

- [ ] **Шаг 5: Убрать `--gradient` из оставшихся мест**

Найти в HTML все упоминания `var(--gradient)` через Grep и заменить:
- В `.nav-logo-mark`: `background: var(--purple)`
- В `.author-avatar`: `background: var(--purple)`
- В `.gradient-text` (hero h1): заменить на просто цвет `color: var(--purple); -webkit-text-fill-color: var(--purple)`

---

### Task 7: Финальная чистка и проверка

**Files:**
- Modify: `index.html`

- [ ] **Шаг 1: Удалить переменную `--gradient` из `:root`**

Убедиться что в `:root` нет строки `--gradient: ...` (уже удалено в Task 1).

- [ ] **Шаг 2: Grep на cyan**

```bash
grep -n "00D4FF\|cyan\|var(--cyan)" /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: 0 результатов. Если есть — заменить на `var(--purple)` или убрать.

- [ ] **Шаг 3: Grep на gradient**

```bash
grep -n "linear-gradient\|var(--gradient)" /Users/shantropa/Desktop/vsCode/index.html
```

Ожидание: только aurora-эффекты в hero (они допустимы с прозрачностью) и больше ничего критичного.

- [ ] **Шаг 4: Проверить мобильную вёрстку**

В браузере открыть DevTools → переключить на мобильный вид (375px).
Ожидание: светлые/тёмные секции корректно отображаются, текст читаем.

- [ ] **Шаг 5: Открыть финальную версию**

```bash
open /Users/shantropa/Desktop/vsCode/index.html
```

Прокрутить весь сайт, убедиться в консистентности стиля.
