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
