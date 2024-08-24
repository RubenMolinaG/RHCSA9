## SELinux

### Verificar el Estado de SELinux.

- **Enforcing**: SELinux aplica estrictamente las políticas de seguridad, bloqueando cualquier acción que no esté permitida en las mismas.

- **Permissive**: SELinux NO bloquea acciones, pero registra todas las violaciones de políticas en los logs. Útil para el diagnóstico de problemas.

- **Disabled**: SELinux está completamente deshabilitado y no aplica ni registra ninguna política de seguridad.

`sestatus` &rarr; Muestra el estado de SELinux.

```bash
setenforce 0	# Cambia SELinux a modo `permissive` (temporalmente).
setenforce 1	# Cambia SELinux a modo `enforcing` (temporalmente).
```

`sudo vim /etc/selinux/config` &rarr; Cambia el estado de SELinux a **enforcing**, **permissive** o **disabled**. Este cambio se aplica después de reiniciar el sistema.

```bash
# Example config file entry:
SELINUX=enforcing
```
---

### Identificación del Contexto Actual.

```bash
ls -Z /path/to/file	# Muestra el contexto de SELinux de un archivo.
ps -eZ | grep proc-name	# Muestra el contexto de SELinux de un proceso.
semanage port -l | grep <puerto> # Muestra el contexto SELinux para un puerto específico.
```
---

### Diagnóstico de Problemas.

`cat /var/log/audit/audit.log | grep AVC` &rarr; Filtra los registros de SELinux en el log de auditoría para encontrar mensajes de Control de Acceso Voluntario (AVC).

`sealert -a /var/log/audit/audit.log` &rarr; Utiliza *sealert* para analizar los logs de SELinux y generar un reporte detallado de posibles problemas y soluciones.

`audit2allow -a` &rarr; Crea políticas de SELinux a partir de los logs. 

---

### Aplicación de Cambios Necesarios.

`chcon -t httpd_sys_content_t /var/www/html/index.html` &rarr; Cambia el tipo de contexto del fichero *index.html* a *httpd_sys_content_t*, que es adecuado para archivos servidor por un servidor web.

`semanage fcontext -a -t httpd_sys_content_t /var/www(/.*)?` &rarr; Añade una regla para asignar el contexto correcto de forma pemanente.

`restorecon -Rv /var/www/html` &rarr; Restaura el contexto SELinux por defecto de un archivo o directorio basado en las políticas del sistema.

---

### Configuración de Booleanos de SELinux.

`getsebool -a` &rarr; Lista todos los booleanos de SELinux y su estado actual.

`setsebool httpd_can_network_connect on` &rarr; Activa el booleano *httpd_can_network_connect on* temporalmente.

`setsebool -P httpd_can_network_connect on` &rarr; Activa el booleano *httpd_can_network_connect on* permanentemente.

---

```bash
# Asegura que el servidor Apache pueda acceder a sus archivos y conectar a bases de datos remotas.
chcon -R -t httpd_sys_content_t /var/www/html/
setsebool -P httpd_can_network_connect_db on
```

```bash
# Permite a los usuarios autenticados subir archivos a un directorio específico.
chcon -R -t public_content_rw_t /var/ftp/uploads/
setsebool -P ftp_home_dir on
```
---

`touch /.autorelabel` &rarr; Fuerza a SELinux a reetiquetar todos los archivos del sistema durante el próximo arranque. Útil cuando los contextos del archivo se han corrompido.
