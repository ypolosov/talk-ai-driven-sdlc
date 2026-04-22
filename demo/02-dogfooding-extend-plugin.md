---
name: demo-02-dogfooding-extend-plugin
type: demo-scenario
target: /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin
plugin: /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin (>= v0.2.1)
duration: ~12-15 минут
resumable: true
feature: добавить роль analyst в catalogs/roles.md
---

# Демо 2: плагин применяется к самому себе (dogfooding)

Плагин — **одновременно** целевая система и система создания.
На сцене добавляю **новую роль `analyst`** в `catalogs/roles.md`:
vision → requirements → architecture → testing → development → audit → commit.

## Что показывает

- Принцип 12: плагин применим к любой IT-системе, включая самого себя.
- Плагин уже dogfooded — артефакты SDLC в корне плагина с прошлых волн.
- `memom.md` не меняется (принципы не трогаем, принцип 15).
- `check-readme-inventory.sh` зелёный (публичная поверхность не меняется, принцип 16).

## Предусловия (проверить ДО доклада)

- Claude Code открыт в `/home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin` — `pwd` в integrated terminal.
- Плагин `ai-driven-sdlc` включён (`/plugin` → enabled, >= v0.2.1).
- MCP `context7` активен.
- `demo-02-start` тег существует (см. «Одноразовая подготовка»).

---

## Одноразовая подготовка baseline

```bash
cd /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin
git checkout main
git tag -f demo-02-start
```

---

## Reset перед каждым прогоном (прямо на main)

```bash
cd /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin

# BACKUP .env (содержит токены — не терять!)
[[ -f .env ]] && cp .env /tmp/demo-02.env.bak

git reset --hard demo-02-start
git clean -fd

# RESTORE .env
[[ -f /tmp/demo-02.env.bak ]] && cp /tmp/demo-02.env.bak .env
```

---

## Прогон

> В Claude Code: открыть каталог `/home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin`.
> Все решения передаю **inline в промпте**; плагин может всё равно открыть SME-опрос —
> в диалоге подтверждаю что ответ уже в промпте или выбираю рекомендованный.
> **Важно**: новые артефакты фаз для этой фичи создаются с префиксом `add-analyst-*.md`,
> чтобы не затереть существующие dogfooded-файлы плагина от прошлых волн.

---

### Шаг 0 — показать исходное состояние и проверить cwd

**Скажи залу:** «Плагин — target, dogfooding. Добавлю роль аналитика через весь цикл».

```bash
pwd                                    # /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin
ls .claude/sdlc/phases/                # все фазы dogfooded с прошлых волн
git branch --show-current              # main
grep -c "^### " catalogs/roles.md      # 8
```

---

### Шаг 1 — `/sdlc-continue`

**Скажи залу:** «Моя роль — method-engineer, развиваю методологию».

```
/sdlc-continue роль - method-engineer, задача - добавить роль analyst в catalogs/roles.md
```

**Выбираю:** `/sdlc-phase vision`.

---

### Шаг 2 — `/sdlc-phase vision`

**Скажи залу:** «Зачем нужна роль».

```
/sdlc-phase vision уровень - pet, автономность - hitl, фокус - плагин (dogfooding), вижен - нет явной роли аналитика между product-owner и architect, добавить analyst с ответственностью за формализацию требований и работу со стейкхолдерами, артефакт сохрани как .claude/sdlc/phases/vision/add-analyst-vision.md (НЕ затирай существующий vision.md), предложи варианты инструментов, подходов
```

---

### Шаг 3 — `/sdlc-phase requirements`

```
/sdlc-phase requirements уровень - mid, автономность - hitl, фокус - плагин, требования - одна user story «как method-engineer хочу добавить analyst в roles.md», AC - запись соответствует схеме раздела «Схема записи», grep подтверждает запись, check-readme-inventory.sh зелёный, артефакт .claude/sdlc/phases/requirements/add-analyst-requirements.md (НЕ затирай существующий requirements.md), traces_from add-analyst-vision.md, предложи варианты инструментов, подходов
```

---

### Шаг 4 — `/sdlc-phase architecture`

```
/sdlc-phase architecture уровень - pet, автономность - hitl, фокус - плагин, архитектура - правка одного файла catalogs/roles.md, не трогаем skills / commands / agents / memom.md, артефакт .claude/sdlc/phases/architecture/add-analyst-architecture.md (НЕ затирай architecture.md), traces_from add-analyst-requirements.md, предложи варианты инструментов, подходов
```

---

### Шаг 5 — `/sdlc-phase testing`

**Скажи залу:** «Smoke — bash-команды, без тест-фреймворка».

```
/sdlc-phase testing уровень - pet, автономность - hotl, фокус - плагин, виды тестов - smoke как bash-команды (grep -c по catalogs/roles.md + bash scripts/check-readme-inventory.sh), НЕ создавай тест-фреймворк, артефакт .claude/sdlc/phases/testing/add-analyst-testing.md (НЕ затирай testing.md), запусти команды сейчас до реализации и ожидай red (grep вернёт 0 совпадений для analyst), предложи варианты инструментов, подходов
```

---

### Шаг 6 — `/sdlc-phase development` (РЕАЛЬНАЯ ПРАВКА)

```
/sdlc-phase development уровень - pet, автономность - hotl, фокус - плагин, git - прямо на main (откат через тег demo-02-start после демо), правка - добавить запись analyst в catalogs/roles.md после product-owner и в итоговую таблицу «role → phases → alphas обязательные», после правки запусти smoke и покажи green, НЕ делай git commit — я сделаю вручную в следующем шаге, предложи варианты инструментов, подходов
```

**Содержание записи** (передаю при первом же уточнении):

```
### analyst
title: Системный аналитик
phases: [vision, requirements]
alphas: [Opportunity, Stakeholders, Requirements]
interests: [формализация требований, интересы стейкхолдеров, непротиворечивость модели]
methods: [stakeholder-analysis, requirements-elicitation]
```

---

### Шаг 7 — `/sdlc-audit`

```
/sdlc-audit
```

**Ожидаемо:** `audit.md` `pass` или единичные note. Если всплывают старые расхождения dogfooded-артефактов прошлых волн — показываю их залу как честный результат сквозной проверки всего плагина, не только новой фичи.

---

### Шаг 8 — commit + diff

**Скажи залу:** «Коммит прямо в main. После демо — откатится через тег».

```bash
# селективный add: только файлы фичи + журналы
git add catalogs/roles.md
git add .claude/sdlc/phases/vision/add-analyst-vision.md
git add .claude/sdlc/phases/requirements/add-analyst-requirements.md
git add .claude/sdlc/phases/architecture/add-analyst-architecture.md
git add .claude/sdlc/phases/testing/add-analyst-testing.md
git add .claude/sdlc/alphas.md .claude/sdlc/decisions.md .claude/sdlc/audit.md

git status   # проверка — что именно в staged

git commit -m "feat(catalogs): add analyst role

Refs: dogfooding demo 02 (принцип 12)."

git log -1 --stat
git diff demo-02-start -- catalogs/roles.md | head -30
```

---

## Контрольные артефакты после прогона

```
catalogs/roles.md                                             # +запись analyst + строка в итоговой таблице
.claude/sdlc/phases/vision/add-analyst-vision.md              # новый, без затирания vision.md
.claude/sdlc/phases/requirements/add-analyst-requirements.md  # новый
.claude/sdlc/phases/architecture/add-analyst-architecture.md  # новый
.claude/sdlc/phases/testing/add-analyst-testing.md            # новый
.claude/sdlc/alphas.md, decisions.md, audit.md                # обновлены
git: main, 1 коммит сверх baseline-тега demo-02-start
```

---

## Reset после прогона (прямо на main)

```bash
cd /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin

# BACKUP .env (содержит токены — не терять!)
[[ -f .env ]] && cp .env /tmp/demo-02.env.bak

git reset --hard demo-02-start
git clean -fd

# RESTORE .env
[[ -f /tmp/demo-02.env.bak ]] && cp /tmp/demo-02.env.bak .env
```

---

## Резервный план

- **`check-readme-inventory.sh` упал** — скрипт проверяет skills/commands/agents/scripts/meta-templates, не catalogs; фича безопасна.
- **`check-memom-consistency.sh` блокирует** — `CLAUDE.md` случайно в staged; `git reset HEAD CLAUDE.md` и коммит снова.
- **`/sdlc-audit` вернул fail** — показать отчёт, разобрать пункт в проблеме. Если важные — применить fix (`/sdlc-audit --apply`) и повторить.
- **Claude затёр существующий `vision.md` / `requirements.md`** — прервать (Esc), `git checkout .claude/sdlc/phases/ -- <файл>` из baseline-тега, перезапустить соответствующий шаг с явным указанием нового пути.
- **Claude автоматически сделал `git commit`** — `git reset --soft HEAD~1`, продолжить с ручным коммитом в шаге 8.
- **Не тот каталог** — `pwd` должна быть `/home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin`.
- **Что-то пошло совсем не так** — reset-блок целиком возвращает состояние: `git reset --hard demo-02-start && git clean -fd`.
