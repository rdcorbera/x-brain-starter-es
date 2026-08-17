# Skill: Plan (`/x-plan`)

Crea, re-planifica o reporta el `PLAN.md` de un proyecto: las tareas que llevan hasta "entregado", con responsable, estado y fecha límite. Es el skill que le da al cerebro una respuesta a "¿cuánto falta?".

`/x-nueva-iniciativa` genera el plan de los proyectos nuevos, pero corre una sola vez. Este skill es la vía para los proyectos que ya existen y para re-planificar a mitad de camino.

Preguntar (si no lo dijo ya): **¿de qué proyecto?** y **¿crear, re-planificar o reportar?** Si el proyecto no tiene `PLAN.md`, el modo es crear.

## Reglas que atraviesan los tres modos

- **Toda tarea rastrea a "entregado".** La definición de éxito del `CONTEXT.md` es la raíz: si una tarea no aporta a eso, no entra — y si el usuario insiste, es señal de que "entregado" está mal escrito y hay que corregirlo ahí primero.
- **Nunca fabricar.** Las tareas se proponen desde lo que ya está escrito (insumos, reuniones, decisiones). Lo que no esté en el material se pregunta o queda como hueco; una tarea inventada es peor que una tarea faltante porque nadie la va a cuestionar.
- **El plan no es la lista de pendientes personales.** Solo entra trabajo necesario para entregar el proyecto, lo haga el usuario o un tercero. Lo que alguien debe pero no es trabajo del proyecto vive en la tabla "Pendientes conmigo" de su ficha `Persona`. Lo que no se sabe es una `Pregunta`, no una tarea.
- **Mostrar antes de escribir**, siempre: el plan completo en modo crear, el diff en modo re-planificar.

## Modo crear

1. **Leer el proyecto entero** antes de proponer nada: `CONTEXT.md` (la definición de "entregado" y el flujo), `00-insumos/` (los requerimientos), `01-reuniones/` (lo acordado), `02-decisiones/` (lo que ya se resolvió) y `05-preguntas/` (lo que bloquea).
2. **Preguntar lo que el material no dice** — una pregunta a la vez, máximo tres:
   - **¿Dónde vive hoy el plan de este proyecto?** (Jira, Asana, un Excel, la cabeza, no existe). Define `fuente-de-verdad`: `cerebro` si el plan es la autoridad, `externa` si ya vive en un tracker. Con `externa`, el plan guarda **solo la tajada del usuario** más el puntero en `tracker-externo`, y ningún skill afirma progreso global.
   - **¿Qué fechas o hitos ya están fijos?** Solo las que no se mueven: comités, salidas a producción, vencimientos de contrato. Van como línea `> **Hito:**` de la fase que corresponda.
   - **¿Algo no puede arrancar hasta que pase otra cosa?** Las dependencias reales, que son lo que después permite decir "esto está esperando a X".
3. **Proponer las tareas agrupadas por fase.** Las fases salen del flujo de trabajo del `CONTEXT.md` (y, si el proyecto no lo tiene claro, de las subcarpetas). Cada tarea con su responsable, su límite si lo hay, y el enlace de origen.
4. **Escribir** `PLAN.md` en la raíz del proyecto (plantilla `plan.md`), tras confirmación.

## Modo re-planificar

Para cuando el proyecto cambia de rumbo y hay que mover varias tareas a la vez (una sola tarea se cierra sola en `/x-procesar-inbox` o en el briefing).

1. Mostrar el plan vigente con el estado de cada tarea y qué está vencido.
2. Recoger los cambios: tareas nuevas, cerradas, reprogramadas o descartadas; fases que se agregan o desaparecen.
3. **Mostrar el diff** (qué se agrega, qué cambia de estado, qué se descarta y por qué) y confirmar antes de escribir.
4. Las tareas descartadas **no se borran**: pasan a `estado: descartada` y su razón va a "Fuera de alcance", que es lo que evita que la misma discusión vuelva cada dos semanas.

## Modo reportar

No escribe nada salvo que el usuario lo pida. Entregar en el chat:

1. **Avance por fase** — cuántas tareas hechas sobre el total, y qué falta para cerrar la fase en curso.
2. **Vencidas** — con cuántos días de atraso y de quién es cada una.
3. **Bloqueadas** — con el enlace a la `Pregunta` o decisión que las traba. Una tarea bloqueada sin nada enlazado es un error del plan: señalarlo.
4. **Sin dueño ni fecha** — las que no se van a mover solas.
5. **Riesgo contra los hitos** — si un hito fijo tiene tareas abiertas que no llegan, decirlo.

Si `fuente-de-verdad: externa`, encabezar el reporte con la advertencia: el cerebro solo ve la tajada del usuario y `ultima-revision` es de tal fecha.

## Convenciones del plan

- **Estados:** `pendiente | en-progreso | bloqueada | hecha | descartada`. Son el mismo vocabulario que ya usan `Iniciativa` y `Pregunta`.
- **Ids estables:** `TNN` secuencial por proyecto. **Nunca se reusan ni se renumeran** — los logs, las preguntas y las notas de reunión los citan.
- **Dependencias** como sufijo en la celda de la tarea: `(tras T03)`.
- **`bloqueada` exige un enlace** en Origen a la `Pregunta` o decisión que la traba. Sin eso, "bloqueada" no dice nada y nadie la puede perseguir.
- **Las tareas `hecha` no se borran:** el plan es también el registro de lo hecho y el insumo del retro en `/x-cierre-periodo`.

## Cerrar

1. Actualizar `ultima-revision` del plan.
2. Regenerar `cerebro/PENDIENTES.md` (ver formato en el propio archivo: por proyecto, vencidas primero, más la sección "Sin proyecto" con los pendientes de fichas `Persona`).
3. Espejar en la ficha `Persona` de cada responsable externo las tareas que le toquen, con enlace a la fila del plan — la ficha es vista derivada, nunca lista independiente.
4. Loguear en el `log.md` del proyecto y en `cerebro/log.md` global.
