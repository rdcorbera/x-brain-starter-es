# Skill: Crear Skill (`/x-crear-skill`)

Meta-skill: crea un skill propio del usuario como plugin, sin tocar el kernel. La lógica queda en `plugins/skills/` y los stubs de invocación en `.claude/skills/` y `.github/prompts/` — mismo patrón que los skills del kernel.

## 1. Entrevistar

Una pregunta a la vez, solo lo que falte:

1. **¿Cómo se llama?** Nombre kebab-case, corto y verbal (ej. `reporte-clientes`). El nombre de invocación llevará el prefijo del sistema: `/x-reporte-clientes`. Verificar que no colisione con ningún skill existente (`ls .claude/skills/`, `plugins/skills/`).
2. **¿Qué hace y cuándo se corre?** Una frase de cada una — serán la `description` del stub y la primera línea del skill.
3. **¿Qué lee?** Qué partes del cerebro necesita como contexto (fichas, proyectos, GOALS, preguntas...).
4. **¿Qué produce y dónde lo escribe?** Documentos nuevos (¿de qué `type`? ¿hace falta un tipo nuevo → sugerir /x-crear-plantilla primero?), actualizaciones a páginas existentes, o solo salida en el chat.
5. **¿Cuáles son los pasos?** El flujo en 3-6 pasos. Si el usuario no lo tiene claro, proponerle uno a partir de lo anterior y iterar.
6. **¿Interactivo o directo?** ¿Entrevista al usuario o corre de una?

## 2. Validar contra las reglas del sistema

El skill generado DEBE respetar `kernel/AGENTS.md`:
- Solo escribe en `cerebro/` (y jamás en `kernel/`, `raw/` — salvo que su propósito sea la ingesta y siga la convención del manifiesto — ni `.github/`).
- Usa las plantillas del catálogo (`kernel/esquema/plantillas/` o `plugins/plantillas/`), nunca inventa formatos.
- No fabrica información: lo desconocido es una `Pregunta`.
- Quien escribe, loguea: termina actualizando `index.md` afectados y el `log.md` del alcance.

Si lo pedido viola alguna regla, señalarlo y proponer la variante que no la viole.

## 3. Generar

1. **La lógica** → `plugins/skills/<nombre>.md`, con la misma estructura que los módulos del kernel (`# Skill: <Nombre> (/x-<nombre>)` + secciones numeradas con los pasos).
2. **Stub Claude Code** → `.claude/skills/x-<nombre>/SKILL.md`:
   ```markdown
   ---
   name: x-<nombre>
   description: <la descripción acordada>
   ---

   Skill de usuario (plugin). Lee `kernel/AGENTS.md` (reglas del sistema) y `cerebro/PERFIL.md` (contexto del usuario) si aún no están cargados, y luego ejecuta las instrucciones de `plugins/skills/<nombre>.md`.
   ```
3. **Stub Copilot** → `.github/prompts/x-<nombre>.prompt.md`: mismo contenido con frontmatter `mode: agent` + `description`.

## 4. Confirmar y cerrar

Mostrar los tres archivos ANTES de escribir. Al confirmar: escribirlos y loguear en `cerebro/log.md`: `**Extension**: Skill propio /x-<nombre> creado.` Recordar al usuario que puede editar `plugins/skills/<nombre>.md` cuando quiera afinar el comportamiento — esa carpeta es suya y las actualizaciones del sistema no la tocan.
