# Plugins — extensiones del usuario

Esta carpeta es **tuya**: el kernel nunca la toca y las actualizaciones del sistema jamás la modifican. Aquí vive todo lo que extiende el sistema más allá de lo que trae de fábrica.

```
plugins/
├── skills/       ← lógica de tus skills propios (los crea /x-crear-skill)
└── plantillas/   ← plantillas OKF de tus tipos de documento propios (las crea /x-crear-plantilla)
```

## Cómo extender el sistema

- **Un skill nuevo** (un flujo de trabajo propio, un reporte recurrente, una automatización): correr `/x-crear-skill`. Escribe la lógica en `plugins/skills/` y registra los stubs de invocación en `.claude/skills/` y `.github/prompts/` con el prefijo `x-`.
- **Un tipo de documento nuevo** (ej. `Cliente`, `Experimento`, `Caso`): correr `/x-crear-plantilla`. Crea la plantilla en `plugins/plantillas/` y registra el tipo en el catálogo de `cerebro/ESQUEMA.md`.

## Reglas

1. **No editar el kernel.** Si un skill del kernel hace algo que no te sirve, crea uno propio aquí que lo reemplace en tu flujo — no modifiques `kernel/` (perderías la actualización limpia).
2. Los skills propios llevan el mismo prefijo `x-` que los del kernel.
3. Si compartes tu cerebro con otra persona y usa tipos propios, comparte también `plugins/plantillas/` (o basta con `cerebro/ESQUEMA.md`, que documenta los campos de cada tipo y permite regenerar la plantilla).
