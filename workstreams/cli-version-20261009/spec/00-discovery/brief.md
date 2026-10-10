---
schema: discovery-brief
schema_version: 1
spec_stage: discovery
status: draft
generated_by: discovery-runtime
generated_at: '2026-10-09T19:55:51Z'
validation: pass
interview:
  frame: customer
  sessions:
  - participant_role: owner
coverage:
  goals: covered
  personas: covered
  jobs: covered
  functions: covered
  nfr: covered
  constraints: covered
  success_metrics: covered
  out_of_scope: covered
  risks: missing
  gate_passed: true
open_questions: 0
blocking_open_questions: 0
conflicts: 0
traces_to: []
---

# Discovery Brief — andrei-shtanakov/spec-loop-sandbox (customer-фрейм)

## Goals

- **G-01** По команде --version пользователь за один запуск узнаёт имя инструмента и его версию.
- **G-02** Вывод пригоден для вставки в баг-репорт как есть, без доработки.

## Personas

- **P-01** Пользователь утилиты, присылающий баг-репорты.
- **P-02** Сопровождающий утилиты, разбирающий баг-репорты.

## Jobs-to-be-done

- **J-01** Когда я пишу баг-репорт, я хочу одной командой узнать версию, чтобы сразу указать её в отчёте.
  traces: [G-01, G-02]

## Functional Requirements

- **FR-01** --version печатает одной строкой `<имя> <версия>`.
  **Priority**: Must
  **Acceptance**: Вывод совпадает с версией пакета.
  traces: [J-01]
- **FR-02** При --version программа завершается с кодом 0.
  **Priority**: Must
  **Acceptance**: `echo $?` после запуска даёт 0.
  traces: [J-01]
- **FR-03** При --version прочие аргументы не обрабатываются.
  **Priority**: Should
  **Acceptance**: `--version --foo` печатает версию и не ругается на `--foo`.
  traces: [J-01]

## Non-Functional

- **NFR-01** При --version нет сетевых обращений.
  **Category**: safety
  **Target**: 0 сетевых вызовов
- **NFR-02** При --version не записываются файлы.
  **Category**: safety
  **Target**: 0 записанных файлов
- **NFR-03** Время ответа не больше обычного запуска.
  **Category**: perf
  **Target**: ≤ 100 мс сверх старта интерпретатора

## Constraints

- **CON-01** Версия берётся из единственного источника (метаданные пакета), без ручного дублирования.
- **CON-02** Без новых зависимостей.

## Success Metrics

- **M-01** Доля баг-репортов с указанной версией.
  **Target**: baseline 0% → ≥ 90% через 3 месяца
  traces: [G-01, G-02]

## Out of Scope

- **OUT-01** Проверка обновлений и сравнение с последней версией.
- **OUT-02** Машиночитаемый (JSON) вывод.