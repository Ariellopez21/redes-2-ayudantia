## Modos de topología

### ad hoc

Conexión entre 2 dispositivos de igual a igual (inalámbricamente) sin AP ni routers.

Puede ser mediante bluetooth o wifi direct.

> [!important] IEEE 802.11 se refiere a esto como un conjunto de servicios básicos independientes (IBSS)

### infraestructura

Cuando los clientes se conectan mediante router inalámbrico o AP.

> [!info] Los AP se conectar por cable a la infraestructura de red, normalmente a través de switches

### anclaje a red

Variante del ad hoc.

Es cuando usas un teléfono o tablet con datos móviles para crear un Personal Access Point.

## BSS, ESS, y BSA

### BSA

Un área de cobertura básico es un circulo alrededor del AP o router inalámbrico que limita su conectividad.
### BSS

Conjunto de servicios básicos.

Sí un cliente está dentro de un BSA específico y se mueve a otro área ya no puede comunicarse directamente con otros clientes de la antigua BSA (imaginemos que este área es relativamente grande así que "mudarse" puede significar irse de tu hogar a un mall o algo que represente una larga distancia recorrida).

### ESS

Permite conectar (por cableado) varios BSS a través de un sistema de distribución (DS).

Un ESS es la unión de dos o más BSS interconectados por un DS cableado.

Ahora sí es posible mudarse de un BSA a otro sin perder conectividad con los otros clientes del BSA antiguo.

El ESS se denomina: área extendida de servicios y aparece como un rectángulo que engloba todos los círculos que proporcionan el área de conectividad que existen dentro de la red que se formó.

> [!NOTE] ESS
> ![[Pasted image 20251104072659.png]]

