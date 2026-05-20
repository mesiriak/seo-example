# Розділ 1. Базовий аудит сайту (ДО оптимізації)

## 1.1. Опис об'єкта дослідження

| Параметр | Значення |
|----------|----------|
| **Назва** | SEO Demo Site |
| **URL** | https://mesiriak.github.io/seo-example/ |
| **Тестована сторінка** | https://mesiriak.github.io/seo-example/index.html |
| **Тип сайту** | Навчальний статичний вебсайт |
| **Технологія** | HTML/CSS, GitHub Pages |
| **Дата аудиту** | 20.05.2026 |
| **Інструмент** | Google PageSpeed Insights (Lab Data) |

**Примітка:** у розділі «Discover what your real users are experiencing» відображається **No Data** — недостатньо польових даних (CrUX) для цього URL. У звіті використовуються **лабораторні показники** (Lighthouse).

---

## 1.2. Загальні оцінки Lighthouse (ДО)

| Категорія | Mobile | Desktop |
|-----------|--------|---------|
| Performance | 98 | 100 |
| Accessibility | 100 | 100 |
| Best Practices | 92 | 100 |
| SEO | 100 | 100 |

📸 *Скріншот 1.1 — PageSpeed Insights, Mobile (до оптимізації)*  
📸 *Скріншот 1.2 — PageSpeed Insights, Desktop (до оптимізації)*

---

## 1.3. Core Web Vitals та метрики продуктивності (ДО)

| Метрика | Mobile (до) | Оцінка Mobile | Desktop (до) | Оцінка Desktop | Норма (добре) |
|---------|-------------|---------------|--------------|----------------|---------------|
| **Performance Score** | 98 | ✅ | 100 | ✅ | 90+ |
| **LCP** (Largest Contentful Paint) | 2,4 с | ✅ | 0,7 с | ✅ | ≤ 2,5 с |
| **INP** (Interaction to Next Paint) | — * | — | — * | — | ≤ 200 мс |
| **CLS** (Cumulative Layout Shift) | 0 | ✅ | 0 | ✅ | ≤ 0,1 |
| **FCP** (First Contentful Paint) | 0,8 с | ✅ | 0,2 с | ✅ | ≤ 1,8 с |
| **TTFB** (Time to First Byte) | — ** | — | — ** | — | ≤ 800 мс |
| **TBT** (Total Blocking Time) | 0 мс | ✅ | 0 мс | ✅ | низький |
| **Speed Index** | 2,0 с | ✅ | 0,4 с | ✅ | низький |

\* На скріншоті PageSpeed для цієї сторінки у блоці метрик відображено **TBT** замість INP; INP у Field Data відсутній (No Data).  
\** TTFB на зведеному екрані не виведено окремо — за потреби переглянути розділ **Diagnostics** у PSI.

### Інтерпретація

- **Mobile LCP 2,4 с** — у зеленій зоні, близько до верхньої межі «добре» (2,5 с); головний кандидат на покращення після оптимізації зображень — hero-зображення (picsum.photos).
- **Desktop** — усі ключові метрики в зеленій зоні, Performance 100.
- **CLS 0** на обох пристроях — макет стабільний (частково завдяки `width`/`height` на частині зображень або малому контенту above the fold).
- **Best Practices 92 (Mobile)** — можливі дрібні зауваження Lighthouse (перевірити вкладку Best Practices у повному звіті PSI).

---

## 1.4. Додаткові категорії (ДО)

| Показник | Mobile | Desktop |
|----------|--------|---------|
| Accessibility | 100 | 100 |
| SEO (Lighthouse) | 100 | 100 |
| Best Practices | 92 | 100 |

---

## 1.5. Рекомендації PageSpeed (Opportunities / Diagnostics) — ДО

*Заповнити після розгортання розділів «Improve performance» / «Opportunities» у PSI. Типові для сайтів з зовнішніми зображеннями:*

| № | Рекомендація PSI | Статус на сайті (ймовірно) | План оптимізації (лаб. 03) |
|---|------------------|----------------------------|-----------------------------|
| 1 | Serve images in next-gen formats (WebP/AVIF) | Зображення з picsum.photos (JPEG) | Крок 3 — WebP + `<picture>` |
| 2 | Properly size images | Зовнішні URL, можливе надлишкове роздільність | Крок 3 — локальні WebP, width/height |
| 3 | Defer offscreen images | Не всі img з `loading="lazy"` | Крок 4 — lazy loading |
| 4 | Reduce unused CSS | Мінімальний CSS | Моніторинг |
| 5 | Efficient cache policy | GitHub Pages CDN | Обмежено налаштуванням хостингу |

📸 *Скріншот 1.3 — блок Opportunities / Diagnostics (Mobile або Desktop)*

---

## 1.6. Висновок розділу 1 (базовий аудит ДО)

До технічної оптимізації сайт **SEO Demo Site** показує **високі лабораторні показники**: Performance 98–100, LCP у нормі (на Mobile — 2,4 с), CLS 0. Основний резерв покращення — **оптимізація зображень** (зовнішній picsum, формат JPEG, lazy loading) для закріплення Mobile LCP нижче 2,0 с та підготовки до польових даних у GSC. Польові дані Core Web Vitals на момент аудиту **відсутні** (No Data).
