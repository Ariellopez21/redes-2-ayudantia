
Como tal, STP no posee comandos variados de configuración.

Nos interesan los siguientes, relacionados a cambios en su modo de empleo y los `show` necesarios para saber lo que está ocurriendo.

## Configuración Global

### Modos

Cambia el algoritmo de STP según el elegido, packet tracer posee algunos como: pvst y rapid-pvst.

```bash
 S1(config)#spanning-tree mode [mode]
 ```

### PortFast

La configuración de portfast viene dada por

```bash
 S1(config)#spanning-tree portfast [bpduguard | default]
 ```

### VLAN

Puedes acceder a configurar cada STP por vlan. Recuerda que, esto se debe a que está configurado como pvst y por defecto solo está activa la vlan 1, sin embargo, se puede configurar stp para varias vlans.

```bash
 S1(config)#spanning-tree vlan 1 [priority | root]
 ```

#### Prioridad

Se puede configurar la prioridad del switch en el spanning tree a través de:

```bash
 S1(config)#spanning-tree vlan 1 priority [number]
 ```

#### Root Bridge

Se puede configurar como root primary o secundary a través de:

```bash
 S1(config)#spanning-tree vlan 1 root [primary | secundary]
 ```

## Interfaces

El mismo tipo de configuración general se puede utilizar a través de una interfaz para configurar el **costo**, **tipo de enlace**, a qué **vlan** pertenece, **portfast** y **bpduguard**, todo a través de:

 ```bash
 Switch(config-if)# spanning-tree [many-options-config]
 ```

Ej:

 ```bash
 Switch(config-if)# spanning-tree vlan 1 cost 19
 ```
