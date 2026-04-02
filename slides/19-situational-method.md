---
title: Situational method
---

<v-clicks>

- Это и есть Situational Method Engineering — выбор подходов под масштаб.
  - (показать сводную таблицу: этапы SDLC × масштаб проекта)

| SDLC Phase | Pet Project | Mid Project | Enterprise Solution |
|---|---|---|---|
| **00 — Vision & Business Architecture** | README.md с идеей, 1 бизнес-модель на салфетке | Lean Canvas, Value Stream Mapping, стейкхолдер-анализ | BMC полный, ArchiMate, capability map, compliance-анализ |
| **01 — Requirements** | TODO-список, user stories в голове | User Stories + Acceptance Criteria, MoSCoW-приоритизация | Use Cases, SRS (IEEE 830), Concern/Viewpoint (ISO 42010), трассировка требований |
| **02 — Architecture & Design** | Никакой — «просто пишем код» | ADR (Architecture Decision Records), C4 level 1-2, ADD 3.0 lite | ADD 3.0 полный, ISO 42010 views, ATAM/QAW, reference architectures, PoC |
| **03 — Development** | Один разработчик, main-ветка, vim/IDE | Git Flow / Trunk-based, PR review, линтеры, CI | Feature toggles, inner source, coding standards, code ownership (CODEOWNERS) |
| **04 — Testing** | Ручной «покликал — работает» | Unit + Integration тесты, TDD, CI-прогон | Пирамида тестирования полная, contract tests, performance/security/chaos testing |
| **05 — Deployment** | `git push` + Vercel / ручной deploy | CI/CD pipeline, staging-окружение, blue-green | GitOps, canary releases, multi-region, rollback strategy, change approval board |
| **06 — Operations & Evolution** | Логи в консоли, «упало — починим» | Мониторинг (Grafana), alerting, SLO, incident runbooks | SRE-практики, SLA/SLO/SLI, observability (traces, metrics, logs), post-mortems, FinOps |

</v-clicks>

<!-- Notes -->
