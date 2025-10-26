### Técnicas de mitigación en el Switch

- Tipos:
	- Seguridad de puertos
	- DHCP snooping
	- Inspección ARP dinámica (DAI)
	- Protección de IP de origen (IPSG)
- Estas soluciones de Capa 2 no serán efectivas si los protocolos de administración no son seguros.
- protocolos administrativos Syslog, Protocolo Simple de Administración de Red (SNMP), Protocolo Trivial de Transferencia de Archivos (TFTP), Telnet, Protocolo de Transferencia de Archivos (FTP) y un largo etcetera... Todos estos, no son seguros.
- se recomiendan las siguientes estrategias:
	- Utilice siempre variantes seguras de protocolos de administración como SSH, Protocolo de Copia Segura (SCP), FTP Seguro (SFTP) y Seguridad de capa de sockets seguros / capa de transporte (SSL / TLS).
	- Considere usar una red de administración fuera de banda para administrar dispositivos.
	- Usar una VLAN de administración dedicada que solo aloje el tráfico de administración.
	- Use ACL para filtrar el acceso no deseado.

## Mitigación de ataques LAN

> Acá debe ir todo el contenido de **Mitigación Ataques**
