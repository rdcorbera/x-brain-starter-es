# Skill: Setup del Brain (`/x-setup`)

Inicializar y **personalizar** la base de conocimiento para el rol de quien la instala. Este skill es el adaptador del sistema: lo que en otros brains está cableado, aquí se genera según las respuestas. Regla central: **no fabricar nada** — si una respuesta es delgada, la sección queda delgada; usar las palabras del usuario, no reescribirlas en tono corporativo.

**Regla de zonas:** todo lo que este skill genera vive en `cerebro/` (y plantillas propias en `plugins/`). Jamás edita `kernel/`, `.github/` ni los stubs de `.claude/skills/`.

**El guion de la entrevista vive en `kernel/modulos/onboarding/cuestionario-setup.md`** — las 6 rondas con sus preguntas, un ejemplo de respuesta por cada una y el detalle de para qué sirve. Este archivo define el proceso; ese define qué se pregunta. Leerlo antes de la Fase 2.

## Fase 0 — Escanear

Revisar el estado de `cerebro/`:

1. **Brain virgen** (PERFIL.md con TODOs, sin proyectos): seguir a la Fase 1.
2. **Brain ya personalizado** (PERFIL.md completo, hay contenido): preguntar si quiere empezar de cero o construir sobre lo existente.
3. **Cerebro adoptado** — el usuario copió aquí un `cerebro/` que le compartieron (el PERFIL describe a otra persona, o él lo indica): leer `cerebro/ESQUEMA.md` para entender su estructura y tipos. Si usa tipos propios, verificar que sus plantillas estén en `plugins/plantillas/` — si faltan, ofrecer regenerarlas desde la especificación de campos del ESQUEMA. Luego correr solo las rondas de identidad (1, 2 y 5) para el nuevo dueño, **sin tocar el conocimiento heredado**, y actualizar PERFIL.md. Si en cambio recibió una carpeta `raw/`, lo que corresponde es `/x-reconstruir`.

## Fase 1 — De dónde salen las respuestas

Antes de preguntar nada, ofrecer las tres vías. Muchas de las respuestas ya existen escritas en algún lado, y arrancar una entrevista de 30 minutos con material que el usuario ya tiene es hacerle repetir trabajo.

1. **Un cuestionario ya respondido.** El usuario copió `kernel/modulos/onboarding/cuestionario-setup.md` a `inbox/` (o a otra ruta fuera del kernel), lo llenó y da la ruta. Es también la vía para armar cerebros de demo o de prueba con respuestas ficticias.
2. **Documentos existentes.** Descripción del cargo, CV, presentación del equipo, organigrama, documento de OKRs, plan trimestral, acta de un comité — lo que sirva. En `inbox/` o en una ruta que indique. Puede combinarse con la vía 1.
3. **Entrevista en vivo.** El default: se conduce la Fase 2 conversando, sin material previo.

Si el usuario aporta material (vías 1 o 2):

- **Leerlo antes de preguntar.** Binarios (`.pdf`, `.docx`, `.pptx`, …) se convierten con `kernel/scripts/a-markdown.py` y se lee el `.md`; nunca se abre el binario directamente.
- **Precargar las rondas** con lo que el material responde, y **mostrar el mapeo** al usuario: qué ronda quedó cubierta, con qué fuente, y qué preguntas siguen abiertas.
- **La Fase 2 se reduce a confirmar y completar huecos.** No re-preguntar lo que el material ya respondió — es la regla de "no repetir preguntas cuya respuesta ya está en la base", aplicada al material de entrada.
- **No fabricar por inferencia.** Un CV dice el rol, no dice qué energiza a la persona ni cómo quiere que le hablen. Lo que el material no diga se pregunta o se deja como hueco; nunca se deduce.
- **Archivar los originales** en `raw/` siguiendo la convención de `/x-procesar-inbox` (`YYYY-MM-DD-descripcion-tiny_uuid.ext` + fila en `raw/manifiesto.md`), y vaciar de `inbox/` lo consumido. Así el setup queda reconstruible con `/x-reconstruir` igual que cualquier otra ingesta.
- **Confidencialidad primero.** Si el material trae datos sensibles (credenciales, datos personales de terceros), no entran al cerebro aunque estén en la fuente: se señala y se omite.

## Fase 2 — Entrevista (6 rondas)

Conducir según `kernel/modulos/onboarding/cuestionario-setup.md`. Conversacional, una ronda a la vez — no volcar el cuestionario entero de golpe. Al cerrar cada ronda, resumir brevemente lo capturado para que corrija antes de avanzar. Si una respuesta es vaga, sondear UNA vez y seguir. Si el usuario no sabe algo, se anota como hueco a llenar con el uso: no se presiona ni se inventa.

Los *ejemplos* del cuestionario son para desatascar: si una pregunta no se entiende, se ofrece el ejemplo — nunca como respuesta sugerida que el usuario solo tenga que aceptar.

| Ronda | Qué captura | Qué produce |
|---|---|---|
| 1 | Quién eres | `PERFIL.md` → "Quién soy"; idioma del cerebro |
| 2 | Tu proceso de trabajo | `PERFIL.md` → "Mi rol y proceso"; **formato de periodo** |
| 3 | El mapa de personas | Fichas `Persona` + `ORGANIGRAMA.md` |
| 4 | Tus áreas de conocimiento | Carpetas de `02-areas/`, `Lineamiento`s, tipos propios, carpetas de `03-recursos/` |
| 5 | Reglas de comunicación | `PERFIL.md` → "Reglas de comunicación" y "Confidencialidad" |
| 6 | Objetivos del periodo | `GOALS.md` (3 bloques) |

## Fase 3 — Generar

1. Completar `cerebro/PERFIL.md` (en primera persona, con su voz): "Quién soy", "Mi rol y proceso" (incluido el formato de periodo), "Reglas de comunicación", "Confidencialidad" y "Estado actual".
2. Completar `cerebro/GOALS.md` con los 3 bloques (si el periodo no es trimestral, ajustar las menciones a "trimestre").
3. Crear las carpetas de áreas y recursos acordadas, con sus `index.md`.
4. Crear las fichas de Personas y regenerar `cerebro/02-areas/personas/ORGANIGRAMA.md` (Mermaid `graph TD` desde los campos `reporta-a`; relaciones desconocidas = nodos con "¿reporta a?" y su Pregunta transversal).
5. Crear los Lineamientos capturados y, si hubo tipos propios, sus plantillas en `plugins/plantillas/` + registro en `cerebro/ESQUEMA.md` (siguiendo `kernel/modulos/extension/crear-plantilla.md`).
6. Actualizar la cabecera de `cerebro/ESQUEMA.md`: dueño, fecha de setup, versión del kernel (`kernel/VERSION`), formato de periodo.
7. Por cada proyecto de la Ronda 6 que quiera arrancar ya, sugerir correr `/x-nueva-iniciativa` (no crearlos aquí).

## Fase 4 — Revisar y confirmar

Mostrar TODO lo generado antes de escribir. Iterar ediciones puntuales hasta que confirme. Solo entonces escribir archivos, actualizar `index.md` afectados y loguear en `cerebro/log.md`: `**Initialization**: Setup completado — N personas, N áreas, N lineamientos, N tipos propios, GOALS.md.` Si hubo material de entrada, agregar a la línea: `Respuestas desde <fuente>, archivada en /raw/.`
