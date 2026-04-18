---
name: demo-01-target-todo-list
type: demo-scenario
target: /home/ypolosov/DEV/GITS/todo-list
plugin: /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin (wave-1 MVP)
duration: ~15 минут
---

# Демо-сценарий 1: плагин как система создания для todo-list

Плагин применяется к стороннему проекту `/home/ypolosov/DEV/GITS/todo-list`.
Пользователь проходит фазы SDLC со смешанными уровнями pet/mid.
Проверяется: артефакты появляются в целевом, не в плагине.

## Предпосылки

- Плагин `ai-driven-sdlc` установлен и активен.
- Рабочий каталог Claude Code открыт в `/home/ypolosov/DEV/GITS/todo-list`.
- Git целевого находится в чистом состоянии.
- У целевого корневой `README.md` уже существует — плагин не перезаписывает его (принцип 17: refuse, Волна 2).

## Шаг 0. Проверка исходного состояния

- Показать структуру `todo-list/` — уже есть код, но нет `.claude/sdlc/`.
- Показать, что плагин пуст от артефактов целевого.

## Шаг 1. `/sdlc-init`

- Пользователь запускает `/sdlc-init`.
- Плагин проверяет отсутствие `.claude/sdlc/` — режим по умолчанию `--fail-if-exists` проходит.
- Плагин задаёт 5 вопросов:
  - Размер проекта: pet / mid / enterprise? → **pet** (маленький).
  - Активная роль сейчас? → **product-owner**.
  - Текущая целевая система? → корень todo-list.
  - Где хранить состояние работ? → `TODO.md` в корне (kind=file).
  - Уровень автономности по умолчанию? → **hitl**.

**Ожидаемо создано:**
- `todo-list/.claude/CLAUDE.md`
- `todo-list/.claude/sdlc/{profile,plugin-config,alphas,system-context,roles,decisions}.md`
- `todo-list/.env.example`, обновлённый `.gitignore` с `.env`.
- Запись в `decisions.md` о первых выборах.

**Проверка:**
- В плагине — ничего нового (git status plugin = clean).

## Шаг 2. `/sdlc-continue` (роль: product-owner)

- Плагин читает состояние через `sdlc-state-reader`.
- Предлагает: `/sdlc-phase vision` (рекомендация), `/sdlc-focus`, `/sdlc-phase requirements`.
- Выбор: `/sdlc-phase vision`.

## Шаг 3. `/sdlc-phase vision` (уровень pet)

- `sdlc-method-engineering` задаёт мета-вопросы (стейкхолдеры, ценность).
- Предлагает инструменты из матрицы (pet): README-as-vision, Elevator Pitch, Mission Statement.
- Выбор: **README-as-vision**.
- Через `context7` подтягивается референсная структура.
- Инстанцируется `todo-list/.claude/sdlc/phases/vision/readme-as-vision.md`.
- `sdlc-alpha-tracker` продвигает Opportunity → Value Established, Stakeholders → Recognized.
- Запись в `decisions.md` с альтернативами.

**Проверка:**
- Артефакт существует, валиден (`validate-artifact.sh` прошёл PostToolUse).
- `alphas.md` отражает новые состояния.

## Шаг 4. `/sdlc-phase requirements` (уровень mid)

- Смена роли: `--role developer` или через диалог.
- Уровень повышен до **mid**.
- Выбор инструмента: **User Stories + Gherkin AC**.
- Инстанцируется `phases/requirements/user-stories.md` с 3 историями для todo-list:
  - Добавить задачу.
  - Отметить задачу как выполненную.
  - Удалить задачу.
- `traces_from` ссылается на `phases/vision/readme-as-vision.md`.

## Шаг 5. `/sdlc-phase architecture` (уровень pet)

- Выбор инструмента: ASCII box-and-arrow в одностраничном описании.
- Инстанцируется `phases/architecture/one-pager.md`.
- `sdlc-alpha-tracker` продвигает Software System → Architecture Selected.

## Шаг 6. `/sdlc-focus` на подсистему

- `/sdlc-focus frontend` (allow manual slug).
- Плагин спрашивает: materialized или logical; путь; роль.
- Выбор: materialized, `todo-list/web/` как путь, subsystem.
- Обновляется `system-context.md`.

## Шаг 7. `/sdlc-phase testing` перед development (TDD-first)

- Выбор инструмента mid: unit + integration.
- Инстанцируется `phases/testing/test-plan.md`.
- Настраивается `plugin-config.md` для стека (tdd_pairs, scope).

## Шаг 8. `/sdlc-phase development` с HITL

- Выбор git-модели mid: GitHub Flow.
- Выбор форматера и линтера (обязательно по принципу 6).
- `plugin-config.md` дополняется `formatter.command`, `linter.command`.
- Запись в `profile.md`: строка development с инструментами.

**Проверка срабатывания hooks:**
- Попытка `Write` файла исходника без парного теста → TDD hook (HITL) запрашивает подтверждение.
- Попытка записать код с комментарием → no-comments hook блокирует.
- Попытка записать код без форматирования → format/lint hook блокирует.

## Шаг 9. `/sdlc-audit`

- `sdlc-consistency-auditor` запускается полным прогоном.
- Детерминированные скрипты проходят (artifact-validator, check-cross-refs).
- LLM-проверки: трассируемость, соответствие уровню SME, альфы vs артефакты.
- Отчёт сохраняется в `todo-list/.claude/sdlc/audit.md`.

**Ожидаемый статус:** `pass`.

## Шаг 10. Контроль granица плагин/целевой

- В `/home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin/`: git status — clean.
- В `/home/ypolosov/DEV/GITS/todo-list/`: все артефакты в `.claude/sdlc/phases/**`.
- grep по плагину на имена конкретных инструментов — только в `catalogs/method-tool-matrix.md`.

## Контрольные артефакты в todo-list

- `.claude/CLAUDE.md`
- `.claude/sdlc/profile.md` (с 4 строками: vision=pet, requirements=mid, architecture=pet, development=mid, testing=mid)
- `.claude/sdlc/plugin-config.md` (state_artifact, tdd_pairs, formatter, linter)
- `.claude/sdlc/alphas.md` (продвинутые альфы)
- `.claude/sdlc/system-context.md` (две системы: root и frontend-subsystem)
- `.claude/sdlc/roles.md`
- `.claude/sdlc/decisions.md` (≥5 записей)
- `.claude/sdlc/phases/vision/readme-as-vision.md`
- `.claude/sdlc/phases/requirements/user-stories.md`
- `.claude/sdlc/phases/architecture/one-pager.md`
- `.claude/sdlc/phases/testing/test-plan.md`
- `.claude/sdlc/phases/development/<git-workflow>.md`
- `.claude/sdlc/audit.md` (status: pass)
- `.env.example`
- обновлённый `.gitignore` (с `.env`)

## Что демонстрирует

- Плагин technology-agnostic: имена конкретных инструментов встречаются только как пользовательский выбор.
- Альтернативы всегда порождаются и фиксируются (принцип 1).
- Границы целевой системы переносятся вниманием (принцип 7).
- TDD работает мягкой блокировкой (принцип 5).
- Форматер и линтер обязательны (принцип 6).
- Все артефакты пишутся в целевом, не в плагине (принцип 3).
- Многоуровневый фокус внимания поддерживается (принцип 7; Волна 2 добавит README систем).

## Ограничения Волны 1

- `README.sdlc.md` систем внимания — Волна 2 (принцип 17).
- `memom.md` плагина — Волна 2 (принцип 15).
- `check-readme-inventory.sh` и `check-system-readmes.sh` — Волна 2.
- Dogfooding сценарий (02-dogfooding-extend-plugin.md) — Волна 2.
