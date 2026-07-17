# Skill: Procesar Inbox (`/x-procesar-inbox`)

El Bibliotecario, modo ingesta. Procesar TODO lo que haya en `inbox/` (excepto README.md). Principio rector: **integrar, no solo archivar** — una fuente nueva puede tocar muchas páginas existentes.

## 0. Regla de formatos (eficiencia de tokens)

La ingesta debe ser eficiente en tokens: **solo se leen e ingieren directamente `.md` (markdown), `.txt` (notas) y `.vtt` (transcripciones)**. Para todo lo demás:

- **Convertible** (`.pptx .docx .xlsx .pdf .drawio .html .yaml`) → se transforma PRIMERO a markdown con `kernel/scripts/a-markdown.py` (paso 2.5) y se ingesta el `.md` resultante. El original jamás se abre ni se interpreta: leerlo quema miles de tokens y abre la puerta a inventar.
- **No convertible** (cualquier otra extensión: imágenes, audio, video, `.zip`, binarios legacy `.doc/.ppt/.xls`, formatos desconocidos) → **no se intenta ingestar**. Se deja en `inbox/` y se informa al usuario al final: qué archivo es, por qué no se pudo, y qué haría falta (ej. exportarlo a un formato moderno, pasarle OCR, pegar el contenido como texto). Nunca "deducir" el contenido de un archivo que no se puede leer.

Determinar qué es cada archivo (transcripción, documento recibido, nota rápida, diagrama, correo) y a qué proyecto o área pertenece. Si es ambiguo, preguntar — nunca adivinar el proyecto.

## 2. Preservar el original (capa cruda inmutable, en un solo lugar)

Antes de transformar: mover el original de `inbox/` a **`raw/`** con nombre:

```
YYYY-MM-DD-descripcion-tiny_uuid.ext
```

- **Fecha**: la del contenido si se conoce (ej. la fecha de la reunión o la del prefijo del nombre original); si no, la de hoy.
- **Descripción**: kebab-case, corta y autocontenida.
- **tiny_uuid**: sufijo único de 6 caracteres hex para evitar colisiones. Generarlo con `python3 -c "import uuid; print(uuid.uuid4().hex[:6])"` (en Windows: `python`); si Python no está disponible, elegir 6 hex al azar y verificar que el nombre no exista ya en `raw/`.

Registrar el archivo en `raw/manifiesto.md` (agregar fila al final de la tabla): archivo en raw, nombre original, destino (proyecto o área), y páginas generadas (se completa al terminar el paso 4).

Los archivos de `raw/` NUNCA se editan ni se borran — son la fuente de verdad que el wiki cita, y junto con el manifiesto permiten reconstruir el cerebro con `/x-reconstruir`.

## 2.5 Normalizar a markdown (si el original no es `.md`/`.txt`/`.vtt`)

Aplicando la Regla de formatos (paso 0): `.pptx .docx .xlsx .pdf .drawio .html .yaml` **no se abren ni se interpretan directamente** — se convierten:

```bash
python3 kernel/scripts/a-markdown.py raw/<archivo> --out <cerebro/01-proyectos/<proyecto>/00-insumos/> --origen /raw/<archivo>
```

En Windows el intérprete se llama `python` (o `py`), no `python3`. El resto es idéntico: el script se re-ejecuta solo dentro de su venv en cualquier plataforma.

Deja un `.md` (`type: Insumo`; `type: Diagrama` si es `.drawio` → va a `03-diagramas/`) que cita al raw con el puntero `/raw/...`. **Leer ese `.md`, nunca el binario:** la conversión es determinista y cuesta cero tokens; leer el binario los quema y abre la puerta a inventar.

- Completar el `description: <pendiente>` que dejó el script — es el único campo que necesita criterio.
- Si trae **«Avisos de conversión»**, atenderlos, no borrarlos: dicen qué se perdió. Un PDF sin capa de texto o una hoja truncada que importe → decírselo al usuario o abrir una `Pregunta`; nunca rellenar el hueco a ojo.
- `.doc/.ppt/.xls` legacy: el script falla pidiendo «Guardar como» moderno. Reportarlo y dejar el archivo en el inbox (no moverlo a `raw/` hasta tener la versión legible).

El `.md` derivado es un insumo más: sigue al paso 3 y alimenta al wiki como cualquier otra fuente.

## 3. Transformar según tipo

Todo lo que se crea vive en `cerebro/`. Plantillas base en `kernel/esquema/plantillas/`; tipos propios en `plugins/plantillas/` (catálogo vigente: `cerebro/ESQUEMA.md`).

**Transcripción de reunión (`.vtt` o texto)** → nota `Reunion` (plantilla `reunion.md`) en `01-reuniones/` del proyecto, nombre `YYYY-MM-DD-tema.md`, con Citation al raw (`/raw/...`). **Regla para `.vtt`:** antes de integrar, elaborar un **resumen extenso y detallado** de la transcripción que capture: los participantes, los temas tratados, los acuerdos alcanzados, las preguntas surgidas, y todo lo relevante para una reunión de trabajo (compromisos con fecha, decisiones, riesgos mencionados, datos nuevos). Ese resumen es el cuerpo de la nota `Reunion` — la transcripción cruda no se copia al wiki, se cita. Redactar autocontenido: que se entienda sin abrir el `.vtt`.

**Documento recibido u otro insumo** → `.md` convertido en `00-insumos/` del proyecto (o en la carpeta de `cerebro/03-recursos/` correspondiente si es transversal) + entrada descriptiva en el `index.md` del alcance + dudas nuevas como Preguntas.

**Nota rápida / correo** → convertir al tipo OKF correspondiente o anexar a un documento existente. **Regla para correos:** los nombres que aparecen en las cabeceras `To`, `From` y `CC` **no se registran como Personas** por el solo hecho de estar ahí — una lista de distribución extensa no es conocimiento. Solo se crea o actualiza una ficha `Persona` si alguien es relevante en la conversación (toma un compromiso, decide algo, es la referencia de un tema, o el usuario interactúa con esa persona regularmente).

## 4. Integrar al wiki (el paso que compone)

Por cada dato extraído, actualizar las páginas afectadas:
- Pendientes → tabla "Pendientes conmigo" de cada ficha `Persona`.
- Preguntas abiertas → documentos `Pregunta` en `05-preguntas/` del proyecto. Si la fuente RESPONDE una pregunta existente, cerrarla (estado, respuesta, cita).
- Decisión relevante → proponer /x-decision (no crearlo solo).
- Conocimiento permanente (lineamiento, dato de sistema, relación de reporte) → actualizar Lineamiento / ficha Sistema / ficha Persona.

**Detección de contradicciones (obligatorio):** si algo de la fuente contradice una página existente (un lineamiento que cambió, un dato de sistema desactualizado, una decisión que ya no aplica), NO sobrescribir en silencio ni ignorar. Señalarlo al usuario: "La reunión dice X pero [página] dice Y — ¿cuál vale?". Al resolver, la página se actualiza dejando nota de supersesión: `> Hasta YYYY-MM-DD se creía X (fuente); superado por Y (fuente).`

## 5. Mantener el sistema

- Completar la columna "Páginas generadas" de las filas nuevas de `raw/manifiesto.md`.
- Regenerar `cerebro/PREGUNTAS-ABIERTAS.md` (bloqueantes primero, luego antigüedad; enlace + responsable + días abierta).
- Regenerar `cerebro/02-areas/personas/ORGANIGRAMA.md` si cambió alguna ficha Persona.
- Actualizar los `index.md` tocados. Loguear en el `log.md` de cada proyecto tocado y en `cerebro/log.md` global.
- El inbox queda vacío: todo procesado tiene su original en `raw/` y su línea en el manifiesto.

## 6. Reportar

Resumen final: N fuentes procesadas, páginas creadas/actualizadas, preguntas nuevas/cerradas, contradicciones encontradas y su resolución, y lo que requiere decisión del usuario.
