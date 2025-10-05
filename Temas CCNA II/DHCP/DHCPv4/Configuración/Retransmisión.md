Generalmente, los clientes de red no se encuentran en la misma subred que esos servidores.

> [!NOTE] Red de ejemplo para retransmisión
> ![[Pasted image 20250929105633.png|800|center]]
> La PC1 intenta adquirir una dirección IPv4 de un servidor de DHCPv4 mediante un mensaje de difusión. 
> En esta situación, el router R1 no está configurado como servidor de DHCPv4 y no reenvía el mensaje de difusión. 
> Dado que el servidor de DHCPv4 está ubicado en una red diferente, la PC1 no puede recibir una dirección IP mediante DHCP. 
> R1 debe configurarse para retransmitir mensajes DHCPv4 al servidor DHCPv4.

![[Temas CCNA II/DHCP/DHCPv4/Comandos#Retransmisión DHCP]]
