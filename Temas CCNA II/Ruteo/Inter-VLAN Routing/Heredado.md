Se propone el siguiente esquema:

> [!NOTE] Topología de una red con Inter-VLAN routing
> ![[Pasted image 20250830233903.png|800|center]]

La siguiente red propone asignar más de un gateway dentro del mismo router, es decir, cada puerto ya sea gigabit o fastethernet puede ser un gateway, en este caso, se asignan 2 gateway porque el ejemplo muestra solo 2 VLANs.

> [!warning] Hablamos de gateway como concepto, no se refiere a ejecutar el comando `default-gateway` del switch.

Nótese que al seguir la siguiente serie de pasos tendremos un esquema como lo aprendimos en el [[Lab 3 - 26-08/Módulo 3|Módulo 3]] sobre VLANs:

1. A cada PC asignarle su respectiva ip y su respectivo def-gateway.
2. Ir al router y en cada interfaz gigabit asignar las ip de las subredes correspondientes.
3. Ir al Switch y crear las VLAN 10 y 20, además de asignar como `switchport mode access` a los puertos que van directamente a los PCs.
4. Por último deberíamos asignar como `switchport mode trunk` las interfaces que conectan entre el switch y el router.

> [!info] Se obviaron detalles importantes a lo largo de la serie de pasos anteriores que se asume que el lector ya sabe aplicar.

Con esta serie de 4 pasos, la comunicación entre VLANs no se permite. Sin embargo, esto **no es lo que queremos**, porque *el paso 4 no se aplica*.

Más bien, queremos una pequeña variación, es decir:

4. Por último debemos asignar como `switchport mode access` a las interfaces que conectar entre switch y router, y finalmente ejecutar `switchport access vlan [id]` donde cada vlan que se permite el paso debe ser solamente a la correspondiente a su subred, o sea, en el puerto G0/0/0 solo se debe permitir el acceso de la vlan 10 y en el G0/0/1 la de la vlan 20.

¿Qué permitimos con esto? Un ruteo entre VLANs que dividiría a la red de la forma clásica que ha aprendido a rutear pero sin necesidad de usar `ip route`; La subred se vería como algo así:

> [!NOTE] Topología simulada de la situación expuesta
> ![[Excalidraw/Módulo 4.md#^frame=JfLayTiOBBb6AnVwx5cvr|800|center]]

> [!warning] Desventaja
> La necesidad de utilizar un puerto físico en el router para cada VLAN por si se necesita establecer comunicación.

