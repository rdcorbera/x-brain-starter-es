# X-Brain — instrucciones para Claude Code

Las reglas del sistema viven en el kernel y el contexto del usuario en su cerebro. Ambos se cargan automáticamente en cada sesión:

@kernel/AGENTS.md

@cerebro/PERFIL.md

## Notas para Claude Code

- Los skills se invocan con el prefijo `x-` (`/x-setup`, `/x-procesar-inbox`, `/x-consultar`, ...). Los de `.claude/skills/` son stubs: la lógica real está en `kernel/modulos/` (skills del kernel) o `plugins/skills/` (skills del usuario). **Editar la lógica de un skill del kernel es editar el kernel: no se hace** — los ajustes propios van como plugins (`/x-crear-skill`).
- Este archivo es parte del kernel: no editarlo localmente. La personalización vive en `cerebro/PERFIL.md`.
