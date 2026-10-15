# Plan v2 — "De esquíticos a ECU": Arquitectura + Protocolos Automotrices

**Ritmo:** 7-10 h/semana · **Duración estimada:** ~8 meses · **Modo:** mentoría (conceptos y preguntas, no código)

## Reglas de la mentoría

1. Nunca código de golpe — solo conceptos, preguntas guía y referencias.
2. Cada fase: conceptos → preguntas guía → el usuario implementa → diff → review + repaso.
3. Cada bloque cierra con REPASO para refrescar la ventana de contexto.
4. El plan se revisa al cerrar cada bloque — si algo no aporta, se cambia.

---

## Bloque 0 — Cimientos: Repo y workflow con IA (1 semana)

**Conceptos:** estructura de repo profesional (`docs/`, `specs/`, `src/`, `tests/`), ADRs, AGENTS.md como contexto para IA, test-first con IA.

**Entregable:** repo reestructurado + primer ADR + documentación de contexto legible por IA.

**Práctica IA:** workflow base: spec → diseño crítico con IA → implementación por unidades → review → registro de aprendizajes.

---

## Bloque 1 — Del cooperativo al mini-RTOS (6-7 semanas)

### Fase 1 — Madurar el scheduler actual
- **Conceptos:** prioridades estáticas, `task_delay` real (diferencia con soft_timer), medición de ejecución, starvation.
- **Preguntas guía:** ¿qué pasa si una tarea excede su período? ¿dónde se escribe el nuevo `next_run_time` de una tarea dormida? ¿cómo sabe `task_delay` qué tarea es?

### Fase 2 — Preempción
- **Conceptos:** stack frame Cortex-M (M33 y M4), modo handler vs thread, SVC/PendSV, TCB, pilas privadas, cambio de contexto por tick.

**Entregable:** scheduler v2, preemptivo, con prioridades y delay.
**🔁 REPASO #1:** flashcards de Bloque 0-1 (30 min).

---

## Bloque 2 — Arquitectura por capas (3-4 semanas)

**Conceptos:** capas (app → servicio → protocolo → driver → HAL → hardware), contratos entre módulos, inversión de dependencias, portabilidad, top-half/bottom-half en ISRs, higiene de headers.

**Ejercicio clave:** refactorizar el código Pico actual para que compile también para STM32F407 tras una capa HAL — separar *qué hace* de *dónde corre*.

---

## Bloque 3 — Protocolos: de driver a stack (10-12 semanas)

Orden pedagógico: de lo simple a lo complejo; cada protocolo aplica la arquitectura del Bloque 2.

| Fase | Protocolo | Conceptos clave | Hardware |
|---|---|---|---|
| 3a | **I2C + SPI** | framing, clock polarity, ACK/NACK, polling→IRQ→DMA, ring buffers | BMP280/MPU6050 (~$2) + MCP2515 (es SPI) |
| 3b | **UART avanzado + LIN** | break detection, checksums, master con scheduling table, transporte | transistor/level shifter (~$1) |
| 3c | **CAN** | bit timing (TQ, sample point), arbitraje CSMA/CA, filtros/máscaras, contadores de error | 2× SN65HVD230 + STM32F407 (bxCAN) |
| 3d | **SENT** | canal rápido/lento, sync, CRC, bit-bang sin reloj | GPIO + level shifter |

**🔁 REPASO #2:** comparativa cruzada de protocolos (¿por qué LIN en carrocería y CAN en powertrain?).

---

## Bloque 4 — Capa de servicios y API unificada (3 semanas)

**Conceptos:** abstracción de frame común sobre protocolos distintos, modelo de suscripción, enrutamiento gateway, base de mensajes tipo DBC, diseño de API pública.

**Entregable:** gateway expone **una sola API** sin importar si el dato llegó por CAN, LIN o SENT.

---

## Bloque 5 — RTOS real + verificación (4 semanas)

**Conceptos:** FreeRTOS por dentro (comparado con el mini-RTOS propio), heap vs estática, tickless idle, APIs ISR-safe, herencia de prioridad.

**Banco de pruebas:** 2da Pico como dispositivo emulador (esclavo I2C/LIN/SENT), Raspberry Pi con Python orquestando tests, CI compilando para Pico **y** STM32, fuzzing con IA.

---

## Bloque 6 — Proyecto integrador + REPASO FINAL (3 semanas)

**Entregable:** **Gateway ECU funcional**: recibe por CAN/LIN/SENT → procesa → expone por UART/USB, con tests automatizados y documentación de arquitectura (ADRs + diagrama de capas). Luego repaso general estilo "explícame el sistema completo de punta a punta".

---

## Lista de compras (~$15-20)

| Item | Precio aprox. |
|---|---|
| Analizador lógico 24MHz | $10 |
| 2× SN65HVD230 (CAN transceiver) | $3 |
| Módulo BMP280 o MPU6050 | $2 |
| 2da Pico 2 | ~$5 |
| Resistencias/transistores (LIN, level shifting) | $1 |
