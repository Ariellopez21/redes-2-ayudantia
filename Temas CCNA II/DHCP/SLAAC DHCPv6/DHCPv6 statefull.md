Esta opción es la más **similar a DHCPv4**. En este caso, el **mensaje RA** indica al cliente que obtenga **toda la información** de direccionamiento de un **servidor DHCPv6 stateful**, *excepto la dirección del default gateway* que es la dirección link-local IPv6 de origen de la RA.

Esto se conoce como DHCPv6 stateful, debido a que el **servidor de DHCPv6 mantiene información de estado de IPv6**. Esto es similar a la asignación de direcciones para IPv4 por parte de un servidor de DHCPv4.

> [!NOTE] Flujo de anuncio (RA) y respuesta
> ![[Pasted image 20250930105843.png|800|center]]
> 1. PC1 recibe un **mensaje RA DHCPv6** con el flag O establecido en 0 y el **flag M establecido en 1, lo que indica a PC1 que recibirá toda su información de direccionamiento IPv6 de un servidor DHCPv6 stateful.**
> 2. PC1 envía un mensaje **DHCPv6 SOLIT** buscando un servidor DHCPv6 stateful.


La tabla se ve así:

| Flag | Value |
| ---- | ----- |
| A    | 0     |
| O    | 0     |
| M    | 1     |

Ingresar el siguiente comando para activarlo:

![[Temas CCNA II/DHCP/SLAAC DHCPv6/Comandos#Router como DHCP statefull|Comandos]]

¿Por qué dos comandos? Porque el **segundo comando** ingresado determina `A = 0`, de no hacerse, algunos sistemas operativos como Windows crearán una **dirección IPv6** mediante **SLAAC** y obtendrán una **dirección diferente** del **servidor DHCPv6** stateful.

