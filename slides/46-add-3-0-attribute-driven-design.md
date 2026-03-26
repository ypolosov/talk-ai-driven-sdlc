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
