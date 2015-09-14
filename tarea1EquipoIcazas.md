####diff - Muestra las diferencias entre revisiones

	diff [-lR] [-k kflag] [format_options] [[-r rev1 | -D date1] [-r rev2 | -D date2]] [files…]
*Requerimientos*: directorio de trabajo, repositorio.  
*Cambios*: ninguno.

El comando **diff** es usado para comparar diferentes revisiones de archivos. La acción predeterminada es comparar sus archivos de trabajo con las revisiones que se basaron en el, y reportar cualquier diferencia encontrada.

####export - Exporta fuentes desde CVS, similar al comando checkout.

	export [-flNnR] [-r rev|-D date] [-k subst] [-d dir] module…
*requerimientos*: repositorio.  
*cambios*: directorio actual.

Este comando es una variante de checkout, es usado cuando quieres una copia de la fuente para el módulo sin los directorios administrativos de CVS. Por ejemplo, podrías usar export para preparar fuentes para su envio fuera de sitio.Este comando requiere que se especifique una fecha o una etiqueta (con '-D' ó '-r') de modo que usted puede contar con la reproducción de la fuente de envíos a otros(y por lo tanto siempre se tendran directorios vacios ).

A menudo le gustaría usar '-kv' con cvs export. Esto hace que cualquier palabra clave que se amplie de tal manera que al importarla a algún otro sitio no se pierdan las palabas clave en la revisión de la información.Pero tenga en cuenta que no maneja una exportación que contiene los archivos binarios correctamente.También tenga en cuenta que después de haber usado '-kv', Ya no se puede usar el comando **ident**(que es parte de la suite RCS), que busca cadenas de palabras clave. Si usted quiere ser capaz de utilizar **ident** no debe usar '-kv'.

####history - Muestra el status de archivos y usuarios#####

	history [-report] [-flags] [-options args] [files…]


*Requerimientos*: el archivo ‘$CVSROOT/CVSROOT/history’  
*cambios*: nada.

CVS puede mantener un archivo histórico que rastrea cada uso de checkout, commit, rtag, update, y comandos release. Puede usar history para mostrar esta información en varios formatos.

Loggin debería estar habilitado para la creación del archivo ‘$CVSROOT/CVSROOT/history’.

history usa ‘-f’, ‘-l’, ‘-n’, and ‘-p’ de manera que entra en conflicto con el uso normal dentro de CVS.

####import - importación de fuentes en CVS usando ramas de desarrollo.   	

	import [-opciones] ETIQUETALIBERACIÓN etiquetadesarrollo repositorio ...  

*Requerimientos*: directorio de distribución de repositorio, fuente.   
*Cambios*: repositorio.

Use **import** para incorporar una fuente de distribución de la totalidad de una fuente externa (por ejemplo, un proveedor de origen) en el directorio de repositorio de código fuente. Puede utilizar este comando, tanto para la creación inicial de un repositorio, y actualizaciones al por mayor en el módulo de la fuente externa.

El argumento repositorio da un nombre de directorio (o una ruta de acceso a un directorio) bajo el  directorio CVS raíz de repositorios; si no existiera el directorio, import lo crea.

Cuando usas import para actualizaciónes de código que han sido modificadas en su repositorio de fuentes(desde una importación antes), será norificado por algún conflicto de archivos en las dos ramas de desarrollo; usa 'checkout -j' para reconciliar las diferencias, tal como import instruye hacerlo. 

Si CVS decide que un archivo deberia ser ignorado, no lo importarlo e imprime una 'I 'seguido de el nombrede archivo

Si el archivo "$ CVSROOT / CVSROOT / cvswrappers 'existe, cualquier archivo cuyo nombre coincida con las especificaciones de ese archivo será tratado como paquetes y el filtrado adecuado se realizará en el directorio / archivo antes de ser importado. Ver el archivo cvswrappers.

La fuente externa se guarda en una rama de primer nivel, por defecto 1.1.1. Las actualizaciones son hojas de esta rama; por ejemplo, los archivos de la primera colección importada de la fuente será la revisión 1.1.1.1, a continuación, los archivos de la primera actualización importados serán la revisión 1.1.1.2, y así sucesivamente.

Se requieren al menos tres argumentos. Repositorio es necesario para identificar la colección de fuente. Vendortag es una etiqueta para toda la rama (por ejemplo, por 1.1.1). También debe especificar al menos una RELEASETAG para identificar los archivos en las hojas creadas cada vez que ejecute **import**. El RELEASETAG debe ser nuevo, no existentes previamente en el archivo de depósito, e identificar de forma única el import release.

Note que **import** no cambia el directorio en el que se invoca.En particular, no se estableció ese directorio como  directorio de trabajo CVS; si quieres trabajar con las fuentes importarlas primero y luego compruebalo a cabo en un directorio diferente.



