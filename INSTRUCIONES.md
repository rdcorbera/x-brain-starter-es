# Plan de refactorización

Existe un sistema de "Second Brain" o "Segundo Cerebro" que busca como finalidad poder recordar y enlazar la informacion de diferentes proyectos.

Puedes leer mas al respecto en estos artículos que escribi:

https://medium.com/@rdcorbera/el-conocimiento-que-no-se-va-a-casa-el-segundo-cerebro-que-tu-empresa-necesita-para-ser-ai-native-e055c5044c0f

https://medium.com/@rdcorbera/ejemplos-y-uso-de-tu-segundo-cerebro-con-ia-el-paso-a-paso-1493392b410c

Y encontrar mi sistema inicial en Github: https://github.com/rdcorbera/second-brain-starter-es

# Problemática

Este sistema ha sido diseñado para ir modificando archivos base del sistema y esas modificaciones dificultan poder realizar actualizaciones futuras ya que la estructura base y los cambios propios que hace el usuario al usar el sistema puede generar errores de conflicto.

Otro inconveniente es que los archivos procesados de la carpeta 00-inbox terminan metidos en otras carpetas y es dificil volver a recrear todo el conocimiento con un solo comando. Seria bueno tener todos los archivos iniciales o raw en una sola carpeta para poder volver a reprocesarlos de ser necesario en un nuevo cerebro.

Otro inconveniente es que si ya tengo una base de conocimiento tambien me gustaria poder portarla en otro sistema o pasarsela a otra persona para que pueda usar mi cerebro, por lo cual seria bueno tener una carpeta unicamente donde se va formando la base de conocimiento, estructuras y conexiones.

# Propuesta de solución

Te voy a dar un par de ideas de posibles soluciones.

1. Aprende como esta estruturado el sistema actual revisando el proyecto "second-brain-starter-es" de Github.
2. Mantener la filosofía y los pilares del sistema que son una LLM Wiki, organizado por un PARA Method, siguiendo un formato OKF.
3. El sistema debe estar abierto a nuevas funcionalidades del usuario, pero cerrado a modificaciones de como funciona el kernel del sistema. Podrias verlo como que debe soportar la inclusión de "plugins" en lo que respecta a que el usuario puede agregar Skills propios para extender la funcionalidad y tambien crear plantillas nuevas de OKF. Para esto seria bueno crear unos skills que puedan crear skills nuevos y plantillas OKF
4. El Kerndel del sistema debe estar en una carpeta aparte de los archivos procesados y del cerebro para que sea facilmente actualizable obteniendo los cambios de github cuando encuentre actualizaciones
5. Considerar si es necesario incluir un archivo o archivos que detallen el esquema de datos. Para si se da el caso de compartir un cerebro a otra persona, el nuevo sistema sepa como funciona su base de conocimiento leyendo el esquema de datos.
6. Considerar otra carpeta para agregar ahi los "plugins"
7. El Kernel debe estar modularizado, para tener modulos como por ejemplo: el onboarding (todo lo referente al setup), la ingesta (todo lo relacionado a la ingesta de informacion), consulta (todo lo relacionado a como el suario puede hacer consultas)

Vamos a partir con esto inicialmente, solo son propuestas de solución, puedes tomarlas, cuestionarlas y proponer otras.