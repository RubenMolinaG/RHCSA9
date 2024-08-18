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
