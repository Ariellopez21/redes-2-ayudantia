## Qué es

Solo requiere de una interfaz física para poder enrutar varias VLANs.

Se tiene un router con una interfaz, por ejemplo, G0/0/0, dicha interfaz se configura como un `trunk` usando la **encapsulación 802.1Q** y se conecta a un puerto `trunk` de un switch de capa 2.

Luego, tendremos múltiples subinterfaces pertenecientes a G0/0/0 las cuales podemos enumerar a gusto como $$G0/0/0.X \rightarrow X \in \mathbb{N}$$
Está claro que la utilidad presente en este método de inter-VLAN routing es que se puede asignar un número $X$ correspondiente a la VLAN que se necesita.

## Cómo funciona

> [!NOTE] Cómo funciona router-on-a-stick (1)
> ![[Excalidraw/Módulo 4.md#^frame=QJw1Rv-QFCPiRTQL7OYaO|800|center]]
> - Los paquetes se envían con normalidad hacia la interfaz G0/0/0 con un enlace `trunk` buscando su gateway.
> - Cada paquete es enviado desde su subred correspondiente, digamos desde la VLAN 10 siendo 192.168.10.0/24, y así con los demás.
> - Llegan al router y este les avisa que su gateway se encuentra dentro de la subinterfaz de G0/0/0.


> [!NOTE] Cómo funciona router-on-a-stick (2)
> ![[Excalidraw/Módulo 4.md#^frame=EpWGyukB52SCw9oa1Bc0F|800|center]]
> - Los paquetes encuentran su destino puesto que cada subinterfaz de G0/0/0 posee la ip que necesitan así que pasan por dicha interfaz virtual.


> [!NOTE] Cómo funciona router-on-a-stick (3)
> ![[Excalidraw/Módulo 4.md#^frame=4UmGTGPsJ7iZw1mqX_2eQ|800|center]]
> - Los paquetes se devuelven por el mismo enlace en el que llegaron pero internamente cambiaron de subred.
> - Es decir, el ejemplo que dimos en el paso (1) sobre el paquete que fue enviado desde la VLAN 10 perteneciente a la subred 192.168.10.0/24, supongamos que debía enviar su paquete hacía la VLAN 30, por lo que, ahora mismo dicho paquete se encuentra dentro de la subred 192.168.30.0/24 para llegar a la VLAN 30.


## Configuración

### Switch

La misma serie de pasos que hemos aprendido de manera general

**Paso 1**. Crear y nombrar las VLANs.

**Paso 2**. Crear la interfaz de administración (VLAN 99)

**Paso 3**. Configurar puertos de acceso.

**Paso 4**. Configurar puertos de enlace troncal.

### Router

Esta es una nueva serie de pasos agregada a la configuración común

**Paso 1**. Crear subinterfaces de la interfaz que se usa como troncal

**Paso 2**. Asignar ip y encapsular con el protocolo `dot1q`

**Paso 3**. Configurar `no shut` en la interfaz troncal.

## Red de ejemplo

> [!NOTE] Red de ejemplo para configurar router-on-a-stick
> ![[Pasted image 20250831021153.png||800|center]]

En los PC:

- Se asignan sus ip y gateway correspondientes a cada subred de acuerdo a la VLAN.

En el switch S1:

- Creamos las VLAN 10, 20 y 99
- El puerto f0/6 le asignamos `mode access` y le permitimos el paso de la VLAN 10
- El puerto f0/1 y f0/5 le asignamos `mode trunk`
- Ingresamos a la interfaz `int vlan 99` y le asignamos la ip `192.168.99.2` con máscara `255.255.255.0`
- En el modo `config` asignamos como `default-gateway` la ip `192.168.99.1`

> [!important] Pro Tip
> Puedes hacer uso del siguiente comando `# int range f0/1-5` para configurar ambos puertos al mismo tiempo.

En el switch S2, repetimos la mayoría de pasos pero con el siguiente detalle:

- Ingresamos a la interfaz `int vlan 99` y le asignamos la ip `192.168.99.3` con máscara `255.255.255.0`

En el router R1:

- Ingresamos a la subinterfaz ``G0/0/0.10``, ``G0/0/0.20`` y ``G0/0/0.99``
- En cada una de ellas permitimos el paso de la VLAN correspondiente usando `# encapsulation dot1q [id]`, por ejemplo, en la subinterfaz `G0/0/0.10` debemos usar `# encapsulation dot1q 10`
- Asignamos ip a cada subinterfaz, por ejemplo, `ip add 192.168.99.1 255.255.255.0`
- Luego de configurar todas las subinterfaces, vamos a la interfaz `# int G0/0/0` y la activamos con `# no shut`
