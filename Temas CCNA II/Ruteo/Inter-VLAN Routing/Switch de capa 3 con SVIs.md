## Qué es 

El tercer método de ruteo entre VLANs es el que posee más ventajas y solo una desventaja: Es más caro $ $ $. 

> [!NOTE] red con un switch de capa 3 y VLANs
> ![[Pasted image 20250831145928.png|800|center]]

Las mayores ventajas de este método son:

- Mayor velocidad porque utiliza hardware a diferencia de router-on-a-stick que usa software.
- Es un método extremadamente compatible con [[Temas CCNA II/EtherChannel/Descripción|EtherChannel]].
- La latencia es muchísimo menor puesto que los datos no se enrutan pasando entre subredes, simplemente utiliza el mismo switch actuando como capa 2 y capa 3 al mismo tiempo.

> [!important] Un Switch de capa 3 convierte un puerto de switch de capa 2 en una interfaz de capa 3 (es decir, un puerto enrutado). 

## Configuración

Un switch de capa 3 **reduce** varios pasos de configuración que se realizan en ambos métodos anteriormente vistos.

La serie de pasos es la siguiente y se realiza **únicamente en el Switch de capa 3**:

**Paso 1**. Crear las VLAN.

**Paso 2**. Crear las interfaces VLAN SVI.

**Paso 3**. Configurar puertos de acceso.

**Paso 4**. Habilitar IP routing.

## Enrutamiento en un switch de capa 3

Para habilitar el enrutamiento en un switch de capa 3, se debe configurar un puerto enrutado.

Un puerto enrutado se crea en un switch de Capa 3 **deshabilitando la función switchport** de un switch de Capa 2 que está conectado a otro dispositivo de Capa 3.


> [!NOTE] Escenario de enrutamiento en un switch de capa 3
> ![[Pasted image 20250831150911.png|800|center]]

Para que exista ruteo entre la subred de la izquierda y sus respectivas VLANs, y la subred de la derecha donde está el servidor, se necesita deshabilitar el puerto **G0/0/1** del Switch de capa 3 para que deje de ser de capa 2 y pasar a ser un puerto de capa 3.

Seguido de ello activar el `ip routing` del modo de configuración global del Switch porque este, **no solo permite la comunicación entre VLANs, sino que también permite el enrutamiento con dispositivos de capa 3**.

Finalmente, enrutar.

Más detalles en [[Temas CCNA II/Ruteo/Inter-VLAN Routing/Comandos#Rutear entre Switch de capa 3 y otros dispositivos de capa 3|Rutear entre Switch de capa 3 y otros dispositivos de capa 3]].
