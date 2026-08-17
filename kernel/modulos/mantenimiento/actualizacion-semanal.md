# Skill: Actualización Semanal (`/x-actualizacion-semanal`)

Pulso semanal: objetivos (3 bloques), estado de cada proyecto contra su plan, y pendientes vencidos.

## Fase 1 — Escanear antes de preguntar

Leer: "Estado actual" de `cerebro/PERFIL.md`, `cerebro/GOALS.md`, el `CONTEXT.md` **y el `PLAN.md`** de cada proyecto en `cerebro/01-proyectos/`, `cerebro/PREGUNTAS-ABIERTAS.md`, `cerebro/PENDIENTES.md`, y los pendientes de las fichas Persona. El objetivo: preguntar solo por lo que pudo cambiar, no hacer repetir todo.

## Fase 2 — Pulso semanal

Mostrar lo que decía la semana pasada y preguntar: ¿qué está funcionando?, ¿qué no?, ¿qué estás postergando o debes decidir?, ¿hacia qué te sientes jalado?, ¿deadlines próximos? ("igual" = mantener lo anterior).

## Fase 3 — Objetivos (los 3 bloques de GOALS.md)

Por bloque (iniciativas / personales / área): ¿algún avance, número nuevo o cambio de plan? Tight: si nada cambió, seguir. No hacer re-justificar objetivos existentes.

## Fase 4 — Proyectos (contra el plan, no contra la memoria)

Por cada proyecto activo **con `PLAN.md`**: mostrar su avance por fase, las tareas `en-progreso` y las vencidas, y preguntar por esas — no "¿qué cambió en X?" a mano abierta. Una tanda por proyecto, máximo un follow-up. Cada respuesta actualiza el estado de la tarea (`hecha`, `en-progreso`, `bloqueada`, `descartada`), igual que en el briefing.

Si el proyecto **no tiene `PLAN.md`**: mostrar su Estado actual y preguntar "¿Qué cambió en [X] esta semana?", como siempre. Al cerrar la fase, ofrecer `/x-plan` una vez para los proyectos activos sin plan — sin insistir, y nunca más de una vez por sesión.

Si el plan tiene `fuente-de-verdad: externa`, advertirlo antes de preguntar: el cerebro solo ve la tajada del usuario, y su `ultima-revision` es de tal fecha.

## Fase 5 — Higiene

- Listar pendientes de terceros vencidos (>7 días): "¿sigue vivo, lo escalas o lo sueltas?"
- Listar tareas vencidas sin movimiento (>14 días): "¿sigue, se reprograma o se descarta?" — las que se descartan pasan a `descartada` con su razón en "Fuera de alcance", no se borran.
- Listar tareas `bloqueada` sin `Pregunta` enlazada: son un error del plan, hay que enlazarlas o desbloquearlas.
- Listar preguntas abiertas >14 días sin avances: ¿siguen importando? Las muertas pasan a `estado: respondida` con nota "ya no relevante".
- Si `inbox/` tiene material sin procesar, avisar y ofrecer correr /x-procesar-inbox primero.

## Fase 6 — Escribir

Mostrar resumen de todos los cambios ANTES de editar. Luego: "Estado actual" en `cerebro/PERFIL.md` (con fecha), `cerebro/GOALS.md` (solo lo que cambió), sección "Estado actual" del CONTEXT.md de cada proyecto que cambió, el `PLAN.md` de cada proyecto tocado (con su `ultima-revision`), `cerebro/PREGUNTAS-ABIERTAS.md`, `cerebro/PENDIENTES.md`, y logs (`cerebro/log.md` global + `log.md` de proyectos tocados). **Nunca reestructurar** un CONTEXT.md ni un PLAN.md durante la semanal: solo estado y progreso. Re-planificar de verdad —agregar fases, rehacer el árbol de tareas— es `/x-plan`.
