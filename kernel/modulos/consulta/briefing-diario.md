# Skill: Briefing Diario (`/x-briefing-diario`)

El Interrogador: ritual de inicio del día (5 minutos). Repasa las preguntas abiertas y registra lo averiguado. Tono: conciso, cero relleno.

## 1. Priorizar

Leer `cerebro/PREGUNTAS-ABIERTAS.md` y los CONTEXT.md de proyectos activos. Seleccionar las **3-5 preguntas más relevantes hoy** con este criterio, en orden:
1. Bloqueantes de proyectos en estado `bloqueada` o `en-progreso`.
2. Preguntas cuyo responsable es alguien con quien el usuario se reúne hoy (preguntar al inicio: "¿Con quién tienes reuniones hoy?" — si responde, cruzar).
3. Las más antiguas sin avances registrados.

## 2. Interrogar

Por cada pregunta seleccionada, una a la vez:
> "[Pregunta] — responsable: [X], abierta hace [N] días. ¿Averiguaste algo?"

- Respuesta parcial → agregar entrada fechada en la sección **Avances** del documento Pregunta.
- Respuesta completa → llenar **Respuesta**, cambiar `estado: respondida`, y evaluar si la respuesta debe promoverse a Lineamiento o a ficha de Sistema (proponerlo).
- "Nada aún" → seguir sin insistir.
- Si al responder menciona algo nuevo que no cuadra → proponer crear una Pregunta nueva.

## 3. Cerrar

- Regenerar `cerebro/PREGUNTAS-ABIERTAS.md` si hubo cambios.
- Mencionar pendientes vencidos de terceros: "[Persona] te debe [X] desde hace [N] días — ¿lo persigues hoy?"
- Loguear en `cerebro/log.md` solo si hubo respuestas registradas.
- Terminar con las 1-3 cosas más importantes del día según los estados de proyecto.
