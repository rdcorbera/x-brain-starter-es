# Inbox

Aquí va TODO lo crudo, sin pensar: transcripciones de reuniones, documentos recibidos, capturas, notas rápidas, correos pegados como texto.

Regla de oro: nada se queda aquí más de un día. Correr `/x-procesar-inbox` para clasificar.

Convención sugerida para nombres: `YYYY-MM-DD-descripcion-corta.ext`. No hace falta ser prolijo — el Bibliotecario clasifica y renombra al archivar en `/raw/`; solo evita nombres como `notas3.txt`.

## Agrupar por proyecto o área

Si ya sabes a dónde va lo que sueltas, ponlo en una carpeta con el nombre del proyecto o del área: todo lo que esté adentro se atribuye ahí, sin que el Bibliotecario pregunte archivo por archivo.

```
inbox/
├── notas-sueltas.txt          ← se clasifica por contenido
└── migracion-erp/             ← todo esto va a 2026-q3-migracion-erp/
    ├── brief.docx
    └── 2026-07-20-kickoff.vtt
```

El nombre no tiene que ser exacto: `migracion-erp/` encuentra a `2026-q3-migracion-erp/` sin el prefijo de periodo. Si la carpeta no corresponde a ningún proyecto ni área, no se inventa nada: te pregunta y te ofrece crear el proyecto con `/x-nueva-iniciativa`. Las carpetas también desaparecen al procesar.

Esta carpeta es transitoria: después de procesar, cada original vive en `raw/` (renombrado e inmutable) y su conocimiento queda integrado en `cerebro/`.
