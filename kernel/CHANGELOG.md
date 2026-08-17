# Changelog del kernel

Historial de versiones del sistema. `/x-actualizar-sistema` muestra las entradas nuevas al actualizar; si una versión requiere pasos de migración, se listan en su sección **Migración**.

## 1.4.0 — 2026-08-16

El cerebro pasa de saber *qué no sabes* a saber *cuánto falta*. Hasta ahora rastreaba preguntas abiertas y pendientes sueltos de cada reunión, pero ningún proyecto tenía un plan contra el cual medirse: la actualización semanal preguntaba "¿qué cambió?" a mano abierta porque no había nada con qué comparar.

- **Tipo nuevo `Plan`**: cada proyecto puede tener un `PLAN.md` en su raíz, junto al `CONTEXT.md`, con las tareas que llevan hasta "entregado" agrupadas por fase, cada una con responsable, estado, fecha límite y el enlace a la fuente de donde salió. Estados: `pendiente | en-progreso | bloqueada | hecha | descartada` — el mismo vocabulario que ya usaban `Iniciativa` y `Pregunta`. El catálogo base pasa de 11 a 12 tipos.
- **Skill nuevo `/x-plan`**: crea el plan de un proyecto que no lo tiene (leyendo sus insumos, reuniones y decisiones), re-planifica en bloque cuando el proyecto cambia de rumbo, o reporta cuánto falta por fase, qué está vencido y qué está bloqueado. Es la vía para los proyectos que ya existían antes de esta versión.
- **Índice global `cerebro/PENDIENTES.md`**: gemelo de `PREGUNTAS-ABIERTAS.md`, autogenerado, con las tareas de todos los proyectos —vencidas primero— más una sección "Sin proyecto" para los pendientes de fichas `Persona` que no son trabajo de proyecto. Un solo lugar que mirar cada mañana.
- **El plan se mantiene solo con el uso**: `/x-procesar-inbox` convierte los acuerdos de cada reunión en filas del plan y cierra las que se entregaron; `/x-briefing-diario` interroga por lo vencido y lo bloqueado junto con las preguntas abiertas; `/x-actualizacion-semanal` hace el pulso de cada proyecto contra su plan en vez de contra la memoria; `/x-curar` audita que los planes no se estén podriendo; `/x-cierre-periodo` migra las tareas sin terminar y arranca el retro comparando lo planificado con lo que pasó.
- **Regla de fuente única**: lo que hace falta para entregar un proyecto vive en su `PLAN.md`, lo haga quien lo haga; las tablas "Pendientes conmigo" de las fichas `Persona` pasan a ser espejos con enlace a la fila, nunca listas independientes. Así `/x-preparar-reunion` cobra pendientes que no están vencidos en el papel y vigentes en la realidad.
- **`fuente-de-verdad: cerebro | externa`**: si las tareas ya viven en Jira, Asana o un Excel del área, el plan se declara espejo, guarda solo la tajada del usuario con un puntero al tracker real, y ningún skill afirma progreso global. Evita que el cerebro se vuelva una segunda fuente de verdad que se desactualiza y miente.
- **Dos preguntas nuevas en `/x-nueva-iniciativa`** (8 y 9): qué fechas o hitos ya están fijos, y dónde vive hoy el plan del proyecto. Se saltan sin insistir si el proyecto no da para un plan. Además, `/x-diagrama` gana la clase `cronograma`, que genera un `gantt` de Mermaid desde el plan.

### Migración

Los cerebros ya creados siguen funcionando sin cambios: **si un proyecto no tiene `PLAN.md`, cada skill se comporta exactamente como antes** y ofrece correr `/x-plan` una vez, sin insistir. Para ponerse al día:

1. **Correr `/x-curar`.** Detecta que el catálogo de tipos de tu `cerebro/ESQUEMA.md` no tiene `Plan` y propone actualizar esa tabla, crea `cerebro/PENDIENTES.md` si falta, y agrega su línea a `cerebro/index.md`. Esta actualización va por `/x-curar` y no por `/x-actualizar-sistema` a propósito: `cerebro/` es tu zona y el kernel no escribe en ella.
2. **Correr `/x-plan` en los proyectos activos** que quieras seguir con plan. No hace falta hacerlo en todos ni de una sola vez.

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
