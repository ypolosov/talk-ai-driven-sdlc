---
name: demo-02-dogfooding-extend-plugin
type: demo-scenario
target: /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin
plugin: /home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin (wave-2)
duration: ~15 минут
---

# Демо-сценарий 2: плагин расширяет сам себя (dogfooding)

Плагин `ai-driven-sdlc` применяется к собственному репозиторию как целевой системе.
Демонстрирует принцип 12: плагин применим к любому IT-продукту, включая самого себя.
Опора — Том 2 гл. 8 «Графы создания» (самопорождающие циклы).

## Цель фичи

Добавить в `catalogs/roles.md` новую роль `security-officer` с соответствующей привязкой.
Эта фича — простая, методологически осмысленная; не требует нового кода.
Показывает, как каркас плагина ведёт свою собственную разработку.

## Предпосылки

- Плагин установлен; Волны 1 и 2 влиты в `main`.
- Рабочий каталог Claude Code открыт в `/home/ypolosov/DEV/GITS/ai-driven-sdlc-plugin`.
- Git плагина в чистом состоянии; создана ветка `feat/add-security-officer-role`.

## Шаг 0. Показать исходное состояние

- Плагин ещё не имеет `.claude/sdlc/` (целевой проект = сам плагин).
- `catalogs/roles.md` содержит 8 ролей без `security-officer`.

## Шаг 1. `/sdlc-init --merge`

- Плагин обнаруживает отсутствие `.claude/sdlc/`.
- Режим `--merge` (или дефолтный `--fail-if-exists`) проходит, создаётся каркас.
- Вопросы bootstrap:
  - Размер проекта: **pet** (плагин маленький).
  - Активная роль: **method-engineer** (кто ещё развивает методологический каркас).
  - Целевая система: корень плагина (slug: `ai-driven-sdlc-plugin`).
  - State-артефакт: `TODO.md` в корне плагина или `BACKLOG.md` в `.claude/sdlc/`.
  - Автономность: **hitl**.

**Создано в целевом (= плагине):**
- `.claude/CLAUDE.md` (конституция «целевого» = плагина).
- `.claude/sdlc/{profile,plugin-config,alphas,system-context,roles,decisions}.md`.
- `.env.example`, обновлённый `.gitignore`.

## Шаг 2. `/sdlc-focus ai-driven-sdlc-plugin`

- Перенос внимания на плагин как целевую систему.
- `kind=materialized`, `role_vs_target=target`.
- Создаётся `README.sdlc.md` в корне плагина (sidecar; корневой `README.md` не трогается — политика refuse).
- Обновляется `system-context.md`.

## Шаг 3. `/sdlc-phase vision` (уровень pet)

- Мета-вопросы: зачем нужна роль `security-officer`?
- Инструмент pet: README-as-vision (Mission Statement) для фичи.
- Инстанцируется `phases/vision/add-security-officer-vision.md`:
  - проблема: без роли нет явной ответственности за безопасность в SDLC;
  - цель: добавить роль с интересами и привязкой к фазам.
- `sdlc-alpha-tracker` продвигает Opportunity → Value Established.

## Шаг 4. `/sdlc-phase requirements` (уровень mid)

- Инструмент: user stories (одна-две).
- Инстанцируется `phases/requirements/user-stories.md`:
  - story 1: «Как method-engineer, я хочу добавить security-officer в roles.md, чтобы зафиксировать ответственность за ИБ».
  - acceptance: `roles.md` содержит запись; `check-readme-inventory.sh` проходит.
- `traces_from`: артефакт vision.

## Шаг 5. `/sdlc-phase architecture` (уровень pet)

- Инструмент: одностраничное описание структуры изменений.
- Описывает: какие файлы меняются (`catalogs/roles.md`); где потом упоминается (`method-tool-matrix.md` при необходимости).
- `sdlc-alpha-tracker` продвигает Software System → Architecture Selected.

## Шаг 6. `/sdlc-phase testing` (pet, до кода — TDD)

- Смоук-тест: `grep -F 'security-officer' catalogs/roles.md` должен вернуть >0 строк после внесения.
- Инстанцируется `phases/testing/grep-roles-test.md`.

## Шаг 7. `/sdlc-phase development`

- Правка `catalogs/roles.md`: новая роль:
  ```
  ### security-officer
  title: Инженер по информационной безопасности
  phases: [development, testing, deployment, operations]
  alphas: [Software System, Way of Working]
  interests: [безопасная разработка, SAST/DAST, управление секретами, комплаенс]
  methods: [software-construction, software-testing, continuous-delivery]
  ```
- TDD hook: у нас pet-уровень, TDD-пары не настроены — hook пропускает изменение каталога.
- Format/lint hook: pet уровень, минимальные требования — проходит.
- No-comments hook: markdown-файл, пропуск.
- Validate-artifact: каталог — не артефакт SDLC в `.claude/sdlc/**`, пропуск.

## Шаг 8. Обновление README плагина

- Добавить `security-officer` в раздел «Roles» README плагина (если роль публична).
- `check-readme-inventory.sh` не ругается, потому что проверяет только skills/commands/agents/scripts/meta-templates.
- **Не забыть:** при изменении принципов — обновить `memom.md` (в этой фиче принципы не меняются).

## Шаг 9. `/sdlc-audit`

- `sdlc-consistency-auditor` запускается.
- Проверяет:
  - Трассируемость: vision → requirements → architecture → testing → реализация.
  - Альфы: Opportunity → Value Established, Software System → Architecture Selected.
  - Осиротевшие ссылки — нет.
- Отчёт в `.claude/sdlc/audit.md`: **status: pass**.

## Шаг 10. Commit и merge

- Создан коммит в ветке `feat/add-security-officer-role`:
  - `catalogs/roles.md`: +роль;
  - `.claude/sdlc/**`: артефакты фаз по dogfooding.
- `check-memom-consistency.sh` (pre-commit): `CLAUDE.md` не менялся — проход.
- PR в main, review, merge.

## Контрольные артефакты в плагине

- `.claude/CLAUDE.md`
- `.claude/sdlc/profile.md` (5 фаз со смешанными уровнями).
- `.claude/sdlc/plugin-config.md`.
- `.claude/sdlc/alphas.md` (продвинутые альфы).
- `.claude/sdlc/system-context.md` (плагин как materialized target).
- `.claude/sdlc/roles.md` (активна method-engineer).
- `.claude/sdlc/decisions.md` (≥5 записей).
- `README.sdlc.md` в корне плагина (sidecar — не перезаписывает `README.md`).
- `.claude/sdlc/phases/vision/add-security-officer-vision.md`.
- `.claude/sdlc/phases/requirements/user-stories.md`.
- `.claude/sdlc/phases/architecture/one-pager.md`.
- `.claude/sdlc/phases/testing/grep-roles-test.md`.
- `.claude/sdlc/audit.md` (status: pass).

## Что демонстрирует

- Принцип 12: плагин применим к самому себе.
- Принцип 17: `README.sdlc.md` как sidecar не перезаписывает существующий `README.md`.
- Принцип 15: `memom.md` — журнал; изменение не требует записи, потому что принципы не менялись.
- Принцип 16: `check-readme-inventory.sh` остаётся зелёным, потому что имена skills/commands/agents/scripts не трогались.
- Принцип 13: dogfooding демонстрирует полноту аудита.
- Граф создания (Левенчук Том 2 гл. 8): плагин — одновременно целевая и система-создатель.

## Если принципы меняются

Если в ходе dogfooding обнаруживается необходимость поправить принцип:
1. Обновить `CLAUDE.md` плагина.
2. В том же коммите — добавить запись в `memom.md` с формулировкой до/после, мотивом, последствиями.
3. `check-memom-consistency.sh` блокирует коммит, если запись пропущена.

## Ограничения сценария

- Не меняется публичная поверхность плагина (skills/commands/agents).
- Расширение каталога — типичный кейс эволюции методологии.
- Более сложные dogfooding-сценарии (добавление skill, новой фазы) демонстрируются отдельно.
