# Open Knowledge Format (OKF v0.1) — especificación y catálogo base

Esta es la especificación del formato que usa el cerebro y el catálogo de tipos que trae el kernel de fábrica. Es parte del kernel: **no se edita**. Los tipos propios del usuario se registran en `/cerebro/ESQUEMA.md` (vía `/x-crear-plantilla`), nunca aquí.

## El bundle

Un bundle OKF es una carpeta de markdown navegable por humanos y agentes. En este sistema, el bundle es **`/cerebro/`**.

1. **Frontmatter tipado.** Todo archivo `.md` de conocimiento (excepto `index.md` y `log.md`) lleva frontmatter YAML con `type` obligatorio. Campos recomendados: `title`, `description` (una sola oración), `tags`, `timestamp` (ISO 8601).
2. **`index.md` por directorio** — lista de enlaces con la descripción de cada concepto, para divulgación progresiva. Sin frontmatter (excepto el de la raíz del bundle, que declara `okf_version: "0.1"`).
3. **`log.md` por alcance** — historia de cambios agrupada por fecha (`## YYYY-MM-DD`), más reciente primero. Existe uno global en la raíz del bundle y uno por proyecto. **Regla: quien escribe, loguea.** Todo skill que cree o modifique archivos termina agregando su entrada al log del alcance correspondiente.
4. **Enlaces bundle-relativos** — empezar con `/` (ej. `[Ana García](/02-areas/personas/ana-garcia.md)`), resueltos desde la raíz del bundle. Los enlaces rotos se toleran: representan conocimiento aún no escrito.
5. **Puntero externo `/raw/...`** — prefijo reservado que apunta fuera del bundle, a la carpeta de fuentes crudas del sistema. Si el cerebro se comparte sin sus fuentes, estos enlaces quedan rotos: es aceptable y esperado.
6. **Citations** — cuando un documento afirma algo con fuente, listar las fuentes al final bajo `# Citations`, numeradas.

## Catálogo base de tipos

Usar exactamente estos valores en `type`. Cada tipo tiene su plantilla en `kernel/esquema/plantillas/` — los skills SIEMPRE parten de la plantilla.

| Tipo | Qué es | Plantilla |
|---|---|---|
| `Iniciativa` | El CONTEXT.md de cada proyecto u objetivo con entidad propia | `contexto-iniciativa.md` |
| `Plan` | El PLAN.md de cada proyecto: las tareas que llevan hasta "entregado", agrupadas por fase, con responsable, estado y fecha límite | `plan.md` |
| `Insumo` | Documento recibido convertido a markdown, con puntero a su original en `/raw/`. Lo genera `a-markdown.py`; no se redacta a mano | `insumo.md` |
| `Reunion` | Nota procesada de una reunión | `reunion.md` |
| `Decision` | Registro de una decisión con su contexto, alternativas y consecuencias (inspirado en los ADR) | `decision.md` |
| `Pregunta` | Duda abierta con estado y responsable | `pregunta.md` |
| `Persona` | Ficha de una persona de la organización | `persona.md` |
| `Sistema` | Ficha de un sistema, herramienta, producto o proceso de la organización | `sistema.md` |
| `Lineamiento` | Estándar, política o regla de trabajo vigente | `lineamiento.md` |
| `Diagrama` | Diagrama en Mermaid/PlantUML con su contexto (flujos, procesos, organización, etc.) | `diagrama.md` |
| `Playbook` | Proceso reutilizable paso a paso, o un análisis/síntesis archivado | — (estructura libre con frontmatter) |
| `Glosario` | Término, sigla o jerga interna de la organización | `glosario.md` |

## Extensión del catálogo

El catálogo se extiende con tipos propios del rol (ej. `Cliente`, `Experimento`, `Caso`) **sin tocar este archivo**: `/x-crear-plantilla` crea la plantilla en `plugins/plantillas/` y registra el tipo —con la especificación de sus campos— en `/cerebro/ESQUEMA.md`, que es el catálogo vigente y completo de cada cerebro. Ante cualquier diferencia, `cerebro/ESQUEMA.md` manda: es lo que hace al cerebro autodescriptivo y portable.

## Convenciones de nombres

- Archivos: kebab-case, descriptivos y autocontenidos.
- Reuniones: `YYYY-MM-DD-tema-corto.md`. Decisiones: `dec-NNN-tema-corto.md` (secuencial por proyecto). Diagramas: `<clase>-<tema>-vYYYY-MM-DD.md`.
- Originales en `/raw/`: `YYYY-MM-DD-descripcion-tiny_uuid.ext` (fecha de ingesta, descripción kebab-case, sufijo único de 6-8 caracteres hex).
