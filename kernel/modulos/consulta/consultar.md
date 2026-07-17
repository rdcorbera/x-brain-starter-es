# Skill: Consultar (`/x-consultar`)

El Consultor: responder una pregunta del usuario usando SOLO el contenido del brain (más conocimiento general si él lo pide explícitamente).

## 1. Buscar (índice primero)

1. Leer `cerebro/index.md` raíz y los `index.md` relevantes para ubicar candidatos — nunca barrer todo el repositorio a ciegas.
2. Abrir solo las páginas prometedoras: CONTEXT.md, decisiones, fichas de Sistema/Persona, Lineamientos, reuniones, `cerebro/PREGUNTAS-ABIERTAS.md`, y `cerebro/04-archivo/` si la pregunta es histórica.
3. Los `log.md` sirven para preguntas del tipo "¿qué pasó en X las últimas semanas?".

## 2. Responder

- Toda afirmación con su fuente: enlace bundle-relativo al documento (y decisión/reunión específica cuando aplique).
- Si hay contradicción entre páginas, decirlo explícitamente con ambas fuentes — no elegir en silencio.
- Si la base no tiene la respuesta, decirlo sin inventar, y ofrecer crear el documento `Pregunta` con el responsable probable según el organigrama y las fichas.
- Formato según la pregunta: prosa, tabla comparativa, o diagrama Mermaid si es estructural.

## 3. Archivar (el paso que compone)

Si la respuesta implicó síntesis real (comparación entre opciones, análisis cruzando varios proyectos, una conexión no escrita en ninguna página), ofrecer:

> "¿Archivo este análisis como página para que no se pierda?"

Si acepta: crear el documento (type: `Playbook` para análisis/procesos, `Decision` si en realidad fue una decisión) en el proyecto o recurso correspondiente, con `# Citations` apuntando a las páginas usadas. Actualizar `index.md` y loguear. Respuestas triviales (un dato puntual ya escrito en una ficha) NO se archivan.
