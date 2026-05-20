# Розділ 2. Оптимізація зображень (Крок 3)

## 2.1. Інвентаризація зображень (ДО)

| № | Сторінка | URL / файл (до) | Формат | Розмір | Роздільність | alt | width/height |
|---|----------|-----------------|--------|--------|--------------|-----|--------------|
| 1 | index.html | `https://picsum.photos/900/300?random=1` | JPEG (CDN) | ~20 КБ* | 900×300 | ✅ | ✅ |
| 2 | blog-seo-audit.html | `https://picsum.photos/800/400?random=2` | JPEG (CDN) | ~48 КБ* | 800×400 | ✅ | ✅ |
| 3 | blog-redirects.html | — (лише в JSON-LD) | JPEG (CDN) | ~29 КБ* | 800×400 | — | — |

\* Розмір знято після завантаження оригіналу з picsum.photos для порівняння (локальні копії в `images/*.jpg`).

**Проблеми до оптимізації:**
- Зовнішній хостинг зображень (додатковий DNS, TLS, затримка TTFB/LCP).
- Формат JPEG без WebP.
- Немає `<picture>` з fallback.
- На `blog-redirects.html` не було видимого `<img>` у контенті.

---

## 2.2. Процес оптимізації

**Інструмент:** [Squoosh](https://squoosh.app/) / CLI `cwebp` (якість 75–82%).

**Дії:**
1. Завантажено оригінали у папку `/images/`.
2. Конвертовано у **WebP** (якість 82 для hero, 75 для article-seo-audit, 82 для article-redirects).
3. Збережено **JPEG** як резервний формат для `<picture>`.
4. Оновлено HTML: `<picture>` + `<source type="image/webp">` + `<img>` з `width`/`height`.
5. Оновлено URL у JSON-LD Article на абсолютні посилання на `.webp`.

---

## 2.3. Таблиця порівняння «до / після»

| Файл | Сторінка | Формат до | Розмір до | Формат після | Розмір після (WebP) | Зменшення |
|------|----------|-----------|-----------|--------------|---------------------|-----------|
| hero | index.html | JPEG (CDN) | 20,2 КБ | WebP + JPEG fallback | **14,0 КБ** | **31%** |
| article-seo-audit | blog-seo-audit.html | JPEG (CDN) | 48,3 КБ | WebP + JPEG fallback | **35,9 КБ** | **26%** |
| article-redirects | blog-redirects.html | JPEG (CDN) | 28,7 КБ | WebP + JPEG fallback | **24,0 КБ** | **16%** |

**Сумарно (локальні файли):** ~97 КБ JPEG → ~74 КБ WebP (**≈24% менше**).

---

## 2.4. Приклад оновленого HTML

### Головна (hero, без lazy loading — above the fold)

```html
<picture>
  <source srcset="images/hero.webp" type="image/webp">
  <img src="images/hero.jpg"
       alt="Демонстраційне зображення SEO аудиту сайту"
       width="900"
       height="300">
</picture>
```

### Стаття блогу

```html
<picture>
  <source srcset="images/article-seo-audit.webp" type="image/webp">
  <img src="images/article-seo-audit.jpg"
       alt="Ілюстрація до статті про SEO аудит сайту"
       width="800"
       height="400">
</picture>
```

---

## 2.5. Очікуваний вплив на CWV

| Метрика | Очікування |
|---------|------------|
| **LCP** | Покращення за рахунок меншого файлу WebP та хостингу на GitHub Pages (той самий домен) |
| **CLS** | Без змін (width/height збережено) |
| **FCP** | Незначне покращення через менший обсяг даних |

📸 **Скріншоти для звіту:**
1. Squoosh / cwebp — порівняння розміру до/після  
2. DevTools → Network → Img (тип webp на підтримуваних браузерах)  
3. Сторінка index.html після деплою  

---

## 2.6. Висновок розділу 2

Виконано конвертацію **3 зображень** у **WebP** з резервним JPEG, імплементовано `<picture>`, зображення перенесено на **локальний хостинг** репозиторію. Підтверджено зменшення розміру файлів на **16–31%**. Наступний крок лабораторної — **lazy loading** для зображень нижче першого екрана (крок 4).
