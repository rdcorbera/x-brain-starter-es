# Skill: Reconstruir (`/x-reconstruir`)

Reconstruye el cerebro completo reprocesando las fuentes crudas de `raw/` en orden cronológico, guiado por `raw/manifiesto.md`. Caso de uso típico: alguien copia su carpeta `raw/` (+ manifiesto) a un starter limpio y recrea todo el conocimiento con un comando.

**Qué reconstruye y qué no:** recrea todo lo derivable de las fuentes (reuniones, insumos, preguntas, fichas, integraciones). Lo que se escribió a mano después de la ingesta original (ediciones manuales, respuestas registradas en el chat, curaduría) no está en `raw/` y no puede recrearse — avisarlo al inicio. Para portar un cerebro *curado* tal cual está, la vía correcta es copiar la carpeta `cerebro/` (ver kernel/GUIA-DE-USO.md).

## 0. Precondiciones

1. `raw/` debe tener archivos. Si está vacía, no hay nada que hacer.
2. Si `cerebro/` ya tiene contenido real (proyectos, fichas), **detenerse y preguntar**: ¿integrar sobre lo existente (reprocesar solo lo que falta) o se trata de un cerebro nuevo? Nunca sobrescribir contenido existente sin confirmación explícita.
3. Si el usuario aún no corrió `/x-setup`, sugerir correrlo primero (el perfil orienta la clasificación); se puede reconstruir sin él, dejando TODOs.

## 1. Ordenar

Leer `raw/manifiesto.md` y ordenar las fuentes cronológicamente (el orden importa: las contradicciones y supersesiones deben resolverse igual que la primera vez). Para archivos sin fila en el manifiesto, usar el prefijo de fecha del nombre; si el destino no se conoce, clasificar por contenido y **preguntar** en los ambiguos — nunca adivinar el proyecto.

## 2. Reprocesar (por lotes, siguiendo a /x-procesar-inbox)

Por cada fuente, en orden:

1. **No moverla ni renombrarla** — ya está en su lugar definitivo.
2. Si es binaria, convertirla: `python3 kernel/scripts/a-markdown.py raw/<archivo> --out <destino en cerebro/> --origen /raw/<archivo>` y leer el `.md` resultante.
3. Si el destino es un proyecto que aún no existe, crearlo mínimo (CONTEXT.md con TODOs, `index.md`, `log.md`, subcarpetas estándar) — sin entrevista; se completa después con `/x-nueva-iniciativa` o a mano.
4. Aplicar los pasos 3 y 4 de `kernel/modulos/ingesta/procesar-inbox.md` (transformar según tipo + integrar al wiki, con detección de contradicciones).
5. Registrar en el manifiesto las páginas generadas (o crear la fila si no existía).

Procesar por lotes (ej. por proyecto o por mes) mostrando avance; en cerebros grandes, ofrecer pausar entre lotes.

## 3. Cerrar

- Regenerar `cerebro/PREGUNTAS-ABIERTAS.md`, `cerebro/02-areas/personas/ORGANIGRAMA.md` y todos los `index.md` tocados.
- Loguear en `cerebro/log.md`: `**Rebuild**: Cerebro reconstruido desde raw/ — N fuentes, N proyectos, N páginas.`
- Reportar: fuentes procesadas, proyectos creados, páginas generadas, ambigüedades resueltas por el usuario, y lo que quedó con TODOs.
