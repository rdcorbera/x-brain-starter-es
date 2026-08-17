# Skill: Briefing Diario (`/x-briefing-diario`)

El Interrogador: ritual de inicio del día (5 minutos). Repasa las preguntas abiertas y los pendientes vencidos, y registra lo averiguado y lo avanzado. Tono: conciso, cero relleno.

## 1. Priorizar

Leer `cerebro/PREGUNTAS-ABIERTAS.md`, `cerebro/PENDIENTES.md` y los CONTEXT.md de proyectos activos. Seleccionar **3-5 ítems para hoy** de los dos índices juntos, con este criterio, en orden:

1. **Tareas vencidas** (fecha límite pasada) y **tareas bloqueadas** de proyectos activos.
2. Preguntas bloqueantes de proyectos en estado `bloqueada` o `en-progreso`.
3. Ítems cuyo responsable es alguien con quien el usuario se reúne hoy (preguntar al inicio: "¿Con quién tienes reuniones hoy?" — si responde, cruzar).
4. Los más antiguos sin avances registrados.

Mezclar los dos tipos en una sola lista corta: para el usuario no son dos rituales, es "qué tengo encima hoy". Si un proyecto no tiene `PLAN.md`, se prioriza solo con preguntas, como siempre, y se puede ofrecer `/x-plan` al cerrar (una vez, sin insistir).

## 2. Interrogar

Uno a la vez. Según el tipo:

**Pregunta:**
> "[Pregunta] — responsable: [X], abierta hace [N] días. ¿Averiguaste algo?"

- Respuesta parcial → agregar entrada fechada en la sección **Avances** del documento Pregunta.
- Respuesta completa → llenar **Respuesta**, cambiar `estado: respondida`, y evaluar si debe promoverse a Lineamiento o a ficha de Sistema (proponerlo). Si la pregunta bloqueaba una tarea, desbloquearla en el plan.
- "Nada aún" → seguir sin insistir.

**Tarea:**
> "[T04] [Tarea] — [X], vencía el [fecha] ([N] días). ¿Avanzó?"

- Avanzó y quedó lista → `estado: hecha` en el `PLAN.md`, sin borrar la fila.
- Avanzó pero sigue → `en-progreso`, y si la fecha ya no aplica, preguntar la nueva (una vez; si no la sabe, dejarla y anotarlo).
- No avanzó porque algo la traba → `bloqueada` + crear la `Pregunta` correspondiente y enlazarla desde la fila. Una tarea bloqueada sin nada enlazado no se puede perseguir.
- Ya no tiene sentido → `descartada`, con la razón en "Fuera de alcance" del plan.

Si al responder menciona algo nuevo que no cuadra → proponer crear una Pregunta, o una tarea nueva si es trabajo del proyecto.

## 3. Cerrar

- Regenerar `cerebro/PREGUNTAS-ABIERTAS.md` y `cerebro/PENDIENTES.md` si hubo cambios, y actualizar `ultima-revision` de los planes tocados.
- Mencionar pendientes vencidos de terceros: "[Persona] te debe [X] desde hace [N] días — ¿lo persigues hoy?"
- Loguear en `cerebro/log.md` solo si hubo respuestas o avances registrados.
- Terminar con las 1-3 cosas más importantes del día, leídas del estado de los proyectos y de lo que está por vencer.
