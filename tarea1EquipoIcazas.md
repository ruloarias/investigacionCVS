#####diff—Muestra las diferencias entre revisiones#####

*Sintaxis*: diff [-lR] [-k kflag] [format_options] [[-r rev1 | -D date1] [-r rev2 | -D date2]] [files…]
*Requerimientos*: directorio de trabajo, repositorio.
*Cambios*: ninguno.

El comando **diff** es usado para comparar diferentes revisiones de archivos. La acción predeterminada es comparar sus archivos de trabajo con las revisiones que se basaron en el, y reportar cualquier diferencia encontrada.

#####export- Exporta fuentes desde CVS, similar al comando checkout.#####

*sintaxis*: export [-flNnR] [-r rev|-D date] [-k subst] [-d dir] module…
*requerimientos*: repositorio.
*cambios*: directorio actual.

Este comando es una variante de checkout, es usado cuando quieres una copia de la fuente para el módulo sin los directorios administrativos de CVS. Por ejemplo, podrías usar export para preparar fuentes para su envio fuera de sitio.Este comando requiere que se especifique una fecha o una etiqueta (con '-D' ó '-r') de modo que usted puede contar con la reproducción de la fuente de envíos a otros(y por lo tanto siempre se tendran directorios vacios ).

A menudo se le gustaría usar '-kv' con cvs export. Esto hace que cualquier palabra clave que se amplie de tal manera que al importarla a algún otro sitio no se pierdan las palabas clave en la revisión de la información.Pero tenga en cuenta que no maneja una exportación que contiene los archivos binarios correctamente.También tenga en cuenta que después de haber usado '-kv', Ya no se puede usar el comando **ident**(que es parte de la suite RCS), que busca cadenas de palabras clave. Si usted quiere ser capaz de utilizar **ident** no debe usar '-kv'.

#####history- Muestra el status de archivos y usuarios#####

- *Sintaxis*: history [-report] [-flags] [-options args] [files…]


- *Requerimientos*: el archivo ‘$CVSROOT/CVSROOT/history’

CVS puede mantener un archivo histórico que rastrea cada uso de checkout, commit, rtag, update, y comandos release. Puede usar history para mostrar esta información en varios formatos.

Loggin debería estar habilitado para la creación del archivo ‘$CVSROOT/CVSROOT/history’.

history usa ‘-f’, ‘-l’, ‘-n’, and ‘-p’ de manera que entra en conflicto con el uso normal dentro de CVS.















