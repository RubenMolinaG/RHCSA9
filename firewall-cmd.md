## Firewall-cmd

`firewall-cmd --state` &rarr; Ver estado del Firewall.

`firewall-cmd --get-default-zone` &rarr; Muestra la zona predeterminada.

`firewall-cmd --get-active-zones` &rarr; Muestra las zonas activas y sus interfaces.

`firewall-cmd --info-zone=public` &rarr; Muestra información de una zona específica.

---

`firewall-cmd --set-default-zone=home` &rarr; Cambia la zona predeterminada.

`firewall-cmd --zone=work --add-interface=eth0` &rarr; Añadir una interfaz en una zona.

`firewall-cmd --zone=work --change-interface=eth0` &rarr; Cambia la interfaz de zona. En este ejemplo, dejaría de estar en `public` para estar en `work`.

`firewall-cmd --new-zone=zona-personal --permanent` &rarr; Crear una zona personal.

`firewall-cmd --zone=zona-personal --add-interface=eth1 --permanent` &rarr; Añadir una interfaz a la zona.

---

`firewall-cmd --zone=public --add-port=8080/tcp --permanent` &rarr; Abre el puerto 8080/tcp de forma permanente.

`firewall-cmd --zone=public --remove-port=8080/tcp --permanent` &rarr; Cierra el puerto 8080/tcp de forma permanente.

`firewall-cmd --zone=public --add-service=http --permanent` &rarr; Habilita el servicio http de forma permanente.

`firewall-cmd --zone=public --remove-service=http --permanent` &rarr; Deshabilita el servicio http.

---

`firewall-cmd --zone=public --add-source=192.168.1.100 --permanent` &rarr; Permite todo el tráfico desde la IP `192.168.1.100` de forma permanente.

`firewall-cmd --zone=public --add-rich-rule='rule family="ipv4" source address="192.168.1.100" port port=22 protocol=tcp accept' --permanent` &rarr; Crea una *rich rule* que permite el acceso al puerto `22/tcp` desde la IP `192.168.1.100` de forma permanente.

`firewall-cmd --zone=public --add-forward-port=port=80:proto=tcp:toport=8080 --permanent` &rarr; Redirige el tráfico del puerto `80/tcp` al puerto `8080/tcp` de la zona `public`.

---

`firewall-cmd --zone=public --add-icmp-block=echo-request` &rarr; Bloque las solicitudes de ping entrantes.

`firewall-cmd --zone=public --remove-icmp-block=echo-request` &rarr; Permite las solicitudes de ping entrantes.

---

`firewall-cmd --reload` &rarr; Recarga la configuración del firewall para aplicar los cambios permanentes.

`firewall-cmd --check-config` &rarr; Verifica la configuración del firewall sin aplicar los cambios.

---

`firewall-cmd --panic-on` &rarr; Bloquea todo el tráfico entrante y saliente en todas las zonas.

`firewall-cmd --panic-off` &rarr; Desbloquea el tráfico después de haber activado el modo pánico.

