# Cuestionario de setup — las 6 rondas de `/x-setup`

Este archivo es el guion de la entrevista de `/x-setup`. Tiene tres usos:

1. **El agente lo conduce** — cada ronda trae, además de las preguntas, un bloque *Para qué sirve* que explica qué decisión del sistema depende de esa respuesta, y un *Produce* con los archivos que genera.
2. **El usuario lo lee para prepararse** — cada pregunta trae un *Ejemplo* de respuesta real, para saber qué nivel de detalle se espera.
3. **Se llena y se entrega** — copiar este archivo, responder las líneas `**Respuesta:**` y pasarle la ruta al skill (ver Fase 1 de `setup.md`). Sirve para responder en frío, para delegar el llenado, y para armar cerebros de demo o de prueba con respuestas ficticias.

> **Zona kernel.** Este archivo no se edita localmente (regla de zonas de `kernel/AGENTS.md`). Para llenarlo, copiarlo a `inbox/` — que sí es zona del usuario — o a cualquier ruta fuera del kernel. Para cambiar las preguntas del sistema, issue o PR al starter.

**Regla que atraviesa todas las rondas: no fabricar.** Si una respuesta viene delgada o vacía, la sección del perfil queda delgada — se anota como hueco a llenar con el uso. Nunca rellenar con supuestos, ni traducir las palabras del usuario a tono corporativo: el perfil se escribe con su voz.

---

## Ronda 1 — Quién eres

**Para qué sirve.** Es la identidad que todo agente carga al inicio de cada sesión, junto con `kernel/AGENTS.md`. De aquí sale el encuadre con el que se interpreta todo lo demás: qué vocabulario usar, qué es relevante para esta persona y qué no, y en qué idioma se escribe el cerebro entero.

**Produce.** `cerebro/PERFIL.md` → sección "Quién soy". El idioma queda como configuración del sistema.

**1.1 ¿Cómo te llamas y en qué organización trabajas?**
*Ejemplo:* Ana García, en Meridian Salud (aseguradora, ~800 personas).
**Respuesta:**

**1.2 ¿Cuál es tu rol exacto y hace cuánto lo ocupas?**
*Ejemplo:* Líder de Producto del área de Siniestros, hace 8 meses (antes 3 años como analista funcional en la misma empresa).
*Por qué importa:* la antigüedad calibra cuánto contexto de la organización se puede dar por sabido y cuánto hay que documentar desde cero.
**Respuesta:**

**1.3 ¿Qué entregables produce tu trabajo? Es decir, ¿qué cosas concretas salen de tus manos?**
*Ejemplo:* Documentos de requerimientos, el roadmap trimestral del área, presentaciones para el comité, y actas de decisión de producto.
*Por qué importa:* los entregables son la salida del sistema. Definen qué vive en `04-entregables/` de cada proyecto y qué tipo de documento le sirve al usuario cuando consulta la base.
**Respuesta:**

**1.4 De todo eso, ¿qué parte te da energía y cuál sientes más como trámite?**
*Ejemplo:* Me energiza diseñar la solución con el equipo técnico y ver un piloto salir a producción. El trámite es el reporte mensual al comité y perseguir aprobaciones.
*Por qué importa:* no es una pregunta de satisfacción laboral. Marca dónde poner el énfasis cuando el agente tiene margen de criterio: qué destacar primero en `/x-briefing-diario` y `/x-actualizacion-semanal`, y qué conviene resumir corto en vez de desarrollar.
**Respuesta:**

**1.5 ¿En qué idioma quieres el contenido del cerebro?**
*Ejemplo:* Español. (Default si no se responde.)
*Por qué importa:* todo el cerebro se escribe en este idioma, incluso si la conversación con el agente ocurre en otro.
**Respuesta:**

**1.6 ¿Hay contexto personal que los agentes deban tener presente?**
*Ejemplo:* Trabajo remoto desde otra zona horaria que el resto del equipo; las reuniones con Casa Matriz son siempre temprano. Estoy cursando una certificación los viernes.
*Por qué importa:* restricciones reales de agenda y disponibilidad que afectan cómo se prioriza y cuándo se sugiere hacer las cosas. Opcional — si no hay nada, se deja vacío.
**Respuesta:**

---

## Ronda 2 — Tu proceso de trabajo

**Para qué sirve.** Define el **ciclo de planificación** (el "periodo" del sistema), que a su vez determina el nombre de las carpetas de proyecto y la cadencia de `/x-actualizacion-semanal` y `/x-cierre-periodo`. Y define la cadena de insumos y entregas, que es lo que permite al agente saber qué documento espera a cuál.

**Produce.** `cerebro/PERFIL.md` → sección "Mi rol y proceso", incluido el formato de periodo.

**2.1 ¿Cómo fluye tu trabajo de inicio a fin?**
*Ejemplo:* Llega una necesidad del área comercial o de un incidente operativo → la levanto como iniciativa y la valido con el equipo técnico → escribo el documento de requerimientos → pasa a comité para aprobación de presupuesto → se construye → yo hago el seguimiento y la validación funcional → sale a producción.
*Por qué importa:* con esto el agente sabe en qué etapa está cada proyecto y qué falta para cerrarlo, sin preguntarlo cada vez.
**Respuesta:**

**2.2 ¿De quién recibes insumos y a quién entregas?**
*Ejemplo:* Recibo de Comercial (necesidades) y de Operaciones (incidentes). Entrego a Tecnología (requerimientos) y al Comité de Inversiones (casos de negocio).
*Por qué importa:* define qué llega al `inbox/` y de quién, y a quién apuntan los entregables. También alimenta el mapa de personas de la Ronda 3.
**Respuesta:**

**2.3 ¿Tu planificación es trimestral, mensual, por sprints, continua?**
*Ejemplo:* Trimestral, alineada al comité. → el periodo es `2026-Q3` y las carpetas de proyecto quedan `2026-Q3-nombre-del-proyecto/`.
*Otros formatos:* mensual → `2026-08-...`; sprints → `2026-S14-...`; continua → sin prefijo de periodo, se acuerda una convención.
*Por qué importa:* es la decisión estructural más importante de esta ronda. Todas las carpetas de `01-proyectos/` y el archivado de `04-archivo/` dependen de ella.
**Respuesta:**

**2.4 ¿Hay rituales o hitos fijos en ese ciclo?**
*Ejemplo:* Comité de Inversiones el primer martes de cada mes; planning trimestral la última semana del trimestre; weekly de área los lunes.
*Por qué importa:* son fechas recurrentes contra las cuales `/x-briefing-diario` y `/x-preparar-reunion` pueden anticipar qué hay que tener listo. Opcional.
**Respuesta:**

---

## Ronda 3 — El mapa de personas

**Para qué sirve.** El conocimiento de una organización es inseparable de quién lo tiene. Este mapa permite que el agente sepa a quién hay que preguntarle algo, quién decide qué, y que `/x-preparar-reunion` pueda armar una agenda real. Las relaciones `reporta-a` construyen el organigrama.

**Produce.** Una ficha por persona en `cerebro/02-areas/personas/` (plantilla `persona.md`) + `cerebro/02-areas/personas/ORGANIGRAMA.md` (Mermaid `graph TD`).

**3.1 ¿Con qué personas y roles interactúas regularmente?**

Una fila por persona. Lo que no se sepa se deja vacío: un `reporta-a` desconocido es un hueco legítimo del organigrama y genera su propia `Pregunta`, no un supuesto.

| Nombre | Rol | Reporta a | Cómo trabaja / qué tener en cuenta |
|---|---|---|---|
| *Carlos Méndez* | *Gerente de Tecnología* | *Dirección General* | *Decide arquitectura. Prefiere propuestas escritas antes de reunirse; no improvisa en vivo.* |
| *Laura Pinto* | *Analista de Siniestros* | *Carlos Méndez* | *La referencia de todo lo operativo del proceso actual. Responde rápido por chat.* |
|  |  |  |  |

**3.2 ¿Alguien de esa lista es una relación clave o delicada?**
*Ejemplo:* Con Carlos hay que llegar con el análisis cerrado; si le llevo una idea a medias la descarta. Con el Comité el trato es formal y siempre por escrito.
*Por qué importa:* ajusta el tono y el nivel de preparación que el agente propone para cada interacción.
**Respuesta:**

---

## Ronda 4 — Tus áreas de conocimiento

**Para qué sirve.** Las áreas son las responsabilidades **permanentes** — lo que sigue siendo tuyo cuando los proyectos terminan. Es la diferencia entre `01-proyectos/` (temporal, con fecha de cierre) y `02-areas/` (continuo). También es donde se decide si este rol necesita **tipos de documento propios**, que es lo que adapta el sistema a oficios que el catálogo base no cubre.

**Produce.** Carpetas en `cerebro/02-areas/` con su `index.md`; documentos `Lineamiento`; si aplica, tipos propios (plantilla en `plugins/plantillas/` + registro en `cerebro/ESQUEMA.md`) y carpetas extra en `cerebro/03-recursos/`.

**4.1 ¿Cuáles son tus responsabilidades continuas y dominios de conocimiento?**
*Ejemplo (Líder de Producto):* proceso de siniestros, producto de salud, regulación del sector, relación con proveedores tecnológicos.
*Otros roles:* un vendedor → clientes, producto, competencia. Un abogado → contratos, regulación, litigios. Un investigador → líneas de investigación, instrumental, publicaciones.
**Respuesta:**

**4.2 ¿Qué estándares, políticas o reglas de trabajo ya conoces y quieres dejar registrados?**
*Ejemplo:* Todo requerimiento pasa por validación de Legal antes de ir a comité. Ningún proyecto arranca sin presupuesto aprobado. Las integraciones con terceros exigen contrato de datos firmado.
*Por qué importa:* cada uno se guarda como documento `Lineamiento` y pasa a ser una regla contra la cual `/x-decision` valida las decisiones nuevas — así el sistema detecta cuando algo contradice una política vigente.
**Respuesta:**

**4.3 ¿Tu trabajo necesita tipos de documento que el catálogo base no tiene?**
*Catálogo base:* `Iniciativa`, `Insumo`, `Reunion`, `Decision`, `Pregunta`, `Persona`, `Sistema`, `Lineamiento`, `Diagrama`, `Playbook`, `Glosario`.
*Ejemplo:* Sí — necesito `Producto` (cada producto de seguro con su ficha técnica y estado regulatorio) y `Incidente` (los eventos operativos que disparan iniciativas).
*Por qué importa:* es el mecanismo de adaptación del sistema al oficio. Se crean siguiendo `kernel/modulos/extension/crear-plantilla.md`. Si un tipo base ya cubre el caso, proponerlo antes de crear uno nuevo.
**Respuesta:**

**4.4 ¿`cerebro/03-recursos/` necesita carpetas además de `sistemas-y-herramientas/` y `glosario/`?**
*Ejemplo:* Sí — `normativa/` para las circulares del regulador y `proveedores/` para las fichas de los que integramos.
**Respuesta:**

---

## Ronda 5 — Reglas de comunicación

**Para qué sirve.** Es el contrato de trato entre el usuario y los agentes, y el límite duro de qué información no entra al cerebro. Se aplica en todas las sesiones, no solo en el setup.

**Produce.** `cerebro/PERFIL.md` → secciones "Reglas de comunicación" y "Confidencialidad".

**5.1 ¿Cómo quieres que los agentes te hablen?**
*Ejemplo:* Directo y sin preámbulos. Si algo está mal, dímelo de frente. No quiero resúmenes de lo que acabas de hacer si ya lo vi.
*Opciones de referencia:* directo / con matices / balanceado.
**Respuesta:**

**5.2 ¿Tienes manías o reglas específicas de formato?**
*Ejemplo:* Nada de emojis. Las tablas antes que las listas largas. Los documentos para comité siempre arrancan con la recomendación, no con el contexto.
**Respuesta:**

**5.3 ¿Qué restricciones de confidencialidad aplican en tu organización?**
*Ejemplo:* Ningún dato identificable de asegurados (nombre, cédula, diagnóstico). Los montos de siniestros individuales no salen del sistema core. Los nombres de proveedores en negociación no se escriben hasta que se firma.
*Base que aplica siempre:* nunca credenciales, secretos, tokens ni datos personales de clientes o terceros. Ante la duda, el dato sensible no entra.
**Respuesta:**

**5.4 ¿Qué cosas NO deben hacer los agentes nunca?**
*Ejemplo:* Nunca escribir en nombre mío como si fuera un mensaje enviado. Nunca dar por cerrada una decisión que no confirmé. Nunca asumir la posición del área comercial sin fuente.
**Respuesta:**

---

## Ronda 6 — Objetivos del periodo

**Para qué sirve.** Es la vara contra la cual el sistema mide si el trabajo avanza. `/x-briefing-diario` prioriza contra estos objetivos, `/x-actualizacion-semanal` los revisa y `/x-cierre-periodo` hace el retro. Sin esto el cerebro archiva bien pero no orienta.

**Produce.** `cerebro/GOALS.md` con los 3 bloques. Por cada proyecto que el usuario quiera arrancar ya, se sugiere correr `/x-nueva-iniciativa` (no se crean aquí).

**Empujar suavemente por especificidad:** "certificación X antes de septiembre" vale diez veces más que "aprender más". Una métrica y una fecha cuando se pueda.

**6.1 Bloque 1 — Proyectos o iniciativas asignadas activas.** Nombre + una línea cada una.
*Ejemplo:*
- *Migración del core de siniestros — reemplazar el sistema legado antes de fin de año; estoy a cargo del lado funcional.*
- *App de autoservicio para asegurados — piloto con 500 usuarios en septiembre.*
**Respuesta:**

**6.2 Bloque 2 — Objetivos personales del periodo.** Con métrica y fecha si es posible.
*Ejemplo:*
- *Certificación de Product Management antes del 30 de septiembre.*
- *Reducir a la mitad el tiempo que dedico a reportes manuales (hoy ~6 h/semana).*
**Respuesta:**

**6.3 Bloque 3 — Objetivos de tu equipo o área que te tocan o quieres impulsar.**
*Ejemplo:*
- *Bajar el tiempo promedio de resolución de siniestros de 12 a 8 días (meta del área).*
- *Instalar la práctica de registrar decisiones por escrito — hoy se pierden en reuniones.*
**Respuesta:**
