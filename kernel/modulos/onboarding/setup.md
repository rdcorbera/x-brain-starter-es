# Skill: Setup del Brain (`/x-setup`)

Inicializar y **personalizar** la base de conocimiento para el rol de quien la instala. Este skill es el adaptador del sistema: lo que en otros brains está cableado, aquí se genera según las respuestas. Regla central: **no fabricar nada** — si una respuesta es delgada, la sección queda delgada; usar las palabras del usuario, no reescribirlas en tono corporativo.

**Regla de zonas:** todo lo que este skill genera vive en `cerebro/` (y plantillas propias en `plugins/`). Jamás edita `kernel/`, `.github/` ni los stubs de `.claude/skills/`.

## Fase 0 — Escanear

Revisar el estado de `cerebro/`:

1. **Brain virgen** (PERFIL.md con TODOs, sin proyectos): seguir a la Fase 1.
2. **Brain ya personalizado** (PERFIL.md completo, hay contenido): preguntar si quiere empezar de cero o construir sobre lo existente.
3. **Cerebro adoptado** — el usuario copió aquí un `cerebro/` que le compartieron (el PERFIL describe a otra persona, o él lo indica): leer `cerebro/ESQUEMA.md` para entender su estructura y tipos. Si usa tipos propios, verificar que sus plantillas estén en `plugins/plantillas/` — si faltan, ofrecer regenerarlas desde la especificación de campos del ESQUEMA. Luego correr solo las rondas de identidad (1, 2 y 5) para el nuevo dueño, **sin tocar el conocimiento heredado**, y actualizar PERFIL.md. Si en cambio recibió una carpeta `raw/`, lo que corresponde es `/x-reconstruir`.

## Fase 1 — Entrevista (6 rondas)

Conversacional, una ronda a la vez. Al cerrar cada ronda, resumir brevemente lo capturado para que corrija antes de avanzar. Si una respuesta es vaga, sondear UNA vez y seguir.

**Ronda 1 — Quién eres.** Nombre, organización, rol exacto, hace cuánto, qué entregables produce tu trabajo, qué te energiza, idioma preferido para el contenido (default: español), contexto personal relevante.

**Ronda 2 — Tu proceso de trabajo.** ¿Cómo fluye tu trabajo de inicio a fin? ¿De quién recibes insumos y a quién entregas? ¿Tu planificación es trimestral, mensual, por sprints, continua? (esto define el "periodo" del sistema y el nombre de las carpetas de proyecto, ej. `2026-Q3-...` o `2026-08-...` — queda registrado en PERFIL.md).

**Ronda 3 — El mapa de personas.** Con qué roles y personas interactúas regularmente: nombre, rol, a quién reporta (si lo sabes), cómo trabaja. **Cada persona genera una ficha** con la plantilla `persona.md` en `cerebro/02-areas/personas/`.

**Ronda 4 — Tus áreas de conocimiento.** ¿Cuáles son tus responsabilidades continuas y dominios de conocimiento? (ej. para un vendedor: clientes, producto, competencia; para un abogado: contratos, regulación, litigios). Por cada área:
- Crear su carpeta en `cerebro/02-areas/` (kebab-case) con un `index.md` mínimo.
- Capturar los estándares, políticas o reglas que ya conoce como documentos `Lineamiento`.
- Preguntar si el rol necesita **tipos de documento propios** (ej. `Cliente`, `Experimento`, `Caso`). Si sí: crearlos siguiendo `kernel/modulos/extension/crear-plantilla.md` — plantilla en `plugins/plantillas/` y registro del tipo en `cerebro/ESQUEMA.md`. **Nunca** editando el catálogo del kernel.
- Preguntar si `cerebro/03-recursos/` necesita carpetas adicionales (crear las acordadas).
Lo que no sepa NO se inventa: se anota como hueco a capturar con el uso.

**Ronda 5 — Reglas de comunicación.** Cómo quiere que los agentes le hablen (directo / con matices / balanceado), manías o reglas específicas, restricciones de confidencialidad propias de su organización, y cualquier cosa que los agentes NUNCA deban hacer. Todo va a PERFIL.md.

**Ronda 6 — Objetivos del periodo (3 bloques).**
1. Proyectos/iniciativas asignadas activas (nombre + una línea cada una).
2. Objetivos personales del periodo (con métrica y fecha si es posible).
3. Objetivos de tu equipo o área que te tocan o quieres impulsar.
Empujar suavemente por especificidad: "certificación X antes de septiembre" vale 10 veces más que "aprender más".

## Fase 2 — Generar

1. Completar `cerebro/PERFIL.md` (en primera persona, con su voz): "Quién soy", "Mi rol y proceso" (incluido el formato de periodo), "Reglas de comunicación", "Confidencialidad" y "Estado actual".
2. Completar `cerebro/GOALS.md` con los 3 bloques (si el periodo no es trimestral, ajustar las menciones a "trimestre").
3. Crear las carpetas de áreas y recursos acordadas, con sus `index.md`.
4. Crear las fichas de Personas y regenerar `cerebro/02-areas/personas/ORGANIGRAMA.md` (Mermaid `graph TD` desde los campos `reporta-a`; relaciones desconocidas = nodos con "¿reporta a?" y su Pregunta transversal).
5. Crear los Lineamientos capturados y, si hubo tipos propios, sus plantillas en `plugins/plantillas/` + registro en `cerebro/ESQUEMA.md`.
6. Actualizar la cabecera de `cerebro/ESQUEMA.md`: dueño, fecha de setup, versión del kernel (`kernel/VERSION`), formato de periodo.
7. Por cada proyecto de la Ronda 6 que quiera arrancar ya, sugerir correr `/x-nueva-iniciativa` (no crearlos aquí).

## Fase 3 — Revisar y confirmar

Mostrar TODO lo generado antes de escribir. Iterar ediciones puntuales hasta que confirme. Solo entonces escribir archivos, actualizar `index.md` afectados y loguear en `cerebro/log.md`: `**Initialization**: Setup completado — N personas, N áreas, N lineamientos, N tipos propios, GOALS.md.`
