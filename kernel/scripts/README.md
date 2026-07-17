# Scripts del sistema

## `a-markdown.py` — convertir insumos a markdown

Convierte un binario del inbox a markdown legible por un LLM. **Es determinista y no usa
modelo: cuesta cero tokens.** Ese es el punto — la eficiencia no viene de elegir un modelo
más barato, viene de que el binario nunca entre en contexto. El agente lee el `.md`, nunca
el original.

### Requisitos: hay que instalar Python

**Python 3.10+** (lo exige markitdown). No viene garantizado en ninguna plataforma:

| | Trae Python | ¿Sirve? |
|---|---|---|
| macOS | 3.9.6 | **No** — se queda corto. `brew install python@3.13` |
| Windows | Ninguno (`python` es un stub que abre la Microsoft Store) | **No** — python.org o `winget install Python.Python.3.13` |
| Linux | Según distro | A veces. Debian/Ubuntu necesitan además `python3-venv` aparte |

El script comprueba la versión y, si se queda corto, dice qué instalar en tu plataforma en
vez de fallar más tarde y más lejos. Solo el **venv** necesita ser 3.10+: el intérprete que
lo lanza puede ser más viejo, porque el script se re-ejecuta dentro del venv antes de nada.

Nada de esto es opcional ni evitable: sin Python no hay conversión, y sin conversión el
agente no puede leer un `.pptx` sin quemar tokens e inventar.

### Instalación

Va en un venv: Python de Homebrew (y el de muchas distros) bloquea `pip install` global
por PEP 668.

**macOS / Linux**

```bash
python3 -m venv kernel/scripts/.venv
kernel/scripts/.venv/bin/pip install -r kernel/scripts/requirements.txt
```

**Windows**

```powershell
python -m venv kernel\scripts\.venv
kernel\scripts\.venv\Scripts\pip install -r kernel\scripts\requirements.txt
```

El script se re-ejecuta solo dentro de ese venv, así que se invoca con el intérprete normal
— `python3` en macOS/Linux, `python` (o `py`) en Windows:

```bash
python3 kernel/scripts/a-markdown.py <archivo> [--out DIR] [--filas N] [--origen RUTA] [--stdout]
```

### Multiplataforma

Funciona en macOS, Linux y Windows. Lo específico de cada plataforma está resuelto dentro
del script, no en quien lo llama:

- **Ruta del venv** — `bin/python3` en POSIX, `Scripts\python.exe` en Windows.
- **Re-ejecución** — `os.execv` en POSIX; en Windows no reemplaza el proceso (lanza otro y
  mata el actual, y la shell da por terminado el comando antes de tiempo), así que allí usa
  `subprocess`.
- **Consola** — se fuerza UTF-8 en stdout/stderr: la consola de Windows no lo usa por defecto
  y `--stdout` reventaría con `UnicodeEncodeError` ante cualquier acento.
- **BOM** — los archivos guardados en Windows suelen llevarlo; se lee con `utf-8-sig` para
  que no se cuele como un carácter invisible en la salida.
- **Saltos de línea** — el `.md` se escribe siempre con LF, para que el mismo insumo no dé
  diff según quién lo convirtió.

> Probado en macOS (incluidos fixtures con BOM + CRLF, que es como llegan los archivos de
> Windows). Los arreglos de Windows están hechos por construcción pero **no verificados en
> una máquina Windows real** — si sos el primero en usarlo ahí, avisá si algo chirría.

- `--out DIR` — dónde escribir el `.md` (por defecto, junto al original).
- `--filas N` — filas por hoja en `.xlsx` (por defecto 50).
- `--origen RUTA` — ruta bundle-relativa del raw a citar. Si se omite, se deduce.
- `--stdout` — imprime en vez de escribir.

### Motor por formato, y el porqué

| Formato | Motor | Por qué |
|---|---|---|
| `.docx` `.pdf` `.pptx` | MarkItDown | Es exactamente su caso de uso. En `.pptx` incluye las notas del orador. |
| `.html` | bs4 → MarkItDown | MarkItDown quita `script`/`style` pero **no** `nav`/`footer`. Se limpian antes. |
| `.xlsx` | openpyxl propio | Muestreo, no volcado. Ver abajo. |
| `.drawio` | stdlib propio | Ninguna herramienta lo cubre. Sale Mermaid, como pide el repo. |
| `.yaml` `.yml` | passthrough | Ya es texto casi óptimo: convertirlo costaría tokens y perdería fidelidad. |
| `.doc` `.ppt` `.xls` | error accionable | Binarios legacy: nadie los lee sin LibreOffice. Pide «Guardar como» moderno. |

### Por qué `.xlsx` no usa MarkItDown

Es la bomba de tokens nº1. Medido sobre una hoja de 1.500 filas:

| | caracteres | ~tokens |
|---|---|---|
| MarkItDown (vuelca todo) | 75.308 | ~18.800 |
| este script (muestrea) | 3.327 | ~830 |

**95,6% menos.** Por hoja: cabecera + primeras 50 filas, fórmulas → valores, hojas vacías
omitidas, y una línea honesta de dimensiones (`1.501 filas × 6 columnas — se muestran las
primeras 50`). El dato completo no se pierde: el `.xlsx` íntegro sigue en `raw/` y se
consulta a demanda.

> **Ojo con las fórmulas.** openpyxl no las evalúa: lee el valor que Excel dejó en caché.
> Un libro generado por un script y nunca abierto en Excel no tiene ese caché y sus columnas
> calculadas salen vacías. El script lo detecta y lo dice en «Avisos de conversión» en vez
> de callarse.

### Sobre `.pptx`

Hubo aquí un conversor propio con python-pptx, escrito sobre la creencia —repetida en varios
artículos— de que MarkItDown se salta las notas del orador. **Se midió contra markitdown
0.1.6 y es falso:** las incluye bajo `### Notes:`, con mejor estructura que el código propio.
Se borró. Si alguna vez se comprueba que se pierden, `conv_pptx` es el sitio.

### Avisos

Cuando la conversión pierde algo o sospecha de algo, no lo esconde: lo escribe en una sección
«Avisos de conversión» del `.md` (para que el agente lo vea) y en stderr (para que lo veas
vos). PDF sin capa de texto, hoja truncada, fórmulas sin caché, plantilla web descartada.

### Salida

Frontmatter OKF (`type: Insumo`, o `type: Diagrama` para `.drawio`) + cuerpo + `# Citations`
apuntando al original. El campo `description` queda como `<pendiente>` a propósito: lo
completa `/x-procesar-inbox` al integrar. El script no inventa — regla del repo.
