# Skill: Diagrama (`/x-diagrama`)

Genera o actualiza diagramas (flujos, procesos, secuencias, organización, arquitectura) a partir del contexto del proyecto. Usar el modelo más capaz disponible (Opus).

## 1. Contexto obligatorio antes de dibujar

Preguntar proyecto y clase de diagrama si no está claro: flujo | proceso | secuencia | entidades | organización | arquitectura | cronograma | otro. Luego leer, en este orden:
1. `CONTEXT.md` del proyecto.
2. `PLAN.md` del proyecto, si existe — obligatorio para la clase `cronograma`.
3. `00-insumos/` — la documentación recibida.
4. `02-decisiones/` — TODAS las decisiones aceptadas del proyecto (el diagrama debe reflejarlas).
5. Fichas de los Sistemas involucrados y Lineamientos aplicables de `cerebro/02-areas/`.
6. Versión anterior del mismo diagrama en `03-diagramas/`, si existe.

## 2. Generar

- Formato: Mermaid (`flowchart` para flujos y procesos; `sequenceDiagram` para secuencias; `erDiagram` para entidades; `graph TD` para organización; `gantt` para cronogramas; sintaxis C4 si el rol es técnico y lo pide). PlantUML solo a pedido.
- **Clase `cronograma`:** se genera desde el `PLAN.md`, una sección `gantt` por fase, cada tarea con su límite y sus dependencias (`after Tnn`). Las tareas sin fecha no se dibujan: se listan en "Supuestos y pendientes" como lo que impide que el cronograma esté completo. Al ser derivado, se regenera en vez de editarse a mano — si el plan cambió, se rehace.
- Plantilla `diagrama.md` (`kernel/esquema/plantillas/`), en `03-diagramas/`, nombre `<clase>-<tema>-vYYYY-MM-DD.md`. Si actualiza uno previo, versionar en el mismo archivo (historial de versiones) salvo cambio mayor.
- **Regla dura: nada inventado.** Todo elemento del diagrama debe rastrearse a un insumo, decisión, ficha o lineamiento. Lo que haga falta asumir se lista en "Supuestos y pendientes", y cada supuesto sin confirmar genera su documento `Pregunta` en `05-preguntas/`.
- Llenar "Decisiones reflejadas" con enlaces a las decisiones.

## 3. Revisar y cerrar

Mostrar el diagrama y los supuestos. Iterar hasta conformidad. Al confirmar: escribir, actualizar `index.md` y `log.md` del proyecto, regenerar `cerebro/PREGUNTAS-ABIERTAS.md` si se crearon preguntas.
