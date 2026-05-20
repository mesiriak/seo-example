# Розділ 3. Structured data — одна таблиця

**Сайт:** https://mesiriak.github.io/seo-example/  
**До:** structured data відсутня · **Після:** 8 блоків JSON-LD, 5 типів Schema.org  
**Валідація:** [Rich Results Test](https://search.google.com/test/rich-results)

| № | URL | Тип Schema.org | Ключові поля JSON-LD | Обґрунтування | Rich Results Test | SERP features | Скріншот |
|---|-----|----------------|----------------------|---------------|-------------------|---------------|----------|
| 1 | /index.html | **WebSite** | name, url, description, publisher | Hub-сторінка, ідентифікація сайту | — | Sitelinks | *[META SEO Inspector: WebSite]* |
| 2 | /faq.html | **FAQPage** | mainEntity: 5× Question + Answer | Вимога лаби (FAQ), 5 питань на сторінці | **Valid** | FAQ rich results | *[Rich Results: faq.html Valid]* |
| 3 | /blog-seo-audit.html | **Article** | headline, image, author, publisher, dates, mainEntityOfPage | Стаття блогу, H1 = headline | **Valid** | Розширений сніпет | *[Rich Results: Article Valid]* |
| 4 | /blog-redirects.html | **Article** | headline «Чому важливі redirect?», аналогічно п.3 | Друга стаття блогу | **Valid** | Розширений сніпет | *[Rich Results: blog-redirects]* |
| 5 | /service-technical-audit.html | **Service** | name, description, provider, areaServed, url | SEO-послуга (не Product) | Schema Validator | Звичайний сніпет | *[скрін]* |
| 6 | /service-onpage.html | **Service** | on-page SEO, title/meta/JSON-LD | Тема лабораторної | Schema Validator | Звичайний сніпет | *[скрін]* |
| 7 | /service-linkbuilding.html | **Service** | link building, internal linking | Кластер послуг | Schema Validator | Звичайний сніпет | *[скрін]* |
| 8 | /contacts.html | **ContactPage** | name, url, description | Контакти | — | Knowledge panel | *[скрін]* |

**Правила:** абсолютні URL · ISO-дати · schema = контент сторінки · JSON-LD у `<head>`.

**Висновок:** FAQPage та Article — Valid; 8 сторінок з розміткою; готово до індексації.
