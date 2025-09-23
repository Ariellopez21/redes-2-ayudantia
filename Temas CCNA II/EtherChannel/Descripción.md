EtherChannel permite redundancia sin bucles gracias a que se puede acoplar muy bien con STP.

> [!important] Seguimos hablando de redundancia en Capa 2.

## EtherChannel

### Preludio

En redes puede ser necesario más ancho de banda o redundancia de la que ofrece un solo enlace. Una opción es conectar varios enlaces entre los mismos dispositivos, pero el protocolo Spanning Tree (STP), activado por defecto en los switches Cisco, bloqueará los enlaces redundantes para evitar bucles como se aprendió en el [[Lab 5 - 08-09/Módulo 5|Módulo 5]].

EtherChannel resuelve este problema al agrupar varios enlaces Ethernet físicos en un solo enlace lógico. Con esto se consigue:

- Mayor ancho de banda.
    
- Balanceo de carga.
    
- Redundancia.
    
- Tolerancia a fallos.
    

Este mecanismo se aplica entre switches, routers y servidores.

> [!NOTE] Topología lógica del etherchannel
> ![[Pasted image 20250922153800.png|center|500]]

### Qué es

Cisco desarrolló la tecnología EtherChannel como una técnica switch a switch LAN para agrupar varios puertos Fast Ethernet o gigabit Ethernet en un único canal lógico.

Cuando se configura un EtherChannel, la interfaz virtual resultante se denomina “canal de puertos”.

### Ventajas

- La configuración se realiza en la **interfaz EtherChannel**, *no en cada puerto individual*, lo que garantiza coherencia entre enlaces.
    
- No requiere enlaces más rápidos ni costosos: *aprovecha los puertos existentes para aumentar el ancho de banda*.
    
- El **balanceo de carga** se reparte entre los enlaces físicos del canal. Según el hardware, puede hacerse con base en:
    
    - MAC de origen/destino.
        
    - IP de origen/destino.
        
- EtherChannel se presenta como un **único enlace lógico**.
    
    - Si existen **varios EtherChannel** entre switches, *STP puede bloquear* un canal completo para evitar bucles.
        
    - Si **solo hay un EtherChannel**, todos sus enlaces físicos quedan activos porque *STP lo reconoce como un único enlace*.
        
- Proporciona **redundancia**:
    
    - La pérdida de un enlace físico no cambia la topología ni obliga a recalcular STP.
        
    - Mientras quede al menos un enlace activo, el EtherChannel sigue funcionando (aunque con menor capacidad).

### Restricciones

- **Tipos de interfaz:** no se pueden mezclar (ej. Fast Ethernet con Gigabit Ethernet en el mismo canal).
    
- **Cantidad de puertos:** hasta **8 puertos Ethernet compatibles** por EtherChannel.
    
    - FastEtherChannel: hasta **800 Mbps full-duplex**.
        
    - Gigabit EtherChannel: hasta **8 Gbps full-duplex**.
        
- **Límites del equipo:**
    
    - Cisco Catalyst 2960 soporta hasta **6 EtherChannels**.
        
    - En IOS y plataformas más recientes, puede aumentar la cantidad de puertos y de canales soportados.
        
- **Consistencia de configuración:**
    
    - Todos los puertos deben configurarse igual en ambos dispositivos.
        
    - Si un lado es troncal, el otro también debe ser troncal y con la **misma VLAN nativa**.
        
    - Todos los puertos deben ser de **capa 2**.
        
- **Interfaz lógica:** cada EtherChannel se gestiona desde una **interfaz de canal de puertos**; lo configurado allí se aplica automáticamente a todos los puertos físicos asociados.
