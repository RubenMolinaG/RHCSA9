# RHCSA9

## Utilizar la redirección de entrada-salida (>, >>, |, 2>, etc.)
**Ejercicio 1**: Crea un archivo llamado output.txt que contenga la lista de todos los archivos y directorios en el directorio /etc. Utiliza la redirección adecuada para sobrescribir cualquier contenido existente en output.txt.

**Ejercicio 2**: Añade al archivo output.txt la lista de todos los archivos y directorios en el directorio /var/log. Utiliza la redirección adecuada para mantener el contenido existente en output.txt y añadir la nueva información al final.

**Ejercicio 3**: Intenta listar un directorio que no existe (/no_existe) y redirige el mensaje de error a un archivo llamado errors.log.

**Ejercicio 4**: Redirige tanto la salida estándar como los mensajes de error del comando find / -name "*.conf" a un archivo llamado find_output.log.

**Ejercicio 5**: Usa un comando que liste todos los archivos en /usr/bin que comiencen con la letra a y contenga la palabra "bash". Filtra la salida utilizando un pipe (|) para que solo se muestren las líneas que contienen la palabra "bash".

**Ejercicio 6**: Utiliza el comando cat para mostrar el contenido del archivo /etc/hosts, redirigiendo la entrada desde el archivo en lugar de escribirlo manualmente en el terminal.

**Ejercicio 7**: Ejecuta un comando que liste todos los archivos en el directorio /var y redirige la salida estándar a un archivo llamado var_list.txt. Además, redirige cualquier error generado a un archivo llamado var_errors.log.

**Ejercicio 8**: Redirige la salida de errores del comando grep "root" /etc/* a la salida estándar y luego redirige toda la salida combinada a un archivo llamado root_search.log.

**Ejercicio 9**: Usa el comando sort para ordenar el contenido del archivo output.txt y redirige la salida ordenada a un archivo llamado sorted_output.txt.

**Ejercicio 10**: Encuentra todos los archivos en el directorio /home que contengan la palabra "password" en su nombre. Redirige la salida estándar a un archivo llamado password_files.txt y cualquier error al archivo password_errors.log. Luego, usa un pipe para contar el número de líneas en password_files.txt y guarda ese número en un archivo llamado count.txt.

**Ejercicio 11**: Ejecuta un comando que liste el contenido del directorio /usr/bin. Duplica la salida estándar al archivo stdout.log y la salida de error al archivo stderr.log, de manera que ambos archivos contengan tanto la salida estándar como los errores.

**Ejercicio 12**: Encuentra todos los archivos en /etc que contengan la palabra "config" en su nombre. Filtra la salida para mostrar solo las líneas que contienen la palabra "network", redirigiendo esta salida filtrada a un archivo llamado network_configs.txt. Redirige cualquier error a un archivo llamado config_errors.log.

**Ejercicio 13**: Lista todos los archivos en el directorio /var/log, usa un pipe para filtrar solo aquellos archivos que contienen la palabra "error" en su nombre, luego usa otro pipe para contar cuántos de esos archivos existen. Redirige el conteo final a un archivo llamado error_count.txt.

**Ejercicio 14**: Intenta crear un archivo en un directorio para el cual no tienes permisos (por ejemplo, /root/testfile). Redirige el error al archivo permission_errors.log y utiliza ese archivo como entrada para un comando que cuente cuántas veces aparece la palabra "Permission denied".

**Ejercicio 15**: Ejecuta un comando que liste todos los archivos en /usr/share. Redirige la salida estándar a /dev/null, de manera que solo los errores sean visibles en la terminal.

## Utilizar expresiones regulares y grep para analizar textos

**Ejercicio 1**: Busca todas las líneas en el archivo **/var/log/secure** que contengan la palabra "**Failed**" (independientemente de las mayúsculas o minúsculas).

**Ejercicio 2**: En el archivo **/etc/passwd**, muestra todas las líneas que contienen la palabra "**bin**" como una palabra completa, sin que sea parte de otra palabra.

**Ejercicio 3**: Encuentra todas las líneas en el archivo **/etc/hosts** que comiencen con "**127.0.0.1**".

**Ejercicio 4**: En el archivo **/etc/services**, busca todas las líneas que terminen con el puerto "**80/tcp**".

**Ejercicio 5**: En el archivo **/etc/passwd**, muestra todas las líneas que **NO** contienen la palabra "**nologin**".

**Ejercicio 6**: Cuenta cuántas líneas en el archivo **/var/log/messages** contienen la palabra "**error**".

**Ejercicio 7**: En el archivo **/var/log/secure**, encuentra todas las líneas que contienen una dirección IP en el rango "10.x.x.x", donde x puede ser cualquier número de 1 a 3 dígitos.

**Ejercicio 8**: En el archivo **/var/log/messages**, busca la palabra "warn" y muestra las 3 líneas anteriores y 3 líneas posteriores a cada coincidencia.

**Ejercicio 9**: Encuentra en el archivo **/etc/passwd** todas las líneas que contengan las palabras "**root**" o "**sysadmin**".

**Ejercicio 10**: En el archivo **/var/log/secure**, busca todas las líneas que contengan una dirección IP en el rango "**192.168.x.x**" y que también incluyan la palabra "**sshd**".

**Ejercicio 11**: Encuentra en el archivo **/etc/services** todas las líneas que contengan un número de puerto mayor a 5000.

**Ejercicio 12**: En el archivo **/usr/share/dict/words**, encuentra todas las palabras que contengan tanto la letra "e" como la letra "t" en cualquier orden.

**Ejercicio 13**: Encuentra en el archivo **/etc/ssh/sshd_config** todas las líneas que contengan la frase exacta "**PermitRootLogin yes**".

**Ejercicio 14**: Encuentra todas las líneas en un archivo llamado **contacts.txt** que contengan un número de teléfono en el formato "**XXX-XXX-XXXX**".

**Ejercicio 15**: Encuentra en el archivo **/var/log/secure** todas las líneas que contengan la palabra "**Accepted**" y cuántas de ellas tienen una dirección IP de origen en el rango "**192.168.x.x**".

**Ejercicio 16**: Encuentra en el archivo **/etc/passwd** todas las líneas donde el nombre del usuario tenga exactamente **5 caracteres**.

**Ejercicio 17**: En el archivo **/etc/group**, muestra todas las líneas que contienen la palabra "**admin**" pero excluye aquellas que también contengan la palabra "**sudo**".

**Ejercicio 18**: Busca en el archivo **/var/log/messages** la palabra "**critical**" y resalta todas las coincidencias en la salida.

**Ejercicio 19**: Busca la palabra "**fatal**" en todos los archivos dentro del directorio **/var/log**.

**Ejercicio 20**: Encuentra en el archivo **/etc/ssh/sshd_config** todas las líneas que no estén comentadas (que no comiencen con un #) y contengan la palabra "**Permit**".
