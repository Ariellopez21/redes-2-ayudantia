## Recordando conceptos

[[GUA y LLA|¡Has clic aquí para recordar lo que era una LLA y una GUA!]]

## Configuración de host con IPv6

Las direcciones **GUA** se pueden configurar manualmente en routers y hosts, pero es lento y propenso a errores. Por ello, en la práctica, los hosts suelen adquirirlas dinámicamente mediante SLAAC o DHCPv6.

> [!NOTE] Obtener IPv6 address automáticamente
> ![[Pasted image 20250929151616.png|800|center]]

## IPv6 Host Link-Local Address

Al iniciar un host con la opción **Obtain an IPv6 address automatically** seleccionada, este genera automáticamente una **dirección link-local (LLA)**. 

Si no hay un router en la red que envíe mensajes RA, el host no crea una GUA, solo una LLA. En Windows, esta puede aparecer con un “%n” que indica la interfaz asociada.

## IPv6 GUA Assignment

Los routers anuncian información IPv6 mediante **RA ICMPv6**, lo que permite a los hosts obtener su configuración. Esta puede hacerse por métodos **stateless (SLAAC, DHCPv6 stateless)** o **stateful (DHCPv6 stateful)**. La decisión final la toma el host.

> [!NOTE] Sobre DHCPv6
> Todos los métodos stateless y stateful de este módulo utilizan **mensajes de RA ICMPv6** para sugerir al host cómo crear o adquirir su configuración IPv6. Aunque los sistemas operativos del host siguen la sugerencia del RA, la decisión real depende en última instancia del host.

### Formas de asignar GUA

> [!NOTE] Formar en que un Host puede obtener su GUA
> ![[Pasted image 20250929225157.png|800|center]]

A continuación un desglose y reestructuración de la explicación de la imagen anterior:
#### 🔹 Dos enfoques principales

1. **Stateless** → No hay seguimiento centralizado de direcciones.
    - El host se autoconfigura con la info de los RA.
    - Puede que necesite un servidor DHCPv6 solo para datos extra (DNS, etc.).

2. **Stateful** → Un servidor DHCPv6 administra y lleva control de las direcciones asignadas.
    - El host obtiene toda su configuración de este servidor.
#### Modos de operación

##### 1. Solo SLAAC (Stateless puro)

- El **router envía RA** con todo lo necesario: prefijo de red, longitud y gateway.
- El host genera su propia GUA usando esa info.  
    👉 No hay servidor DHCPv6.

##### 2. SLAAC + DHCPv6 Stateless

- Los **RA indican** que el host debe consultar también a un servidor DHCPv6.
- **El host genera su GUA** con la info de RA.
- **Datos extra** (DNS, dominio, etc.) vienen del servidor DHCPv6.  
    👉 Se combina autoconfiguración con configuración adicional.

##### 3. DHCPv6 Stateful

- Los **RA avisan** al host que debe usar un servidor DHCPv6 para todo.
- El host recibe del servidor su **GUA y demás parámetros IPv6**.
- El **gateway predeterminado** siempre se aprende de los RA, no de DHCPv6.  
    👉 Aquí el DHCPv6 funciona parecido al clásico de IPv4.

### Diagrama de Flujo - Mensaje RA


> [!NOTE] Diagrama de Flujo - Mensaje RA para la obtención de la GUA de un Host
> ![[Excalidraw/Módulo 8#^frame=h-WiCFJkDmffIObM-FDC_|center|1800]]

### Tabla resumen

| Método                       | Quién da la dirección GUA | Qué más da                                    |
| ---------------------------- | ------------------------- | --------------------------------------------- |
| **Solo SLAAC**               | Host la crea con RA       | Gateway y prefijo desde RA                    |
| **SLAAC + DHCPv6 Stateless** | Host la crea con RA       | Info extra (DNS, etc.) desde DHCPv6           |
| **DHCPv6 Stateful**          | Servidor DHCPv6           | Toda la info (menos gateway, que viene de RA) |

## Tres flags de mensaje RA

Los mensajes **RA ICMPv6** incluyen tres flags que indican al host cómo obtener su dirección:

- **A (Autoconfig)**: SLAAC para crear un GUA.
- **O (Other)**: información adicional desde un servidor DHCPv6 stateless.
- **M (Managed)**: obtener GUA con un servidor DHCPv6 stateful.