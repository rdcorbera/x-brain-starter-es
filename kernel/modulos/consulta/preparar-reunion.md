# Skill: Preparar Reunión (`/x-preparar-reunion`)

Genera la agenda para una reunión: pendientes con esa persona, preguntas de su dominio y contexto relevante.

Preguntar (si no lo dijo ya): **¿con quién es la reunión y sobre qué proyecto/tema?**

## Recolectar

1. Ficha `Persona` del asistente (`cerebro/02-areas/personas/`): historial relevante y pendientes que no son trabajo de proyecto.
2. `cerebro/PENDIENTES.md` y el `PLAN.md` de los proyectos donde esta persona es responsable: **el plan es la fuente de los pendientes de trabajo**; la tabla de la ficha es un espejo que puede estar viejo. Leer los dos y, si no coinciden, señalarlo al usuario y corregir el espejo.
3. `cerebro/PREGUNTAS-ABIERTAS.md`: preguntas cuyo `responsable` es esta persona o su rol, y preguntas del dominio que maneja.
4. Si hay proyecto: `CONTEXT.md`, últimas notas de `01-reuniones/` con esta persona, y decisiones recientes que la involucren.
5. Lineamientos de su área que estén `en-revision` o con TODOs.

## Entregar

Una agenda en el chat (no crear archivo salvo que lo pida):

1. **Objetivo de la reunión** (una línea).
2. **Preguntas a hacer** — ordenadas: bloqueantes primero. Cada una con el enlace a su documento Pregunta.
3. **Pendientes a cobrar** — lo que esta persona debe, con su id de tarea, fecha límite y días de atraso si está vencida.
4. **Pendientes a entregar** — lo que yo le debo, igual.
5. **Contexto útil** — 2-3 líneas de historial que conviene tener presente.

Al final recordar: "Después de la reunión, suelta la transcripción o tus notas en inbox/ y corre /x-procesar-inbox."
