# INSTALL.md — Instrucciones para la IA que instala X-Brain

> Este archivo no es para el humano: es un instructivo dirigido a ti, agente de IA, para cuando alguien te comparte la URL de este repositorio y te pide que se lo instales. Si eres el humano y llegaste aquí por curiosidad, la puesta en marcha pensada para ti está en el [README](README.md) y el detalle completo en `kernel/GUIA-DE-USO.md` (una vez clonado el repo).

## 0. Primero, entiende qué puedes hacer tú

Antes de dar cualquier paso, confirma qué capacidades tienes en esta conversación — no lo asumas, compruébalo:

- **¿Tienes ejecución de comandos (shell) y sistema de archivos?** (Claude Code, Cursor, un agente con herramienta de terminal, VS Code + Copilot en modo Agent con acceso a terminal). → Sigue la **Ruta A**.
- **¿Eres un chat sin ejecución de código** (por ejemplo, te compartieron esta URL en un chat sin herramientas)? → Sigue la **Ruta B**: no puedes instalar nada tú mismo; tu trabajo es guiar al humano paso a paso.

Si no estás seguro de tener acceso a shell, prueba un comando inocuo (`pwd` o `git --version`) antes de prometer que vas a clonar el repo.

## 1. Qué vas a instalar

X-Brain es una base de conocimiento personal operada por agentes de IA (el README del repo trae el pitch completo). La instalación tiene tres piezas, en orden: clonar el repositorio, dejar disponible un agente de código para operarlo día a día, y opcionalmente Python 3.10+ para convertir adjuntos del inbox. Este archivo cubre esas tres. La personalización real (quién es el usuario, sus áreas, su cerebro) es un paso aparte, `/x-setup`, que se corre después y ya está descrito en la sección 2, Paso 6.

## 2. Ruta A — tienes shell y sistema de archivos

### Paso 1 — Preguntar lo que no puedes adivinar

Antes de tocar nada, pregúntale al humano:

- ¿Dónde quiere clonar el repo? (carpeta destino, nombre de carpeta)
- ¿Va a usar este starter directamente, o prefiere crear su propio repositorio privado como respaldo? (recomendado si va a contener información de trabajo real — ver Paso 4)
- ¿Con qué herramienta lo va a operar día a día? (Claude Code / VS Code + GitHub Copilot / esta misma sesión)

### Paso 2 — Verificar prerequisitos

```bash
git --version
```

Si falta, indica instalarlo desde https://git-scm.com/downloads (o el gestor de paquetes del sistema) y espera confirmación antes de seguir.

### Paso 3 — Clonar

```bash
git clone <URL-que-te-compartió-el-usuario> <carpeta-destino>
cd <carpeta-destino>
```

Usa la URL que el usuario te dio, no la hardcodees: puede ser un fork o un mirror.

### Paso 4 — (Recomendado) Repositorio privado propio

Si el humano va a volcar información de trabajo real, sugiere — no impongas — crear un repositorio privado propio y dejar este starter como `upstream`, para que `/x-actualizar-sistema` siga trayendo versiones nuevas del kernel sin que su contenido quede expuesto en el repo público:

```bash
git remote rename origin upstream
git remote add origin <URL-de-su-repo-privado>
git push -u origin main
```

Esto requiere que el humano ya haya creado el repositorio vacío en su proveedor (GitHub, GitLab, etc.) y te pase la URL. Recuérdale verificar antes la política de su organización sobre dónde puede alojarse esta información.

### Paso 5 — Python para insumos binarios (opcional, se puede saltar)

Solo hace falta si va a recibir PDF, Word, Excel, PowerPoint o draw.io en el inbox. Pregunta si quiere hacerlo ahora o más adelante — el sistema funciona igual con texto plano sin este paso. Si dice que sí:

```bash
python3 --version   # necesita 3.10+; macOS trae 3.9.6 y no alcanza
python3 -m venv kernel/scripts/.venv
kernel/scripts/.venv/bin/pip install -r kernel/scripts/requirements.txt
```

En Windows es `python` en vez de `python3`, con rutas `kernel\scripts\...`. Detalle completo y solución de problemas (Python viejo, dependencias faltantes, etc.) en `kernel/GUIA-DE-USO.md`, secciones 2 y 9, una vez que el repo ya esté clonado.

### Paso 6 — Entregar la posta

Este archivo termina aquí: la personalización real la hace el skill `/x-setup`, que necesita `kernel/AGENTS.md` y `cerebro/PERFIL.md` cargados como contexto de sistema — algo que en una conversación de puro bootstrap probablemente todavía no está pasando.

- Si estás corriendo **dentro de Claude Code o VS Code + Copilot**, ya posicionado en la carpeta clonada, y los comandos `/x-*` están disponibles: dile al humano que ya puede correr `/x-setup`, y ofrécete a correrlo tú mismo en esta misma sesión si te lo pide.
- Si esta conversación es una sesión distinta de la que va a operar el brain (lo más común: te compartieron el repo en un chat de bootstrap y el humano va a abrir Claude Code o Copilot por su cuenta después): dile explícitamente que abra el editor en la carpeta `<carpeta-destino>` y corra `/x-setup` ahí. No lo intentes tú si no vas a seguir siendo la sesión que opera el repo.
- **Si la herramienta es VS Code + Copilot**: los skills no se detectan en una ventana ya abierta antes del clonado, ni tampoco si VS Code abrió la carpeta por primera vez con la extensión de Copilot ya cargada. Dile al humano que cierre VS Code por completo y lo vuelva a abrir posicionado en `<carpeta-destino>` — recién ahí `/x-setup` va a aparecer al escribir `/` en Copilot Chat. Este reinicio va antes de correr `/x-setup`, no después.

No corras `/x-setup` a ciegas ni inventes respuestas de la entrevista en su nombre: es una entrevista guiada que el skill conduce con el humano presente.

## 3. Ruta B — eres un chat sin ejecución de comandos

No puedes clonar nada tú. Tu trabajo es darle al humano los comandos exactos para que los corra en su propia terminal, y pedirle que te copie y pegue la salida si necesitas diagnosticar un error. Guíalo con los mismos pasos de la Ruta A (Pasos 1 a 5), en formato "corre esto tú y cuéntame qué salió". En el Paso 6, explícale que tiene que abrir el repositorio clonado con Claude Code o VS Code + Copilot y correr `/x-setup` ahí — esta conversación no puede continuar la instalación ni la entrevista.

## 4. Qué no hacer

- No fabriques la URL del repositorio si el usuario no la compartió: pídesela.
- No respondas tú la entrevista de `/x-setup`: personaliza el sistema al humano, no a ti.
- No asumas que tiene Python si no lo preguntaste: es opcional y no bloquea el resto de la instalación.
- No edites nada dentro de `kernel/` en ningún paso de este proceso. Si algo de la instalación falla por un problema del propio kernel, es un caso para reportar al starter en GitHub, no para parchear localmente.

---

Con el repositorio clonado y el agente de código activo, la referencia deja de ser este archivo: sigue con `README.md`, `kernel/GUIA-DE-USO.md` (instructivo completo) y `kernel/AGENTS.md` (reglas del sistema).
