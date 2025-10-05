En **DHCPv6 stateless**, el **router** le da al host, mediante los mensajes RA, todo lo necesario para que **genere su propia dirección IPv6 (GUA)** a través de SLAAC.
Sin embargo, los RA también le avisan al host que puede pedir **información adicional** a un servidor DHCPv6 (por ejemplo, DNS, nombre de dominio, NTP, etc.).

Ese servidor se llama **stateless** porque **no guarda registro de las direcciones** de los hosts, ya que no las asigna. Solo entrega parámetros extra cuando se le consulta.


> [!NOTE] Flujo de anuncio (RA) y respuesta
> ![[Pasted image 20250930105541.png|800|center]]
> 1. PC1 recibe un mensaje de **RA DHCP stateless**. El mensaje RA contiene el prefijo de red y la longitud del prefijo. El flag M para DHCP stateful se establece en el valor predeterminado 0. El flag A=1 indica al cliente que use SLAAC. **El flag O=1 flag se utiliza para informarle al cliente que hay información de configuración adicional disponible de un servidor de DHCPv6 stateless**.
> 2. El cliente envía un mensaje **DHCPv6 SOLIT** buscando un servidor DHCPv6 stateless para obtener información adicional (por ejemplo, direcciones de servidor DNS).


La tabla se ve así:

| Flag | Value |
| ---- | ----- |
| A    | 1     |
| O    | 1     |
| M    | 0     |

Ingresar el siguiente comando para activar SLAAC + DHCPv6 Stateless:

![[Temas CCNA II/DHCP/SLAAC DHCPv6/Comandos#Router como DHCP stateless|Comandos]]

