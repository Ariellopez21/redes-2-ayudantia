#### Características

- Estándar IEEE (originalmente **802.3ad**, ahora **802.1AX**).
    
- Permite **agrupar varios puertos físicos en un único canal lógico**.
    
- Similar a PAgP, pero al ser estándar puede usarse en **entornos multi-vendor**.
    
- Verifica compatibilidad de configuraciones antes de formar el EtherChannel.
    

#### Modos de operación

- **On** → Fuerza el canal sin usar LACP (sin negociación).
    
- **Activo** → Inicia la negociación enviando paquetes LACP.
    
- **Pasivo** → Espera y responde a paquetes LACP, no inicia negociación.
    

#### Características

- Hasta **8 enlaces activos** y **8 de respaldo** (standby).
    
- Si un enlace activo falla, uno de los de respaldo entra en funcionamiento automáticamente.

#### Tabla resumen

| S1     | S2            | Establecimiento del canal |
| ------ | ------------- | ------------------------- |
| On     | On            | Sí                        |
| On     | Activo/pasivo | No                        |
| Activo | Activo        | Sí                        |
| Activo | Pasivo        | Sí                        |
| Pasivo | Activo        | Sí                        |
| Pasivo | Pasivo        | No                        |
Aunque realmente, lo que importa es el siguiente contenido:

| LACP            |
| --------------- |
| active - active |
| active - pasive |

Con dicha configuración sabes que habrá un EtherChannel asegurado.