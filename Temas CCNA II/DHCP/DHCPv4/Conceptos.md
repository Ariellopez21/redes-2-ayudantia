## Cliente - Servidor

Dynamic Host Configuration Protocol v4 (DHCPv4) **asigna direcciones IPv4** y otra información de configuración de red dinámicamente. Un **servidor de DHCPv4 dedicado** es escalable y relativamente fácil de administrar.

El servidor DHCPv4 asigna dinámicamente, o arrienda, una **dirección IPv4 de un conjunto de direcciones** durante un período limitado elegido por el servidor o hasta que el cliente ya no necesite la dirección.

> [!NOTE] Sobre SOHO
> En una **sucursal pequeña** o ubicación **SOHO**, se puede configurar un **router** Cisco para proporcionar servicios **DHCPv4** sin necesidad de un **servidor dedicado**.

El arrendamiento típicamente dura de 24 horas a una semana o más. Cuando **caduca el arrendamiento**, el cliente debe **solicitar otra dirección**, aunque generalmente se le vuelve a asignar la misma.

> [!NOTE] Flujo de información
> ![[Pasted image 20250929084715.png|center|600]]
> 1. El proceso de concesión DHCPv4 comienza con el cliente enviando un mensaje solicitando los servicios de un servidor DHCP.
> 2. Si hay un servidor DHCPv4 que recibe el mensaje, responderá con una dirección IPv4 y otra información de configuración de red posible.
> - El servidor DHCPv4 dedicado, puede ser también un router.

## Contrato de arrendamiento

Cuando el cliente arranca (o quiere unirse a una red), comienza un proceso de cuatro pasos para obtener un arrendamiento.

Esta es una serie de 4 pasos, como se observa a continuación:

> [!NOTE] Flujo de información detallado del contrato
> ![[Pasted image 20250929085118.png|700|center]]

### DHCPDISCOVER

El cliente, sin IP, envía un mensaje de difusión (broadcast) con su MAC para buscar servidores DHCP disponibles.

### DHCPOFFER

El servidor propone una **dirección IPv4 disponible** para el cliente junto con **otros datos** de configuración, como la máscara de subred, la puerta de enlace predeterminada y servidores DNS. Además, **el servidor “reserva” esa IP temporalmente** para ese cliente, evitando que otro dispositivo la use.

### DHCPREQUEST

El cliente recibe las ofertas de los servidores, pero solo elige una. Para aceptar, envía un **DHCPREQUEST** en forma de difusión. De esta manera confirma al servidor seleccionado que quiere usar la dirección ofrecida y, al mismo tiempo, rechaza las demás ofertas que pudo haber recibido.

#### Renovación

Este mismo mensaje también se utiliza más adelante cuando el cliente necesita **renovar su dirección**.

### DHCPACK

El servidor que fue aceptado recibe el **DHCPREQUEST** y confirma la asignación enviando un **DHCPACK**. Este mensaje contiene la configuración final (la misma que en el DHCPOFFER, pero confirmada). 

Antes de entregarla, el servidor revisa que la IP no esté en uso.

## Renovar un contrato de arrendamiento

Antes de la expiración de la concesión, el cliente inicia un proceso de dos pasos para renovar la concesión con el servidor DHCPv4, como se muestra en la figura:

> [!NOTE] Flujo de información para renovación
> ![[Pasted image 20250929085802.png|800|center]]

### Detección DHCP (DHCPREQUEST)

Antes de que caduque el arrendamiento, el cliente envía un mensaje **DHCPREQUEST** directamente al **servidor de DHCPv4 que ofreció la dirección IPv4 en primera instancia**. Si no se recibe un mensaje DHCPACK dentro de una cantidad de tiempo especificada, el cliente transmite otro mensaje **DHCPREQUEST** de modo que uno de los **otros servidores de DHCPv4** pueda extender el arrendamiento.

### Ofrecimiento de DHCP (DHCPACK)

Al recibir el mensaje **DHCPREQUEST**, el servidor **verifica la información** del arrendamiento al devolver un **DHCPACK**.
