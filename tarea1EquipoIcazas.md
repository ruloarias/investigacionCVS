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

Si CVS decide que un archivo deberia ser ignorado, no lo importa e imprime una 'I 'seguido de el nombrede archivo

Si el archivo "$ CVSROOT / CVSROOT / cvswrappers 'existe, cualquier archivo cuyo nombre coincida con las especificaciones de ese archivo será tratado como paquetes y el filtrado adecuado se realizará en el directorio / archivo antes de ser importado. Ver el archivo cvswrappers.

La fuente externa se guarda en una rama de primer nivel, por defecto 1.1.1. Las actualizaciones son hojas de esta rama; por ejemplo, los archivos de la primera colección importada de la fuente será la revisión 1.1.1.1, a continuación, los archivos de la primera actualización importados serán la revisión 1.1.1.2, y así sucesivamente.

Se requieren al menos tres argumentos. Repositorio es necesario para identificar la colección de fuente. Vendortag es una etiqueta para toda la rama (por ejemplo, por 1.1.1). También debe especificar al menos una RELEASETAG para identificar los archivos en las hojas creadas cada vez que ejecute **import**. El RELEASETAG debe ser nuevo, no existentes previamente en el archivo de depósito, e identificar de forma única el import release.

Note que **import** no cambia el directorio en el que se invoca.En particular, no se estableció ese directorio como  directorio de trabajo CVS; si quieres trabajar con las fuentes importarlas primero y luego compruebalo en un directorio diferente.

#### log - Imprime información de registro para los archivos

	log [options] [files…]   
*Requerimientos*: repositorio, directorio de trabajo.   
*Cambios*: ninguno.  
*Sinónimo*: parche.    

Muestra la información de registro para los archivos. Log utiliza para llamar a la RCS la utilidad rlog. Aunque esto ya no es así en las fuentes actuales, esta historia determina el formato de la salida y las opciones, que no están muy al estilo de los demás comandos CVS.
La salida incluye la ubicación de el archivo RCS, la revisión pincipal (la última revisión en el tronco), todos los nombres simbólicos (etiquetas) y algunas otras cosas. Para cada revisión, el número de revisión, el autor, el número de líneas añadidas / eliminadas y el mensaje de registro se imprimen. Todas las horas se muestran en hora universal coordinada (UTC). (Otras partes de CVS tiempos de impresión en la zona horaria local).

#### rdiff - formatos 'patch' diff entre versiones.

	rdiff [-flags] [-V vn] [-r t|-D d [-r t2|-D d2]] modules…    
*Requerimientos*: repositorio.          
*Cambios*: ninguno.     
*Sinónimo*: parche.  
    
Construye un parche formato Larry Wall (1) Archivo entre dos lanzamientos, que se pueden alimentar directamente en el parche de programa para llevar una vieja versión puesta al día con la nueva versión. (Esta es una de las pocos comandos CVS que operan directamente desde el repositorio, y no requiere una comprobación previa.) La salida diff se envía al dispositivo de salida estándar.
Puede especificar (usando el estándar '-r' y '-D' opciones) cualquier combinación de uno o dos revisiones o fechas. Si se especifica una sola revisión o la fecha, el archivo de revisión refleja las diferencias entre esa revisión o la fecha y las revisiones de cabecera actuales en el archivo RCS.
Tenga en cuenta que si la versión de software afectado está contenido en más de un directorio, entonces puede ser necesario especificar la opción '-p' para el comando patch cuando se parchean las fuentes antiguas, de modo que el parche es capaz de encontrar los archivos que se encuentran en otros directorios.


#### release - indica que un módulo ya no está en uso.
	release [-d] directories…   
*Requerimientos*: Directorio de trabajo.    
*Cambios*: Directorio de trabajo, registro de la historia.     

Este comando está destinado a cancelar de forma segura el efecto de 'cvs checkout'. Desde CVS no bloquea los archivos, no es estrictamente necesario el uso de este comando. Usted siempre puede simplemente borrar su directorio de trabajo, si se quiere; pero corre el riesgo de perder los cambios que pueda haber olvidado, y no deja ningún rastro en el archivo histórico CVS si es que usted ha abandonado su checkout.

Use ‘cvs release'para evitar estos problemas. Este comando comprueba que no haya cambios no confirmados presentes; que se está ejecutando desde inmediatamente por encima de un directorio CVS de trabajo; y que el repositorio de grabado para sus archivos es el mismo que el definido en el repositorio de la base de datos del módulo.
Si todas estas condiciones se cumplen, 'cvs release' deja constancia de su ejecución (que acredite que intencionalmente quiere abandonar su checkout)  registro en el CVS del histórico.

#### remove -  elimina archivos de uso activo. 
 
	remove [-flR] [files...]  
*Requerimientos*: repositorio, directorio de trabajo.   
*Cambios*: directorio de trabajo.

El comando remove se utiliza para eliminar archivos no deseados de su uso activo. El usuario elimina normalmente los archivos desde el directorio de trabajo antes de la invocación del comando remove. Sólo el directorio de trabajo se actualiza. Los cambios en el repositorio no se realizan hasta que el comando commit es ejecutado.

El comando remove no elimina archivos desde el repositorio. CVS mantiene todos los datos históricos en el repositorio de manera que es posible reconstruir los estados anteriores de los proyectos bajo control de revisión.   
Para deshacer el comadno remove CVS  ó para resucitar los archivos que se han eliminado previamente, consulte la Sección complemento Agregar archivos y directorios en el repositorio.    

#### update - trae el árbol de trabajo en sincronizació con  el repositorio.

	update [-ACdflPpR] [-I name] [-j rev [-j rev]] [-k kflag] [-r tag|-D date] [-W spec] files…

*Requerimientos*: repositorio, directorio de trabajo.    
*Cambios*: directorio de trabajo.

Después de ejecutar un checkout para crear su copia privada de la fuente desde el repositorio común, otros desarrolladores continuarán cambiando la fuente central. De vez en cuando, cuando sea conveniente en su proceso de desarrollo, puede utilizar el comando **update** desde dentro de su directorio de trabajo para conciliar su trabajo con las revisiones aplicadas al repositorio de código fuente desde el último checkout ó update.




