## LLA – Link-Local Address

- **Qué es:** Dirección IPv6 que **se crea automáticamente en cada interfaz**, sin necesidad de router ni configuración manual.
    
- **Prefijo fijo:** `FE80::/10` (todas las LLAs empiezan con FE80).
    
- **Alcance:** Solo sirve dentro del **enlace local** (la red directa, sin pasar por routers).
    
- **Obligatoria:** Todos los dispositivos IPv6 tienen al menos una LLA.
    
- **Usos principales:**
    
    - Comunicación con vecinos inmediatos (Neighbor Discovery).
        
    - Comunicación host–router (el router responde a LLAs).
        
    - Base para protocolos como SLAAC o DHCPv6.
        

> [!example] Ejemplo en Windows/Linux:
> ```
fe80::1a2b:3c4d:5e6f%12
> ```
> El `%12` indica la interfaz a la que pertenece.

## GUA – Global Unicast Address

- **Qué es:** Dirección IPv6 equivalente a una dirección IPv4 pública. Se usa para comunicación **global** en Internet.
    
- **Prefijo típico:** `2000::/3` (ej.: 2001:db8::/32 en ejemplos).
    
- **Alcance:** Global, enrutada en Internet.
    
- **Cómo se obtiene:**
    
    - Manualmente (configuración estática).
        
    - Automáticamente mediante **SLAAC** o **DHCPv6** (stateless o stateful).
        
- **No es obligatoria:** Solo la tienen los dispositivos que necesitan acceso a Internet o a otras redes externas.
    

Ejemplo:

```
2001:db8:acad:1::100
```

## Diferencias

| Característica | **LLA**                           | **GUA**                                |
| -------------- | --------------------------------- | -------------------------------------- |
| Prefijo        | `FE80::/10`                       | `2000::/3`                             |
| Creación       | Automática, siempre               | Manual, SLAAC o DHCPv6                 |
| Alcance        | Solo enlace local                 | Global (Internet)                      |
| Obligatoria    | Sí                                | No                                     |
| Función        | Comunicación básica y con routers | Comunicación global, acceso a Internet |

## Resumen

- **LLA** es como tu **dirección dentro del edificio** (solo vecinos la usan).
    
- **GUA** es tu **dirección oficial de la ciudad** (sirve para que cualquiera en el mundo te contacte).