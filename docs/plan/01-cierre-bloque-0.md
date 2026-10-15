# Cierre Bloque 0 — Sesión 2026-10-14

## Decidido y aprobado

- **Plan v2** ("De esquíticos a ECU": Arquitectura + Protocolos) — aprobado sin cambios. Ritmo 7-10 h/semana, modo mentoría.
- **ADR-0001** (arquitectura por capas) — aprobado por Mangel.
- **Repo nuevo** `automotive-ecu-gateway` creado en `C:\dev\automotive-ecu-gateway` (WSL: `/mnt/c/dev/automotive-ecu-gateway`), rama `main`, commit inicial `629cf4a`.
- **Migración del proyecto 04**: código intacto, solo reorganizado (`src/kernel`, `src/drivers`, `src/hal/pico2`, `src/app`, `main.c`). Verificado: compila y genera `.uf2` idéntico en comportamiento al 04.
- Hardware del usuario: Pico 2 W, STM32F407 (bxCAN), Raspberry Pi 1, 2da Pico 2 por llegar. Lista de compras ~$15-20 en el roadmap.
- Git en WSL: identidad configurada (Miguel Angel Sanchez Mares).

## Pendientes de Mangel

- [ ] Crear repo en GitHub y hacer push
- [ ] Flashear `build/automotive-ecu-gateway.uf2` para confirmar comportamiento igual al 04 (opcional)
- [ ] Abrir opencode desde `C:\dev\automotive-ecu-gateway` (la sesión de Bloque 0 vivía en el dir del proyecto 04)

## Próximo paso: Bloque 1, Fase 1

Objetivo: prioridades estáticas + `task_delay` real en `src/kernel/scheduler.c`.
Mentoría: conceptos y preguntas guía → Mangel implementa → diff → review.
Preguntas guía ya planteadas en sesión:
1. ¿Qué pasa si `task_blink` tarda 600ms (período 500ms)?
2. ¿Dónde se escribe el nuevo `next_run_time` de una tarea dormida (ver `scheduler.c:73`)?
3. ¿Cómo sabe `task_delay` qué tarea es (el índice `i` de `scheduler_run` no se registra en ningún lado)?

Nota: diferencia clave ya aprendida — `soft_timer` retrasa un *evento*; `task_delay` retrasa la *propia tarea* (el scheduler la excluye hasta su nueva fecha).
