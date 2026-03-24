---
theme: default
title: AI-driven SDLC
info: |
  ## AI-driven SDLC
  от первых принципов через системное мышление до production

  Полосов Юрий · Solution Architect & Platform Engineer
author: Полосов Юрий
transition: slide-left
colorSchema: dark
fonts:
  sans: Inter
  mono: Fira Code
highlighter: shiki
drawings:
  persist: false
---

# AI-driven SDLC

## от первых принципов через системное мышление до production

<div class="abs-br m-6 flex gap-2">
  <a href="https://github.com/ypolosov/talk-ai-driven-sdlc" target="_blank" class="text-xl slidev-icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!-- Открытие: "Сколько ваших архитектурных решений задокументировано до кода?" -->
<!-- Тезис: AI не пишет код за тебя — AI операционализирует твоё мышление -->

---
layout: intro
---

# Полосов Юрий

<div class="leading-8 opacity-80">
20 лет в IT<br>
Solution Architect & Platform Engineer<br>
B2B2C iGaming Platform startup<br>
<br>
GitHub: github.com/ypolosov<br>
LinkedIn: linkedin.com/in/ypolosov<br>
Telegram: @ypolosov
</div>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Вы строите сложные системы.

Кто принимает архитектурные решения в вашей команде?

Как новый человек понимает, почему система устроена именно так?

Если человек уходит — знание уходит с ним?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Прежде чем говорить об AI — давайте разберёмся<br>
как мы думаем о системах вообще
</div>
</v-click>

---
layout: section
---

# Системное мышление

---

# Системное мышление (Systems Thinking)

<v-clicks>

- Способ думать о сложных системах через **структуру**, а не через детали реализации
- **Безмасштабность:** одни и те же паттерны работают от производства пирожков до enterprise SaaS
- Ключевые вопросы: **что** создаётся, **чем** создаётся, **для кого** создаётся

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Вы разрабатываете продукт. Кто ваш заказчик?

А кто заказчик вашего заказчика?

Есть ли уровни между вами и конечным пользователем?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Эти уровни — не организационная структура.<br>
Это системные уровни. И у каждого своя логика создания ценности
</div>
</v-click>

---

# Целевая система, Система создания, Надсистема

<v-clicks>

- **Целевая система (ЦС)** — то, что создаётся
- **Система создания (СС)** — то, чем создаётся
- **Надсистема** — контекст, ради которого ЦС существует
- Правило: **ЦС(N) = инструмент для СС(N-1)**

</v-clicks>

---

# Методы, Практики и Роли

<v-clicks>

- **Метод / практика** — способ выполнения работы (алгоритм, культура, стиль)
- **Роль** — функциональная позиция агента, определяемая методом который он исполняет
- **Агент** — исполнитель роли: человек или AI — не имеет значения, важен метод
- **Мастерство** — способность агента исполнить метод
- Главный принцип: **разговаривай с ролями, а не с людьми**
- В software: «Архитектор» — это роль, не должность. Роль определяется методом (ADD 3.0, arc42), а не записью в контракте

</v-clicks>

---

# Бизнес-модель (Business Model Canvas)

<v-clicks>

- Бизнес-модель описывает как организация **создаёт, доставляет и получает** ценность
- Business Model Canvas (Остервальдер) — 9 блоков: Customer Segments, Value Propositions, Channels, Customer Relationships, Revenue Streams, Key Resources, Key Activities, Key Partnerships, Cost Structure
- Ключевой вопрос: **кому, что, как и за счёт чего?**
- Две организации могут производить одно и то же — но иметь принципиально разные бизнес-модели

</v-clicks>

---

# Поток создания ценности (Value Stream)

<v-clicks>

- **Value Stream** — последовательность шагов, которая доставляет ценность от идеи до потребителя
- Два вида (SAFe / Lean):
  - **Operational Value Stream (OVS)** — доставляет ценность конечному потребителю (пирожок → прохожему, игра → игроку)
  - **Development Value Stream (DVS)** — создаёт системы которые обеспечивают OVS (создание духовки, создание платформы)
- Ключевой вопрос: **где в цепочке создаётся ценность и для кого?**

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Сейчас я покажу сложную IT-систему через пирожки.

Если паттерн одинаково работает для пирожков и для enterprise SaaS — это доказательство его универсальности

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Смотрим на Bakery Factory
</div>
</v-click>

---
layout: section
---

# Bakery Factory
## через бизнес-модели и Value Streams

---

# Bakery Factory · BM1 (B2B)

**Кто:** компания пекарного оборудования
**Что продаёт:** духовки пекарям
**Value Proposition:** промышленная духовка как инструмент производства пирожков

<v-clicks>

- **DVS:** проектирование → производство → продажа духовки
- **OVS:** доставка → установка → обучение → поддержка пекаря

</v-clicks>

<v-click>

| | |
|---|---|
| ЦС | Духовка |
| СС | Фабрика + конвеер |
| Надсистема | Пекарня пекаря |

**ЦС(духовка) = инструмент СС пекаря**

</v-click>

---

# Bakery Factory · BM2 (B2C)

**Кто:** пекарь
**Что продаёт:** пирожки прохожим
**Value Proposition:** свежая выпечка здесь и сейчас

<v-clicks>

- **DVS:** рецепт → закупка → подготовка
- **OVS:** замес → выпечка → продажа → потребление

</v-clicks>

<v-click>

| | |
|---|---|
| ЦС | Пирожок |
| СС | Пекарь + духовка (инструмент) |
| Надсистема | Прохожий |

</v-click>

---

# Bakery Factory · Лабораторная модель

<v-clicks>

- **Проблема BM1:** обратная связь о качестве духовки приходит через жалобы клиентов, задержка — месяцы
- **Лабораторная модель:** компания строит фабрику-лабораторию и лабораторию-пекарню
- **Добавляет собственный OVS:** выпечка пирожков → продажа прохожим

</v-clicks>

<v-click>

**Value Stream петля:**
духовка → лаборатория-пекарня → пирожки → прохожие → feedback → **лучшая духовка**

DVS (производство духовок) улучшается через обратную связь из собственного реального OVS

</v-click>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Вы узнали паттерн?

У вас есть B2B продукт?

Ваши клиенты используют ваш продукт, чтобы создавать что-то для своих клиентов?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Это B2B2C. Структура та же самая.<br>
Посмотрим как это выглядит в iGaming
</div>
</v-click>

---
layout: section
---

# iGaming Platform
## через бизнес-модели и Value Streams

---

# iGaming Platform · BM1 (B2B SaaS)

**Кто:** platform company
**Что продаёт:** operator tenants операторам
**Value Proposition:** готовая iGaming инфраструктура как сервис (SaaS)
**Revenue Streams:** subscription fee, revenue share

<v-clicks>

- **DVS:** разработка платформы → деплой → поддержка
- **OVS:** onboarding оператора → настройка tenant → запуск → поддержка

</v-clicks>

<v-click>

| | |
|---|---|
| ЦС | Operator tenant |
| СС | iGaming Platform |
| Надсистема | Бизнес оператора |

**ЦС(tenant) = инструмент СС оператора**

</v-click>

---

# iGaming Platform · BM2 (B2C через оператора)

**Кто:** оператор
**Что продаёт:** доступ к играм игрокам
**Value Proposition:** игровой опыт, азарт, выигрыш
**Revenue Streams:** депозиты игроков, GGR

<v-clicks>

- **DVS:** настройка и развитие iGaming сайта
- **OVS:** регистрация → депозит → игра → выплата → retention

</v-clicks>

<v-click>

| | |
|---|---|
| ЦС | Сайт с играми |
| СС | Оператор + tenant (инструмент) |
| Надсистема | Игрок |

</v-click>

---

# iGaming Platform · Лабораторная модель

<v-clicks>

- **Проблема BM1:** обратная связь о качестве tenant приходит через тикеты операторов, задержка — недели
- **Лабораторная модель:** platform company создаёт тестовый operator tenant и тестовый iGaming сайт
- **Добавляет собственный OVS:** продажа доступа к играм реальным игрокам

</v-clicks>

<v-click>

**Value Stream петля:**
tenant → тестовый сайт → игроки → реальный опыт → feedback → **лучший tenant**

DVS (разработка платформы) улучшается через обратную связь из собственного реального OVS

</v-click>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Мы видели два примера с одинаковой структурой.

Может ли инструмент разработки иметь ту же самую структуру?

Что если Claude Code Plugin — это тоже продукт со своей бизнес-моделью и value streams?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Смотрим
</div>
</v-click>

---
layout: section
---

# Claude Code Plugin
## через бизнес-модели и Value Streams

---

# Claude Code Plugin · BM1 (B2D)

**Кто:** команда разработки плагина
**Что продаёт:** Plugin разработчикам IT-продуктов
**Value Proposition:** операционализированная методология AI-driven SDLC как установленный плагин
**Revenue Streams:** open source (reputation) / commercial license / consulting

<v-clicks>

- **DVS:** разработка SKILL.md, commands, hooks, agents
- **OVS:** установка → onboarding → сессия разработки → рабочий артефакт (ADR, тест, код)

</v-clicks>

<v-click>

| | |
|---|---|
| ЦС | Claude Code Plugin |
| СС | Claude Code runtime |
| Надсистема | Процесс разработки команды |

</v-click>

---

# Claude Code Plugin · BM2 (B2D → B2B2C)

**Кто:** разработчик, использующий Plugin
**Что создаёт:** IT-продукт (напр. iGaming Platform)
**Value Proposition:** IT-продукт, созданный по правильному методу — быстрее и качественнее

<v-clicks>

- **DVS:** разработка IT-продукта с помощью Plugin
- **OVS:** IT-продукт доставляет ценность пользователям IT-продукта

</v-clicks>

<v-click>

| | |
|---|---|
| ЦС | IT-продукт (iGaming Platform) |
| СС | Разработчик + Plugin (инструмент) |
| Надсистема | Пользователь IT-продукта |

</v-click>

---

# Claude Code Plugin · Лабораторная модель

<v-clicks>

- **Проблема BM1:** обратная связь о качестве Plugin приходит через issues в GitHub, задержка — недели
- **Лабораторная модель:** команда использует Plugin для создания iGaming Platform (реальный enterprise-проект)
- **Добавляет собственный DVS→OVS:** iGaming Platform → операторы → игроки

</v-clicks>

<v-click>

**Value Stream петля:**
Plugin → iGaming Platform → реальный опыт → feedback → **лучший Plugin**

DVS (разработка Plugin) улучшается через обратную связь из самого сложного реального кейса создателей

</v-click>

---

# Три системы · полный изоморфизм

<style>
table { font-size: 0.7em; }
</style>

| Уровень | Bakery Factory | iGaming Platform | Claude Code Plugin |
|---|---|---|---|
| **Система создания** | Компания оборудования | Platform company | Команда плагина |
| **Инструмент СС** | Фабрика + конвеер | iGaming Platform | Claude Code runtime |
| **ЦС** | Духовка | Operator tenant | Claude Code Plugin |
| **СС след. уровня** | Пекарь + духовка | Оператор + tenant | Разработчик + Plugin |
| **ЦС след. уровня** | Пирожок | Сайт с играми | IT-продукт |
| **Надсистема** | Прохожий | Игрок | Пользователь IT-продукта |
| **OVS** | Пирожок → прохожему | Игра → игроку | IT-продукт → пользователю |
| **DVS** | Производство духовок | Разработка платформы | Разработка Plugin |
| **Лаб. модель** | Лаборатория-пекарня | Тестовый tenant + сайт | Plugin на iGaming Platform |

**Вывод:** один паттерн, три масштаба — системное мышление безмасштабно

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Паттерн понятен.

Как в вашей команде принимаются решения?

Кто-нибудь помнит почему был выбран именно этот фреймворк / база данных / паттерн?

Есть ли трейс от бизнес-цели до строчки кода?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Это не проблема памяти. Это проблема метода.<br>
Давайте разберём где SDLC её создаёт
</div>
</v-click>

---
layout: section
---

# Классический SDLC
## и где он теряет качество

---

# Классический SDLC

<v-clicks>

- **Software Development Lifecycle** — жизненный цикл разработки ПО
- Фазы: Vision → Requirements → Architecture → Development → Testing → Deployment → Ops
- Каждая фаза — набор методов работы и артефактов
- Агенты (люди) выполняют роли, используя инструменты

</v-clicks>

---

# Где классический SDLC теряет качество

<v-clicks>

- Решения умирают в Slack и в головах
- Метод работы неявный → результат невоспроизводим
- Связи между фазами рвутся: требование не трейсируется до теста, ADR не трейсируется до кода
- Переход: нужен **явный метод** — это первые принципы

</v-clicks>

---

# Первые принципы (P-A..E)

<v-clicks>

- **P-A:** система создания определяет качество ЦС
- **P-B:** метод работы должен быть явным и трейсируемым
- **P-C:** сложность метода соразмерна сложности системы
- **P-D:** эволюция через умные мутации описания, не хотфиксы
- **P-E:** агент — исполнитель роли, роль определяется методом

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Вы деплоите код в production.

Что именно туда попадает?

Код — это сам продукт?

Или код — это описание того, как продукт должен работать, а production — воплощение?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Этот вопрос не философский.<br>
От ответа зависит как мы думаем об изменениях и эволюции системы
</div>
</v-click>

---
layout: section
---

# Мемом и Феном

---

# Мемом и Феном (Левенчук)

<v-clicks>

- **Мемом** — описание системы: геном, живёт у создателей
- **Феном** — воплощённая система: организм, живёт в надсистеме
- Пример: рецепт пирожка (мемом) vs испечённый пирожок (феном)
- В software: **git-репозиторий** (мемом) vs **production** (феном)
- Изменять феном «напильником» дорого; изменять мемом — дёшево и безопасно

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Итак: мемом и феном — два разных объекта.

Когда вы последний раз синхронизировали их намеренно?

Не «задеплоили» — а обновили ADR, тесты, документацию вместе с кодом?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Если этого не делать — мемом и феном расходятся.<br>
Это называется <strong>architectural drift</strong>.<br>
Причина drift: мы думаем в двух временах, а нужно в трёх
</div>
</v-click>

---
layout: section
---

# Continuous Everything
## три времени

---

# Continuous Everything · три времени

<v-clicks>

- Классический SDLC: **два времени**
  - **Dev-time:** мемом воплощается в феном
  - **Ops-time:** феном работает в production
- Проблема: кто отвечает за эволюцию мемома? В классическом SDLC — никто явно
- **Continuous Everything** добавляет третье время:
  - **Evo-time:** мемом намеренно эволюционирует через умные мутации на основе наблюдений из Ops-time
- Именно **Evo-time** предотвращает architectural drift

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Три времени — понятно.

Кто инициирует мутацию мемома?

Что является сигналом что мутация нужна?

Как сделать мутацию умной, а не случайной?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Есть конкретный цикл. Он замкнут.<br>
И лабораторная модель занимает в нём ключевое место
</div>
</v-click>

---

# Canonical Evolution Loop

<v-clicks>

- **Ops-time:** феном работает, мы наблюдаем (метрики, инциденты, user feedback)
- **Сигнал:** нарушение fitness condition или появление новой возможности
- **Evo-time:** DRR — аргументированная умная мутация мемома (новый ADR, обновлённый SKILL.md)
- **Dev-time:** обновлённый мемом воплощается в новый феном
- **Ops-time:** наблюдаем снова → цикл замкнулся

</v-clicks>

<v-click>

**Лабораторная модель в этом цикле:** тестовый сайт / лаборатория-пекарня = ускоритель Ops-time. Сигналы для Evo-time поступают до попадания к реальным клиентам.

**Хотфикс без DRR = мутация без аргументации = накопление долга мемома**

</v-click>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Система работает. Все довольны.

Как вы называете то, что создаёте?

«Мы делаем платформу» — а что именно?

Разные люди в команде называют по-разному?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Это не вопрос терминологии. Это вопрос адресации.<br>
Если нельзя точно назвать что создаёшь — нельзя правильно это спроектировать
</div>
</v-click>

---
layout: section
---

# Адресация и проектирование

---

# Принцип почтальона

<v-clicks>

- Называя систему — ты даёшь её **адрес** в понятийном пространстве
- Каждый уровень адресации однозначно сужает пространство поиска
- Пропуск уровня → адрес недействителен

</v-clicks>

<v-click>

<div class="mt-4 grid grid-cols-2 gap-4">
<div class="p-4 bg-red-500/20 rounded-lg">

**FAIL:** «Платёжная экосистема»

</div>
<div class="p-4 bg-green-500/20 rounded-lg">

**PASS:** «B2B2C multi-tenant SaaS iGaming Platform с PAM и bonus engine»

</div>
</div>

</v-click>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Вы писали архитектурную документацию.

Кто-нибудь читал её через год?

Почему нет?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Проблема не в лени команды.<br>
Проблема в отсутствии структуры:<br>
<strong>кому важно → как описываем → что получаем</strong>
</div>
</v-click>

---

# Concern, Viewpoint, View (ISO 42010)

<v-clicks>

- **Concern** — что важно роли в системе (предмет интереса)
- **Viewpoint** — метод описания этого concern (нотация, стандарт, шаблон)
- **View** — конкретное описание по этому методу (ADR, диаграмма, тест)
- Три отдельных разговора, не один
- **Нет viewpoint → нет view → vibe coding**

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Как принимается архитектурное решение в вашей команде?

Кто-то предлагает → все соглашаются на митинге?

Или есть структурированный процесс: явные quality attributes, trade-off анализ, задокументированный rationale?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Есть метод который делает этот процесс воспроизводимым.<br>
Называется <strong>ADD 3.0</strong>
</div>
</v-click>

---

# ADD 3.0 (Attribute-Driven Design)

<v-clicks>

- Итерационный метод проектирования архитектуры через **quality attributes**
- Шаги: Utility Tree → architectural drivers → design concept → ADR → следующая итерация
- **Utility Tree:** бизнес-цель → quality attribute → scenario → метрика

</v-clicks>

<v-click>

<div class="mt-4 grid grid-cols-2 gap-4">
<div class="p-4 bg-red-500/20 rounded-lg">

**FAIL:** «Высокая производительность»

</div>
<div class="p-4 bg-green-500/20 rounded-lg">

**PASS:** «p99 ≤ 200ms при 10k concurrent sessions на tenant»

</div>
</div>

</v-click>

---

# ADR (Architecture Decision Record)

<v-clicks>

- Артефакт, фиксирующий архитектурное решение
- Структура: **problem frame → decision → rationale → consequences**
- ADR без rationale — это лог решений, не аргумент
- **ADR в git = трейсируемая умная мутация мемома**

</v-clicks>

---

# От функции к продукту (IEC 1392)

<v-clicks>

- Сначала: **что** система должна делать (функциональные объекты)
- Потом: **из чего** она будет состоять (конструктивные объекты)
- Каждое соответствие функция → реализация = архитектурное решение (ADR)
- **ADD 3.0** — формализованный процесс этого перехода

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Кто пишет тесты после кода?

Кто пишет тесты до кода?

Кто думает о тесте как о спецификации, а не как о проверке?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Разница принципиальная.<br>
Тест-как-спецификация = мемом поведения системы.<br>
Это не про тестирование — это про <strong>проектирование</strong>
</div>
</v-click>

---
layout: section
---

# TDD и автономия агентов

---

# TDD (Test-Driven Development)

<v-clicks>

- **Red** = функциональный объект не воплощён
- **Green** = функциональный объект воплощён в рабочем коде
- **Refactor** = улучшаем код, тесты остаются зелёными
- **Test suite = мемом поведения системы**
- Тест без трейса до concern — тест ради теста

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Вы доверяете AI писать код автономно?

В каких случаях да, в каких — нет?

Где граница между «пусть делает сам» и «здесь нужно моё решение»?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Эта граница — не интуиция.<br>
Её можно формализовать. И она разная<br>
для разных фаз и разной сложности системы
</div>
</v-click>

---

# Автономия агентов

<v-clicks>

- **Human in the loop:** каждое решение согласуется с человеком
- **Human on the loop:** агент действует, человек мониторит и может вмешаться
- **Human out of the loop:** агент действует полностью автономно
- Выбор зависит от **фазы SDLC** и **стоимости ошибки**

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Вы используете один и тот же процесс для side project и для production enterprise?

Если да — что-то явно избыточно или недостаточно

Если нет — как вы решаете что применять?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Метод должен быть соразмерен сложности системы.<br>
Давайте это формализуем
</div>
</v-click>

---
layout: section
---

# Адаптивный SDLC
## SME-матрица

---

# SME-матрица (Situational Method Engineering)

<v-clicks>

- **SME:** метод соразмерен сложности системы
- TOGAF для todo-app — **cargo cult**; napkin sketch для enterprise — **катастрофа**
- Матрица: **7 фаз × 3 уровня сложности** (pet / mid / enterprise) × human loop

</v-clicks>

---

# Фаза 00 · Vision & Business Architecture

| | Pet | Mid | Enterprise |
|---|---|---|---|
| **Методы** | Личная цель, napkin sketch | Lean Canvas, VPC, JTBD, OKR | BCM, VSM, TOGAF BA, SAFe |
| **Human loop** | in | in | in |
| **Fitness** | — | — | ЦС адресована по принципу почтальона |

Стоимость ошибки максимальна → всегда **human in the loop**

---

# Фаза 01 · Requirements

| | Pet | Mid | Enterprise |
|---|---|---|---|
| **Методы** | Notes, user stories, AC | USM, BDD/Gherkin, MoSCoW, Kano | QAW, MTW, Utility Tree, IREB, IEEE 830 |
| **Human loop** | in | in/on | in/on |
| **Fitness** | — | — | Каждый NFR трейсируется до first principle |

Domain expert валидирует каждый QA scenario

---

# Фаза 02 · Architecture & Design

| | Pet | Mid | Enterprise |
|---|---|---|---|
| **Методы** | Napkin sketch, MVC | C4, arc42, ADR, DDD тактический | ADD 3.0, arc42, TOGAF ADM, 4+1, DDD, SABSA |
| **Human loop** | in | in | in |
| **Fitness** | — | — | Каждый ADR трейсируется до concern |

Решения необратимы → всегда **human in the loop**

---

# Фаза 03 · Development

| | Pet | Mid | Enterprise |
|---|---|---|---|
| **Методы** | Just code, git basics | TDD, BDD, Clean Code, SOLID, Feature Flags | TDD+BDD, Contract Testing, DDD, Mutation Testing |
| **Human loop** | out | on | on |
| **Fitness** | — | — | Каждый тест трейсируется до QA scenario |

Subagents + мониторинг drift от ADR

---

# Фаза 04 · Testing

| | Pet | Mid | Enterprise |
|---|---|---|---|
| **Методы** | Manual smoke, happy path | Auto unit/integ/E2E, SAST, perf | ATAM, Chaos Eng, Mutation, Contract, k6, DAST |
| **Human loop** | out | out | out/in |
| **Fitness** | — | — | Нарушение = нарушение арх. инварианта |

Out для авто-проверок; in при нарушении fitness function

---

# Фаза 05 · Deployment

| | Pet | Mid | Enterprise |
|---|---|---|---|
| **Методы** | Manual deploy, single env | CI/CD, Docker, Blue-Green, Feature Flags | GitOps, Canary, SAFe Release Trains, SRE |
| **Human loop** | out | out | in/out |
| **Fitness** | — | — | Deployment strategy зафиксирована в ADR |

In для go/no-go (enterprise); out при прохождении всех gates

---

# Фаза 06 · Operations & Evo-time

| | Pet | Mid | Enterprise |
|---|---|---|---|
| **Методы** | Fix when broken | Monitoring, SLO+alerting, Post-mortem | SRE, ITIL, Chaos Eng, AIOps, Fitness Functions |
| **Human loop** | out | on | out/on/in |
| **Fitness** | — | — | Каждый инцидент → DRR или «не менять мемом» |

Out для auto-scaling; on при аномалиях; in для умных мутаций мемома

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Мы разобрали методологию.

Кто из вас сегодня вечером откроет ноутбук и начнёт применять всё это вручную?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Никто. Потому что это слишком сложно без инструмента.<br>
Что если весь этот стек можно установить<br>
<strong>одной командой в Claude Code?</strong>
</div>
</v-click>

---
layout: section
---

# Claude Code артефакты
## строительные блоки расширения

---

# Claude Code артефакты

<v-clicks>

- Семь типов: **CLAUDE.md**, **Skills** (SKILL.md), **Commands**, **Subagents**, **Hooks**, **MCP Servers**, **Plugins**
- Два класса:
  - **Детерминированные** (всегда выполняются): CLAUDE.md, Hooks
  - **Вероятностные** (Claude применяет по контексту): Skills, Commands, Subagents

</v-clicks>

---

# Маппинг артефактов → SDLC

<style>
table { font-size: 0.78em; }
</style>

| Артефакт | Тип | Роль в SDLC | Фаза |
|---|---|---|---|
| **CLAUDE.md** | детерм. | Мемом системы создания | Все |
| **SKILL.md** | вероят. | Viewpoint (ISO 42010) | Все |
| **Commands** | вероят. | Точки входа в фазы | Все |
| **Subagents** | вероят. | Параллельная реализация | Dev, Test |
| **Hooks** | детерм. | Fitness functions | Test, Deploy |
| **MCP Servers** | детерм. | Интеграция с надсистемой | Deploy, Ops |
| **Plugins** | — | Дистрибутив методологии | Все |

---

# CLAUDE.md → SDLC

<v-clicks>

- **Что:** markdown-файл, загружается в каждую сессию автоматически
- **Детерминированный:** всегда в контексте, без исключений
- **Роль в SDLC:** мемом системы создания — контекст проекта, инварианты, правила команды
- **Пример:** «Всегда создавай ADR перед изменением архитектуры», «Тесты обязательны до кода»
- **Аналог: CLAUDE.md = конституция команды**

</v-clicks>

---

# SKILL.md (Skills) → SDLC

<v-clicks>

- **Что:** директория с SKILL.md, загружается автоматически по контексту
- **Вероятностный:** Claude решает когда применять
- **Роль в SDLC:** viewpoint по ISO 42010 — метод работы агента для конкретной роли и фазы
- **Маппинг:**
  - `systems-thinking` → Vision / Requirements
  - `add3-workflow` → Architecture
  - `tdd-workflow` → Development / Testing
  - `ce-workflow` → Deployment / Ops
- **Главный тезис: SKILL.md = viewpoint — не метафора**

</v-clicks>

---

# Commands → SDLC

<v-clicks>

- **Что:** slash-команды, инициируемые пользователем
- **Вероятностный:** пользователь запускает явно
- **Роль в SDLC:** явные точки входа в фазы — человек инициирует переход между фазами
- **Маппинг:** `/vision` → Vision, `/arch` → Architecture, `/adr` → ADR, `/tdd` → TDD, `/deploy` → Deployment
- **Human loop:** slash-команда = явный сигнал «человек передаёт управление агенту»

</v-clicks>

---

# Subagents → SDLC

<v-clicks>

- **Что:** агент с изолированным контекстом, запускается для конкретной задачи
- **Вероятностный:** Claude делегирует задачу
- **Роль в SDLC:** параллельная реализация независимых задач без засорения основного контекста
- **Маппинг:**
  - Development: один subagent = одна задача
  - Testing: параллельный запуск тест-сценариев
  - Architecture: параллельный анализ drivers
- **Human loop:** on — мониторинг drift от ADR

</v-clicks>

---

# Hooks → SDLC

<v-clicks>

- **Что:** shell-скрипты на событиях жизненного цикла
- **Детерминированный:** всегда, без исключений
- **Роль в SDLC:** fitness functions и quality gates
- **Маппинг:**
  - PreToolUse: блокирует коммит если тесты красные
  - PostToolUse: запускает линтер после каждого edit
  - Session: инжектирует актуальный контекст
- **Принцип: правила безопасности — только через Hooks, не через SKILL.md**

</v-clicks>

---

# MCP Servers → SDLC

<v-clicks>

- **Что:** Model Context Protocol серверы — внешние инструменты, подключаемые к Claude
- **Детерминированный:** всегда доступны когда подключены
- **Роль в SDLC:** интеграция с надсистемой
- **Маппинг:**
  - GitHub MCP → Deployment (PR, review, merge)
  - Jira / Linear MCP → Requirements
  - Grafana MCP → Ops (метрики → мутации мемома)
- **Human loop:** out для чтения; in для деструктивных действий

</v-clicks>

---

# Plugins → SDLC

<v-clicks>

- **Что:** упакованный набор всех артефактов (SKILL.md + Commands + Subagents + Hooks + MCP)
- **Роль в SDLC:** дистрибутив методологии — устанавливается один раз, работает везде
- **Plugin marketplace = рынок методологий**, а не рынок инструментов
- Plugin для iGaming = упакованная система создания iGaming-продуктов: domain SKILLs, compliance hooks, iGaming-specific commands

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Все строительные блоки разобраны.

Если SKILL.md — это просто файл с инструкциями, чем он отличается от любого другого prompt?

Что делает его частью методологии, а не просто подсказкой?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
SKILL.md — это viewpoint по ISO 42010. Не метафора. Смотрим
</div>
</v-click>

---
layout: section
---

# SKILL.md = Viewpoint
## не метафора

---

# SKILL.md = viewpoint (ISO 42010)

<v-clicks>

- SKILL.md описывает метод работы агента — это **viewpoint по ISO 42010**
- ISO 42010 формально: viewpoint **specify/governs** → view **addresses** → concern
- SKILL.md **specify/governs** → ADR/тест **addresses** → QA scenario
- **Изоморфизм полный**
- Агент без SKILL.md создаёт view без viewpoint — **vibe coding**
- **Качество SKILL.md = качество всех артефактов сессии**

</v-clicks>

---

# Claude Code Plugin · интеллект-стек

<v-clicks>

- 6 SKILL.md = **6 viewpoints**
- Порядок загрузки = **P2W** (от первых принципов до работы):
  1. `fpf-thinking` — первые принципы
  2. `systems-thinking` — системное мышление
  3. `add3-workflow` — архитектура
  4. `tdd-workflow` — разработка
  5. `ce-workflow` — деплой и операции
  6. `adaptive-context` — адаптация к сложности
- Каждый следующий SKILL операционализирует предыдущий
- Human loop матрица: **фаза × сложность системы**

</v-clicks>

---
layout: center
class: text-center
---

# Вопрос к залу

<div class="text-xl">

Звучит хорошо. Но есть и другие подходы.

Чем этот плагин отличается от того, что уже существует?

Почему не взять BMAD или spec-kit?

</div>

<v-click>
<div class="mt-8 p-4 bg-blue-500/10 rounded-lg text-lg">
Давайте сравним честно
</div>
</v-click>

---
layout: section
---

# Сравнение с конкурентами

---

# AI-driven SDLC Plugin vs конкуренты

<style>
table { font-size: 0.52em; }
th, td { padding: 0.25em 0.4em; }
</style>

| | BMAD-METHOD | spec-kit | OpenSpec | AI-driven SDLC |
|---|---|---|---|---|
| **GitHub** | 35k+ ⭐ | 68k+ ⭐ | — | — |
| **Подход** | Agile + multi-agent | Spec-Driven Dev | Lightweight SDD | ST + AI-driven SDLC |
| **Фундамент** | Agile personas (неявный) | Spec+TDD (явный) | Fluid SDD (явный) | FPF+ST+ADD 3.0+ISO 42010 |
| **Охват SDLC** | Analysis → Impl | Specify → Impl | Feature-level | Vision → Ops → Evo-time |
| **Адаптация** | Scale-adaptive | Нет матрицы | Нет матрицы | SME: pet/mid/enterprise |
| **Трейсинг** | Нет | Частичный | Частичный | concern→ADR→тест→код→fitness |
| **Human loop** | In на планировании | Validates gates | Fluid | Per фаза × per сложность |
| **CE / Evo-time** | Нет | Нет | Нет | Canonical Evolution Loop |
| **Value Streams** | Нет | Нет | Нет | DVS + OVS явно |
| **Fitness** | Нет | Нет | Частично | Hooks + Architecture FF |
| **TDD** | Нет явного | Обязателен | Нет | Обязателен + BDD |

---

# Позиционирование

<v-clicks>

- **BMAD** — лучший для мультиагентной Agile-команды из AI-персон (35k ⭐)
- **spec-kit** — лучший для строгого SDD с обязательным TDD, GitHub-backed (68k ⭐)
- **OpenSpec** — лучший для lightweight SDD в brownfield без жёстких фаз
- **AI-driven SDLC Plugin** — единственный подход с **полным трейсингом** от первых принципов до production, явными Value Streams, Continuous Everything и адаптацией к сложности

</v-clicks>

---
layout: section
---

# Живое демо

---
layout: center
---

# Демо · Plugin hello-world

<v-clicks>

- Три SKILL.md: `systems-thinking` + `add3-workflow` + `tdd-workflow`
- Установка плагина в Claude Code
- Запуск первой сессии: **Vision → системная модель → один ADR**

</v-clicks>

---
layout: center
---

# Демо · iGaming Platform hello-world

<v-clicks>

- Тестовый operator tenant + сайт с одной игрой
- Один ADR с полным трейсингом: **concern → decision → rationale → consequences**
- Одна fitness function: «данные tenant A недоступны tenant B»
- Полный **P2W** на экране: first principle → работающий артефакт

</v-clicks>

---

# Итог · что меняется

<v-clicks>

- **До:** агент выполняет роль по неявному методу — результат невоспроизводим
- **После:** агент выполняет роль по SKILL.md — явно, трейсируемо, воспроизводимо
- **Роль архитектора:** из «человека который всё знает» → **куратор viewpoints команды**
- **Лабораторная модель** — не бонус: это структурное требование к зрелой системе создания

</v-clicks>

---
layout: center
---

# Три вещи которые можно сделать завтра

<v-clicks>

1. **Назвать** свою ЦС по принципу почтальона
2. **Написать** один ADR в DRR-структуре
3. **Создать** один SKILL.md для самого частого метода в команде

</v-clicks>

---
layout: two-cols
---

# Ссылки

**Системное мышление**
- Левенчук А. «Системное мышление 2024»
- FPF — github.com/ailev/FPF

**Бизнес-моделирование**
- BMC (Остервальдер) — strategyzer.com
- SAFe Value Streams

**Архитектурные практики**
- ADD 3.0 — Bass, Clements, Kazman
- ISO 42010:2022
- arc42.org · c4model.com
- «Building Evolutionary Architectures»

::right::

<div class="mt-12">

**AI-driven разработка**
- BMAD-METHOD
- spec-kit (GitHub)
- OpenSpec

**Claude Code**
- claude.ai/code
- code.claude.com/docs

**SDLC методологии**
- SAFe · TOGAF ADM
- «Accelerate» — Forsgren, Humble, Kim

**Доклад и плагин**
- github.com/ypolosov/ai-driven-sdlc-plugin
- github.com/ypolosov/talk-ai-driven-sdlc

</div>

---
layout: end
---

# Спасибо!

Полосов Юрий · @ypolosov
