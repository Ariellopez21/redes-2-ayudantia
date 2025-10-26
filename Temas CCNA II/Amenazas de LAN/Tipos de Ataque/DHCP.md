## Ataques DHCP

#### Recapitulación DHCP

Tenemos servidores que van a proveer dinámicamente direccionamiento IPv4 (o IPv6).

Esto incluye:
- IP address
- subnet mask
- default gateway
- DNS server
- etc...

Mensajes DHCP son representados con las siglas DORA:

- Discover
- Offer
- Request
- Acknowledge

Tenemos 2 tipos de ataque DHCP:

- DHCP Starvation Attack
- DHCP Spoofing Attack

### Ataque de inanición de DHCP

El objetivo del actor de amenaza es crear una denegación de servicios para los clientes que desean conectarse y recibir su direccionamiento.

El actor de amenaza va a recibir todas las direcciones utilizables que el servidor DHCP provee.

### Ataque de suplantación de DHCP

Imagina que hay un actor de amenaza poniendo su propio servidor DHCP en la red y cuando los clientes usan el proceso DORA, tenemos que, en el primer paso Discover, los hosts envían un broadcast a todos los servidores DHCP, y si el servidor del actor de amenaza es el primero en responder y concreta el proceso completo DORA, entonces entregará información incorrecta al host (IP address, gateway, DNS, etc...).

Lo que ocurrirá es que los hosts que sean clientes del actor de amenaza no se podrán comunicar en la red.

Para prevenir esto, debemos usar salvaguardas e implementaciones de seguridad.

> [!info] [[Temas CCNA II/Seguridad LAN/Mitigación Ataques/DHCP|Mitigación DHCP]]
