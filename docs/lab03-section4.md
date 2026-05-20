# Розділ 4. Lazy loading зображень

## 4.1. Принцип та правила застосування

**Lazy loading** (`loading="lazy"`) — браузер завантажує зображення лише коли воно наближається до viewport, зменшуючи початковий обсяг даних і покращуючи LCP для контенту **above the fold**.

| Правило | Застосування на SEO Demo Site |
|---------|------------------------------|
| **Не** використовувати lazy на LCP-зображенні | Hero на `index.html` — без `loading="lazy"`, додано `fetchpriority="high"` |
| **Не** lazy на першому великому img статті | `blog-seo-audit.html`, `blog-redirects.html` — головне `<picture>` без lazy |
| **Застосовувати** lazy нижче fold | Превʼю статей на `index.html` та `blog.html` |
| Завжди `width` + `height` | Усі `<img>` — для зниження CLS |
| WebP через `<picture>` | Превʼю також у WebP + JPEG fallback |

---

## 4.2. Таблиця зображень: lazy loading та обґрунтування

| № | Сторінка | Зображення | Файл | `loading="lazy"` | Обґрунтування |
|---|----------|------------|------|------------------|---------------|
| 1 | index.html | Hero (above the fold) | hero.webp / hero.jpg | **Ні** | Кандидат на **LCP**; lazy затримував би завантаження |
| 2 | index.html | Превʼю статті SEO аудит | thumb-seo-audit.webp | **Так** | Секція «Останні статті» — нижче першого екрану |
| 3 | index.html | Превʼю статті redirect | thumb-redirects.webp | **Так** | Нижче fold |
| 4 | blog.html | Превʼю SEO аудит | thumb-seo-audit.webp | **Так** | Після заголовка H2 і тексту — зазвичай below fold |
| 5 | blog.html | Превʼю redirect | thumb-redirects.webp | **Так** | Друга картка — нижче fold |
| 6 | blog-seo-audit.html | Ілюстрація статті | article-seo-audit.webp | **Ні** | Перше велике зображення на сторінці → **LCP** |
| 7 | blog-redirects.html | Ілюстрація статті | article-redirects.webp | **Ні** | Перше велике зображення на сторінці → **LCP** |

**Додатково:** на lazy-зображеннях — `decoding="async"` (не блокує рендер тексту).

---

## 4.3. Приклади HTML-коду

### Без lazy (hero, LCP)

```html
<picture>
  <source srcset="images/hero.webp" type="image/webp">
  <img src="images/hero.jpg"
       alt="Демонстраційне зображення SEO аудиту сайту"
       width="900"
       height="300"
       fetchpriority="high">
</picture>
```

### З lazy (превʼю нижче fold)

```html
<picture>
  <source srcset="images/thumb-seo-audit.webp" type="image/webp">
  <img class="card-preview-img"
       src="images/thumb-seo-audit.jpg"
       alt="Превʼю статті про SEO аудит"
       width="400"
       height="200"
       loading="lazy"
       decoding="async">
</picture>
```

---

## 4.4. Перевірка в браузері (DevTools)

**Порядок дій для скріншоту звіту:**

1. Відкрити `https://mesiriak.github.io/seo-example/index.html`
2. **F12** → вкладка **Network** → фільтр **Img**
3. **Ctrl+Shift+R** (hard refresh)
4. **До прокрутки:** у списку має з’явитись переважно **hero** (webp/jpg), без thumb-файлів
5. **Прокрутити** до блоку «Останні статті блогу»
6. **Після прокрутки:** з’являються запити `thumb-seo-audit.webp`, `thumb-redirects.webp`

| Етап | Очікуваний результат |
|------|----------------------|
| Завантаження сторінки | 1–2 img (hero) |
| Прокрутка вниз | +2 img (thumbnails) |
| Lazy працює | Thumb **не** в Network до scroll |

📸 **Скріншот 4.1** — Network / Img одразу після reload (лише hero)  
📸 **Скріншот 4.2** — Network / Img після прокрутки (з’явились thumb)

**Альтернатива:** Elements → обрати `<img loading="lazy">` → у DevTools побачити відкладене завантаження.

---

## 4.5. Порівняння до / після (lazy loading)

| Параметр | До (крок 3) | Після (крок 4) |
|----------|-------------|----------------|
| `loading="lazy"` | Ніде | 4 зображення (превʼю) |
| Початкове завантаження img на index | 1 (hero) | 1 (hero) |
| Img на blog.html | 0 | 2 (lazy, після scroll) |
| LCP-зображення з lazy | — | Свідомо **без** lazy |
| `fetchpriority="high"` на hero | Ні | Так |

---

## 4.6. Висновок розділу 4

На сайті налаштовано **нативний lazy loading** для 4 превʼю-зображень нижче першого екрану. **Hero** та **ілюстрації в статтях** залишено без lazy, щоб не погіршувати **LCP**. Перевірка через DevTools Network підтверджує відкладене завантаження thumb до моменту прокрутки. У поєднанні з WebP (розділ 2) це зменшує початковий payload і покращує сприйняття швидкості сторінки.
