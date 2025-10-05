> [!NOTE] Sobre puertos UDP
> Los mensajes **DHCPv6 de servidor a cliente** utilizan el puerto de destino **UDP 546**, mientras que los mensajes **DHCPv6 de cliente a servidor** utilizan el puerto de destino UDP **547**.

## Funcionamiento

### Proceso de solicitud

Los pasos 1 y 2 comprender que el host está buscando generar una IPv6 GUA, por lo que, envía un **RS** a todos los **routers habilitados** y ellos con un **RA** responden **indicando** dónde está el **servidor DHCPv6**.

> [!NOTE] El servidor puede ser el mismo router que está respondiendo, pero sí el servidor se encuentra en otro lado, al host le sirve para saber dónde dirigirse.

A continuación, ambos pasos:

#### Paso 1

El host envía un mensaje RS a todos los routers habilitados con IPv6.

#### Paso 2

Los routers reciben el RS y responden con un RA indicando que el cliente debe iniciar la comunicación con un servidor DHCPv6.

### Proceso de asignación

Sí comprendió el [[Temas CCNA II/DHCP/DHCPv4/Conceptos#Contrato de arrendamiento|Funcionamiento de DHCPv4]], estos cuatro pasos funcionan de la misma forma, con la diferencia de que a partir del Paso 1 y Paso, en el Paso 5, el cliente ya sabe si es stateless o statefull, debido a que el mismo router en el Paso 2 le indica sí debe rellenar su GUA con SLAAC o no.

A continuación, la serie de pasos:

#### Paso 3: SOLIT

El cliente, ahora un **cliente DHCPv6**, necesita **localizar** un **servidor DHCPv6** y envía un mensaje **DHCPv6 SOLICIT** a la dirección reservada de todos los servidores DHCPv6 de **multidifusión** IPv6 de `ff02::1:2`. 

Esta dirección de multidifusión tiene alcance link-local, lo cual significa que los routers no reenvían los mensajes a otras redes.

#### Paso 4: ADVERTISE

Los **servidores** DHCPv6 **responden** con un mensaje **unidifusión** DHCPv6 ADVERTISE El mensaje **ADVERTISE** le informa al cliente DHCPv6 que el **servidor** se encuentra **disponible** para el servicio DHCPv6.

#### Paso 5: REQUEST | INFO-REQUEST

La respuesta varía sí el cliente es Stateless o Statefull:

- **Cliente DHCPv6 Stateless** - El cliente crea una dirección IPv6 utilizando el prefijo en el mensaje RA y una ID de interfaz autogenerada. El cliente envía un mensaje DHCPv6 **INFORMATION-REQUEST** al servidor de DHCPv6 en el que solicita solamente parámetros de configuración, como la dirección del servidor DNS.

- **Cliente DHCPv6 Stateful** - el cliente envía un mensaje **DHCPv6 REQUEST** al servidor para obtener una dirección IPv6 y todos los demás parámetros de configuración del servidor.

#### Paso 6: REPLY

El **servidor** envía un mensaje de **unidifusión** **DHCPv6 REPLY** al cliente. El contenido del mensaje varía en función de si responde a un mensaje REQUEST o INFORMATION-REQUEST

> [!NOTE] Sobre REPLY
> La info que contiene REQUEST o INFORMATION-REQUEST depende de:
> - REQUEST: Esto es **statefull**, entonces, se solicita **todo**.
> - INFORMATION-REQUEST: Esto es **stateless**, se solicita información **adicional**.

> [!important] Importante
> El **cliente** usara la direccion IPv6 link-local de origen del RA como su dirección **default gateway**. Un **servidor DHCPv6 no proporciona esta información**.

> [!NOTE] Ilustración del flujo de mensajes
> ![[Pasted image 20250930104711.png|800|center]]


## DHCPv6 stateless

![[DHCPv6 stateless]]

## DHCPv6 statefull

![[DHCPv6 statefull]]

## Servidor DHCPv6

![[Temas CCNA II/DHCP/SLAAC DHCPv6/Configuración|Configuración]]