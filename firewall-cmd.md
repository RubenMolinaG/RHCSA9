`firewall-cmd --state` &rarr; Ver estado del Firewall.

`firewall-cmd --get-default-zone` &rarr; Muestra la zona predeterminada.

`firewall-cmd --get-active-zones` &rarr; Muestra las zonas activas y sus interfaces.

`firewall-cmd --info-zone=public` &rarr; Muestra información de una zona específica.

`firewall-cmd --set-default-zone=home` &rarr; Cambia la zona predeterminada.

`firewall-cmd --zone=work --add-interface=eth0` &rarr; Añadir una interfaz en una zona.

`firewall-cmd --zone=work --change-interface=eth0` &rarr; Cambia la interfaz de zona. En este ejemplo, dejaría de estar en `public` para estar en `work`.

`firewall-cmd --new-zone=zona-personal --permanent` &rarr; Crear una zona personal.

`firewall-cmd --zone=zona-personal --add-interface=eth1 --permanent` &rarr; Añadir una interfaz a la zona.

`firewall-cmd --zone=public --add-port=8080/tcp --permanent` &rarr; Abre el puerto 8080/tcp de forma permanente.

`firewall-cmd --zone=public --remove-port=8080/tcp --permanent` &rarr; Cierra el puerto 8080/tcp de forma permanente.


