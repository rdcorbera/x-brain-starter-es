# Skill: Actualizar Sistema (`/x-actualizar-sistema`)

Trae la última versión del kernel desde el repositorio del starter en GitHub. Gracias a las zonas de propiedad (el upstream solo toca `kernel/`, los stubs y los archivos raíz; el contenido del usuario vive en `cerebro/`, `raw/`, `inbox/` y `plugins/`), la actualización es un merge limpio por construcción.

## 1. Precondiciones

1. Verificar que estamos en un repo git con working tree limpio. Si hay cambios sin commitear, ofrecer commitearlos primero (`brain: respaldo pre-actualización`) — nunca actualizar sobre trabajo sin guardar.
2. Verificar el remote `upstream`:
   - Si no existe, proponerlo y agregarlo: `git remote add upstream https://github.com/rdcorbera/x-brain-starter-es` (confirmar la URL con el usuario — puede usar un fork).
   - Si el repo se clonó directo del starter y `origin` apunta ahí, usar `origin` como upstream.

## 2. Comparar versiones

```bash
git fetch upstream
git show upstream/main:kernel/VERSION    # versión disponible
cat kernel/VERSION                       # versión instalada
```

- Si son iguales: informar "ya estás al día" y terminar.
- Si hay versión nueva: mostrar las entradas de `kernel/CHANGELOG.md` del upstream posteriores a la versión instalada (`git show upstream/main:kernel/CHANGELOG.md`), y un resumen del diff (`git diff HEAD..upstream/main --stat`). Confirmar con el usuario antes de aplicar.

## 3. Aplicar

```bash
git merge upstream/main
```

- **Merge limpio** (lo esperado): continuar al paso 4.
- **Conflicto**: solo puede ocurrir si alguien editó localmente archivos del kernel, violando la regla de zonas. Mostrar los archivos en conflicto y explicar la causa. Resolución recomendada: conservar la versión del upstream para todo lo que esté bajo `kernel/`, `.github/` y los stubs `x-*` (`git checkout --theirs -- <ruta>`), y avisar que las personalizaciones locales del kernel se pierden — si eran valiosas, rescatarlas como plugin (`/x-crear-skill`) o proponerlas al starter.

## 4. Post-actualización

1. Releer las entradas nuevas del CHANGELOG: si alguna versión trae sección **Migración**, aplicar sus pasos (o guiar al usuario) antes de dar por cerrada la actualización.
2. Si cambió `kernel/scripts/requirements.txt`, recordar recrear el venv del conversor.
3. Actualizar la versión de kernel anotada en `cerebro/ESQUEMA.md`.
4. Loguear en `cerebro/log.md`: `**Update**: Kernel actualizado <versión anterior> → <versión nueva>.`
5. Reportar: versión nueva, cambios relevantes para el usuario, migraciones aplicadas.
