# Changelog del kernel

Historial de versiones del sistema. `/x-actualizar-sistema` muestra las entradas nuevas al actualizar; si una versión requiere pasos de migración, se listan en su sección **Migración**.

## 1.3.0 — 2026-08-16

La entrevista de `/x-setup` se vuelve un guion propio, con ejemplos, y deja de exigir responder en vivo:

- **Cuestionario como archivo aparte**: las 6 rondas viven ahora en `kernel/modulos/onboarding/cuestionario-setup.md`. `setup.md` define el proceso; el cuestionario define qué se pregunta. Editar las preguntas ya no obliga a tocar la lógica del skill.
- **Cada pregunta con ejemplo y propósito**: toda pregunta trae un *Ejemplo* de respuesta real —para que el usuario entienda qué nivel de detalle se espera— y cada ronda un bloque *Para qué sirve* que explica al agente qué decisión del sistema depende de esa respuesta. Los ejemplos son para desatascar, nunca para sugerir la respuesta.
- **Origen de las respuestas (Fase 1 nueva)**: antes de preguntar nada, el skill ofrece tres vías — un cuestionario ya respondido, documentos que el usuario ya tenga (descripción del cargo, organigrama, OKRs), o la entrevista en vivo. Con material, la entrevista se reduce a confirmar y llenar huecos, y los originales se archivan en `raw/` con su fila en el manifiesto, dejando el setup reconstruible con `/x-reconstruir`.
- **Sin inferencias**: lo que el material no diga se pregunta o queda como hueco. Un CV dice el rol, no dice qué energiza a la persona ni cómo quiere que le hablen.
- **Cerebros de demo**: llenar una copia del cuestionario con respuestas ficticias es ahora la vía soportada para armar brains de prueba.
- **"Qué te energiza" reformulada**: la pregunta confundía. Ahora es "de todo eso, ¿qué parte te da energía y cuál sientes más como trámite?", con su ejemplo y la explicación de que calibra el énfasis de `/x-briefing-diario` y `/x-actualizacion-semanal`.

### Migración

Ninguna. `/x-setup` se sigue invocando igual y los cerebros ya generados no se ven afectados.

## 1.2.0 — 2026-07-21

Las carpetas del inbox ahora dicen a dónde va su contenido en `/x-procesar-inbox`:

- **Carpeta como señal de destino**: si una carpeta del inbox corresponde a un proyecto, un área o una carpeta de recursos, todo lo que cuelga de ella se atribuye ahí (recursivo, a cualquier profundidad) sin preguntar archivo por archivo. La carpeta decide el destino; el contenido sigue decidiendo el tipo.
- **Correspondencia tolerante**: se compara en kebab-case, sin acentos y sin el prefijo de periodo, así que `inbox/migracion-erp/` encuentra a `01-proyectos/2026-q3-migracion-erp/`.
- **Nunca adivinar**: si el nombre no corresponde a nada existente —o corresponde a varios— se pregunta y se ofrece crear el proyecto con `/x-nueva-iniciativa`; si el contenido de un archivo contradice a su carpeta, se señala en vez de forzarlo.
- **Limpieza**: al terminar se borran las carpetas que quedaron vacías; las que retienen archivos no convertibles se conservan y se reportan. `raw/` sigue siendo plano: el destino vive en el manifiesto.

## 1.1.0 — 2026-07-17

Lineamientos de ingesta reforzados en `/x-procesar-inbox`:

- **Regla de formatos explícita**: solo se leen e ingieren directamente `.md`, `.txt` y `.vtt`; los formatos convertibles pasan primero por `a-markdown.py`, y los no convertibles se reportan al usuario sin intentar ingestarlos (eficiencia de tokens, cero invención).
- **Transcripciones `.vtt`**: antes de integrar se elabora un resumen extenso y detallado — participantes, temas, acuerdos, preguntas y lo relevante de la reunión — que es el cuerpo de la nota `Reunion`; la transcripción cruda se cita, no se copia.
- **Correos**: los nombres de `To`/`From`/`CC` no generan fichas `Persona` por sí solos; solo se registra a quien es relevante en la conversación.

## 1.0.0 — 2026-07-16

Primera versión de X-Brain, evolución de [second-brain-starter-es](https://github.com/rdcorbera/second-brain-starter-es). Misma filosofía (LLM Wiki + PARA + OKF v0.1), nueva arquitectura:

- **Zonas de propiedad**: `kernel/` (el sistema, actualizable desde GitHub sin conflictos), `cerebro/` (el conocimiento, portable), `raw/` (fuentes crudas únicas e inmutables + manifiesto), `plugins/` (extensiones del usuario), `inbox/` (entrada transitoria).
- **La personalización ya no toca el kernel**: `/x-setup` escribe `cerebro/PERFIL.md` y `cerebro/ESQUEMA.md` en vez de editar las instrucciones del sistema.
- **Skills con prefijo `x-`** y patrón stub: la lógica vive una sola vez en `kernel/modulos/` (onboarding, ingesta, consulta, registro, mantenimiento, extension); `.claude/skills/` y `.github/prompts/` solo la invocan.
- **Skills nuevos**: `/x-actualizar-sistema` (actualización del kernel), `/x-reconstruir` (reconstruir el cerebro desde `raw/`), `/x-crear-skill` y `/x-crear-plantilla` (extensión vía plugins).
- **Raw único**: los originales procesados se archivan en `/raw/` como `YYYY-MM-DD-descripcion-tiny_uuid.ext`, registrados en `manifiesto.md` — ya no se dispersan por proyecto.
