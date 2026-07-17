# Skill: Decision (`/x-decision`)

Registra una decisión importante con su contexto y alternativas, validando contra decisiones previas y lineamientos. Usar el modelo más capaz disponible (Opus) — aquí el razonamiento importa. Aplica a cualquier decisión con consecuencias: técnica, comercial, de proceso, de contratación, de priorización.

## 1. Capturar

Preguntar solo lo que falte: ¿qué se decidió (o qué hay que decidir)?, ¿en qué proyecto?, ¿qué opciones se consideraron?, ¿quiénes decidieron?

Dos modos:
- **Registro** — la decisión ya se tomó (típicamente en una reunión): documentarla fielmente.
- **Deliberación** — la decisión está abierta: ayudar a estructurar opciones y trade-offs ANTES de decidir. En este modo, el documento se crea con `estado: propuesta`.

## 2. Validar (el paso que agrega valor)

Antes de escribir, cruzar contra la base:
1. **Decisiones previas** — buscar en `02-decisiones/` de todos los proyectos (activos y en `cerebro/04-archivo/`) decisiones sobre el mismo tema. Si contradice una: señalarlo explícitamente y preguntar si esta decisión la reemplaza (entonces la anterior pasa a `estado: reemplazada` con enlace cruzado).
2. **Lineamientos** — revisar `cerebro/02-areas/` por estándares o políticas aplicables. Si la decisión viola uno vigente, advertirlo con el enlace; el usuario decide si procede como excepción (documentarla en Consecuencias).
3. **Fichas de Sistema** — verificar que lo asumido sobre sistemas/herramientas involucrados coincida con sus fichas. Discrepancia = Pregunta nueva.

## 3. Escribir

Plantilla `decision.md` (`kernel/esquema/plantillas/`), numeración `dec-NNN` secuencial dentro del proyecto, en `02-decisiones/`. Citations obligatorias: la reunión o fuente donde se decidió. Después:
- Actualizar fichas de Sistema afectadas (sección "Decisiones históricas").
- Actualizar `index.md` y `log.md` del proyecto + `cerebro/log.md` global.
- Si algún diagrama o documento existente queda desactualizado por esta decisión, avisar y ofrecer actualizarlo.
