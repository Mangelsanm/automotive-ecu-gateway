# Learnings — Flashcards y repasos

Registro de aprendizajes para refrescar la ventana de contexto. Cada bloque cierra con un **REPASO**: responder las tarjetas del bloque anterior sin mirar, en voz alta o por escrito.

**Formato de tarjeta:** `## [Bloque/Fase] Pregunta` → respuesta debajo (ocultar al repasar).

---

## Repaso #1 (al cerrar Bloque 1)

_(tarjetas se añaden durante Bloque 1)_

## Repaso #2 (al cerrar Bloque 3)

_(tarjetas se añaden durante Bloques 2-3)_

## Repaso final (Bloque 6)

_(tarjetas de todo el plan)_

---

# Tarjetas

## [B0] ¿Qué es un ADR y cuándo se escribe?
Una Architecture Decision Record documenta una decisión de arquitectura relevante: contexto, decisión, consecuencias. Se escribe al tomarla, no después. No todo cambio es ADR: solo las decisiones que cuesta revertir o que guían futuras.

## [B0] ¿Cuál es la regla de capas del proyecto?
app → services → protocols → drivers → hal. Un módulo solo incluye cabeceras de su capa o inferior. Lo único que toca registros es `hal/` (raspBerryPico.h).

## [B0] ¿Qué es test-first con IA en este workflow?
1) spec en `specs/` antes que código, 2) IA propone diseño → yo critico/decido, 3) implemento en unidades pequeñas, 4) IA revisa el diff (preguntas, no reescribir), 5) aprendizaje en learnings.md.
