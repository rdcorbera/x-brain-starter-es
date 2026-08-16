# X-Brain

Base de conocimiento personal de trabajo, mantenida por agentes de IA — para **cualquier rol, en cualquier organización**. Evolución de [second-brain-starter-es](https://github.com/rdcorbera/second-brain-starter-es): misma filosofía (LLM Wiki + método PARA + Open Knowledge Format), nueva arquitectura.

Tú aportas las fuentes (reuniones, documentos, lo que averiguas en el día) y haces las preguntas; los agentes clasifican, resumen, cruzan referencias, detectan contradicciones y mantienen todo al día. El sistema se **personaliza a tu rol** al correr `/x-setup`.

> **¿Eres una IA a la que le compartieron esta URL para instalar el sistema?** Sigue [`INSTALL.md`](INSTALL.md) — está escrito para ti, no para la persona que te la compartió.

## Qué cambia respecto al sistema original

El repo está dividido en **zonas con dueño único**, y de ahí salen las tres propiedades nuevas:

```
├── kernel/    ← EL SISTEMA: skills, esquema, plantillas, scripts. Solo lectura.
├── cerebro/   ← EL CONOCIMIENTO: tu wiki completo. Portable por sí solo.
├── raw/       ← LAS FUENTES: todos los originales, inmutables, en un solo lugar.
├── inbox/     ← LA ENTRADA: suelta aquí todo lo crudo; se vacía al procesar.
└── plugins/   ← TUS EXTENSIONES: skills y plantillas propias.
```

1. **Actualizable sin conflictos.** Nada de tu uso diario toca el kernel (ni siquiera `/x-setup`, que antes editaba las instrucciones del sistema — ahora escribe tu perfil en `cerebro/PERFIL.md`). Actualizar es correr `/x-actualizar-sistema`: un merge limpio desde GitHub.
2. **Reprocesable con un comando.** Cada original procesado se archiva en `raw/` como `YYYY-MM-DD-descripcion-tiny_uuid.ext`, registrado en `raw/manifiesto.md`. Copia `raw/` a un starter limpio y `/x-reconstruir` recrea todo el conocimiento.
3. **Cerebro portable.** `cerebro/` es un bundle OKF autodescriptivo: su `ESQUEMA.md` documenta tipos (incluidos los tuyos), estructura y convenciones. Puedes moverlo a otro sistema o compartirlo — quien lo reciba corre `/x-setup` y el sistema lo adopta.
4. **Extensible sin tocar nada.** `/x-crear-skill` y `/x-crear-plantilla` generan tus skills y tipos de documento propios como plugins, con las mismas garantías que los de fábrica.

## Puesta en marcha

1. Clonar este repositorio (o usarlo como template) y abrirlo con [Claude Code](https://claude.com/claude-code) o VS Code + GitHub Copilot (modo Agent, con `chat.promptFiles: true`).
2. Correr `/x-setup`. La entrevista (6 rondas, ~30 min) personaliza el sistema a tu rol: contexto, áreas, mapa de personas, tipos propios y GOALS.
3. Ritual diario: soltar todo en `inbox/` → `/x-procesar-inbox` → `/x-briefing-diario`.
4. Ritual semanal: `/x-actualizacion-semanal`.

La guía completa está en `kernel/GUIA-DE-USO.md`; las reglas del sistema, en `kernel/AGENTS.md`.

## Recomendado: Obsidian como visor

Abre la carpeta `cerebro/` como bóveda de Obsidian, en paralelo: los agentes escriben, tú navegas. El **graph view** muestra la forma del conocimiento y el plugin **Dataview** genera tablas dinámicas sobre el frontmatter OKF (preguntas por responsable, decisiones por estado, etc.).

## Escala futura

El patrón índice-primero funciona bien hasta cientos de páginas. Si el cerebro crece más allá, considera un buscador local sobre markdown (ej. [qmd](https://github.com/tobi/qmd), con CLI y MCP server) para que los agentes busquen en vez de navegar índices.
