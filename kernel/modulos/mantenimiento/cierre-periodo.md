# Skill: Cierre de Periodo (`/x-cierre-periodo`)

Cierra el periodo de planificación: archiva proyectos terminados extrayendo el conocimiento reutilizable, y hace el retro de objetivos. El "periodo" es el ciclo definido en `cerebro/PERFIL.md` (trimestre, mes, ciclo — lo que /x-setup haya configurado).

## 1. Inventario

Listar proyectos de `cerebro/01-proyectos/` y preguntar por cada uno: ¿entregado, continúa el próximo periodo, o se cancela?

## 2. Extraer antes de archivar (el paso crítico)

Por cada proyecto que se archiva (entregado o cancelado), ANTES de moverlo:
- **Decisiones** — verificar que cada decisión relevante esté referenciada desde las fichas de Sistema afectadas (el archivo no debe esconder decisiones vivas).
- **Conocimiento permanente** — recorrer reuniones y preguntas respondidas buscando lineamientos, datos de sistemas o procesos que merezcan vivir en `cerebro/02-areas/` o `cerebro/03-recursos/`. Proponer promociones.
- **Lecciones** — preguntar: ¿qué funcionó y qué no en este proyecto? Crear `retro.md` (type: Playbook) dentro del proyecto.
- **Preguntas abiertas** — las que siguen importando se mueven a otro proyecto o a transversales; el resto se cierra con nota.

## 3. Archivar

Mover cada proyecto cerrado a `cerebro/04-archivo/<periodo>/`. Los enlaces de otros documentos hacia el proyecto quedan apuntando a la ruta vieja: corregir los de páginas vivas (fichas de Sistema, lineamientos). Los originales de `raw/` NO se mueven: son globales e inmutables. Actualizar: `index.md` de proyectos y archivo, "Estado actual" de `cerebro/PERFIL.md`, `cerebro/PREGUNTAS-ABIERTAS.md`, logs.

## 4. Retro de objetivos

Recorrer los 3 bloques de `cerebro/GOALS.md`: qué se logró, qué no y por qué (breve, sin juicio). Guardar el retro en `cerebro/04-archivo/<periodo>/retro-periodo.md` y dejar `GOALS.md` listo para los objetivos nuevos (mini-entrevista tipo Ronda 6 del /x-setup).

## 5. Log

Entrada en `cerebro/log.md`: proyectos archivados, promociones hechas, objetivos cumplidos.
