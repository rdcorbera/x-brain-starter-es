# X-Brain — Instrucciones para agentes (kernel)

Este repositorio es la base de conocimiento personal de trabajo de una persona en su organización, operada por agentes de IA. Su propósito: documentar todo lo que ocurre (reuniones, decisiones, documentos, personas, aprendizajes) y recuperarlo rápido para trabajar mejor y decidir con contexto completo.

Todo agente que trabaje en este repositorio debe leer, antes de actuar:

1. **Este archivo** — las reglas y la estructura del sistema.
2. **`/cerebro/PERFIL.md`** — quién es el usuario, su rol, sus reglas de comunicación y confidencialidad, y el estado actual de su trabajo. Lo genera `/x-setup`; si tiene TODOs pendientes, sugerir correrlo.
3. **`/cerebro/ESQUEMA.md`** — el esquema de datos de este cerebro: catálogo de tipos (base + propios), semántica de carpetas y convenciones vigentes.

## Zonas de propiedad (la regla que hace todo lo demás posible)

El sistema sigue el principio open/closed: **abierto a extensión, cerrado a modificación del kernel**. Cada carpeta tiene un dueño único:

| Zona | Dueño | Regla |
|---|---|---|
| `kernel/`, `CLAUDE.md`, `README.md`, `.github/`, stubs `x-*` de `.claude/skills/` | **El starter (GitHub)** | Ningún agente ni usuario la edita localmente. Se actualiza con `/x-actualizar-sistema`. |
| `cerebro/` | **El usuario** | Aquí vive TODO el conocimiento. Es portable: se puede copiar entera a otro sistema o compartir. |
| `raw/` | **El usuario** (escribe solo `/x-procesar-inbox`) | Originales inmutables + `manifiesto.md`. Nunca se edita ni se borra nada. |
| `inbox/` | **El usuario** | Puerta de entrada transitoria. Se vacía al procesar. |
| `plugins/` | **El usuario** | Skills y plantillas propias. Las crean `/x-crear-skill` y `/x-crear-plantilla`. |

Consecuencias prácticas para los agentes:

- **Nunca escribir en `kernel/` ni en `.github/`.** Si un skill del kernel necesita cambiar, es un issue/PR al starter en GitHub, no una edición local. Las únicas excepciones: `/x-crear-skill` agrega stubs nuevos (nunca modifica los existentes) y `/x-actualizar-sistema` trae cambios del upstream vía git.
- **Todo lo personalizable vive fuera del kernel:** el contexto del usuario en `cerebro/PERFIL.md`, los tipos propios en `cerebro/ESQUEMA.md` + `plugins/plantillas/`, los skills propios en `plugins/skills/`.
- Si el usuario pide modificar un archivo del kernel, explicarle la regla y ofrecer la alternativa: un plugin, o proponer el cambio al starter.

## Principios (patrón LLM Wiki)

Este brain no es un archivo de notas: es un **wiki compilado que se integra con cada ingesta**.

1. **Integrar, no solo archivar.** Al ingerir una fuente nueva, actualizar todas las páginas afectadas (fichas, lineamientos, organigrama), no solo crear la nota. Una reunión puede tocar 10 documentos.
2. **Señalar contradicciones.** Si información nueva contradice una página existente, nunca dejar que convivan en silencio: señalarlo al usuario, y al resolverse, la versión superada queda anotada como tal (con fecha y fuente), no borrada.
3. **Fuentes crudas inmutables, en un solo lugar.** Los originales (transcripciones, documentos recibidos) se conservan siempre en `/raw/`, renombrados `YYYY-MM-DD-descripcion-tiny_uuid.ext` y registrados en `/raw/manifiesto.md`. El wiki los cita; jamás los edita ni los reemplaza. Con `raw/` + manifiesto se puede reconstruir el cerebro entero (`/x-reconstruir`).
4. **Las respuestas valiosas se archivan.** Una síntesis, comparación o análisis generado al consultar la base no muere en el chat: se ofrece archivarlo como página para que las exploraciones compongan igual que las fuentes.

## Convenciones: Open Knowledge Format (OKF)

El bundle OKF de este sistema es la carpeta **`/cerebro/`** — los enlaces bundle-relativos (`/02-areas/...`) resuelven dentro de ella. La especificación completa y el catálogo base de tipos están en `kernel/esquema/okf.md`; el catálogo vigente de ESTE cerebro (base + tipos propios) está en `/cerebro/ESQUEMA.md`. Reglas esenciales:

1. **Frontmatter tipado.** Todo `.md` de conocimiento (excepto `index.md` y `log.md`) lleva frontmatter YAML con `type` obligatorio del catálogo de `cerebro/ESQUEMA.md`.
2. **`index.md` por directorio** — lista de enlaces con la descripción de cada concepto, para divulgación progresiva.
3. **`log.md` por alcance** — historia de cambios agrupada por fecha, más reciente primero. Uno global en `cerebro/` y uno por proyecto. **Regla: quien escribe, loguea.**
4. **Enlaces bundle-relativos** — empezar con `/` (ej. `[Ana García](/02-areas/personas/ana-garcia.md)`), resueltos desde `cerebro/`. Los enlaces rotos se toleran: representan conocimiento aún no escrito.
5. **Puntero a fuentes crudas** — el prefijo `/raw/...` es un puntero reservado que apunta FUERA del bundle, a la carpeta `raw/` del sistema. Si un cerebro se comparte sin sus fuentes, esos enlaces quedan rotos y es aceptable.
6. **Citations** — cuando un documento afirma algo con fuente, listar las fuentes al final bajo `# Citations`, numeradas.

Las plantillas base están en `kernel/esquema/plantillas/`; las de tipos propios, en `plugins/plantillas/`. Usarlas siempre.

## Reglas para los agentes

- **Idioma: español** por defecto (configurable en `cerebro/PERFIL.md`). Todo el contenido se escribe en el idioma configurado.
- **Nunca fabricar.** Si falta información, se crea un documento `Pregunta` — jamás se inventa una respuesta ni se rellena con supuestos.
- **Nombres de archivo:** kebab-case, descriptivos y autocontenidos. Reuniones: `YYYY-MM-DD-tema-corto.md`. Decisiones: `dec-NNN-tema-corto.md`. Raws: `YYYY-MM-DD-descripcion-tiny_uuid.ext`.
- **Diagramas siempre como texto** (Mermaid preferido, PlantUML aceptado) dentro de markdown. Nunca solo imágenes.
- **Mostrar antes de escribir.** Ante cambios masivos o edición de documentos existentes fuera del alcance del skill en ejecución, mostrar un resumen y pedir confirmación.
- **No repetir preguntas al usuario** cuya respuesta ya está en la base — buscar primero.
- **Confidencialidad:** nunca almacenar credenciales, secretos, tokens ni datos personales de clientes o terceros. Las restricciones específicas de la organización del usuario están en `cerebro/PERFIL.md`; ante la duda, el dato sensible no entra.

## Estructura del repositorio

```
x-brain/
├── CLAUDE.md                     ← carga kernel + perfil en Claude Code (kernel)
├── README.md                     ← presentación y puesta en marcha (kernel)
├── .claude/skills/x-*/           ← stubs de invocación → kernel/modulos/ (kernel)
├── .github/
│   ├── copilot-instructions.md   ← arranque para Copilot (kernel)
│   └── prompts/x-*.prompt.md     ← stubs equivalentes (kernel)
├── kernel/                       ← EL SISTEMA (solo lectura; se actualiza de GitHub)
│   ├── AGENTS.md                 ← este archivo
│   ├── VERSION · CHANGELOG.md    ← versión del kernel y notas de cada release
│   ├── GUIA-DE-USO.md            ← instructivo completo de operación
│   ├── esquema/
│   │   ├── okf.md                ← especificación OKF + catálogo base de tipos
│   │   └── plantillas/           ← plantilla base por cada tipo
│   ├── modulos/                  ← la lógica de los skills, por módulo:
│   │   ├── onboarding/           ← setup (+ cuestionario-setup), actualizar-sistema
│   │   ├── ingesta/              ← procesar-inbox, nueva-iniciativa, reconstruir
│   │   ├── consulta/             ← consultar, briefing-diario, preparar-reunion
│   │   ├── registro/             ← decision, diagrama
│   │   ├── mantenimiento/        ← actualizacion-semanal, curar, cierre-periodo
│   │   └── extension/            ← crear-skill, crear-plantilla
│   └── scripts/                  ← a-markdown.py: insumos binarios → markdown (cero tokens)
├── plugins/                      ← EXTENSIONES DEL USUARIO
│   ├── skills/                   ← lógica de skills propios
│   └── plantillas/               ← plantillas de tipos propios
├── inbox/                        ← puerta de entrada de TODO (transitoria)
├── raw/                          ← originales inmutables + manifiesto.md
└── cerebro/                      ← EL CONOCIMIENTO (bundle OKF, portable)
    ├── PERFIL.md                 ← quién soy, rol, comunicación, estado actual (/x-setup)
    ├── ESQUEMA.md                ← esquema de datos de este cerebro
    ├── index.md · log.md         ← índice raíz y log global del bundle
    ├── GOALS.md                  ← objetivos del periodo (3 bloques)
    ├── PREGUNTAS-ABIERTAS.md     ← índice global de preguntas (autogenerado)
    ├── 01-proyectos/             ← una carpeta por proyecto u objetivo activo
    │   └── <periodo-nombre>/
    │       ├── CONTEXT.md        ← qué es, estado, personas (type: Iniciativa)
    │       ├── index.md · log.md
    │       ├── 00-insumos/       ← insumos convertidos a .md (los originales van a /raw/)
    │       ├── 01-reuniones/     ← notas procesadas (type: Reunion)
    │       ├── 02-decisiones/    ← registros de decisión (type: Decision)
    │       ├── 03-diagramas/     ← flujos, procesos, secuencias (si aplica)
    │       ├── 04-entregables/   ← el producto del proyecto
    │       └── 05-preguntas/     ← dudas abiertas del proyecto (type: Pregunta)
    ├── 02-areas/                 ← conocimiento permanente por responsabilidad
    │   └── personas/             ← fichas + ORGANIGRAMA.md (autogenerado)
    ├── 03-recursos/              ← sistemas-y-herramientas/, glosario/, y lo que el rol necesite
    └── 04-archivo/               ← proyectos cerrados, por periodo
```

## Insumos binarios

El inbox recibe `.pptx`, `.docx`, `.xlsx`, `.pdf`, `.drawio`, `.html` y `.yaml`. **Ningún agente abre un binario ni lo interpreta**: lo convierte con `kernel/scripts/a-markdown.py` y lee el `.md` resultante. La conversión es determinista y cuesta cero tokens; leer el binario los quema y abre la puerta a inventar. Si el `.md` trae una sección «Avisos de conversión», se atiende: dice qué se perdió. Detalle de motores y límites en `kernel/scripts/README.md`.

## Skills disponibles

Todos se invocan con el prefijo `x-`. La lógica de cada uno vive en `kernel/modulos/`; los stubs de `.claude/skills/` y `.github/prompts/` solo la cargan.

| Skill | Módulo | Cuándo | Modelo sugerido |
|---|---|---|---|
| `/x-setup` | onboarding | Inicialización y personalización del brain (una vez); también adopta un cerebro compartido | Sonnet |
| `/x-actualizar-sistema` | onboarding | Traer la última versión del kernel desde GitHub | Sonnet |
| `/x-nueva-iniciativa` | ingesta | Nace un proyecto u objetivo con entidad propia | Sonnet |
| `/x-procesar-inbox` | ingesta | Diario — clasificar y estructurar lo que hay en `inbox/` | Haiku/Sonnet |
| `/x-reconstruir` | ingesta | Reconstruir un cerebro completo desde `raw/` + manifiesto | Sonnet |
| `/x-consultar` | consulta | Preguntar a la base; síntesis con citas, archivable | Sonnet (Opus si es complejo) |
| `/x-briefing-diario` | consulta | Al iniciar el día — repasar preguntas abiertas | Sonnet |
| `/x-preparar-reunion` | consulta | Antes de reunirte con alguien | Sonnet |
| `/x-decision` | registro | Registrar o deliberar una decisión importante | Opus |
| `/x-diagrama` | registro | Generar/actualizar diagramas (flujos, procesos, secuencias) | Opus |
| `/x-actualizacion-semanal` | mantenimiento | Una vez por semana | Sonnet |
| `/x-curar` | mantenimiento | Mantenimiento a demanda (índices, enlaces, duplicados) | Sonnet |
| `/x-cierre-periodo` | mantenimiento | Al cerrar el trimestre/ciclo de planificación | Sonnet |
| `/x-crear-skill` | extension | Crear un skill propio en `plugins/` | Sonnet |
| `/x-crear-plantilla` | extension | Crear un tipo de documento propio con su plantilla | Sonnet |
