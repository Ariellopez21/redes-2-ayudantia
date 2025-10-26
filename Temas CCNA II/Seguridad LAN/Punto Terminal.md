## Seguridad de punto terminal

### Ataques de Red Actuales

- **Negación de Servicio Distribuido (DDoS)**
- **Filtración de Datos**
- **Malware**

### Dispositivos de Seguridad de Red

- Router habilitado con VPN
- NGFWW
- NAC

### Protección de terminales

- Los dispositivos LAN como los switches, los Controladores de LAN Inalámbricos (WLCs), y otros puntos de acceso (AP) interconectan puntos terminales.
- Muchos ataques se originan dentro de la red.
- Los puntos terminales son hosts que generalmente consisten en computadoras portátiles, computadoras de escritorio, servidores y teléfonos IP, así como dispositivos propiedad de los empleados (BYOD).
- Cómo protegerlos:
	- Antivirus/antimalware, firewalls basados en host y sistemas de prevención de intrusiones (HIPS) basados en host.
- Mayor seguridad:
	- Combinación de NAC, software AMP basado en host, un Dispositivo de Seguridad de Correo Electrónico (ESA) y un Dispositivo de Seguridad Web (WSA).

### Dispositivo de Seguridad de Correo Electrónico Cisco (ESA)

- ataque de phishing
- Spear phishing
- El dispositivo Cisco ESA está diseñado para monitorear el Protocolo Simple de Transferencia de Correo (SMTP).
- Cisco Talos, quien detecta y correlaciona las amenazas con un sistema de monitoreo que utiliza una base de datos mundial.
- Cisco ESA extrae estos datos de inteligencia de amenazas cada tres o cinco minutos.
- Funciones de Cisco ESA:
	- Bloquear las amenazas
	- Remediar contra el malware invisible que evade la detección inicial
	- Descartar correos con enlaces malos (como se muestra en la figura).
	- Bloquear el acceso a sitios recién infectados
	- Encriptar el contenido de los correos salientes para prevenir perdida de datos.

### Dispositivo de Seguridad de la Red de Cisco (WSA)

- Mitigación para amenazas basadas en la web.
- Protección avanzada contra malware, visibilidad y control de aplicaciones, controles de políticas de uso aceptable e informes.
- Cisco WSA proporciona un control completo sobre cómo los usuarios acceden a Internet.
- Funciones y aplicaciones, como chat, mensajería, video y audio, pueden permitirse, restringirse con límites de tiempo y ancho de banda, o bloquearse, de acuerdo con los requisitos de la organización.
- La WSA puede realizar listas negras de URL, filtrado de URL, escaneo de malware, categorización de URL, filtrado de aplicaciones web y cifrado y descifrado del tráfico web.