# AGENTS.md — Contexto para asistentes de IA

## Qué es este proyecto

Repositorio de aprendizaje de sistemas embebidos con doble objetivo: (1) convertirme en arquitecto de software embebido, (2) dominar el uso de IA como herramienta profesional. No es código de producción: es un plan de estudio con entregables incrementales.

## Estado del plan

Estamos en **Bloque 0** (estructura + workflow). El plan completo está en `docs/plan/00-roadmap.md`. Nunca saltear bloques: cada fase se implementa solo después de su bloque anterior.

## Reglas de mentoría (IMPORTANTES)

1. **NUNCA dar código completo de golpe.** Dar solo: conceptos, preguntas guía, referencias a documentos/datosheets. El usuario (Mangel) escribe el código.
2. Si el usuario pide código, responder primero con la pregunta guiadora que le haría avanzar.
3. Al revisar código del usuario: señalar problemas como mentor (con preguntas), no reimplementar.
4. Hacer **repasos** al inicio de cada bloque (flashcards de `docs/learnings.md`).
5. El plan se revisa y ajusta con el usuario al cerrar cada bloque.

## Workflow con IA (en cada fase)

1. Escribir/leer la spec en `specs/` antes de implementar (test-first).
2. Pedir a la IA que proponga un **diseño** → el usuario lo critica/decide.
3. Implementar en unidades pequeñas, un archivo a la vez.
4. Review de la IA sobre el diff (señalar bugs y violaciones de capa, no reescribir).
5. Registrar aprendizajes/flashcards en `docs/learnings.md`.
6. Las decisiones de diseño van a `docs/adr/` (Architecture Decision Records).

## Estructura y convenciones de código

- C11, estilo MISRA-ish: sin VLA, `u` en literales uint, prefijos de módulo, `0u` en compares con unsigned.
- Includes planos: `#include "scheduler.h"` (los directorios están en include path de CMake).
- **Regla de capas** (ver ADR-0001): `app/` → `services/` → `protocols/` → `drivers/` → `hal/`. Un módulo solo incluye cabeceras de su capa o inferior. `hal/pico2/raspBerryPico.h` es lo único que toca registros directamente (hoy compartido; en Bloque 2 se mueve a `hal/pico2/` y se separa por board).
- Headers con include guards `#ifndef NAME_H` / `#define NAME_H` / `#endif`.
- Nombres: snake_case, funciones `subjeto_verbo` o `mod_accion` (ej. `scheduler_add_task`, `sw_timer_start`).

## Comandos

- Build Pico 2 W (Windows): `cmake -B build && cmake --build build` — SDK en `C:/Users/mares/.pico-sdk/sdk/2.2.0`
- Board: `pico2_w` (RP2350, dual Cortex-M33)
- Hardware disponible: Pico 2 W, STM32F407, Raspberry Pi 1, 2da Pico 2 (por llegar)
- Logging: UART1 a 9600 baud (GPIO4), NO stdio USB/UART del SDK

## Documentos clave

- `docs/plan/00-roadmap.md` — plan v2 completo con bloques, fases, entregables
- `docs/adr/` — decisiones de arquitectura (leer antes de sugerir cambios estructurales)
- `docs/learnings.md` — flashcards y resúmenes de repaso
- `specs/` — una spec por módulo; escribir spec antes que código
