# SEO Demo Site

Навчальний багатосторінковий сайт для лабораторних робіт з SEO (технічний аудит, on-page оптимізація).

**Публічний URL (після GitHub Pages):** `https://mesiriak.github.io/seo-example/`

## Структура сайту (16 сторінок)

| Сторінка | URL | Призначення |
|----------|-----|-------------|
| Головна | `index.html` | Hub, WebSite schema |
| Послуги | `services.html` | Каталог послуг |
| Блог | `blog.html` | Список статей |
| Про нас | `about.html` | Допоміжна |
| Контакти | `contacts.html` | ContactPage schema |
| FAQ | `faq.html` | FAQPage JSON-LD |
| Політика | `privacy.html` | Допоміжна |
| Стаття: SEO аудит | `blog-seo-audit.html` | Article JSON-LD |
| Стаття: Redirect | `blog-redirects.html` | Article JSON-LD |
| Технічний аудит | `service-technical-audit.html` | Service schema |
| On-page SEO | `service-onpage.html` | Service schema |
| Link Building | `service-linkbuilding.html` | Service schema |
| Рівень 1–4 | `level1.html` … `folder/subfolder/deep/level4.html` | Crawl depth |

## Деплой на GitHub Pages

1. Settings → Pages → Source: **Deploy from branch** → `master` / `/ (root)`
2. Дочекайтесь URL `https://mesiriak.github.io/seo-example/`
3. Перевірте Rich Results Test для `faq.html` та `blog-seo-audit.html`

## Лабораторна 02

- Метадані вже оптимізовані за SEO-формулами (можна зробити скріни «після»)
- Для звіту «до» — збережіть старий `index.html` з git history або зробіть скрін до змін
- JSON-LD: FAQPage, Article (×2), Service (×3), WebSite, ContactPage
