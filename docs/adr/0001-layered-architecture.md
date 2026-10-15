# ADR-0001: Arquitectura por capas (app → services → protocols → drivers → hal)

**Estado:** Aceptado
**Fecha:** 2026-10-14
**Contexto:** Bloque 0 del plan de aprendizaje

## Decisión

Organizar el código en capas estrictas, donde cada módulo solo puede incluir cabeceras de su propia capa o inferior:

```
app/        → lógica de negocio, FSM, tareas
services/   → API unificada, enrutamiento (Bloque 4)
protocols/  → stacks i2c/spi/lin/can/sent (Bloque 3)
drivers/    → periféricos (uart, timer), polling/IRQ/DMA
hal/        → abstracción de board (pico2/, stm32f407/)
hardware    → registros (raspBerryPico.h)
```

## Por qué

1. **Objetivo arquitectónico:** el plan busca pensar como arquitecto; un sistema por capas es el patrón dominante en automotriz (AUTOSAR MCAL/BSW/SWC) e industria embebida.
2. **Portabilidad (Bloque 2):** compilar para Pico 2 W y STM32F407 con la misma lógica de capas superiores solo es posible si el hardware queda aislado abajo.
3. **Testeabilidad:** las capas altas pueden probarse con drivers emulados (banco de pruebas, Bloque 5).
4. **Aprendizaje:** fuerza a definir contratos explícitos entre módulos, que es la habilidad central del perfil objetivo.

## Consecuencias

- Más archivos y headers que un diseño "todo junto" (como el proyecto 04 original): aceptado a cambio de claridad.
- Riesgo de sobre-ingeniería prematura: mitigado — las capas `services/` y `protocols/` nacen vacías hasta sus bloques.
- Viola temporalmente MISRA-ish si algún módulo incluye otra capa por atajo: el review de fase debe cazarlo.

## Referencias

- Plan: `docs/plan/00-roadmap.md` (Bloque 2)
- Contexto IA: `AGENTS.md` → "Regla de capas"
