# Changelog del kernel

Historial de versiones del sistema. `/x-actualizar-sistema` muestra las entradas nuevas al actualizar; si una versión requiere pasos de migración, se listan en su sección **Migración**.

## 1.0.0 — 2026-07-16

Primera versión de X-Brain, evolución de [second-brain-starter-es](https://github.com/rdcorbera/second-brain-starter-es). Misma filosofía (LLM Wiki + PARA + OKF v0.1), nueva arquitectura:

- **Zonas de propiedad**: `kernel/` (el sistema, actualizable desde GitHub sin conflictos), `cerebro/` (el conocimiento, portable), `raw/` (fuentes crudas únicas e inmutables + manifiesto), `plugins/` (extensiones del usuario), `inbox/` (entrada transitoria).
- **La personalización ya no toca el kernel**: `/x-setup` escribe `cerebro/PERFIL.md` y `cerebro/ESQUEMA.md` en vez de editar las instrucciones del sistema.
- **Skills con prefijo `x-`** y patrón stub: la lógica vive una sola vez en `kernel/modulos/` (onboarding, ingesta, consulta, registro, mantenimiento, extension); `.claude/skills/` y `.github/prompts/` solo la invocan.
- **Skills nuevos**: `/x-actualizar-sistema` (actualización del kernel), `/x-reconstruir` (reconstruir el cerebro desde `raw/`), `/x-crear-skill` y `/x-crear-plantilla` (extensión vía plugins).
- **Raw único**: los originales procesados se archivan en `/raw/` como `YYYY-MM-DD-descripcion-tiny_uuid.ext`, registrados en `manifiesto.md` — ya no se dispersan por proyecto.
