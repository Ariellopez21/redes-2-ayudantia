Dentro de una **red conmutada**, las VLAN proporcionan la **segmentación** y la **flexibilidad** organizativa.

Un **grupo de dispositivos** dentro de una **VLAN** se comunica como si *cada dispositivo estuviera conectados al mismo cable*. Las VLAN se basan en **conexiones lógicas**, en lugar de conexiones físicas.

Los paquetes de unidifusión, difusión y multidifusión se reenvían **solamente** a terminales del switch dentro de la VLAN donde los paquetes son de origen.

> [!warning] Importancia de las VLAN
> Varias subredes IP pueden existir en una red conmutada, **sin el uso** de varias VLAN.
> Sin embargo, los dispositivos **estarán en el mismo dominio de difusión de capa 2**. Esto significa que todas las difusiones de capa 2, tales como una solicitud de ARP, serán recibidas por todos los dispositivos de la red conmutada, incluso por aquellos que no se quiere que reciban la difusión.

Los paquetes provenientes de una VLAN X solo se reenvían a las interfaces físicas del switch que pertenezcan a la VLAN X. Esto se debe a que una VLAN crea un **dominio de difusión lógico** que puede abarcar varios **segmentos** **LAN físicos**.

Las VLAN **mejoran el rendimiento** de la red mediante la **división de grandes dominios de difusión** en otros más pequeños.

> [!info] Red conmutada
> Significa que funciona con Switches


> [!info] Red de ejemplo con VLANs
> ![[Pasted image 20250821120524.png | 800 | center]]

> [!NOTE] Rangos VLAN
> Las VLAN de rango normal en estos switches se numeran del 1 al 1005, y las VLAN de rango extendido se numeran del 1006 al 4094.
