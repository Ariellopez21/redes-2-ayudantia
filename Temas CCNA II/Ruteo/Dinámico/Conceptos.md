## Conceptos de routing dinámico

Objetivos:

- Detectar redes remotas
- Mantener la información del router actualizada
- Elegir siempre la mejor ruta hacia las redes de destino
- Encontrar caminos alternativos si la ruta actual falla

Componentes principales:

- **Estructuras de datos**: Usan tablas o bases de datos que generalmente se guarda en RAM.
- **Mensajes de protocolo de routing**: Para descubrir vecinos, intercambiar información de ruteo, descubrir redes, entre otros.
- **Algoritmo**: Como los mencionados con anterioridad. (Vector distancia, Estado de enlace, y Vector ruta).

## Elección del mejor camino

Un protocolo de enrutamiento **compara varias rutas** a la misma red y elige la de **métrica más baja** (más “barata”). _Métrica_ = número que representa “qué tan costoso” es usar esa ruta. Cada protocolo calcula su métrica a su manera.

| Protocolo | Qué mide (métrica)                                                             | Cómo se interpreta                                                                  |
| --------- | ------------------------------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| **RIP**   | **Saltos** (hop count)                                                         | Cada router suma 1. Límite 15. **Menos saltos = mejor**.                            |
| **OSPF**  | **Costo** ≈ 1 / **ancho de banda** del camino (acumulado)                      | Enlaces rápidos → **costo bajo**; lentos → **costo alto**. **Menor costo = mejor**. |
| **EIGRP** | **Compuesto** (por defecto: **ancho de banda mínimo** y **retardo acumulado**) | También puede considerar carga/fiabilidad. **Menor métrica = mejor**.               |

> [!success] Regla de oro: **“Más bajo gana”** (RIP: menos saltos; OSPF: menor costo; EIGRP: menor métrica).

### Cosas que pasan al elegir

- Si **varias rutas empatan** en la mejor métrica, el router puede hacer **balanceo de carga** (**ECMP**) por varias interfaces.
- Para una **misma red**, cada ruta puede salir por **interfaces distintas**.
- La decisión de **qué protocolo** se instala primero si anuncian lo mismo la da la **Distancia Administrativa (AD)**; **luego** se compara la **métrica** dentro del mismo protocolo.

### Mini-ejemplos rápidos

- **RIP:** a 10.10.10.0/24 tengo 2 caminos: 3 saltos vs 4 saltos → **elige 3**.
- **OSPF:** camino A (100 Mb + 100 Mb) vs camino B (1 Gb + 10 Mb). El **costo** del B será mayor por el **enlace lento (10 Mb)**; OSPF **elige A**.
- **EIGRP:** dos caminos con mismo ancho de banda, pero uno tiene **más retardo** (serial larga) → **elige el de menor retardo**.

### Comandos útiles (IOS)

- RIP: `show ip route rip`
- OSPF: `show ip ospf route` / `show ip route ospf`
- EIGRP: `show ip eigrp topology` / `show ip route eigrp`

## Balanceo de cargas

Sí está configurado correctamente, el balanceo de cargas puede aumentar la efectividad y rendimiento de una red.

Los protocolos de ruteo dinámico traen balanceo de carga por defecto.

Consiste en enviar los paquetes por diferentes rutas (sí están en la tabla de ruteo dinámico) hacia el siguiente destino, permitiendo al enlace "descansar" y mejorando el rendimiento de red.

