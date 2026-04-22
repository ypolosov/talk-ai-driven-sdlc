---
name: demo-01-target-todo-list
type: demo-scenario
target: /home/ypolosov/DEV/GITS/todo-list
plugin: /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin (>= v0.2.1)
duration: ~25-40 минут (зависит от npm-кэша и скорости Claude)
resumable: true
stack: Vite + React + TypeScript + Vitest + Playwright (как в теге pre-demo-backup)
---

# Демо 1: плагин как система создания для TODO-приложения

Плагин ведёт меня через **все 7 фаз SDLC** для реального TODO-приложения
с нуля до работающего в браузере. Решения в интерактиве — как в прошлый раз,
когда я этот же проект строил. К концу демо: приложение запущено,
`/sdlc-audit` закрывает цикл (`pass` или единичные note, которые можно объяснить).

## Что показывает

- Плагин technology-agnostic: стек выбираю я, а не плагин.
- SME-уровень pet по всем фазам — минимальный процесс под pet-масштаб.
- TDD-first: Testing идёт **до** Development (принцип 5).
- TDD-hook блокирует код без парного теста.
- Все артефакты — в `<target>/.claude/sdlc/`; плагин не трогается.

## Предусловия (проверить ДО доклада)

- Claude Code открыт в `/home/ypolosov/DEV/GITS/todo-list` — убедиться через `pwd` в integrated terminal.
- Плагин `ai-driven-sdlc` включён (`/plugin` → enabled, версия >= 0.2.1).
- MCP `context7` активен (нужен для SME-опроса).
- npm-кэш прогрет (см. «Pre-warm» ниже).
- Порт 5173 свободен (`lsof -i :5173` → пусто).

---

## Одноразовая подготовка baseline

**DESTRUCTIVE**: wipe текущий main до пустого состояния. Текущее финальное приложение сохраняется в теге `pre-demo-backup` — можно восстановить в любой момент.

```bash
cd /home/ypolosov/DEV/GITS/todo-list
git checkout main
git tag -f pre-demo-backup              # страховка на готовое приложение

git rm -rf .                             # снять все tracked файлы (.env gitignored — остаётся)
cat > README.md <<'EOF'
# TODO list

Учебное приложение, создаваемое вживую во время демо доклада «AI-driven SDLC».
EOF
cat > .gitignore <<'EOF'
node_modules/
dist/
coverage/
.env
.DS_Store
EOF
git add README.md .gitignore
git commit -m "demo: пустой baseline для 01-target-todo-list"
git tag -f demo-01-start                 # baseline прямо на main
```

**Возврат к финальному приложению** (когда оно снова понадобится):

```bash
cd /home/ypolosov/DEV/GITS/todo-list
git reset --hard pre-demo-backup
```

---

## Pre-warm npm-кэша (один раз, до первого тестового прогона)

Ускоряет `npm install` на сцене с ~60-90с до ~10-20с:

```bash
cd /tmp && rm -rf warm-npm && mkdir warm-npm && cd warm-npm
npm init -y >/dev/null
npm install --save-dev vite @vitejs/plugin-react typescript vitest @vitest/ui \
    @testing-library/react @testing-library/jest-dom jsdom \
    @playwright/test \
    eslint @typescript-eslint/eslint-plugin @typescript-eslint/parser \
    prettier >/dev/null 2>&1
npm install react react-dom >/dev/null 2>&1
cd / && rm -rf /tmp/warm-npm
```

Если собираетесь делать E2E — дополнительно прогрейте Playwright-браузеры:
`npx playwright install chromium` (~50 МБ).

---

## Reset перед каждым прогоном (прямо на main)

```bash
cd /home/ypolosov/DEV/GITS/todo-list
pkill -f "vite" 2>/dev/null || true
lsof -ti:5173 | xargs -r kill 2>/dev/null || true

# BACKUP .env (содержит токены — не терять!)
[[ -f .env ]] && cp .env /tmp/demo-01.env.bak

git reset --hard demo-01-start           # main возвращается к пустому baseline
git clean -fdx

# RESTORE .env
[[ -f /tmp/demo-01.env.bak ]] && cp /tmp/demo-01.env.bak .env
```

---

## Прогон

> В Claude Code: открыть каталог `/home/ypolosov/DEV/GITS/todo-list`.
> Все решения передаю **inline в промпте**; плагин всё равно может открыть SME-опрос
> (это обязательно по `sdlc-bootstrap` / `sdlc-method-engineering`) — в диалоге
> подтверждаю, что ответ уже в промпте, или выбираю рекомендованное.

---

### Шаг 0 — показать пустоту и проверить cwd

**Скажи залу:** «Пустой репозиторий — сейчас всё появится».

```bash
pwd    # должен быть /home/ypolosov/DEV/GITS/todo-list
ls -la
```

---

### Шаг 1 — `/sdlc-init`

**Скажи залу:** «Разворачиваю каркас SDLC одной командой».

```
/sdlc-init уровень - pet, роль - product-owner, целевая система - корень репозитория, state-артефакт - .claude/sdlc/tasks.md, автономность - hitl
```

**Ожидаемо:** `.claude/sdlc/` с базовыми файлами, hooks активны.

---

### Шаг 2 — `/sdlc-phase vision`

**Скажи залу:** «Зачем мы это делаем — одним промптом».

```
/sdlc-phase vision уровень - pet, автономность - hitl, фокус - корень проекта, вижен - учебное single-user TODO-приложение на pet-масштабе, предмет вторичен, главное - показать процесс SDLC, предложи варианты инструментов, подходов
```

---

### Шаг 3 — `/sdlc-phase requirements`

**Скажи залу:** «Декомпозирую цель в проверяемые требования».

```
/sdlc-phase requirements уровень - pet, автономность - hitl, фокус - корень проекта, требования - CRUD задач (add / toggle / remove) + фильтр по статусу (активные / выполненные / все), persistence через localStorage, без регистрации, предложи варианты инструментов, подходов
```

---

### Шаг 4 — `/sdlc-phase architecture`

**Скажи залу:** «Значимые архитектурные решения — одной страницей».

```
/sdlc-phase architecture уровень - pet, автономность - hitl, фокус - корень проекта, архитектура - spa, ddd-lite, hexagonal (слои domain / application / adapters), localStorage как storage-адаптер, качественные атрибуты - простота + целостность данных, предложи варианты инструментов, подходов
```

---

### Шаг 5 — `/sdlc-phase testing` (TDD-first!)

**Скажи залу:** «Перед кодом — тесты. Принцип номер пять».

```
/sdlc-phase testing уровень - pet, автономность - hotl, фокус - корень проекта, виды тестов - Vitest unit на domain / application с coverage 100% + Playwright smoke E2E на сквозной сценарий add-toggle-remove, предложи варианты инструментов, подходов
```

---

### Шаг 6 — `/sdlc-phase development` (РЕАЛЬНЫЙ КОД, HOOTL, ~15 мин)

**Скажи залу:** «HOOTL — плагин ведёт разработку бесшовно до конца. TDD-hook всё равно сработает, это системный guardrail, не опрос».

```
/sdlc-phase development уровень - pet, автономность - hootl, фокус - корень проекта, стек - typescript, react, vite, vitest, react-testing-library, playwright, localstorage, TDD Red-Green-Refactor по фиче, предложи варианты инструментов, подходов
```

**После выбора инструментов — один большой промпт, Claude идёт до конца:**

```
Реализуй всё приложение до рабочего состояния в браузере. Не проси подтверждений между шагами. Коммиты не делай — я сделаю вручную после демо. Браузер не открывай — dev-сервер оставь запущенным, я открою сам.

Шаг A. Инфраструктура:
- package.json (scripts: dev, build, preview, test, test:e2e, lint, format),
- tsconfig.json + tsconfig.node.json (второй нужен для vite.config.ts и playwright.config.ts),
- vite.config.ts с base: '/todo-list/' (для GitHub Pages),
- vitest.config.ts (environment jsdom, setupFiles ['src/test-setup.ts']),
- src/test-setup.ts с import '@testing-library/jest-dom',
- eslint.config.js, .prettierrc,
- index.html,
- playwright.config.ts (минимальный, chromium only, baseURL http://localhost:5173),
- .gitignore уже есть.
Запусти npm install.

Шаг B. ВАЖНО — демонстрация TDD-hook. Первой операцией ПОПЫТАЙСЯ создать src/domain/todoList.ts БЕЗ теста (я хочу чтобы в зале сработал TDD-hook PreToolUse блокировка). Это намеренное нарушение TDD для показа guardrail. Команда Write src/domain/todoList.ts { add, toggle, remove }. После блокировки hook — переключись на нормальный TDD-цикл (step C).

Шаг C. TDD по фичам в домене — для каждой фичи (add, toggle, remove, filter by status):
- сначала failing-тест в src/domain/todoList.test.ts, запусти npm test (ожидаем red);
- затем минимальная реализация в src/domain/todoList.ts, npm test (green);
- короткий рефакторинг, npm test (green).

Шаг D. Application-слой + адаптер localStorage (тоже TDD-first: сначала src/application/*.test.ts и src/adapters/localStorage.test.ts, потом реализация). Mock localStorage через vi.stubGlobal или beforeEach.

Шаг E. UI-слой: React-компоненты TodoList, TodoItem, AddForm, FilterTabs с RTL-тестами (TDD). src/main.tsx подключает всё.

Шаг F. E2E-смоук: e2e/smoke.spec.ts — Playwright сценарий add → toggle → remove с assert на видимость элементов. НЕ запускай npx playwright install — считаем что браузер уже есть. Запусти npx playwright test, покажи green.

Шаг G. npm run dev — запусти, выведи URL (http://localhost:5173). Остановись здесь.
```

**Открыть браузер** на `http://localhost:5173` вживую. Добавить задачи, отметить, перезагрузить, переключить фильтр.

---

### Шаг 7 — `/sdlc-phase deployment`

**Скажи залу:** «Куда деплоим».

**Остановить dev** (Ctrl+C).

```
/sdlc-phase deployment уровень - pet, автономность - hotl, фокус - корень проекта, деплой - GitHub Pages через Actions, base путь /todo-list/ (уже в vite.config), rollback - git revert через тот же pipeline, предложи варианты инструментов, подходов
```

**После выбора инструментов:**

```
Собери .github/workflows/deploy.yml для GitHub Pages (triggers: push на main; actions/upload-pages-artifact; deploy-pages). Выполни npm run build локально. Покажи размер dist/. Сам deploy на GitHub не триггерим — только артефакт.
```

---

### Шаг 8 — `/sdlc-phase operations`

```
/sdlc-phase operations уровень - pet, автономность - hootl, фокус - корень проекта, наблюдаемость - ручная проверка URL + GitHub Issues как канал обратной связи, инциденты - revert + 1-строчный postmortem в decisions.md, предложи варианты инструментов, подходов
```

---

### Шаг 9 — `/sdlc-audit`

**Скажи залу:** «Сквозная проверка».

```
/sdlc-audit
```

**Ожидаемо:** `audit.md` со статусом `pass` или единичные note — объясняю залу что это и почему pet-масштаб допускает такие напоминания.

---

### Шаг 10 — контроль границ

**Скажи залу:** «Весь код фичи — в целевом проекте; плагин не получил ни одного коммита».

```bash
cd /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin && git status
cd /home/ypolosov/DEV/GITS/todo-list
find .claude/sdlc/phases -name "*.md" | sort
```

В плагине: `working tree clean`. В целевом: артефакты 7 фаз SDLC.

---

## Контрольные артефакты после прогона

```
.claude/CLAUDE.md
.claude/sdlc/{profile,plugin-config,alphas,system-context,roles,decisions,tasks}.md
.claude/sdlc/phases/vision/vision.md
.claude/sdlc/phases/requirements/requirements.md
.claude/sdlc/phases/architecture/architecture.md
.claude/sdlc/phases/testing/testing.md
.claude/sdlc/phases/development/development.md
.claude/sdlc/phases/deployment/deployment.md
.claude/sdlc/phases/operations/operations.md
.claude/sdlc/audit.md                           # pass или note-уровень
package.json, package-lock.json
tsconfig.json, tsconfig.node.json
vite.config.ts (с base: '/todo-list/')
vitest.config.ts, src/test-setup.ts
playwright.config.ts
eslint.config.js, .prettierrc
index.html
src/domain/** (todoList.ts + .test.ts)
src/application/** (.ts + .test.ts)
src/adapters/localStorage.ts (+ .test.ts)
src/components/** (TodoList, TodoItem, AddForm, FilterTabs + RTL-тесты)
src/main.tsx
e2e/smoke.spec.ts
.github/workflows/deploy.yml
dist/                                            # после npm run build
```

---

## Reset после прогона (прямо на main)

```bash
cd /home/ypolosov/DEV/GITS/todo-list
pkill -f "vite" 2>/dev/null || true
lsof -ti:5173 | xargs -r kill 2>/dev/null || true

# BACKUP .env (содержит токены — не терять!)
[[ -f .env ]] && cp .env /tmp/demo-01.env.bak

git reset --hard demo-01-start
git clean -fdx

# RESTORE .env
[[ -f /tmp/demo-01.env.bak ]] && cp /tmp/demo-01.env.bak .env
```

---

## Резервный план

- **`npm install` тормозит** — narrate про артефакты vision/requirements. На крайний случай `npm install --prefer-offline`.
- **Порт 5173 занят** — `lsof -ti:5173 | xargs -r kill`; если Vite взял 5174+ — обновить URL в narrative.
- **TDD-hook не сработал в Step B** — Claude начал с теста вопреки промпту. Не критично для демо: поясни залу что Claude уже знает принцип, но hook **срабатывает независимо**; попроси вручную: «создай `src/utils.ts` с функцией `noop` без теста — покажи hook». Hook блокирует на любом `Write` в `src/**` без пары.
- **Playwright browsers не установлены** — `npx playwright install chromium` (~30 с при прогретом кэше). Или убрать Step F из промпта и запустить только unit-тесты.
- **Claude залип в HOOTL > 15 мин** — прерви (Esc), `/sdlc-autonomy hitl`, продолжи с конкретного шага.
- **SME-опрос разворачивается несмотря на inline-промпт** — в каждом диалоге выбирай «Other» и вставляй то, что уже в inline-промпте, либо «рекомендованный».
- **`/sdlc-audit` вернул fail** — показать отчёт залу, вместе с кратким «почему» (обычно отсутствующие `traces_from` или устаревшие `updated`). Это честный live-demo момент.
- **Что-то пошло совсем не так** — `git reset --hard demo-01-start && git clean -fdx` и начни с нужного шага.
