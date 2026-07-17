# Skill: Nueva Iniciativa (`/x-nueva-iniciativa`)

Crea un proyecto en `cerebro/01-proyectos/` a partir de un proyecto asignado, objetivo personal o de equipo. Ingiere la documentación inicial.

## Entrevista (una pregunta a la vez, máximo 7)

1. **¿Cómo se llama y de qué origen es?** (proyecto-asignado | objetivo-personal | objetivo-equipo). Carpeta: `cerebro/01-proyectos/<periodo>-nombre-kebab/` (el formato de periodo está definido en `cerebro/PERFIL.md`).
2. **¿Qué es?** Un párrafo: qué se construye/logra, para quién.
3. **¿Qué significa "entregado"?** La definición de éxito — será la directiva del proyecto: si una sesión deriva sin avanzar hacia esto, los agentes lo señalan.
4. **¿Cómo fluye el trabajo en este proyecto de inicio a fin?** Con la respuesta, definir las subcarpetas numeradas (insumos → proceso → salida). **Si no lo sabe aún**, usar el default: `00-insumos/`, `01-reuniones/`, `02-decisiones/`, `03-diagramas/`, `04-entregables/`, `05-preguntas/` — y decirle que puede reestructurarse después. `00-insumos/`, `01-reuniones/`, `02-decisiones/` y `05-preguntas/` existen SIEMPRE (otros skills dependen de ellas). Los originales crudos NO viven en el proyecto: van a `/raw/` global.
5. **¿Qué sistemas, herramientas o productos de la organización toca?** Por cada uno sin ficha en `cerebro/03-recursos/sistemas-y-herramientas/`, crear una ficha mínima con TODOs.
6. **¿Quiénes están involucrados?** Enlazar fichas de Personas existentes; crear fichas mínimas para nuevas.
7. **¿Ya tienes documentación inicial?** (brief, requerimientos, propuesta, contrato — lo que sea que dispara el proyecto). Si sí, pedir que la suelte en `inbox/` o indique la ruta.

Si no sabe algo: usar defaults y dejar `<!-- TODO -->`. No presionar.

## Construcción

1. Crear la estructura: `CONTEXT.md` (plantilla `contexto-iniciativa.md`), `index.md`, `log.md`, y las subcarpetas definidas.
2. **Si hay documentación inicial**, archivar los originales en `raw/` según la convención de `/x-procesar-inbox` (nombre `YYYY-MM-DD-descripcion-tiny_uuid.ext` + fila en `raw/manifiesto.md`; binarios convertidos con `kernel/scripts/a-markdown.py` hacia `00-insumos/`) y generar un primer análisis (`00-insumos/analisis-inicial.md`, type: Playbook):
   - Resumen de la documentación en palabras propias.
   - Inventario de requerimientos/entregables detectados.
   - **Lista de dudas clasificadas por persona o área responsable** de resolverlas. Cada duda se crea como documento `Pregunta` en `05-preguntas/` con su responsable.
3. Actualizar: `cerebro/GOALS.md` (enlazar el proyecto en su bloque), `index.md` de `cerebro/01-proyectos/`, sección "Estado actual" de `cerebro/PERFIL.md`, `cerebro/PREGUNTAS-ABIERTAS.md` si se crearon preguntas.
4. Loguear en `cerebro/log.md` global y en el `log.md` del proyecto.

## Confirmar

Mostrar la estructura creada, el resumen del CONTEXT.md, las preguntas generadas y los TODOs pendientes.
