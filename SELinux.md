## SELinux

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

### Modos de SELinux:

- **Enforcing**: SELinux aplica estrictamente las políticas de seguridad, bloqueando cualquier acción que no esté permitida en las mismas.

- **Permissive**: SELinux NO bloquea acciones, pero registra todas las violaciones de políticas en los logs. Útil para el diagnóstico de problemas.

- **Disabled**: SELinux está completamente deshabilitado y no aplica ni registra ninguna política de seguridad.

---

```bash
ls -Z /path/to/file	# Muestra el contexto de SELinux de un archivo.
ps -eZ | grep proc-name	# Muestra el contexto de SELinux de un proceso.
```

`chcon -t httpd_sys_content_t /var/www/html/index.html` &rarr; Cambia el tipo de contexto del fichero *index.html* a *httpd_sys_content_t*, que es adecuado para archivos servidor por un servidor web.

`restorecon -v /var/www/html/index.html` &rarr; Restaura el contexto SELinux por defecto de un archivo o directorio basado en las políticas del sistema.

---

`semodule -l` &rarr; Lista todos los módulos de políticas de SELinux activos en el sistema.

`semodule -i nueva-politica.pp` &rarr; Instala un nuevo módulo de política de SELinux.

`semodule -r politica-ejemplo` &rarr; Elimina un nodo de política de SELinux.

---

`getsebool -a` &rarr; Lista todos los booleanos de SELinux y su estado actual.

`setsebool httpd_can_network_connect on` &rarr; Activa el booleano *httpd_can_network_connect on* temporalmente.

`setsebool -P httpd_can_network_connect on` &rarr; Activa el booleano *httpd_can_network_connect on* permanentemente.

---

`cat /var/log/audit/audit.log | grep AVC` &rarr; Filtra los registros de SELinux en el log de auditoría para encontrar mensajes de Control de Acceso Voluntario (AVC).
