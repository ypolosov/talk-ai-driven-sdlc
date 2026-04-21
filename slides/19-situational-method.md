---
title: Situational method
---

# Ситуационная инженерия методов

<v-clicks>

Это и есть **Situational Method Engineering** - выбор подходов под масштаб.

</v-clicks>

<table class="text-xs">
<thead>
<tr v-click><th>Phase</th><th>Pet project</th><th>Mid size</th><th>Enterprise solution</th></tr>
</thead>
<tbody>
<tr v-click><td><b>Vision</b></td><td>README + салфетка</td><td>Lean Canvas, VSM, стейкхолдер-анализ</td><td>BMC, ArchiMate, capability map, compliance</td></tr>
<tr v-click><td><b>Requirements</b></td><td>TODO в голове</td><td>User Stories, AC, MoSCoW</td><td>Use Cases, SRS (IEEE 830), ISO 42010, трассировка</td></tr>
<tr v-click><td><b>Architecture</b></td><td>«просто код»</td><td>ADR, C4 L1-2, ADD lite</td><td>ADD 3.0, ISO 42010 views, ATAM/QAW, PoC</td></tr>
<tr v-click><td><b>Development</b></td><td>main-ветка, IDE</td><td>Git Flow, PR review, линтеры, CI</td><td>Feature toggles, inner source, CODEOWNERS</td></tr>
<tr v-click><td><b>Testing</b></td><td>«покликал»</td><td>Unit + Integration, TDD, CI</td><td>Pyramid, contract, performance, security, chaos</td></tr>
<tr v-click><td><b>Deployment</b></td><td>git push + Vercel</td><td>CI/CD, staging, blue-green</td><td>GitOps, canary, multi-region, rollback</td></tr>
<tr v-click><td><b>Operations</b></td><td>логи в консоли</td><td>Grafana, alerting, SLO, runbooks</td><td>SRE, SLA/SLO/SLI, observability, post-mortems</td></tr>
</tbody>
</table>

<!--
здесь не нужно распедаливать
-->
