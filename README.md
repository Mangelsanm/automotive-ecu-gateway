# Automotive ECU Gateway

Proyecto de aprendizaje de sistemas embebidos con enfoque en **arquitectura de software** y **protocolos de comunicación automotrices**, construido para escalar desde un scheduler cooperativo hasta un mini-RTOS y finalmente un gateway multi-protocolo.

## Objetivo

Dominar la ruta completa **driver → HAL → servicio → API** con los protocolos: UART, LIN, CAN, SENT, I2C y SPI — el skill central de un arquitecto de software embebido.

## Estado actual (Bloque 0)

- [x] Estructura de repo por capas
- [x] Migración del scheduler cooperativo (base del Bloque 1)
- [x] Workflow con IA documentado (AGENTS.md)
- [ ] Bloque 1: mini-RTOS preemptivo

## Estructura

```
docs/       plan, ADRs, aprendizajes
specs/      especificaciones por módulo (test-first)
src/
  kernel/   scheduler, timebase, soft_timer, event
  hal/      capa de abstracción (pico2/ hoy, stm32f407/ después)
  drivers/  uart, gpio, timer
  protocols/ i2c, spi, lin, can, sent (vacío — Bloque 3)
  services/ API unificada (vacío — Bloque 4)
  app/      lógica de aplicación
tests/      unit/ e hil/ (banco de pruebas)
```

## Build (Pico 2 W)

Requisitos: Pico SDK 2.2.0 + extensión de VS Code para Pico.

```
cmake -B build
cmake --build build
```

Salida: `automotive-ecu-gateway.uf2` → arrastrar al drive de la Pico.

## Roadmap

Ver [docs/plan/00-roadmap.md](docs/plan/00-roadmap.md).
