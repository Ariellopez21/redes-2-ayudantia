# Parte 1

Configurar la siguiente subred con HSRP para que existe redundancia en la red.

> [!success] Topología de la tarea
> ![[Excalidraw/Módulo 9.excalidraw.md#^frame=JuIIdsM5U6L4n_-rygRMr|center|1800]]

Detalles a tomar en consideración:

- Cuando se habla de *Configurar las int de ambos routers en esta subred* se refiere a las interfaces de cada router que conectan directamente con la subred, en el caso de la subred 192.168.10.0/24 vendrían siendo ambas interfaces `g0/0`, y para la otra subred `g0/1`.
	
- El PC1 y el SV deben configurarse con la gateway del router virtual.
	
- Cada router virtual tendrá su grupo correspondiente (10 y 11).

- Los comandos de configuración puedes hallarlos haciendo [[Temas CCNA II/FHRP/Comandos|clic aquí]].

# Parte 2

Esta es una preparación para la tarea final que contendrá todo lo visto.

En base a la [[#Parte 1]] modificaremos la subred 192.168.11.0/24, para que hallan 3 hosts extras y que el **servidor será un DHCPv4**.

Adicionalmente, en la **subred inferior** (192.168.10.0/24), vamos a configurar los routers para que funcionen como **agentes retransmisores** para entregarle a PC1 una **configuración del servidor DHCPv4** que se encuentra en la red superior (192.168.11.0/24).

> [!important] ¡Importante!
> Ambas partes corresponden a una única entrega.
