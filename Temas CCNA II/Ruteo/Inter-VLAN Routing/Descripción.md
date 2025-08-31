Una duda que surge a partir de lo aprendido en el [[Lab 3 - 26-08/Módulo 3|Módulo 3]] es la expuesta en el siguiente esquema:


> [!NOTE] Esquema de topología lógica con VLANs
> ![[Excalidraw/Módulo 4.md#^frame=THwlVmMizgC0ownroHdW8|800|center]]

Se entiende que los PC1, PC3, PC5 y PC7 pertenecen a la VLAN 10 y los PC2, PC4, PC6 y PC8 pertenecen a la VLAN 20, pero, ¿cómo es posible establecer comunicación entre los PCs que pertenecen a las mismas VLANs pero que están en subredes diferentes?

Es decir, piensa que la red de la izquierda fuera la 192.168.0.1/24, la red de la derecha no puede corresponder también a la 192.168.0.1/24 (*por lo menos no con lo que se ve en CCNA 2*), es decir, la red de la derecha deberá ser la 192.168.0.2/24 (por ejemplo...).

**Inter-VLA routing** es el proceso de reenviar el tráfico de red de una VLAN a otra VLAN, no necesariamente se debe pasar por un router, pero sirve en esos casos también, porque el Inter-VLAN routing permite tanto a PC1 comunicarse con PC5 y PC7 (pertenecientes a la VLAN 10 pero en otra subred) como también le permite comunicarse con PC2 o incluso PC8 que pertenecen a una VLAN diferente.

Las opciones que routeo de VLAN que se verán son las siguientes:

- **Inter-VLAN Routing heredado** - Esta es una solución antigua. No escala bien
- **Router-on-a-stick** - Esta es una solución aceptable para una red pequeña y mediana.
- **Switch de capa 3 con interfaces virtuales (SVIs)** : esta es la solución más escalable para organizaciones medianas y grandes.

