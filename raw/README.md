# Raw — fuentes crudas inmutables

Todos los originales que alguna vez entraron por el inbox viven aquí, en un solo lugar, con nombre `YYYY-MM-DD-descripcion-tiny_uuid.ext` (fecha de ingesta + descripción kebab-case + sufijo único corto para evitar colisiones).

Reglas:

1. **Inmutable.** Nada de esta carpeta se edita ni se borra. El wiki en `cerebro/` los cita (`/raw/...`); jamás los reemplaza.
2. **Solo escribe `/x-procesar-inbox`.** Ningún otro skill (ni el usuario, idealmente) agrega o toca archivos aquí.
3. **`manifiesto.md` es el registro.** Cada archivo tiene su línea: nombre original, destino en el cerebro, fecha y páginas generadas. Lo mantiene `/x-procesar-inbox`; no editar a mano.

Con esta carpeta + `manifiesto.md` se puede reconstruir todo el conocimiento en un starter limpio con `/x-reconstruir`: por eso importa que ningún original quede fuera.
