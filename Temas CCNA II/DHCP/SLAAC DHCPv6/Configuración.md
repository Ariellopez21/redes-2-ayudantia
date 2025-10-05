Un router puede ser:

- **Servidor DHCPv6** - El router proporciona servicios DHCPv6 [[#Router Servidor DHCPv6 stateless|stateless]] o [[#Router Servidor DHCPv6 statefull|statefull]].
- **Cliente DHCPv6** - la interfaz del router adquiere una configuración IP IPv6 de un servidor DHCPv6 ( [[#Router Cliente DHCPv6 stateless|stateless]] o [[#Router Cliente DHCPv6 statefull|statefull]] ).
- [[#Agente de retransmisión]] - Router proporciona servicios de reenvío DHCPv6 cuando el cliente y el servidor se encuentran en diferentes redes.

## Router: Servidor DHCPv6 stateless

> [!info] SLAAC + DHCPv6 stateless
> Con un **servidor DHCPv6 stateless** se requiere que el **router anuncie la información** de direccionamiento de red IPv6 en los **mensajes RA**. Sin embargo, el **cliente** debe ponerse en **contacto con un servidor DHCPv6** para obtener **más información**.

> [!example] Ejemplo 1
> ![[Pasted image 20250930123645.png|800|center]]

### Serie de pasos

#### Paso 1

Permitir routing para pertenecer al grupo de difusión `ff02::2`

```bash
R1(config)# ipv6 unicast-routing
```

#### Paso 2

Crear pool

```bash
R1(config)# ipv6 dhcp pool IPV6-STATELESS 
R1(config-dhcpv6)#
```

#### Paso 3

Configuraciones adicionales

```bash
R1(config-dhcpv6)# dns-server 2001:db8:acad:1::254 
R1(config-dhcpv6)# domain-name example.com 
```

#### Paso 4

Linkear la pool a una interfaz de salida.

¿Qué significa esto? Como el **servidor DHCPv6 stateless** es el mismo **router**, se consulta la información que se rellenó en el paso 3 a través de este linkeo.

Ej:

```bash
R1(config)# interface GigabitEthernet0/0/1 
R1(config-if)# ipv6 address fe80::1 link-local 
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64 
R1(config-if)# ipv6 nd other-config-flag 
R1(config-if)# ipv6 dhcp server IPV6-STATELESS
R1(config-if)# no shut
```

> [!warning] Sin embargo, si el servidor DHCPv6 stateless está en un servidor distinto del router, entonces, la pool tiene que tener el redireccionamiento a dicho servidor para consultar por la información allí.

## Router: Cliente DHCPv6 stateless


> [!example] Ejemplo 2
> ![[Pasted image 20250930150603.png|800|center]]

Un **router también puede ser un cliente DHCPv6** y obtener una configuración IPv6 de un servidor DHCPv6.

### Serie de pasos

#### Paso 1

Permitir routing para pertenecer al grupo de difusión `ff02::2`

```bash
R1(config)# ipv6 unicast-routing
```

#### Paso 2

Configure el router para crear una LLA: 

Podemos hacerlo como generalmente lo hacemos en todas las interfaces.

> [!example] Ejemplo
> ```
> R1(config)# interface GigabitEthernet0/0/1 
> R1(config-if)# ipv6 address fe80::1 link-local 
> ```

También, en este caso, es más sencillo únicamente habilitar el protocolo IPv6 a través de `ipv6 enable`, porque así el router crea automáticamente una LLA en la intefaz:

```bash
R1(config)# interface GigabitEthernet0/0/1 
R1(config-if)# ipv6 enable
```

#### Paso 3

Configurar router para **usar SLAAC**.

Recordemos que este router es cliente stateless, por lo que, **generaremos una GUA**.

```bash
R1(config)# interface GigabitEthernet0/0/1 
R1(config-if)# ipv6 address autoconfig
```

Con esto, el router podrá:

1. Escuchar mensajes RA (Router Advertisement) de un router en la red

2. Generar automáticamente una GUA 

#### Paso 4

Ya que el mismo router crea su GUA a través de SLAAC, podemos verificarlo con

```bash
R1# show ipv6 interface brief
```

#### Paso 5

Verificar que el router haya recibido la información del servidor DHCPv6 correctamente a través de:

```bash
R1# show ipv6 dhcp interface [int][int-id]
```

## Router: Servidor DHCPv6 statefull

La serie de pasos es similar a la de DHCPv6 stateless, con la diferencia de que no existe otro dispositivo que utilice SLAAC, o sea, el servidor que crearemos entregará toda la información que el cliente necesite.

> [!important] Excepto el gateway

### Serie de pasos

#### Paso 1

Permitir routing para pertenecer al grupo de difusión `ff02::2`

```bash
R1(config)# ipv6 unicast-routing
```

#### Paso 2

Crear pool

```bash
R1(config)# ipv6 dhcp pool IPV6-STATEFULL 
R1(config-dhcpv6)#
```

#### Paso 3

Entregar todos los datos necesarios para el cliente y configuraciones adicionales

```bash
R1(config-dhcpv6)# address prefix 2001:db8:acad:1::/64
R1(config-dhcpv6)# dns-server 2001:db8:acad:1::254 
R1(config-dhcpv6)# domain-name example.com 
```

#### Paso 4

Linkear la pool a una interfaz de salida.

¿Qué significa esto? Como el **servidor DHCPv6 stateless** es el mismo **router**, se consulta la información que se rellenó en el paso 3 a través de este linkeo.

Ej:

```bash
R1(config)# interface GigabitEthernet0/0/1 
R1(config-if)# ipv6 address fe80::1 link-local 
R1(config-if)# ipv6 address 2001:db8:acad:1::1/64 
R1(config-if)# ipv6 nd managed-config-flag 
R1(config-if)# ipv6 nd prefix default no-autoconfig
R1(config-if)# ipv6 dhcp server IPV6-STATEFULL
R1(config-if)# no shut
```

> [!success] El servidor DHCPv6 fue configurado con las FLAGS adecuadas para ser statefull y entregar el prefijo, longitud, dns, domain name.

## Router: Cliente DHCPv6 statefull

### Serie de pasos

#### Paso 1

Permitir routing para pertenecer al grupo de difusión `ff02::2`

```bash
R1(config)# ipv6 unicast-routing
```

#### Paso 2

Configure el router para crear una LLA: 

Podemos hacerlo como generalmente lo hacemos en todas las interfaces.

> [!example] Ejemplo
> ```
> R1(config)# interface GigabitEthernet0/0/1 
> R1(config-if)# ipv6 address fe80::1 link-local 
> ```

También, en este caso, es más sencillo únicamente habilitar el protocolo IPv6 a través de `ipv6 enable`, porque así el router crea automáticamente una LLA en la intefaz:

```bash
R1(config)# interface GigabitEthernet0/0/1 
R1(config-if)# ipv6 enable
```

#### Paso 3

Configurar router para **solicitar información a un servidor DHCPv6**.

Recordemos que este router es cliente de un statefull, por lo que, **obtendremos una GUA**

```bash
R1(config)# interface GigabitEthernet0/0/1 
R1(config-if)# ipv6 address dhcp
```

Con esto, el router podrá:

1. Escuchar mensajes RA (Router Advertisement) de un router en la red

2. Obtener toda su información desde el servidor statefull. 

#### Paso 4

Verificamos la GUA generada:

```bash
R1# show ipv6 interface brief
```

#### Paso 5

Verificar que el router haya recibido la información del servidor DHCPv6 correctamente a través de:

```bash
R1# show ipv6 dhcp interface [int][int-id]
```

## Comandos de verificación del servidor

- `show ipv6 dhcp pool`: Enseña los pool creados en el router.
- `show ipv6 dhcp binding`: mostrar la dirección link-local IPv6 del cliente y la GUA asignada por el servidor.

## Agente de retransmisión

Igual al [[Retransmisión|agente de retransmisión]] de DHCPv4.

![[Temas CCNA II/DHCP/SLAAC DHCPv6/Comandos#Retransmisión DHCP|Comandos]]

