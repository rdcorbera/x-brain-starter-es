# Esquema de datos de este cerebro

> Este archivo hace al cerebro **autodescriptivo y portable**: cualquier sistema (u otra persona) que reciba la carpeta `cerebro/` puede entender cómo funciona su base de conocimiento leyendo esto. Lo inicializa `/x-setup` y lo extiende `/x-crear-plantilla`. No documenta nada del kernel que no haga falta para leer los datos.

## Metadatos

| Campo | Valor |
|---|---|
| Formato | OKF v0.1 (markdown + frontmatter tipado) |
| Kernel con el que se creó | x-brain 1.0.0 |
| Dueño | <!-- TODO: /x-setup --> |
| Fecha de setup | <!-- TODO: /x-setup --> |
| Idioma del contenido | español |
| Formato de periodo | <!-- TODO: /x-setup — ej. trimestral (2026-Q3) --> |

## Convenciones de lectura

1. **Bundle**: esta carpeta (`cerebro/`) es la raíz del bundle. Los enlaces que empiezan con `/` (ej. `/02-areas/personas/ana-garcia.md`) se resuelven desde aquí.
2. **Puntero externo `/raw/...`**: apunta a la carpeta de fuentes crudas del sistema que hospeda este cerebro (fuera del bundle). Si recibiste este cerebro sin sus fuentes, esos enlaces estarán rotos: es esperado, el conocimiento integrado está completo igual.
3. Todo `.md` de conocimiento (excepto `index.md` y `log.md`) lleva frontmatter YAML con `type` de los catálogos de abajo. Cada directorio tiene un `index.md` (índice descriptivo) y cada alcance su `log.md` (historia de cambios, más reciente primero).
4. Las fuentes de cada afirmación están al final de cada documento bajo `# Citations`.

## Estructura de carpetas

| Carpeta | Semántica |
|---|---|
| `01-proyectos/` | Trabajo con fecha de fin: una carpeta por proyecto (`<periodo>-nombre/` con CONTEXT.md, insumos, reuniones, decisiones, preguntas...) |
| `02-areas/` | Responsabilidades continuas. Incluye `personas/` (fichas + ORGANIGRAMA.md) |
| `03-recursos/` | Referencia: `sistemas-y-herramientas/`, `glosario/`, y lo que el rol necesite |
| `04-archivo/` | Proyectos cerrados, por periodo, con sus retros |

Archivos raíz: `PERFIL.md` (contexto del dueño), `GOALS.md` (objetivos del periodo), `PREGUNTAS-ABIERTAS.md` (índice global de dudas, autogenerado), `index.md`, `log.md`.

## Catálogo de tipos — base

Los 11 tipos del kernel (especificación completa y plantillas: `kernel/esquema/okf.md` y `kernel/esquema/plantillas/` del sistema que hospeda):

| Tipo | Qué es |
|---|---|
| `Iniciativa` | El CONTEXT.md de cada proyecto u objetivo con entidad propia |
| `Insumo` | Documento recibido convertido a markdown, con puntero a su original en `/raw/` |
| `Reunion` | Nota procesada de una reunión |
| `Decision` | Registro de una decisión: contexto, alternativas y consecuencias |
| `Pregunta` | Duda abierta con estado y responsable |
| `Persona` | Ficha de una persona de la organización |
| `Sistema` | Ficha de un sistema, herramienta, producto o proceso |
| `Lineamiento` | Estándar, política o regla de trabajo vigente |
| `Diagrama` | Diagrama en Mermaid/PlantUML con su contexto |
| `Playbook` | Proceso reutilizable, o un análisis/síntesis archivado |
| `Glosario` | Término, sigla o jerga interna |

## Catálogo de tipos — propios

> Los agrega `/x-crear-plantilla`. Cada entrada debe especificar los campos con el detalle suficiente para regenerar su plantilla sin el plugin (`plugins/plantillas/`).

_Ninguno todavía._
