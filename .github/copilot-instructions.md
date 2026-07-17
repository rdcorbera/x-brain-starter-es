# X-Brain — instrucciones para agentes (arranque Copilot)

Este archivo es solo el punto de entrada. Antes de actuar en este repositorio, **leer en este orden**:

1. `kernel/AGENTS.md` — las reglas del sistema: zonas de propiedad, principios LLM Wiki, convenciones OKF, estructura y skills.
2. `cerebro/PERFIL.md` — quién es el usuario, su rol, reglas de comunicación y confidencialidad, y estado actual.
3. `cerebro/ESQUEMA.md` — el esquema de datos de este cerebro (catálogo de tipos vigente).

Los skills se invocan con el prefijo `x-` y viven como stubs en `.github/prompts/` (requieren `chat.promptFiles: true`); cada stub carga su lógica desde `kernel/modulos/` o `plugins/skills/`.

Este archivo es parte del kernel: no se edita localmente ni lo modifica ningún skill. La personalización vive en `cerebro/PERFIL.md`.
