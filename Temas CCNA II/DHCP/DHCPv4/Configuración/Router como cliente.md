## Cliente CISCO IOS DHCPv4

En ocasiones, los routers Cisco en **oficinas pequeñas** y oficinas domésticas (**SOHO**) y en los sitios de sucursales deben configurarse como **clientes DHCPv4** de manera similar a los equipos cliente. El método específico utilizado depende del ISP. Sin embargo, en su configuración más simple, se utiliza la interfaz Ethernet para conectarse a un cable módem o a un módem DSL.

Para configurar una interfaz Ethernet como cliente DHCP, utilice el ``ip address dhcp`` comando del modo de configuración de interfaz.

> [!example] Ejemplo de oficina pequeña
> ![[Pasted image 20250929110033.png]]

## Configuración por CLI

![[Temas CCNA II/DHCP/DHCPv4/Comandos#Router como cliente (SOHO)|Comandos]]

## Configuración con interfaz

La interfaz Ethernet se usa para conectarse a un **cable o modem DSL**. Para configurar una interfaz Ethernet como cliente DHCP, utilice el **ip address dhcp interface** comando del modo de configuración.

Los routers de los hogares se configuran para recibir información de asignación de dirección IPv4 automáticamente desde el ISP. El tipo de conexión de internet está establecido en **Automatic Configuration - DHCP**. Se utiliza esta selección cuando el router se conecta a un cable módem o DSL y actúa como cliente DHCPv4 y solicita una dirección IPv4 del ISP.

> [!example] Interfaz de un Modem
> ![[Pasted image 20250929110356.png|800|center]]
