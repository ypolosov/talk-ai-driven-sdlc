# AI-driven SDLC: через призму системного мышления

Репозиторий с материалами доклада **«AI-driven SDLC: через призму системного мышления»**. Доклад посвящён применению AI во всех фазах жизненного цикла разработки ПО (от идеи до эксплуатации) и рассматривает SDLC через оптику системного мышления: целевая система, подсистема, надсистема, система создания, цепочки создания ценности (OVS/DVS), цифровые двойники и роли стейкхолдеров.

Презентация построена на [Slidev](https://sli.dev/) с темой `seriph` и аддоном Excalidraw. В `demo/` лежат сценарии живого демо: разработка целевой системы (todo-list) и dogfooding-расширение плагина `ai-driven-sdlc`.

## Структура

```
.
├── slides.md             — корневой файл презентации (импортирует все слайды по порядку)
├── slides/               — отдельные слайды (01-intro … 36-thank-you)
├── demo/                 — сценарии демонстраций
│   ├── 01-target-todo-list.md          — демо на целевом проекте todo-list
│   └── 02-dogfooding-extend-plugin.md  — демо расширения плагина самим собой
├── exports/              — экспортированные PDF и PPTX версии
├── public/               — статические ресурсы (изображения)
└── package.json
```

## Технологии

- [Slidev](https://sli.dev/) — презентация из markdown
- `@slidev/theme-seriph` — визуальная тема
- `slidev-addon-excalidraw` — встраивание Excalidraw-диаграмм
- `@playwright/test` — для экспорта в PDF

## Запуск

Установка зависимостей:

```bash
npm install
```

Запуск презентации в dev-режиме (открывается в браузере, hot-reload):

```bash
npm run dev
```

Сборка статического билда:

```bash
npm run build
```

Экспорт в PDF:

```bash
npm run export
```

## Связанные репозитории

- [ai-driven-sdlc-plugin](https://github.com/ypolosov/ai-driven-sdlc-plugin) — Claude Code плагин, реализующий методологический каркас SDLC
- [todo-list](https://github.com/ypolosov/todo-list) — целевой проект, на котором демонстрируется плагин

## Автор

**Юрий Полосов** — Solution Architect & Platform Engineer, 20 лет в IT.
