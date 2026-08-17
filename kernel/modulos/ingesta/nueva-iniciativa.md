# Skill: Nueva Iniciativa (`/x-nueva-iniciativa`)

Crea un proyecto en `cerebro/01-proyectos/` a partir de un proyecto asignado, objetivo personal o de equipo. Ingiere la documentación inicial.

## Entrevista (una pregunta a la vez, máximo 9)

Conversacional, una pregunta a la vez — no volcar las 9 de golpe. Cada una trae *Por qué importa* (qué decisión del sistema depende de la respuesta) y un *Ejemplo* de respuesta real: **son para desatascar**, se ofrecen si la pregunta no se entiende o la respuesta viene vaga, nunca como respuesta sugerida que el usuario solo tenga que aceptar. Las líneas *Produce* son para el agente: lo que esa respuesta va a crear.

**Si no sabe algo: usar defaults y dejar `<!-- TODO -->`. No presionar.** Y no preguntar lo que ya está en la base: buscar primero en `cerebro/PERFIL.md`, `cerebro/GOALS.md` y los proyectos existentes.

**1. ¿Cómo se llama y de qué origen es?** (proyecto-asignado | objetivo-personal | objetivo-equipo)
*Por qué importa:* el origen define contra qué se mide la iniciativa — a qué bloque de `cerebro/GOALS.md` se engancha (1 asignados, 2 personales, 3 de equipo) y con qué vara la revisa `/x-actualizacion-semanal`. Un objetivo personal que entra como proyecto asignado termina priorizado como si alguien lo estuviera esperando.
*Ejemplo:* "Migración del core de siniestros" — proyecto asignado, me toca el lado funcional.
*Produce:* la carpeta `cerebro/01-proyectos/<periodo>-nombre-kebab/` (el formato de periodo está definido en `cerebro/PERFIL.md`) y los campos `title`, `origen` y `periodo` del frontmatter.

**2. ¿Qué es?** Un párrafo: qué se construye o se logra, para quién, por qué ahora.
*Por qué importa:* es el encuadre que todo agente lee al abrir el proyecto. Sin él, cada sesión arranca preguntando de qué se trata, y las notas de reunión se archivan sin saber qué de lo dicho era relevante.
*Ejemplo:* Reemplazar el sistema legado de siniestros por la plataforma nueva, para el equipo de Operaciones. Ahora porque el proveedor del legado deja de darle soporte en diciembre.
*Produce:* el campo `description` y la sección "Qué es" de `CONTEXT.md`.

**3. ¿Qué significa "entregado"?**
*Por qué importa:* es la directiva del proyecto — la vara contra la cual los agentes leen cada sesión. Si el trabajo deriva sin avanzar hacia esto, lo señalan. Pedir algo verificable: "que quede bien" no permite decidir nada; una condición observable sí. Empujar suavemente por una fecha o una métrica.
*Ejemplo:* Los 4 tipos de siniestro operando en el sistema nuevo, el legado apagado y Operaciones capacitada — antes del 30 de noviembre.
*Produce:* la sección "Qué significa entregado" de `CONTEXT.md`.

**4. ¿Cómo fluye el trabajo en este proyecto de inicio a fin?**
*Repreguntar una vez:* «¿algo de esto no puede arrancar hasta que pase otra cosa?» — las dependencias reales son lo que después permite decir "esto está esperando a X" en vez de mostrar una lista plana.
*Por qué importa:* esta respuesta sirve dos veces. Las subcarpetas numeradas son ese flujo hecho visible (insumos → proceso → salida): si no coinciden con cómo se trabaja de verdad, cada ingesta tiene que improvisar dónde va cada cosa y el proyecto se desordena solo. Y las mismas etapas son las fases del `PLAN.md`.
*Ejemplo:* Recibo el brief del área → levanto requerimientos con Operaciones → diseño la solución con Tecnología → validación funcional por tipo de siniestro → salida a producción por olas.
*Produce:* las subcarpetas del proyecto y las fases del plan. **Si no lo sabe aún**, usar el default y decirle que puede reestructurarse después: `00-insumos/`, `01-reuniones/`, `02-decisiones/`, `03-diagramas/`, `04-entregables/`, `05-preguntas/`. `00-insumos/`, `01-reuniones/`, `02-decisiones/` y `05-preguntas/` existen SIEMPRE (otros skills dependen de ellas). Los originales crudos NO viven en el proyecto: van a `/raw/` global.

**5. ¿Qué sistemas, herramientas o productos de la organización toca?**
*Por qué importa:* los sistemas son conocimiento permanente, no del proyecto: sobreviven a su cierre y se comparten con los demás. Registrarlos acá es lo que permite después preguntar "qué proyectos tocan este sistema" y encontrar el contexto ya escrito en vez de reconstruirlo.
*Ejemplo:* El core legado de siniestros, la plataforma nueva del proveedor, el bus de integración y el tablero de Operaciones.
*Produce:* por cada uno sin ficha en `cerebro/03-recursos/sistemas-y-herramientas/`, una ficha mínima con TODOs (plantilla `sistema.md`), y el campo `sistemas` del frontmatter.

**6. ¿Quiénes están involucrados y con qué rol en esta iniciativa?**
*Por qué importa:* de acá salen los responsables de las preguntas abiertas — y una pregunta sin responsable no se resuelve, se acumula. También es lo que le permite a `/x-preparar-reunion` armar una agenda real cuando toque hablar con cada uno.
*Ejemplo:* Carlos Méndez (Tecnología) decide la arquitectura; Laura Pinto (Siniestros) es la referencia del proceso actual; el Comité aprueba el presupuesto por ola.
*Produce:* enlaces a las fichas de Personas existentes, fichas mínimas para las nuevas (plantilla `persona.md`), la sección "Personas clave" de `CONTEXT.md` y el campo `personas`.

**7. ¿Ya tienes documentación inicial?** (brief, requerimientos, propuesta, contrato — lo que sea que dispara el proyecto)
*Por qué importa:* es la fuente más densa que el proyecto va a tener, y la única que existe antes de la primera reunión. Procesarla ahora convierte el arranque en un inventario de requerimientos y una lista de dudas con responsable, en vez de una carpeta vacía.
*Ejemplo:* Sí, el brief que mandó Comercial y el contrato con el proveedor — los dejo en `inbox/`.
*Produce:* si hay, pedir que la suelte en `inbox/` o indique la ruta, y seguir el paso 2 de Construcción. Si no hay, el proyecto arranca vacío y se llena con `/x-procesar-inbox`.

**8. ¿Qué fechas o hitos ya están fijos?**
*Por qué importa:* sin fechas no hay "vencido", y sin vencido no hay seguimiento — solo una lista estática. Es lo que engancha el plan con la maquinaria que ya existe: los pendientes vencidos del briefing diario y la higiene de la semanal. Interesan las fechas que **no** se mueven, no las estimaciones.
*Ejemplo:* El comité aprueba presupuesto el primer martes de cada mes; el proveedor del legado corta soporte el 31 de diciembre; la primera ola tiene que estar en producción antes del cierre de trimestre.
*Produce:* las líneas `> **Hito:**` de cada fase del `PLAN.md` y las fechas límite de las tareas que cuelgan de ellas.

**9. ¿Dónde vive hoy el plan de este proyecto?** (Jira, Asana, un Excel del área, tu cabeza, no existe todavía)
*Por qué importa:* no es para armar la lista, es **para no duplicarla**. Si las tareas ya viven en un tracker, un plan en el cerebro es una segunda fuente de verdad que se desactualiza en dos semanas — y desde ahí todo lo que el cerebro diga del avance es falso. Es la regla de contradicciones aplicada por adelantado.
*Ejemplo:* Las tareas del equipo técnico viven en Jira y no las manejo yo; lo mío es el seguimiento funcional y lo llevo en la cabeza.
*Produce:* el campo `fuente-de-verdad` del `PLAN.md`. Con `cerebro`, el plan es la autoridad. Con `externa`, guarda **solo la tajada del usuario** más el puntero en `tracker-externo`, y ningún skill afirma progreso global.

> Las preguntas 8 y 9 son de planificación: si el proyecto no da para un plan (un objetivo personal chico, una iniciativa de dos semanas), se saltan sin insistir y el proyecto arranca sin `PLAN.md`. Se puede agregar después con `/x-plan`.

## Construcción

1. Crear la estructura: `CONTEXT.md` (plantilla `contexto-iniciativa.md`), `index.md`, `log.md`, y las subcarpetas definidas.
2. **Si hay documentación inicial**, archivar los originales en `raw/` según la convención de `/x-procesar-inbox` (nombre `YYYY-MM-DD-descripcion-tiny_uuid.ext` + fila en `raw/manifiesto.md`; binarios convertidos con `kernel/scripts/a-markdown.py` hacia `00-insumos/`) y generar un primer análisis (`00-insumos/analisis-inicial.md`, type: Playbook):
   - Resumen de la documentación en palabras propias.
   - Inventario de requerimientos/entregables detectados.
   - **Lista de dudas clasificadas por persona o área responsable** de resolverlas. Cada duda se crea como documento `Pregunta` en `05-preguntas/` con su responsable.
3. **Generar el `PLAN.md`** (plantilla `plan.md`) en la raíz del proyecto, salvo que las preguntas 8 y 9 se hayan salteado. Se arma cruzando lo que ya se respondió — no se pregunta nada nuevo:
   - **Raíz:** la definición de "entregado" de la pregunta 3, copiada literal. Toda tarea rastrea hasta ahí; si una tarea no aporta a eso, no entra.
   - **Fases:** las etapas del flujo de la pregunta 4, con los hitos de la 8 como línea `> **Hito:**`.
   - **Tareas:** el inventario de requerimientos/entregables del paso 2 es la fuente principal; los responsables salen de la pregunta 6 y las dependencias de la repregunta de la 4. Ids `T01`, `T02`… secuenciales.
   - **`fuente-de-verdad`:** lo que respondió la pregunta 9. Si es `externa`, generar solo el esqueleto de fases, la tajada del usuario y el puntero en `tracker-externo` — nunca copiar el tracker completo.
   - **Sin documentación inicial**, el plan sale delgado: las fases y las pocas tareas que el usuario haya mencionado. Es correcto — se completa con `/x-plan` o solo con la ingesta. **No rellenar con tareas plausibles.**
   - Enlazarlo desde el `index.md` del proyecto, como cualquier otra página.
4. Actualizar: `cerebro/GOALS.md` (enlazar el proyecto en su bloque), `index.md` de `cerebro/01-proyectos/`, sección "Estado actual" de `cerebro/PERFIL.md`, `cerebro/PREGUNTAS-ABIERTAS.md` si se crearon preguntas, `cerebro/PENDIENTES.md` si se creó el plan.
5. Loguear en `cerebro/log.md` global y en el `log.md` del proyecto.

## Confirmar

Mostrar la estructura creada, el resumen del CONTEXT.md, **el plan completo**, las preguntas generadas y los TODOs pendientes. El plan es lo que más conviene revisar en voz alta: una tarea mal atribuida se arrastra semanas.
