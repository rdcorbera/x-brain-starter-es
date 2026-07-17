# Guía de uso — X-Brain

Instructivo completo para instalar, configurar y operar la base de conocimiento. Sirve para cualquier rol en cualquier organización: el sistema se adapta a tu trabajo durante el `/x-setup`.

---

## 1. Qué es este sistema

Un **wiki personal mantenido por agentes de IA**. Tú aportas las fuentes (transcripciones, documentos, lo que averiguas en el día) y haces las preguntas; los agentes hacen el trabajo pesado: clasificar, resumir, cruzar referencias, detectar contradicciones, mantener índices y organigrama.

Combina cuatro patrones:

| Patrón | Qué aporta |
|---|---|
| **PARA** | Estructura temporal: proyectos (con fecha de fin), áreas (responsabilidades continuas), recursos, archivo |
| **OKF v0.1** | Formato verificable: markdown + frontmatter tipado, `index.md`, `log.md` |
| **LLM Wiki** | Filosofía: wiki compilado que se integra con cada ingesta, fuentes crudas inmutables |
| **Skills** | Mecánica: comandos `/x-*` que ejecutan flujos de entrevista y mantenimiento |

**Qué lo hace genérico:** nada de tu rol está cableado. El `/x-setup` te entrevista y a partir de tus respuestas crea tus áreas, tu mapa de personas, tus lineamientos, tu ciclo de planificación e incluso tipos de documento propios (ej. `Cliente` para un vendedor, `Caso` para un abogado).

**Qué lo hace actualizable y portable:** las zonas de propiedad. El sistema (`kernel/` + stubs) es del starter y se actualiza desde GitHub; tu conocimiento (`cerebro/`), tus fuentes (`raw/`) y tus extensiones (`plugins/`) son tuyos y ninguna actualización los toca. Regla de oro correspondiente: **tú tampoco tocas el kernel** — si quieres cambiar el comportamiento, es un plugin (`/x-crear-skill`), no una edición.

---

## 2. Herramientas necesarias

### Obligatorias

| Herramienta | Para qué | Instalación |
|---|---|---|
| **Git** | Versionado del brain (historial, respaldo) y actualizaciones del kernel | https://git-scm.com/downloads |
| **Un agente de código** | Los agentes que operan el brain: [Claude Code](https://claude.com/claude-code), o VS Code + GitHub Copilot (Chat, modo Agent) | Según tu herramienta. **Verificar la política de uso de IA de tu organización antes de ingresar información interna** |
| **Python 3.10+** | Convertir los insumos binarios (PDF, Word, Excel, PowerPoint, draw.io) a markdown | Ver **Paso 2**. No viene garantizado en ninguna plataforma — macOS trae 3.9, que se queda corto, y Windows no trae nada |

> **Sobre Python:** sin él, los agentes no pueden leer un `.pdf` ni un `.pptx`. Y si los leyeran directamente, quemarían miles de tokens y se abriría la puerta a que inventen. La conversión la hace un script determinista que cuesta cero tokens. Si todo tu material es texto plano, puedes saltarte el Paso 2 e instalarlo el día que recibas el primer adjunto.

### Recomendadas (opcionales)

| Herramienta | Para qué |
|---|---|
| **Obsidian** | Visor del wiki: abrir `cerebro/` como bóveda — graph view, navegación por enlaces |
| **Plugin Dataview** (Obsidian) | Tablas dinámicas sobre el frontmatter (preguntas por responsable, decisiones por estado) |
| **Obsidian Web Clipper** | Capturar documentación web como markdown directo al inbox |
| **Markdown Preview Mermaid Support** (VS Code) | Previsualizar los diagramas Mermaid |

---

## 3. Instalación inicial (una sola vez)

### Paso 1 — Obtener el repositorio

```bash
git clone https://github.com/rdcorbera/x-brain-starter-es mi-brain
cd mi-brain
```

Recomendado: crear tu repositorio remoto **privado** como respaldo y apuntar `origin` ahí, dejando el starter como `upstream` (así `/x-actualizar-sistema` sabe de dónde traer versiones nuevas):

```bash
git remote rename origin upstream
git remote add origin <url-de-tu-repo-privado>
git push -u origin main
```

(Verifica primero la política de tu organización sobre dónde puede alojarse esta información.)

### Paso 2 — Instalar el conversor de insumos (Python)

Solo si vas a recibir adjuntos (PDF, Word, Excel, PowerPoint, draw.io, HTML). Hace falta **Python 3.10+** (`python3 --version`; en Windows `python --version`):

- **macOS** — el del sistema es 3.9.6 y no sirve: `brew install python@3.13`
- **Windows** — no trae: [python.org](https://www.python.org/downloads/) o `winget install Python.Python.3.13`
- **Linux** — según la distro; Debian/Ubuntu necesitan además `python3.12-venv`

Crear el entorno e instalar dependencias:

```bash
# macOS / Linux
python3 -m venv kernel/scripts/.venv
kernel/scripts/.venv/bin/pip install -r kernel/scripts/requirements.txt
```

```powershell
# Windows
python -m venv kernel\scripts\.venv
kernel\scripts\.venv\Scripts\pip install -r kernel\scripts\requirements.txt
```

Comprobar con cualquier PDF a mano:

```bash
python3 kernel/scripts/a-markdown.py <un-archivo.pdf> --stdout
```

Debe imprimir markdown. Si algo falla, el script dice qué instalar. El `.venv/` no se versiona: cada persona lo crea en su máquina. Detalles de motores y límites en `kernel/scripts/README.md`.

### Paso 3 — Activar los skills en tu herramienta

- **Claude Code**: nada que hacer — los skills de `.claude/skills/` se detectan solos. Escribir `/x-` debe listar los 15.
- **VS Code + Copilot**: activar el setting **Chat: Prompt Files** (`chat.promptFiles: true`), abrir Copilot Chat en modo **Agent** y verificar que `/x-setup` aparece al escribir `/`.

### Paso 4 — Correr el setup (aquí el sistema se vuelve TUYO)

```
/x-setup
```

La entrevista tiene 6 rondas (~30 minutos): quién eres, cómo fluye tu trabajo y tu ciclo de planificación, tu mapa de personas, tus áreas (aquí se crean carpetas y tipos propios), reglas de comunicación y confidencialidad, y objetivos del periodo. **Nada se escribe sin que lo revises y confirmes.** Todo lo generado queda en `cerebro/` (y plantillas propias en `plugins/`); el kernel no se toca.

¿Te compartieron un cerebro o vienes del sistema original? Ver la sección 7.

### Paso 5 — Crear tu primer proyecto

```
/x-nueva-iniciativa
```

Ten a mano la documentación que dispara el proyecto (brief, requerimientos, propuesta): suéltala en `inbox/` cuando el skill la pida. Además de la estructura, genera un análisis inicial con las dudas clasificadas por responsable — tu primera lista de preguntas.

---

## 4. Operación diaria

### El ritual de la mañana (~5-10 min)

```
1. Soltar en inbox/ todo lo pendiente de ayer
   (transcripciones, documentos recibidos, notas sueltas)
2. /x-procesar-inbox      ← clasifica, archiva en raw/, integra, detecta contradicciones
3. /x-briefing-diario     ← repasa preguntas abiertas, registra lo averiguado
```

No hace falta nombrar prolijo lo que sueltas en el inbox — el Bibliotecario clasifica y archiva cada original en `raw/` como `YYYY-MM-DD-descripcion-tiny_uuid.ext`, registrado en `raw/manifiesto.md`. Solo evita nombres como `notas3.txt`.

#### Qué formatos acepta el inbox

Texto plano, y estos adjuntos, que se convierten solos a markdown (requiere el Paso 2):

| Formato | Qué hay que saber |
|---|---|
| `.pdf` | Si está escaneado (sin capa de texto), avisa en vez de devolver vacío |
| `.docx` `.pptx` | En PowerPoint entran también **las notas del orador** |
| `.xlsx` | Se muestrean las primeras 50 filas por hoja (una hoja de 1.500 filas son ~18.800 tokens de ruido; muestreada, ~830). El original completo queda en `raw/` |
| `.drawio` | Se convierte a un diagrama Mermaid legible |
| `.html` `.yaml` | Se limpia la plantilla web (`nav`, `footer`) antes de convertir |
| `.doc` `.ppt` `.xls` | **No se pueden leer** (binarios de antes de 2007). Abrirlos en Office y «Guardar como» al formato moderno |

**Los «Avisos de conversión» importan.** Cuando la conversión pierde algo, el markdown lo dice arriba de todo. No los ignores ni los borres — son la diferencia entre saber que falta un dato y creer que no existe.

### Alrededor de cada reunión

```
ANTES:    /x-preparar-reunion     ← agenda: preguntas a hacer, pendientes a cobrar
DESPUÉS:  soltar transcripción o notas en inbox/ → /x-procesar-inbox
```

### Al trabajar

```
/x-decision   ← registrar o deliberar una decisión (valida contra decisiones previas y lineamientos)
/x-diagrama   ← flujos, procesos, secuencias, organización
/x-consultar  ← preguntar cualquier cosa a la base ("¿qué decidimos sobre X y por qué?")
```

Usar el modelo más capaz disponible (Opus) para `/x-decision` y `/x-diagrama`.

### Commit diario

```bash
git add . && git commit -m "brain: $(date +%F)" && git push
```

Puedes pedirle al agente que lo haga al final de cada `/x-procesar-inbox`.

---

## 5. Rituales periódicos

| Frecuencia | Comando | Qué hace |
|---|---|---|
| **Semanal** (ej. viernes) | `/x-actualizacion-semanal` | Pulso, objetivos (3 bloques), estado por proyecto, pendientes vencidos |
| **Mensual** | `/x-curar` | Lint estructural (índices, enlaces, OKF, manifiesto) y de contenido (contradicciones, huérfanos, obsolescencia) |
| **Por periodo** (según tu ciclo) | `/x-cierre-periodo` | Archiva proyectos extrayendo el conocimiento reutilizable, retro de objetivos, prepara GOALS.md |
| **Cuando haya versión nueva** | `/x-actualizar-sistema` | Trae el kernel más reciente desde GitHub (merge limpio: tu contenido no se toca) |

---

## 6. Referencia rápida de comandos

| Comando | Cuándo usarlo | Modelo |
|---|---|---|
| `/x-setup` | Una sola vez, al inicio (o para rehacer el contexto / adoptar un cerebro) | Sonnet |
| `/x-nueva-iniciativa` | Nace un proyecto u objetivo con entidad propia | Sonnet |
| `/x-procesar-inbox` | Diario, o cada vez que haya material en `inbox/` | Haiku/Sonnet |
| `/x-briefing-diario` | Al iniciar el día | Sonnet |
| `/x-preparar-reunion` | Antes de reunirte con alguien | Sonnet |
| `/x-consultar` | Cualquier pregunta contra la base | Sonnet (Opus si es complejo) |
| `/x-decision` | Al tomar o deliberar una decisión importante | **Opus** |
| `/x-diagrama` | Al crear o actualizar diagramas | **Opus** |
| `/x-actualizacion-semanal` | Una vez por semana | Sonnet |
| `/x-curar` | Mensual o cuando algo se sienta desordenado | Sonnet |
| `/x-cierre-periodo` | Al cerrar tu ciclo de planificación | Sonnet |
| `/x-actualizar-sistema` | Para traer la última versión del kernel | Sonnet |
| `/x-reconstruir` | Para recrear el cerebro desde `raw/` en un starter limpio | Sonnet |
| `/x-crear-skill` | Para agregar un skill propio (plugin) | Sonnet |
| `/x-crear-plantilla` | Para agregar un tipo de documento propio | Sonnet |

---

## 7. Portar, compartir y reconstruir

Las zonas hacen que el conocimiento viaje separado del sistema. Tres escenarios:

**Compartir tu cerebro (o moverlo a otro sistema).** Copia la carpeta `cerebro/` completa. Es un bundle OKF autodescriptivo: su `ESQUEMA.md` explica tipos, estructura y convenciones. Quien lo recibe la coloca en un starter limpio (reemplazando su `cerebro/`) y corre `/x-setup`: el sistema detecta el cerebro heredado, lo adopta sin tocarlo y solo re-entrevista la identidad del nuevo dueño. Si usas tipos propios, comparte también `plugins/plantillas/` (o basta el ESQUEMA, que permite regenerarlas). Compartir `raw/` es opcional: sin él, los punteros `/raw/...` quedan rotos pero el conocimiento integrado está completo.

**Reconstruir desde las fuentes.** Copia `raw/` (con su `manifiesto.md`) a un starter limpio y corre `/x-reconstruir`: reprocesa todo en orden cronológico y recrea el cerebro. Nota: recrea lo derivable de las fuentes; la curaduría manual posterior no está en `raw/` y no se recupera — para portar un cerebro curado, usa el escenario anterior.

**Actualizar el sistema.** `/x-actualizar-sistema` trae la última versión del kernel desde GitHub. Como el upstream solo toca `kernel/`, los stubs y los archivos raíz — y tú nunca los editas — el merge es limpio. Si alguna versión requiere pasos manuales, su entrada en `kernel/CHANGELOG.md` los trae bajo **Migración**.

**¿Vienes del sistema original (second-brain-starter-es)?** La migración automática aún no existe. Camino manual: copiar tus carpetas `01-proyectos/` a `04-archivo/` dentro de `cerebro/`, mover los `raw/` dispersos (los `00-insumos/raw/` de cada proyecto y `03-recursos/raw/`) a la carpeta `raw/` global, pasar la personalización de `.github/copilot-instructions.md` a `cerebro/PERFIL.md`, y correr `/x-curar` para que revise enlaces y manifiesto.

---

## 8. Reglas de oro del operador

1. **Todo pasa por el inbox.** Si no está en el brain, no existe. La disciplina de soltar todo en `inbox/` es lo único que el sistema no puede hacer por ti.
2. **Nada se queda en el inbox más de un día.** El valor está en el conocimiento integrado, no en el material crudo acumulado.
3. **Los originales no se tocan.** `raw/` es inmutable y completo; el wiki lo cita. Es tu seguro para reconstruir.
4. **Lo que no sabes es una Pregunta, no un supuesto.** Nunca dejes que un agente (ni tú) rellene un hueco con una suposición sin registrarla.
5. **El kernel no se edita.** Si un skill hace algo que no te sirve, créate uno propio con `/x-crear-skill` — editar `kernel/` rompe la actualización limpia.
6. **Confidencialidad.** Nunca ingresar credenciales, secretos ni datos personales de terceros. Registra las restricciones de tu organización en el `/x-setup` para que los agentes las respeten.
7. **Revisa antes de confirmar.** Los skills muestran los cambios antes de escribir — ese punto de control existe para usarse, especialmente las primeras semanas.

---

## 9. Solución de problemas

**Los comandos `/x-*` no aparecen.**
Claude Code: verificar que abriste la carpeta raíz del brain (no una subcarpeta). Copilot: (a) `chat.promptFiles: true`; (b) workspace = carpeta del brain; (c) versión reciente de VS Code y Copilot Chat.

**El agente no respeta las convenciones (frontmatter, tipos, logs).**
Verificar que `kernel/AGENTS.md` y `cerebro/PERFIL.md` existen y se cargan (en Claude Code los importa `CLAUDE.md`; en Copilot los referencia `.github/copilot-instructions.md` con `github.copilot.chat.codeGeneration.useInstructionFiles` activo).

**«a-markdown.py necesita Python 3.10+ y este es 3.9.x».**
El Python del sistema en macOS es 3.9.6. `brew install python@3.13`, borrar `kernel/scripts/.venv` y rehacer el Paso 2 con el intérprete nuevo.

**«Falta markitdown» aunque lo instalaste.**
El venv no está donde el script lo busca (`kernel/scripts/.venv`) o se creó con un Python viejo. Borrarlo y rehacer el Paso 2. Comprobar: `kernel/scripts/.venv/bin/python --version` (Windows: `...\.venv\Scripts\python --version`).

**Un `.pdf` se convirtió casi vacío.**
Está escaneado: es imagen, no texto. El markdown lo avisa. Pedir el original digital o pasarle OCR antes. **No dejes que el agente "deduzca" el contenido.**

**Un `.xlsx` salió con columnas vacías.**
Fórmulas sin valor calculado en caché (libros generados por otro sistema y nunca abiertos en Excel). Abrir el libro en Excel/LibreOffice y guardarlo.

**Necesito más de 50 filas de una hoja.**
`python3 kernel/scripts/a-markdown.py <archivo.xlsx> --filas 200 --stdout`. El original íntegro siempre está en `raw/`.

**`/x-actualizar-sistema` reporta conflictos.**
Alguien editó archivos del kernel localmente. Conservar la versión del upstream para `kernel/` y stubs; si la edición local era valiosa, rescatarla como plugin o proponerla al starter en GitHub.

**Los diagramas Mermaid no se ven.**
VS Code: instalar `Markdown Preview Mermaid Support` y abrir con `Ctrl+Shift+V`. Obsidian los renderiza nativo.

**El brain creció y las consultas se sienten lentas o incompletas.**
El patrón índice-primero funciona hasta cientos de páginas. Más allá, instalar un buscador local de markdown como [qmd](https://github.com/tobi/qmd) (CLI + MCP server) y crear con `/x-crear-skill` una variante de consulta que lo use.
