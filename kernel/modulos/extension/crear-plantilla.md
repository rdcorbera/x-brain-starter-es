# Skill: Crear Plantilla (`/x-crear-plantilla`)

Meta-skill: agrega un tipo de documento propio al catálogo OKF del cerebro, con su plantilla como plugin. El catálogo base del kernel (`kernel/esquema/okf.md`) nunca se edita: el tipo nuevo se registra en `cerebro/ESQUEMA.md`, que es el catálogo vigente de este cerebro.

## 1. Entrevistar

Una pregunta a la vez, solo lo que falte:

1. **¿Cómo se llama el tipo?** Sustantivo singular con mayúscula inicial, como los del catálogo (ej. `Cliente`, `Experimento`, `Caso`). Verificar contra `cerebro/ESQUEMA.md` que no exista ya un tipo igual o muy parecido — si un tipo base o propio ya cubre el caso (ej. un `Cliente` que en realidad es una `Persona` externa), proponerlo antes de crear uno nuevo.
2. **¿Qué representa y cuándo se crea un documento de este tipo?** Una oración de cada una.
3. **¿Qué campos lleva el frontmatter?** Además de los obligatorios (`type`, `title`, `description`, `tags`, `timestamp`): campos propios con su significado y valores permitidos (ej. `estado: prospecto | activo | perdido`).
4. **¿Qué secciones lleva el cuerpo?** Los `#` del documento y qué va en cada uno.
5. **¿Dónde viven las instancias?** Carpeta en `cerebro/` (ej. `02-areas/clientes/`) y convención de nombre de archivo. Crear la carpeta con su `index.md` si no existe.

## 2. Generar

1. **La plantilla** → `plugins/plantillas/<tipo-kebab>.md`, siguiendo exactamente el estilo de las de `kernel/esquema/plantillas/`: frontmatter con placeholders `<...>` y comentarios de valores permitidos, cuerpo con las secciones acordadas.
2. **El registro en `cerebro/ESQUEMA.md`** → agregar el tipo a la sección "Tipos propios": nombre, descripción, especificación de campos (nombre, significado, valores), dónde viven las instancias, convención de nombres y ruta de la plantilla. Esta especificación debe bastar para regenerar la plantilla sin el plugin — es lo que hace al cerebro portable.
3. **Actualizar `plugins/README.md`** no hace falta; el `index.md` de la carpeta de instancias sí, si se creó.

## 3. Confirmar y cerrar

Mostrar plantilla y registro ANTES de escribir. Al confirmar: escribir y loguear en `cerebro/log.md`: `**Extension**: Tipo propio <Tipo> agregado al catálogo, plantilla en plugins/plantillas/.`
