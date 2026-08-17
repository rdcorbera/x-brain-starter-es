# Skill: Curar (`/x-curar`)

El Bibliotecario, modo lint: salud estructural Y de contenido del wiki — índices, enlaces, contradicciones, huérfanos, obsolescencia. Mantenimiento a demanda (recomendado: mensual). Correr las verificaciones y presentar un informe con propuestas — **no aplicar cambios masivos sin confirmación**.

## Lint estructural

1. **Conformidad OKF** — todo `.md` de conocimiento en `cerebro/` (excepto index/log/README) tiene frontmatter parseable con `type` del catálogo de `cerebro/ESQUEMA.md`.
2. **Índices** — cada directorio con contenido tiene `index.md` actualizado (cada concepto con su `description`).
3. **Enlaces** — inventariar rotos. Distinguir: (a) conocimiento aún no escrito (válido en OKF — dejar, pero listar) vs (b) rutas mal escritas o archivos movidos (corregir).
4. **Raw y manifiesto** — todo archivo de `raw/` tiene su fila en `raw/manifiesto.md` y viceversa; todo documento `Insumo` cita un raw que existe. Huérfanos o filas sin archivo = reportar.
5. **Organigrama** — regenerar desde las fichas; verificar que cada hueco de `reporta-a` tenga su Pregunta.
6. **Preguntas** — regenerar `cerebro/PREGUNTAS-ABIERTAS.md`; detectar respondidas en el cuerpo pero con `estado: abierta`.
7. **Planes** — regenerar `cerebro/PENDIENTES.md` y auditar cada `PLAN.md`. Es el lint que detecta que un plan se está podriendo antes de que el usuario deje de confiar en él:
   - Tareas `hecha` sin nada en Origen (no se puede saber de dónde salieron ni quién las cerró).
   - Tareas `bloqueada` sin `Pregunta` ni decisión enlazada: nadie las puede perseguir.
   - Tareas sin responsable o sin límite que llevan semanas quietas: no se van a mover solas.
   - Tareas que no rastrean a la definición de "entregado" del `CONTEXT.md` — proponer descartarlas o corregir "entregado", que puede estar mal escrito.
   - Fases vacías, ids duplicados o renumerados (los ids `TNN` son estables: los citan logs y preguntas).
   - Vencimientos de hace más de 30 días sin tocar, y planes con `fuente-de-verdad: externa` cuyo `ultima-revision` tiene más de 30 días: el espejo está viejo y lo que muestre es falso.
   - Proyectos activos sin `PLAN.md`: proponer `/x-plan`, sin insistir.
8. **Catálogo de tipos** — comparar el catálogo base de `cerebro/ESQUEMA.md` contra `kernel/esquema/okf.md`: si el kernel trae tipos que el ESQUEMA no lista (pasa al actualizar a una versión que agregó tipos), proponer la actualización de esa tabla. Es la vía sancionada para esta migración: `/x-actualizar-sistema` no escribe en `cerebro/`. Verificar también que `cerebro/index.md` liste todos los archivos raíz del bundle.
9. **Inbox** — material >2 días sin procesar.
10. **Zonas** — si hay modificaciones locales bajo `kernel/` o en los stubs `x-*` del kernel (visible con `git status` / `git diff upstream/main -- kernel/` si hay upstream), avisar: romperán la próxima actualización. Proponer revertirlas y rescatar lo valioso como plugin.

## Lint de contenido (salud del conocimiento)

11. **Contradicciones entre páginas** — afirmaciones incompatibles entre fichas, lineamientos y decisiones. Listarlas con ambas fuentes; el usuario resuelve; dejar nota de supersesión en la superada.
12. **Obsolescencia** — afirmaciones con `timestamp` viejo que fuentes más recientes superaron, y lineamientos `en-revision` estancados.
13. **Páginas huérfanas** — documentos sin ningún enlace entrante (ni desde índices de contenido). Proponer: enlazarlas donde corresponda, o archivarlas si ya no aportan.
14. **Conceptos sin página** — sistemas, personas o términos mencionados repetidamente en reuniones/decisiones que no tienen su ficha propia. Proponer crearlas (mínimas, con TODOs).
15. **Conocimiento atrapado** — datos permanentes que viven solo en notas de Reunion y deben promoverse a Lineamiento/Sistema/Persona.
16. **Duplicados** — documentos que hablan de lo mismo; proponer fusión conservando Citations. Incluye el doble registro de pendientes: una tarea del plan copiada como pendiente independiente en una ficha `Persona` en vez de espejada con enlace.
17. **Huecos investigables** — sugerir 3-5 preguntas nuevas que el estado del wiki hace evidentes (dependencias sin dueño, decisiones sin registro, áreas sin lineamientos).

## Cierre

Aplicar solo lo confirmado. Loguear en `cerebro/log.md`: `**Update**: Curaduría — hallazgos y acciones aplicadas.`
