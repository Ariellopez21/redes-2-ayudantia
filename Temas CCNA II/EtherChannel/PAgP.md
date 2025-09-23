Patentado por Cisco.

Es un protocolo propietario de Cisco que **facilita la creación de EtherChannels**, validando que las configuraciones de ambos lados sean compatibles antes de activar el canal.

#### Modos de operación

- **On**
    - Fuerza la creación del EtherChannel **sin usar PAgP**.
    - No intercambia paquetes de negociación.
    
- **PAgP desirable**
    - Estado **activo**.
    - Inicia la negociación enviando paquetes PAgP al otro extremo.
        
- **PAgP auto**
    - Estado **pasivo**.
    - Solo responde a los paquetes PAgP recibidos, no inicia la negociación.
        
#### Compatibilidad de modos

- Un puerto en **auto** necesita que el otro extremo esté en **desirable** (activo), de lo contrario el canal no se forma.
    
- Si ambos lados están en **auto**, no habrá negociación.
    
- Si se configura **no pagp** o se deshabilita el protocolo, el EtherChannel también se desactiva.

#### Tabla resumen

| S1         | S2                     | Establecimiento del canal |
| ---------- | ---------------------- | ------------------------- |
| On         | On                     | Sí                        |
| On         | Desdeseable/Automático | No                        |
| Deseado    | Deseado                | Sí                        |
| Deseado    | Automático             | Sí                        |
| Automático | Deseado                | Sí                        |
| Automático | Automático             | No                        |

Aunque realmente, lo que importa es el siguiente contenido:

| PAgP                  |
| --------------------- |
| desirable - desirable |
| desirable - auto      |

Con dicha configuración sabes que habrá un EtherChannel asegurado.
